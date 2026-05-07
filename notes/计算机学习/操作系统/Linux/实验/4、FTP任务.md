## 一、任务背景
1. 客服人员必须使用用户名密码 (kefu/123) 的方式登录服务器来下载相应文档
2. 不允许匿名用户访问
3. 客服部门的相关文档保存在指定的目录里/data/kefu local_root=/data/kefu
4. 客服用户使用用户 kefu/123 登录后就只能在默认的/data/kefu 目录里活动
## 二、创建客服账号
`useradd kefu`
`passwd kefu`
### 三、不允许匿名用户访问
`vim /etc/vsftpd/vsftpd.conf`
12 行 anonymous_enable=NO
配置修改完毕后，一定要重启 vsftpd 服务,`systemctl restart vsftpd`
## 四、指定账号访问的目录
`mkdir /data/kefu -p`
`vim /etc/vsftpd/vsftpd.conf`
## 五、限定 kefu/123 只能在/data/kefu 目录下活动
禁锢 kefu 用户只能在/data/kefu 目录下
`vim /etc/vsftp/vsftpd.conf`
18行 chroot_local_user=YES
配置修改完毕后，一定要重启 vsftpd 服务
`systemctl restart vsftpd`
## 六、匿名登录
![[Pasted image 20260106204614.png]]
服务器拒绝了登录请求，但是客户端仍显示提示符 ，这是因为FTP客户端在TCP连接建立后就会显示提示符，此时您处于 未认证状态 ，只能执行少量不需要权限的命令（如 quit 、 help 等）。
## 七、FTP 常用的命令
### 1、递归列表
`ls -R`
### 2、下载文件
`get Important\ Notes.txt`
![[Pasted image 20260106205515.png]]
**说明**：在Linux/Unix系统中，文件名可以包含空格和大多数特殊字符（除了 / 和空字符 \0 ）
当您需要对包含空格的文件执行操作（如下载、删除）时，可以使用以下方法：
 1. 使用双引号包裹文件名：`get "Important Notes.txt"`
 2. 使用反斜杠转义空格：`get Important\ Notes.txt`
### 3、下载所有可用文件
`wget -m - no-passive ftp: anonymous:anonymous@10.129.14.136`
- -m : 递归下载，即下载指定路径下的所有文件和子目录。
- -no-passive : 禁用被动模式，强制使用主动模式进行 FTP 传输。
- ftp://anonymous:anonymous@10.129.14.136 : FTP 服务器的地址和登录凭据。在这个示例中，使用匿名登录方式，用户名和密码均为 "anonymous"，FTP 服务器的 IP 地址为 10.129.14.136。
### 4、上传文件
`put testupload.txt`
