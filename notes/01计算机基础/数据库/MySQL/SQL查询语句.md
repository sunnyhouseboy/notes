## 一、SQL 查询语句回顾
`select */字段列表 from 数据表名称 where 查询条件;`
## 二、SQL 查询子句
`select * 字段列表 from 数据表名称 where 子句 group by 子句 order by 子句 limit 子句;`
**特别注意**：子句的顺序是固定的，不能颠倒。
### 1、where 子句

| 符号               | 说明          |
| :--------------- | :---------- |
| %                | 匹配0个或任意多个字符 |
| _ (下划线)          | 匹配单个字符      |
| like             | 模糊匹配        |
| =                | 等于, 精确匹配    |
| >                | 大于          |
| <                | 小于          |
| >=               | 大于等于        |
| <=               | 小于等于        |
| != 和 <>          | 不等于         |
| ! 和 not          | 逻辑非         |
| \|\| 和 or        | 逻辑或         |
| && 和 and         | 逻辑与         |
| between...and... | 两者之间        |
| in (...)         | 在...        |
| not in (...)     | 不在          |
==案例1==：like 模糊查询语句，查询姓 " 关 " 的同学信息（name 字段对应值应该以 " 关 " 开头）
`select * from tb_student where name like '关%';`
==案例2==：like 模糊查询语句，查询名字中带 " 蝉 " 字的同学信息
`select * from tb_student where name like '%蝉%';`
==案例3==：like 模糊查询语句，查询云字结尾且名字为两个字的同学信息
`select * from tb_student where name like '_云';`
==案例4==：获取学生表中，id 编号为 3 的同学信息
`select * from tb_student where id=3;`
==案例4==：获取年龄大于 25 周岁的同学信息
`select * from tb_student where age>25;`
==案例5==：获取学生表中，性别不为男的同学信息（获取女同学的信息）
`select * from tb_student where agender!='男';`
==案例6==：获取班级中年龄大于 30 岁的男同学信息
`select * from tb_student where age>30 and agender='男';`
==案例6==：获取 id 值为 1、3、5 的同学信息
`select * from tb_student where id in(1,3,5);`或`select * from tb_student where id=1 or id=3 or id=5;`
==案例7==：获取年龄在 18 周岁~25 周岁之间的同学信息
`select * from tb_student where age between 18 and 25;`或`select * from tb_student where age>=18 or age<=25;`
### 2、DISTINCT 数据去重
==案例==：获取 tb_student 学生表学员年龄的分布情况。
`select distinct age from tb_student;`
### 3、GROUP BY 子句
group by 子句的作用：对数据进行分组操作，为什么要进行分组呢？分组的目标就是进行分组统计。根据给定数据列的查询结果进行分组统计，最终得到一个分组汇总表
**注意**：一般情况下 group by 需与统计函数一起使用才有意义。
#### ①、统计函数

| 常见统计函数 | 说明 |
| :--- | :--- |
| max | 求最大值 |
| min | 求最小值 |
| sum | 求和 |
| avg | 求平均值 |
| count | 求总行数 |
==案例1==：求 tb_student 表中一共有多少个记录
`select count(*) from tb_student;`
==案例2==：针对 id 字段求和
`select sum(id) from tb_student;`
==案例3==：求学员表中年龄的平均值
`select avg(age) from tb_student;`
#### ②、GROUP BY 分组
==案例1==：求 tb_student 表中，男同学的总数量与女同学的总数量
`select gender,count(*) from tb_student group by gender;`
**注意**：在 MySQL5.7 以后版本中，分组字段必须出现在 select 后面的查询字段中
==案例2==：求 tb_student 表中，男同学年龄的最大值与女同学年龄的最大值
`select agender,max(age) from tb_student group by agender;`
### 4、ORDER BY 子句
主要作用的就是对数据进行排序（升序、降序）
升序：`select * from 数据表名称  order by 字段名称 asc;`
降序：`select * from 数据表名称 order by 字段名称 desc;`
### 5、LIMIT 子句
`select * from 数据表名称 limit number;`   查询满足条件的number条数据
`select * from 数据表名称 limit offset,number;` 从偏移量为offset开始查询，查询number条记录offset的值从0开始
## 三、SQL 多表查询
### 1、UNION 联合查询
UNION 联合查询的作用：把多个表中的数据联合在一起进行显示。应用场景：分库分表
`select * from tb_student1 union select * from tb_student2;`
## 四、SQL 语句查询练习
### 1、把 book.sql 上传到/root目录
### 2、把 book.sql 导入 MySQL
先登录MySQL，然后选择要导入数据库表的数据库
`source /root/book.sql;`#把book.sql 导入 名字为book的数据库
### 3、练习
1. 查看表的结构
   `desc books;`或`show create table books;`
2. 查询bId为5的内容
   `select * from books where bId=5;`
3. 查询publishing 出版社为清华大学出版社的内容
   `select * from books where publishing='清华大学出版社';`
4. 查询价格小于50元的书
   `select * from books where price<50;`
5. 查询 价格大于50 且 出版社为 人民邮电出版社
   `select * from books where price>50 and publishing='人民邮电出版社';`
6. 查询 价格大于50 且 出版社为 人民邮电出版社 并且 书名中 有CAD 内容
   `select * from books where price>50 and publishing='人民邮电出版社' and bName like '%CAD%';`
7. 查询出版社为清华大学 或者人民邮电的 书名和价格
   `select bName,price from books where publishing='清华大学出版社' or publishing='人民邮电出版社';`
8. 查询所有图书价格按照从高到底排序
   `select bName,price from books order by price desc;`
9. 查询所有图书价格按照从低到高排序
   `select bName,price from books order by asc;`
10. 查询所有图书价格按照从低到高排序，限制显示一条 也就是价格最低的一本书
     `select bName,price from books order by price asc limit 1;`
11. 查询所有图书价格按照从高到底排序，限制显示三条 也就是价格第二高到第四高的内容
     `select bName,price from books order by price desc limit 1,3;`
12. 修改 表为books的 价格为50 当bId 为3的时候
     `update books set price=50 where bId=3; `
13. 修改表为books的 价格为50 当 书名为 黑客与网络安全
     `update books set price=50 where bName="黑客与网络安全";`
14. 修改表为books的 书名为《黑客与画家》 当 bId 为2
     `update books set bName="黑客与画家" where bId=2;`
15. 删除名字为黑客攻防的内容
     `delete from books where bName="黑客攻防";`
16. 删除价格大于100 的内容
     `delete from books where price >100;`
17. 删除books所有数据 注意不等于 drop table books;
     `delete from books;`