## 一、MySQL简介
### 1、MySQL的特点：
1. 开放源代码
2. 跨平台
   MySQL 可以在不同的操作系统下运行，简单地说，MySQL 可以支持 Windows 系统、UNIX 系统、Linux 系统等多种操作系统平台。这意味着在一个操作系统中实现的应用程序可以很方便地移植到其他的操作系统下。
3. 轻量级
   MySQL 的核心程序完全采用多线程编程，这些线程都是轻量级的进程，它在灵活地为用户提供服务的同时，又不会占用过多的系统资源。因此 MySQL 能够更快速、高效的处理数据。
4. 成本低
### 2、MySQL数据库版本
1. 社区版：MySQL Community Edition (GPL）
   - 可以看做是企业版的“广泛体验版（小白鼠版）”，未经各个专有系统平台的压力测试和性能测试
   - 基于 GPL 协议发布，可以随意下载使用
   - 没有任何官方技术支持服务
2. 企业版：MySQL Enterprise Edition(commercial)
     - 提供了比较全面的高级功能、管理工具及技术支持
     - 安全性、稳定性、可扩展性比较好
3. 集群版：MySQL Cluster CGE(commercial) 
## 二、客户端工具的使用
### 1、客户端工具 mysql 使用
mysql: mysql命令行工具，一般用来连接访问mysql数据库

| 选项 | 说明 |
| :--- | :--- |
| -u, --user=name | 指定登录用户名 |
| -p, --password | 指定登录密码(注意是小写p),一定要放到最后面 |
| -h, --host=name | 指定数据库的主机地址 |
| -P, --port=xxx | 指定数据库的端口号(大写P) |
| -S, --socket=name | 指定socket文件 |
| -e, --execute=name | 使用非交互式操作(在shell终端执行sql语句) |
==案例1==：使用 mysql 客户端工具连接服务器端（用户名：root、密码：123456）
`mysql -uroot -p123456`
**注意**：以上连接方式虽然可以连接进入到 MySQL，但是官方不建议我们直接把密码写入在终端，建议 -p 然后直接回车，然后在终端中输入密码。
==案例2==：连接 10.1.1.100 服务器上的 MySQL 数据库（用户名：root，密码：123456）
`mysql -h 10.1.1.100 -P 3306 -uroot -p`
==案例3==：查看所有的数据库：
`show databases;`
==案例4==：退出的三种方法:
`exit;`或`quit`或`\q`
### 2、默认数据库的了解

| 默认库 | 描述 |
| :--- | :--- |
| information_schema | 1、对象信息数据库，提供对数据库元数据的访问，有关MySQL服务器的信息，例如数据库或表的名称，列的数据类型或访问权限等；<br>2、在INFORMATION_SCHEMA中，有数个只读表，它们实际上是视图，而不是基本表，因此你将无法看到与之相关的任何文件；<br>3、视图，是一个虚表，即视图所对应的数据不进行实际存储，数据库中只存储视图的定义，在对视图的数据进行操作时，系统根据视图的定义去操作与视图相关联的基本表。 |
| mysql | 1、mysql数据库是系统数据库。它包含存储MySQL服务器运行时所需的信息的表。比如权限表、对象信息表、日志系统表、时区系统表、优化器系统表、杂项系统表等。<br>2、不可以删除，也不要轻易修改这个数据库里面的表信息。 |
| performance_schema | MySQL5.5开始新增一个数据库，主要用于收集数据库服务器性能；并且库里表的存储引擎均为PERFORMANCE_SCHEMA，而用户是不能创建存储引擎为PERFORMANCE_SCHEMA的表。 |
| sys | 1、mysql5.7增加了sys系统数据库，通过这个库可以快速的了解系统的元数据信息；<br>2、sys库方便DBA发现数据库的很多信息，解决性能瓶颈；<br>3、这个库是通过视图的形式把information_schema 和 performance_schema结合起来，查询出来更加令人容易理解的数据。 |
### 3、客户端工具 mysqladmin 使用
mysqladmin：客户端管理mysql数据库工具
#### ①常用选项

| 选项                | 描述              |
| :---------------- | :-------------- |
| -h, --host=name   | 指定连接数据库主机       |
| -p, --password    | 指定数据库密码         |
| -P, --port=#      | 指定数据库端口         |
| -S, --socket=name | 指定数据库 socket 文件 |
| -u, --user=name   | 指定连接数据库用户       |
#### ②常用命令

| 命令                      | 描述                |
| :---------------------- | :---------------- |
| password [new-password] | 更改密码              |
| reload                  | 刷新授权表             |
| shutdown                | 停止mysql服务         |
| status                  | 简短查看数据库状态信息       |
| start-slave             | 启动slave           |
| stop-slave              | 停止slave           |
| variables               | 打印可用变量            |
| version                 | 查看当前mysql数据库的版本信息 |
==案例1==：更改 root 账号的密码为 root
`mysqladmin password '新密码' -p`然后输入旧密码
==案例2==：更改密码后，建议刷新授权表
`mysqladmin reload -p`或在数据库中`flush privileges`
==案例3==：停止 mysql
`mysqladmin shutdown -p`
==案例4==：查看 mysql 状态
`mysqladmin status -p`
==案例5==：打印可用变量（mysql 本身预置了很多变量信息）
`mysqladmin variables -p`
==案例6==：查询 mysql 版本
`mysqladmin version -p`
## 三、MySQL 中的 SQL 语句
### 1、SQL 语句的分类
1. DDL(Data Definition Languages) 语句:
   数据定义语言,这些语句定义了不同的数据段、数据库、表、列、索引等数据库对象的定义。常用的语句关键字主要包括 create、drop、alter、rename、truncate。
2. DML(Data Manipulation Language) 语句:
   数据操纵语句,用于添加、删除、更新和查询数据库记录,并检查数据完整性,常用的语句关键字主要包括 insert、delete、update等。
3. DCL(Data Control Language) 语句:
   数据控制语句,用于控制不同数据段直接的许可和访问级别的语句。这些语句定义了数据库、表、字段、用户的访问权限和安全级别。主要的语句关键字包括 grant、revoke 等。
4. DQL(Data Query Language) 语句:
   数据查询语句，用于从一个或多个表中检索信息。主要的语句关键字包括 \*\*select
## 四、SQL 语句的基本操作
### 1、MySQL 的内部结构
![[Pasted image 20260109114709.png]]

一个 MySQL DBMS 可以同时存放多个数据库，理论上一个项目就对应一个数据库。如博客项目 blog 数据库、商城项目shop 数据库、微信项目 wechat 数据库。
一个数据库中还可以同时包含多个数据表，而数据表才是真正用于存放数据的位置。理论上一个功能就对应一个数据表。如博客系统中的用户管理功能，就需要一个 user 数据表、博客中的文章就需要一个 article 数据表、博客中的评论就需要一个 message 数据表。
一个数据表又可以拆分为多个字段，每个字段就是一个属性。
一个数据表除了字段以外，还有很多行，每一行都是一条完整的数据（记录）。
### 2、数据库的基本操作
#### ① 创建数据库
`create database 数据库名称;`
**特别注意**：在 MySQL 中，当一条 SQL 语句编写完毕后，一定要使用分号; 进行结尾，否则系统认为这条语句还没有结束。
==案例==：创建数据库的相关案例
创建db1库：`create database db1;`
创建db1库并指定默认字符集：`create database db1 default charset gbk;`
如果存在不报错：`create database if not exists db1 default character set utf8;`
**说明**：不能创建相同名字的数据库！
**扩展**：编码格式，常见的 gbk（中国的编码格式）与 utf8（国际通用编码格式）
latin1编码256 个字符 （abcd、1234、传统字符）
国内汉字无法通过 256 个字符进行描述，所以国内开发了自己的编码格式 gb2312，升级 gbk
中国台湾业开发了一套自己的编码格式 big5
很多项目并不仅仅只在本地使用，也可能支持多国语言，标准化组织开发了一套通用编码 utf8，后来 5.6 版本以后又进行了升级 utf8mb4
**特别提醒**：编写 SQL 语句是一个比较细致工作，不建议大家直接在终端中输入 SQL 语句，可以先把你要写的 SQL 语句写入一个记事本中，然后拷贝执行。
#### ②查询已创建数据库
显示所有数据库：`show databases;`
显示某个数据库的数据结构：`show create database db_users;`
![[Pasted image 20260109115614.png]]
#### ③ 修改数据库信息
在 MySQL5 以后的版本中，MySQL 不支持更改数据库的名称。我们所谓的修改数据库主要修改的是数据库的编码格式。
`alter database 数据库名称 default charset=新编码格式;`
==案例==：把 db_users 数据库的编码格式更改为 gbk
`alter database db_users default charset=gbk;`
#### ④ 删除数据库
`drop database 数据库名称;`
==案例==：删除 db_users 数据库
`drop database db_users;`
## 五、数据表的基本操作
### 1、数据表的创建
`create table 数据表名称(`
`字段1 字段类型 [字段约束],`
`字段2 字段类型 [字段约束],`
`……`
`);`
==案例==：创建一个 admin 管理员表，拥有 3 个字段（编号、用户名称、用户密码）
`create database db_users;`
`use db_users;`
`create table tb_admin(`
    `id tinyint,`
	`username varchar(20),`
	`password char(32)`
`) engine=innodb default charset=utf8;`
**说明**：
  - tinyint ：微整型，范围 -128 ~ 127，无符号型，则表示 0 ~ 255
  - 表示字符串类型可以使用 char 与 varchar，char 代表固定长度的字段，varchar 代表变化长度的字段
  - text ：文本类型，一般情况下，用 varchar 存储不了的字符串信息，都建议使用 text 文本进行处理。
  - varchar 存储的最大长度，理论值 65535 个字符。但是实际上，有几个字符是用于存放内容的长度的，所以真正可以使用的不足 65535 个字符，另外 varchar 类型存储的字符长度还和编码格式有关。1 个 GBK 格式的占用 2 个字节长度，1 个 UTF8 格式的字符占用 3 个字节长度。GBK = 65532~65533/2，UTF8 = 65532~65533/3
  ### 2、查询已创建数据表
  显示所有数据表（当前数据库）：`use 数据库名称;`       `show tables;`
  显示数据表的创建过程（编码格式、字段等信息）：
  `show create table 数据表名称;`
  ![[Pasted image 20260109142001.png]]
  `desc 数据表名称;`
  ![[Pasted image 20260109141947.png]]
- Field: 表示表中的字段名。
- Type: 字段的数据类型，例如 VARCHAR , INT , DATETIME 等。
- Null: 指示该字段是否可以包含 NULL 值。如果可以，这里会显示 YES ；如果不可以，会显示 NO 。
- Key: 表示该字段是否是表的索引或主键。 PRI 代表主键， UNI 代表唯一键， MUL 可以表示非唯一索引，或者是一个可以包含多个 NULL 值的唯一索引。
- Default: 该字段的默认值。如果没有默认值，则此处通常为空。
- Extra: 包含该字段的额外信息，如 auto_increment 表示该字段会自动增长。
### 3、修改数据表信息
#### ① 数据表字段添加
`alter table 数据表名称 add 新字段名称 字段类型 first|after 其他字段名称;`
**选项说明**：
first：把新添加字段放在第一位
after 字段名称：把新添加字段放在指定字段的后面
==案例==：在 tb_article 文章表中添加一个 addtime 字段，类型为 date(年 - 月 - 日)
`alter table tb_article add addtime date after content;`
#### ② 修改字段名称或字段类型
修改字段名称与字段类型（也可以只修改名称）：
`alter table tb_admin change username user varchar(40);`
仅修改字段的类型：
`alter table tb_admin modify user varchar(20);`
#### ③ 删除某个字段
`alter table tb_article drop 字段名称;`
#### ④ 修改数据表引擎（MyISAM 或 InnoDB）
`alter table tb_article engine=myisam;`
#### ⑤ 修改数据表的编码格式
`alter table tb_admin default charset=gbk;`
#### ⑥ 修改数据表名称或者移动表
移动表到另一个库里并重命名：
`rename table db01.t1 to db02.t11;`或者`alter table db01.t1 rename db02.t11;`
只重命名表名不移动：
`rename table tt1 to tt2;`或者`alter table tt1 rename tt2;`
### 4、删除数据表
`drop table 数据表名称;`
## 六、数据的增删改查
### 1、数据的增加操作
`insert into 数据表名称(字段1,字段2,字段3) values (字段1的值,字段2的值,字段3的值);`或
`insert into 数据表名称 values (字段1的值,字段2的值,字段3的值);`这种方法必须要求与数据库表的字段一一对应。
![[Pasted image 20260109143540.png]]
![[Pasted image 20260109143911.png]]
**注意**：字符串一定要加引号
### 2、数据的查询操作
`select * from 数据表名称 [where 查询条件];`或`select id,username,age from 数据表名称 [where 查询条件];`
### 3、数据的修改操作
`update 数据表名称 set 字段1=更新后的值,字段2=更新后的值,…… where 更新条件;`
**特别说明**：如果在更新数据时，不指定更新条件，则其会把这个数据表的所有记录全部更新一遍。
### 4、数据的删除操作
`delete from 数据表名称 [where 删除条件] ;`
## 七、MySQL 注释
mysql 中的四种注释：
1.  -- 注释内容：这种注释方法不能够实现多行注释，要注意的是 -- 后面是有一个空格的。（-- 后面的内容将不会被识别，因此需要在下一行加上分号来结束该语句）
2. \#注释内容：这种注释方法也不能实现多行注释。
3. / 注释内容*/：这种注释能够实现多行注释。
4. /!注释内容 \*/：这种注释是一种 “条件代码”或 “版本适配” 技巧。它允许开发者写一份SQL脚本，使其能根据数据库版本的不同，智能地决定是否执行某段代码。
   案例：`/*!50110 具体的SQL代码 */`
   说明： 如果当前MySQL服务器的版本**等于或高于**`5.1.10`这个版本号，那么`/*!`和 `*/`之间的SQL代码就会被**执行**。如果当前版本**低于**`5.1.10`，那么整个`/*!50110 ... */`这部分会被当成一个普通的注释**忽略掉**，里面的代码不会执行。