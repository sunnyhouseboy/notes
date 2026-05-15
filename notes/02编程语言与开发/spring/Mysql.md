# Mysql

## insert

insert into 表名 (key1,key2.....) values (值1,值2) [条件];

## update

update 表名 set key1=value1,key2=value1.....[条件];

## delete

delete from 表名 [条件];

## select

select key1,key2.... from 表名 [条件];

基本语法：
mysql> select */字段列表 from 数据表名称 where 子句 group by 子句 having 子句 order by 子句 limit 子句;
①.where 子句
②.group by 子句
③.having 子句
④.order by 子句
⑤.limit子句
特别注意：五子句的顺序是固定的，不能颠倒

1、where

![img](https://img-blog.csdnimg.cn/20210518083218936.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)

2、group by

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210518094612892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)

- 案例：求tb_student表中，男同学的总数量和女同学的总数量
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210518230535461.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)
- 案例：求tb_student表中男同学年龄的最大值和女同学年龄的最大值
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210518230722284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)

3、having

- having与where类似，根据条件对数据进行过滤筛选
- where针对表中的列发挥作用，查询数据
- having针对查询结果集发挥作用，筛选数据

案例：求每个学科中，学科人数大于3人的学科信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021051914244564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)

4、order by



## create

create table 表名(

id int not null auto_increment primary key,

age tinyint unsigned,

sex enum('男','女'),

address varchar(25)

);

## alter

alter table 数据表名称 add 新字段名称 字段类型 first|after 其他字段名称;

 alter table 数据表名称 change 旧字段名 新字段名 类型;

 alter table 数据表名称 modify 字段名 类型;

 alter table 数据表名称 drop 字段名称;

 alter table 旧数据表名称 rename 新数据表名称;

## 数据类型

![这里是引用](https://img-blog.csdnimg.cn/20210516170944344.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)

### 整型

![img](https://img-blog.csdnimg.cn/20210516172536223.png)

### 浮点型

float  4byte   float(8,4)表示有效位数为8，小数点后4位

double 8byte double(8,4)表示有效位数为8，小数点后4位

### 定点类型

decimal和numeric用法类似

![img](https://img-blog.csdnimg.cn/20210517114516598.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ0OTQ0NjQx,size_16,color_FFFFFF,t_70)

### 字符串类型

char 

- char类型的字符串为定长，长度范围是0-255之间的任何值，占用定长的存储空间，不足的部分用空格填充，读取时删掉后面的空格
- 存储空间：CHAR(M)类型的存储空间和字符集有关系，一个中文在utf8字符集中占用3个bytes，gbk占用2个bytes，数字和字符统一用一个字符表示

varchar

- VARCHAR是变长存储，仅使用必要的存储空间
- 存储空间：VARCHAR(M)类型的存储空间和字符集有关，一个中文在utf8字符集中占用3个bytes，gbk统一占用2个bytes，数字和字符一个字节表示

text

1、TEXT代表文本类型的数据，当我们使用VARCHAR类型存储数据库，（早期最大只能存储255个字符，MySQL5版本中，其gbk可以存储3万多个字符，utf8格式可以存储2万多个字符），如超过了VARCHAR的最大存储范围，则可以考虑使用TEXT文本类型。
2、使用习惯：255个字符以内（包括255），定长就使用CHAR类型，变长就使用VARCHAR类型，如果超过255个字符，就使用TEXT文本类型。

### 日期类型

date 年-月-日

time 小时:分钟:秒

datetime 年-月-日 小时:分钟:秒  范围较大

timestamp 年-月-日 小时:分钟:秒

year 年

### 其他类型

BLOB：保存二进制的大型数据（字节串），没有字符集，eg：图片，音频视频等等。（实际运维工作中，很少将文件直接保存在数据库端，一般文件的存储都是基于路径进行操作的）
ENUM枚举类型：多选一，从给定的多个选项中选择一个。如sex enum（‘男’,‘女’)
SET集合类型：多选多，从给定的多个选项中选择多个。如hobby set(‘吃饭’,‘睡觉’,‘打豆豆’)

## 内连接查询

语法：select 字段 from 表一 inner join 表二 on 条件

![image-20231102145707312](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231102145707312.png)

## 外连接查询

1、左连接查询

![image-20231102150814574](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231102150814574.png)

2、左连接查询

![image-20231102150938096](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231102150938096.png)

内连接查询和外连接查询的区别：

- 内连接（inner join）：取出两张表中匹配到的数据，匹配不到的不保留
- 外连接（outer join）：取出连接表中匹配到的数据，匹配不到的也会保留，其值为NULL

## 事务

### 四大特性



![image-20231105152609277](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231105152609277.png)

### 操作流程

1、start transaction/begin;

2、sql语句

3、commit;

4、rollback;