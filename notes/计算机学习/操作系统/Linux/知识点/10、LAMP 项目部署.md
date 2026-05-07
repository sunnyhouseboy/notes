## 一、YUM1.yum
### 1、什么是 YUM
在 CentOS 系统中，软件管理方式通常有三种方式： rpm安装 、 yum安装 以及 编译安装 。

**说明**：编译安装，从过程上来讲比较麻烦，包需要用户自行下载，下载的是源码包，需要进行编译操作，编译好了才能进行安装，这个过程对于刚接触Linux的人来说比较麻烦，而且还容易出错。好处在于是源码包，对于有需要自定义模块的用户来说非常方便。
难度：编译安装 > rpm 安装 > yum 安装（有网络 + yum 源支持）
Yum（全称为 Yellow dog Updater, Modified ）是一个在 Fedora 和 RedHat 以及 CentOS 中的 Shell 前端软件包管理器。

基于 rpm 包管理，能够从指定的服务器(yum 源）自动下载 RPM 包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。

**rpm 和 yum 的区别**：① yum 底层也是基于 rpm 进行安装的（yum 安装的软件，可以通过 rpm -qa 进行查询）② yum 相对于 rpm 最大的优势，可以解决依赖关系。
### 2、YUM 源配置
YUM 源配置文件所在路径 => /etc/yum.repos.d 文件夹
[[01、环境搭建#二、配置环境（centos）#1、配置镜像]]
## 二、Yum 命令详解
### 1、搜索要安装的软件
基本语法：yum search 软件名称的关键词
案例：搜索 firefox 火狐浏览器
示例代码：`yum search firefox`
### 2、使用 Yum 安装软件
基本语法：yum install 软件名称关键词 \[选项]
选项：-y ：yes缩写，确认安装，不提示
案例：使用 yum 命令安装 firefox 浏览器
示例代码：`yum install firefox -y`
### 3、使用 Yum 卸载软件
基本语法：yum remove 软件名称关键词 \[选项]
选项：-y ：yes缩写，确认卸载，不提示
案例：把 firefox 火狐浏览器进行卸载操作
示例代码：`yum remove firefox -y`
### 4、使用 Yum 更新软件
基本语法：yum update 软件名称关键词 \[选项]
选项：-y ：yes缩写，确认更新，不提示
案例：把 firefox 火狐浏览器进行更新操作
示例代码：`yum update firefox -y`
## 三、LAMP 概述
### 1 、什么是 LAMP
LAMP：Linux + Apache + MySQL + PHP LAMP 架构（组合）
LNMP：Linux + Nginx + MySQL + php-fpm LNMP 架构（组合）
LNMPA：Linux + Nginx(80) + MySQL + PHP + Apache Nginx 代理方式
### 2、AMP 三者之间的关系
![[Pasted image 20260105093435.png]]
Apache：用于接收用户的请求（输入网址，返回网页=>结果）
PHP：注册、登录、加入购物车、下单、支付等动态功能（有编程语言的支持）
MySQL：永久保存数据，比如你在网站上注册的用户和密码、你加入购物车的产品、你的产品订单
### 3、Linux 配置
#### ①关闭防火墙与 SELinux
`systemctl stop firewalld`
`systemctl disable firewalld`
`vim /etc/selinux/config`
`SELINUX=disabled关闭selinux`
**注意**：修改完成重启centos虚拟机才生效
#### ②配置公网 YUM 源
- 备份 YUM 配置文件
  `mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup`
- 下载新的 CentOS-Base.repo 到 /etc/yum.repos.d/
  `wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo`
  或`curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo`
- 创建和刷新 YUM 缓存
  `yum makecache`
#### ③安装扩展软件
`yum install bash-completion vim net-tools ntpdate -y`
**说明**：bash-completion 自动补全、vim 编辑器、net-tools 网络工具包以及 ntpdate 时间同步工具
#### ④ntpdate 时间同步
[[08、自有服务及软件包#④时间同步操作]]
### 4、LAMP 部署前期准备
#### ①关闭防火墙
`systemctl stop firewalld`
`systemctl disable firewalld`
#### ②关闭 SELinux
SELinux(Security-Enhanced Linux) 是美国国家安全局（NSA）对于强制访问控制的实现，是 Linux 历史上最杰出的新安全子系统。
获取 SELinux 的状态：`getenforce`
临时关闭 SElinux：`setenforce 0`       重启后 SELinux 还会自动启动 
永久关闭 SELinux：编辑 SELinux 的配置文件
`vim /etc/selinux/config`
`SELINUX=disabled`
**AMP 安装指南**：在 Linux 中安装 AMP 必须先安装 Apache，在安装 MySQL，最后安装 PHP
#### ③关闭重启 Linux
`reboot`
### 5、LAMP 环境之 Apache 安装
Apache：阿帕奇，Apache 基金会
httpd 软件 => 前身 apache，随着时间的推移以及互联网行业的发展，越来越多的软件加入到了 Apache 的基金会。
例如很多软件名称如下 httpd、sshd、mysqld、pptpd 后面都带个 d，这个 d 的意思简单说下，d 是 daemon 名称是守护神的意思，计算机术语是守护进程，没错，这些都是守护进程的意思，守护进程是一类在后台运行的特殊进程，确保其守护的服务正常运行。
#### ①安装 httpd 软件
`yum install httpd -y`
#### ②配置/etc/httpd/conf/httpd.conf 文件
`vim /etc/httpd/conf/httpd.conf`
`/ServerName => 搜索`
`96 ServerName localhost:80`
**说明**：localhost ： 代表本机，对应的 IP 地址可以使 127.0.0.1 或本机的公网 IP
#### ③启动 httpd 服务
`systemctl start httpd`
#### ④把 httpd 服务添加到开机启动项中
`systemctl enable httpd`
#### ⑤使用 ss 或 netstat 命令查询 httpd 占用的端口
`netstat -tnlp |grep httpd`或`ss -naltp |grep httpd`
![[Pasted image 20260105102055.png]]

| 字段 | 示例值 | 说明 |
| :--- | :--- | :--- |
| 协议 | tcp6 | 连接使用 TCP 协议，并支持 IPv6。`:::` 的写法通常也表示同时监听 IPv4。 |
| 接收队列 | 0 | 等待本机程序取走的数据包数量，0 为正常。 |
| 发送队列 | 0 | 等待发送给远程主机的数据包数量，0 为正常。 |
| 本地地址 | :::80 | 服务监听在所有网络接口的 80 端口（HTTP 默认端口）。 |
| 远程地址 | :::* | 可以接受来自任何远程地址和端口的连接。 |
| 状态 | LISTEN | 关键状态，表示该端口正在监听，等待连接。 |
#### ⑥在浏览器中，使用公网 IP 访问你的服务器
![[Pasted image 20260105102309.png]]
### 6、LAMP 环境之 MySQL 安装
#### ①下载 MySQL 的官网 Yum 源
由于 yum 源上默认没有 mysql-server。所以必须去官网下载后在安装
首先安装wget：`yum install wget -y`
`wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm`
#### ②安装 MySQL 的官网镜像源
`rpm -ivh mysql-community-release-el7-5.noarch.rpm`
#### ③使用 Yum 安装 Mysql 最新版软件
`yum install mysql-community-server -y`
MySQL 软件是一个 C/S 架构的软件，拥有客户端与服务器端。mysql-server 服务器端（内部也包含了客户端），community 代表社区版（免费开源）
#### ④启动 mysql，查看端口占用情况
`systemctl start mysqld`
`netstat -tnlp |grep mysqld`
#### ⑤MySQL 数据库初始化
默认情况下，数据库没有密码，也没有任何数据，必须要初始化
1. 初始化数据，设置 Root 密码（MySQL 管理员）
   `mysql_secure_installation`
   ![[Pasted image 20260105103336.png]]
![[Pasted image 20260105103423.png]]
![[Pasted image 20260105103437.png]]
![[Pasted image 20260105103444.png]]
![[Pasted image 20260105103452.png]]
![[Pasted image 20260105103501.png]]
2. 把 Mysqld 服务添加到开机启动项
   `systemctl enable mysqld`
3. 连接 MySQL 数据库，测试
   `mysql -u root -p `
### 7、LAMP 环境之 PHP 安装
#### ①使用 Yum 命令安装 Php 软件
`yum install php -y`
#### ②使用 Yum 命令安装 Php-mysql 扩展包
`yum install php-mysql -y`
#### ③使用 Systemctl 启动 Php 软件（重启 Apache）
`systemctl restart httpd`
为什么启动 php 就是重启 Apache 呢？答：因为 LAMP 架构中，PHP 是以模块的形式追加到 Apache 的内核中，所以启动 php 就相当于重置 Apache 软件
### 8、测试 LAMP 环境是否可以使用
#### ①使用 cd 命令进入/var/www/html 目录
`cd /var/www/html`
**说明**：Apache的项目目录 => /var/www/html，以后程序员开发的代码都是放置于此目录
#### ②使用 vim 命令创建 demo.php 文件
使用 vim 命令创建 demo.php 文件
`vim demo.php`
#### ③编写 php 代码
`<?php`
`echo 'hello world';`
`?>`
编写完成后，保存退出，然后在浏览器中使用 `http://IP/demo.php`
### 9、使用 LAMP 部署 Web 项目
#### ①简介
WordPress 是目前世界上最流行的开源博客程序,功能强大、扩展性强,网 站该有的功能都能通过第三方插件实现。
#### ②下载 Wordpress 博客系统
`curl -O https://wordpress.org/latest.tar.gz`
下载 wordpress 到 /root 目录
#### ③解压
`tar -xvf latest.tar.gz`
#### ④创建一个项目目录
`mv wordpress /var/www/html`   移动到html目录
`cd /var/www/html`                    切换到html目录
`mv wordpress blog`                 修改名字
#### ⑤在数据库中创建一个 Blog 数据库
`create database blog default charset utf8;`
#### ⑥给/var/www/html 目录设置可写权限
`chmod -R a+w /var/www/html`
#### ⑦使用浏览器安装博客
访问： `http://ip/blog`
![[Pasted image 20260105125958.png]]
![[Pasted image 20260105130017.png]]

