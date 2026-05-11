## 1、安装
`apt-get install ufw`
## 2、使用
1. `ufw status` ：查看防火墙状态以及开放的端口
2. `ufw allow 端口号(/tcp或者udp)` ：开放对应端口
3. `ufw allow ssh/http/https` ：开发对应协议所需要的端口
4. `ufw enable` ：让防火墙生效
5. `sudo ufw disable` ：关闭防火墙
6. `ufw delete allow 端口号(/tcp或者udp)` ：删除开发的端口
7. `sudo ufw logging on`：启用ufw的日志记录（记录在/var/log/ufw.log 中）
**说明**：`ufw allow ssh` 等价于 `ufw allow 22/tcp`