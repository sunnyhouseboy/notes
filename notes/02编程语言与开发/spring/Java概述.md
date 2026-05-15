# Java概述

## java三大版本

1、javaSE

2、javaEE

3、javaME

## jvm、jre和jdk的关系

### jvm

Java Virtual Machine是Java虚拟机，Java程序需要运行在虚拟机上，不同的平台有自己的虚拟机，因此Java语言可以实现跨平台。

### jre

Java Runtime Environment包括Java虚拟机和Java程序所需的核心类库等。核心类库主要是java.lang包：包含了运行Java程序必不可少的系统类，如基本数据类型、基本数学函数、字符串处理、线程、异常处理类等，系统缺省加载这个包

如果想要运行一个开发好的Java程序，计算机中只需要安装JRE即可。
### jdk

Java Development Kit是提供给Java开发人员使用的，其中包含了Java的开发工具，也包括了JRE。所以安装了JDK，就无需再单独安装JRE了。其中的开发工具：编译工具(javac.exe)，打包工具(jar.exe)等

### jvm、jre和jdk之间的关系图

![JVM&JRE&JDK关系图](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTclQUUlODAlRTQlQkIlOEIvSlZNJkpSRSZKREslRTUlODUlQjMlRTclQjMlQkIlRTUlOUIlQkUucG5n?x-oss-process=image/format,png)

## 历史

Java的前身：Oak（橡树），1995年更名为Java。

Java在2009年之前是属于Sun公司的，但之后被Oracle（甲骨文公司）收购。

## 关键字和保留字

### 1、关键字

![img](https://img-bbs.csdn.net/upload/201711/14/1510645792_607401.png)

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvSmF2YSVFNSU4NSVCMyVFOSU5NCVBRSVFNSVBRCU5NyVFRiVCQyU4OEphdmElMjA4JUU3JTg5JTg4JUU2JTlDJUFDJUVGJUJDJTg5LnBuZw?x-oss-process=image/format,png" alt="Java关键字(Java 8版本)" style="zoom:200%;" />

<img src="https://img-blog.csdnimg.cn/20191214173453247.png" alt="img" style="zoom:150%;" />

### 2、保留字

`goto、const、byValue、cast、future、 generic、 inner、 operator、 outer、 rest、 var`

## 访问修饰符

1、private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）和接口。

  *声明为私有访问类型的变量只能通过类中公共的 getter 方法被外部类访问。*

2、default (即缺省，什么也不写，不使用任何关键字）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
3、protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）和接口。
4、public : 对所有类可见。使用对象：类、接口、变量、方法。
<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvSmF2YSVFOCVBRSVCRiVFOSU5NyVBRSVFNCVCRiVBRSVFOSVBNSVCMCVFNyVBQyVBNi5wbmc?x-oss-process=image/format,png" alt="访问修饰符图" style="zoom:150%;" />

### 访问继承

1、父类中声明为 public 的方法在子类中也必须为 public。

2、父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。

3、父类中声明为 private 的方法，不能够被子类继承。

## 非访问修饰符

1、static 修饰符，用来修饰类方法和类变量。

2、final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

3、abstract 修饰符，用来创建抽象类和抽象方法。

4、synchronized 和 volatile 修饰符，主要用于线程的编程。

### 一、static修饰符

1、**静态变量：**static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。

2、**静态方法：**static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。

### 二、final修饰符

1、final 变量：final 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。被 final 修饰的实例变量必须显式指定初始值。final 修饰符通常和 static 修饰符一起使用来创建类常量。

2、final方法：父类中的 final 方法可以被子类继承，但是不能被子类重写。声明 final 方法的主要目的是防止该方法的内容被修改。

3、final类：final 类不能被继承，没有类能够继承 final 类的任何特性。

### 三、abstract修饰符

1、抽象类：抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充。

一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误。抽象类可以包含抽象方法和非抽象方法。

```java
public class Main {//这不能表明抽象方法能被实例化，这实际上是创建了一个对象来继承该父类的表现
    public static void main(String[] args) {
       Goods goods=new Goods(){
           int a=super.apple;

           @Override
           void add() {
               System.out.println(1111);
           }

           @Override
           public String toString() {
               return "$classname{" +
                       "apple=" + apple +
                       '}';
           }
       };
        System.out.println(goods);//$classname{apple=1}
       Class<?> clazz=goods.getClass();
        System.out.println(clazz.getName());//Main$1
        System.out.println(clazz.getSuperclass());//class Goods
    }
}
abstract class Goods{
    int apple=1;
    abstract void add();

    @Override
    public String toString() {
        return "Goods{" +
                "apple=" + apple +
                '}';
    }
}
```

2、抽象方法：抽象方法是一种没有任何实现的方法，该方法的具体实现由子类提供。抽象方法不能被声明成 final 和 static。

任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类。

如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法。

## 转义字符

| 转义字符（xml） | 特殊字符 | 含义   |
| :-------------: | -------- | ------ |
|      &lt;       | <        | 小于   |
|      &gt;       | >        | 大于   |
|      &amp;      | &        | 和号   |
|     &apos;      | ’        | 单引号 |
|     &quot;      | "        | 引号   |

在Java中，不管是String.split()，还是正则表达式，有一些特殊字符需要转义，这些字符是
( [ { / ^ - $ ¦ } ] ) ? * + .

一般都是通过用\\实现的

## 进制

java有将其他进制转化成十进制的方法：

![image-20231127213750674](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231127213750674.png)

其中Integer.parseInt(String s,int redix)    s表示待转字符串，redix表示代转字符串的进制

（十六进制中a,b,c,d,e,f分别对应10，11，12，13，14，15。不区分大小写）

### 二进制编码

1、原码=符号位+数字位（符号位1表示负数，0表示整数） 其中0有两种表示方法：00000000，10000000

2、反码：正数反码等于原码，负数符号位不动，其余位取反

3、补码：正数补码等于原码，负数等于其反码加一

例1：一个数的反码为10001111其对应的十进制数为：-112

共有两种方法，一种是直接将其转化成原码计算；另一种是直接计算：-(2^7^-1) + 2^0^+2^1^+2^2^

例2：一个数的补码为10001111其对应的十进制数为:-113         其原码为：11110001

第一问也有两种方法，一种是直接将其转化成原码计算；另一种是直接计算：-(2^7^)+2^0^+2^1^+2^2^

第二问也有两种方法，一种是先将补码减1后在取其反码；另一种是从低位往高位找第一个不为0的数，其不变，其余取反。

### 进制转换

1、十进制转二进制：整数部分除二取余，小数部分乘二取整。

2、十进制转八进制：整数部分除八取余，小数部分乘八取整。

3、十进制转十六进制：整数部分除十六取余，小数部分乘十六取整。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvMTUwJUU1JThEJTgxJUU4JUJGJTlCJUU1JTg4JUI2JUU4JUJEJUFDJUU0JUJBJThDJUU4JUJGJTlCJUU1JTg4JUI2LnBuZw?x-oss-process=image/format,png)

4、二进制转八进制：从小数点位置起向左右两边划分,每三个为一组,不足三个的在最左边或最右边添0补齐,对照上边的表进行计算。

1011010.100101~（2）~=001 011 010.100 101~（2）~=132.45~（8）~

5、八进制转二进制：方法与二进制转八进制相反。

132.45~（8）~=001 011 010.100 101~（2）~=10111010.100101~（2）~

6、二进制转十六进制：从小数点位置起向左右两边划分,每四个为一组,不足四个的在最左或最右添0补齐,对照上边的表进行计算。

1011010.100101~（2）~=0101 1010.1001 0100~（2）~=5A.94~(16)~

7、十六进制转二进制:方法与二进制转十六进制方法相反

8、八进制转十六进制：八进制数→二进制数→十六进制数

9、十六进制转八进制：十六进制数→二进制数→八进制数

## 运算符

### 一、算术运算符

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU3JUFFJTk3JUU2JTlDJUFGJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2LnBuZw?x-oss-process=image/format,png" alt="算术运算符" style="zoom:150%;" />

注意事项：

1、/ 左右两端的类型需要一致；

2、%最后的符号和被模数相同；

3、前++；先+1，后运算 后++；先运算，后+1；

4、+：当String字符串与其他数据类型只能做连接运算；并且结果为String类型。

###  二、比较运算符（关系运算符）

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU2JUFGJTk0JUU4JUJFJTgzJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2LnBuZw?x-oss-process=image/format,png" alt="比较运算符" style="zoom:150%;" />

**注意**：比较运算符的结果都是Boolean值（true或false）

"=="用于比较引用和比较基本数据类型时具有不同的功能，具体如下：

1、基本数据类型：比较的是他们的值是否相等，比如两个int类型的变量，比较的是变量的值是否一样。

2、引用数据类型：比较的是引用的地址是否相同，比如说新建了两个User对象，比较的是两个User的地址是否一样。

### 三、逻辑运算符

注意：

1、& 与 &&以及|与||的区别：&：左边无论真假，右边都会进行运算；&&：如果左边为假，则右边不进行运算；

2、| 与 || 的区别同上；在使用的时候建议使用&&和||；

3、（^）与或（|）的不同之处是：当左右都为true时。

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU5JTgwJUJCJUU4JUJFJTkxJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2LnBuZw?x-oss-process=image/format,png" alt="img" style="zoom:150%;" />

### 四、位运算符

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU0JUJEJThEJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2MS5wbmc?x-oss-process=image/format,png" alt="img" style="zoom:150%;" />

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU0JUJEJThEJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2Mi5wbmc?x-oss-process=image/format,png" alt="位运算符2" style="zoom:150%;" />

### 五、三元运算符

- 三元运算符

<img src="https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU0JUI4JTg5JUU1JTg1JTgzJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2LnBuZw?x-oss-process=image/format,png" alt="三元运算符" style="zoom:150%;" />

注意事项：

1、表达式1与表达式2的类型必须一致；

2、使用三元运算符的地方一定可以使用if…else代替，反之不一定成立；

### 六、运算符优先级

![运算符的优先级](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTUlOUYlQkElRTclQTElODAlRTglQUYlQUQlRTYlQjMlOTUvJUU4JUJGJTkwJUU3JUFFJTk3JUU3JUFDJUE2JUU3JTlBJTg0JUU0JUJDJTk4JUU1JTg1JTg4JUU3JUJBJUE3LnBuZw?x-oss-process=image/format,png)

注意：&&的优先级高于||，在程序里布尔类型的值如果让其等于其他值的话，除了0其他的值都为1。

instanceof是用来判断左边是对象，右边是类；当对象是右边类或子类所创建对象时，返回true；否则，返回false。（对象只要是null无论右边是什么都为false）

顺序由高到低

![image-20231128171246707](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231128171246707.png)

## 流程控制语句

顺序结构：顺序结构是程序中最简单最基本的流程控制，没有特定的语法结构，按照代码的先后顺序，依次执行，程序中大多数的代码都是这样执行的。

分支结构：条件语句可根据不同的条件执行不同的语句。包括if条件语句与switch多分支语句。

循环结构：循环语句就是在满足一定条件的情况下反复执行某一个操作。包括while循环语句、do···while循环语句和for循环语句。

跳出多重循环的三种方法

1、使用带有标号的break语句

2、让外层的循环条件受到内层代码的影响

3、使用try/catch抛出异常强制跳出循环

```java
System.out.println("---------java中跳出多重循环的三种方式：---------");
        System.out.println("---------第一种，使用带有标号的的break语句---------");
        String a1 = "";
        String b1 = "";
        here:
        for (int i = 1; i <= 4; i++) {
            a1 = "外层循环第"+i+"层";
            for (int j = 1; j <= 4; j++) {
                b1 = "内层循环第"+j+"层";
                if (2 == j & 2 == i) {
                    break here;
                }
            }
        }
        System.out.println(a1+b1);
        System.out.println("---------第二种，外层的循环条件收到内层的代码控制限制---------");
        String a2 = "";
        String b2 = "";
        Boolean state =  true;
        for (int i = 1; i <= 4 && state; i++) {
            a2 = "外层循环第"+i+"层";
            for (int j = 1; j <= 4 && state; j++) {
                b2 = "内层循环第"+j+"层";
                if (2 == j & 2 == i) {
                    state = false;
                }
            }
        }
        System.out.println(a2+b2);
        System.out.println("---------第三种，使用try/catch强制跳出循环---------");
        String a3 = "";
        String b3 = "";
        try {
            for (int i = 1; i <= 3; i++) {
                a3 = "外层循环第"+i+"层";
                for (int j = 1; j <= 3; j++) {
                    b3 = "内层循环第"+j+"层";
                    if (2 == j & 2 == i) {
                        throw new Exception();
                    }
                }
            }
        } catch (Exception e) {
            System.out.println(a3+b3);
        }
        System.out.println("---------java中跳出多重循环的两种方式---------");
```

## 数据类型

### 一、基本数据类型 

包括八种：byte,short,int,long,float,double,char,boolean。

#### 1、整型

| 整型  | 占用字节空间大小 | 取值范围             | 默认值 |
| ----- | ---------------- | -------------------- | ------ |
| byte  | 1字节=8bit       | -128 ~ 127           | 0      |
| short | 2字节            | -32768 ~ 32767       | 0      |
| int   | 4字节            | -2^31 ~ （2^31） - 1 | 0      |
| long  | 8字节            | -2^63 ~ （2^63） - 1 | 0L     |

#### 2、浮点型

| 浮点型 | 占用字节空间大小 | 取值范围 | 默认值 |
| ------ | ---------------- | -------- | ------ |
| float  | 4字节            | 10^38    | 0.0F   |
| double | 8字节            | 10^308   | 0.0    |

注意：浮点运算在Java中会出现进度丢失问题，例如：

```java
public static void main(String [] args){
    System.out.println(0.06+0.01);//0.06999999999999999
    System.out.println(1.0-0.42);//0.5800000000000001
    System.out.println(4.015*100);//401.49999999999994
    System.out.println(303.1/1000);//0.30310000000000004
}
```

原因：计算机是二进制的。浮点数没有办法使用二进制进行精确表示。

解决方案：用BigDecimal的new BigDecimal(String s)解决，用new BigDecimal(double num)也会错。

#### 3、字符型

| 字符型 | 占用字节空间大小 | 取值范围  | 默认值        |
| ------ | ---------------- | --------- | ------------- |
| char   | 2字节            | 0 ~ 65535 | ‘\u0000’或者0 |

#### 4、布尔型

| 布尔型  | 占用字节空间大小 | 取值范围    | 默认值 |
| ------- | ---------------- | ----------- | ------ |
| boolean | 视情况而定       | true、false | false  |

注意：Java中没有unsigned数据类型。

### 二、引用数据类型

引用数据类型是建立在八大基本数据类型基础之上，包括数组、接口、类。引用数据类型是由用户自定义，用来限制其他数据类型。简单的说，除八大基本类型之外的所有数据类型，都为引用数据类型。
所有引用类型的默认值都为 null 。

### 三、类型转换

转化从低级到高级：byte,short,char（三者同级）—> int —> long—> float —> double
1、低级转换高级：自动类型转换
2、高级转换低级：强制类型转换

注意：1、强制类型转换过程中可能造成数据丢失；2、强制类型转换时要在需要转换的数据类型前加上 ()。

### 四、包装类

上面说的八种基本数据类型都分别都有对应的包装类，如下表：需要了解的时这些包装类提供了大量的方法，通过这些方法可以完全将基本类型集成到Java的对象层次中。

| 基本数据类型 | 对应包装类 |
| ------------ | ---------- |
| byte         | Byte       |
| short        | Short      |
| int          | Integer    |
| long         | Long       |
| float        | Float      |
| double       | Double     |
| char         | Character  |
| boolean      | Boolean    |

### 五、自动拆箱与装箱

**装箱** ：就是将基本数据类型用他们对应的包装类包装起来。

装箱的时候其实就是自动调用了Integer的valueOf(int)方法。

**拆箱**：就是将包装类型转换为基本数据类型。

在拆箱的时候调用了Integer对象的intValue()方法。

**注意**：我们要了解的是，频繁的装箱拆箱的话，会增加内存的消耗，影响性能。

```java
    Integer i1 = 100;
    Integer i2 = 100;
    Integer i3 = 200;
    Integer i4 = 200;

    Integer one=new Integer(100);
    Integer two=new Integer(100);
    System.out.println(i1==i2);   //1
    System.out.println(i3==i4);   //2    
    System.out.println(one==two);  //3
    System.out.println(i1==100);   //4
    System.out.println(i1==one);   //5
```

1、true。因为i1和i2都在-128到127之间，且被Integer封装起来了故会直接从IntegerCache私有静态类的Integer数组中获取。

2、false。其值大于127则会创建两个不同的对象。

3、false。两个不同的对象。

4、true。将Integer对象进行了拆箱变成了int类型。

5、false。两个不同的对象。

### 六、枚举类型

枚举类型实际上是类的一个实例化对象

```java
enum Season{//枚举类
    SPRING("春天","温暖"),	
    SUMMER("夏天","炎热"),
    AUTUMN("秋天","凉爽"),
    WINNER("冬天","寒冷");
    //这些枚举的数据实际上就相当于类里面的常量，而且他们本质上也是Season类型的，都调用了有参构造
    private String name;
    private String desc;
    Season(){}//无参构造

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", desc='" + desc + '\'' +
                '}';
    }

    Season(String name, String desc) {//有参构造
        this.name = name;
        this.desc = desc;
    }
}
```

```java
public static void main(String[] args) {
    System.out.println(Season.SPRING);
    System.out.println("----------------------------------");
    Season[] seasons=Season.values();//获得枚举类里面的每一个枚举数据
    for (Season s:seasons){
        System.out.println(s);
    }
    System.out.println("----------------------------------");
    System.out.println(Season.AUTUMN.ordinal());//获得对应枚举数据的位置（从0开始）
    System.out.println("----------------------------------");
    Season season=Season.valueOf("SPRING");//获得对应名字的枚举数据。
    System.out.println(season);
}
```

### 七、泛型

泛型，即“参数化类型”。一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？顾名思义，就是将类型由原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。

```java
public class 泛型 {
    public static void main(String[] args) {
        Genericity g1=new Genericity(1);
        Genericity g2=new Genericity(1.0f);
        Genericity g3=new Genericity(1.00);
        Genericity g4=new Genericity("12");
        Genericity g5=new Genericity('a');
        g1.judge();
        g2.judge();
        g3.judge();
        g4.judge();
        g5.judge();
    }
}
class Genericity<T>{
    T num;
    public Genericity(T num){
        this.num=num;
    }
    public Genericity(){}
    public void judge(){
        Class<?> clazz=this.num.getClass();
        System.out.println(clazz.getName()) ;
    }
}
```

当在编译的过程中时会实行类型擦除，其过程如下：

1、将所有的泛型参数用其最左边界（最顶级的父类型）类型替换。

2、移除所有的类型参数。

## 反射

在Java中非常重要的就是反射机制，在正常情况下如果有一个类，则肯定能够通过类创建对象；如果想要使用类的完整名称来创建对象的话，就需要用到Java的反射机制，Java反射机制的基石是Class类Class类表示所有类的本身【也就是一个类在内存中的字节码】，通过Class可以获取到一个类的完整结构，包括此类中的方法、属性、包名、类名等等...

```java
package lianxi;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

public class reflect {
    public static void main(String[] args) throws NoSuchMethodException {
        Student student=new Student("tom",18,'男');
        Class<?> clazz1=student.getClass();
        System.out.println(clazz1);
        System.out.println("-------------------------------------------------");
        Class<Student> clazz=Student.class;
        Constructor<?>[] cs=clazz.getConstructors();//获取该类中的构造方法
        for (Constructor<?> c : cs) {
            System.out.println(c);
        }
        System.out.println("-------------------------------------------------");
        Constructor<?> c=clazz.getConstructor(String.class,int.class,char.class);//获取指定类型的构造方法
        System.out.println(c);
        System.out.println("-------------------------------------------------");
        Field[] fields=clazz.getDeclaredFields();//获取类中的所有字段
        for (Field field : fields) {
            System.out.println(field);
        }
        System.out.println("-------------------------------------------------");
        Field[] fields1=clazz.getFields();//获得类的继承来的字段和public修饰的字段
        for (Field field : fields1) {
            System.out.println(field);
        }
        System.out.println("-------------------------------------------------");
        Method[] method=clazz.getMethods();//获得类中的所有方法以及继承来的非私有方法
        for (Method method1 : method) {
            System.out.println(method1);
        }
        System.out.println("-------------------------------------------------");
        Method m = clazz.getMethod("introduce", String.class, int.class, char.class);
        System.out.println("指定方法："+m);
        System.out.println("-------------------------------------------------");
        //得到Student类实现的全部接口,不包括父类实现的接口
        Class<?>[] cls = clazz.getInterfaces();
        for (Class<?> cl : cls) {
            System.out.println("全部接口："+cl);
        }
        System.out.println("-------------------------------------------------");
        //得到类的名称
        System.out.println(clazz.getName());
        System.out.println("-------------------------------------------------");
        //得到包的名称
        System.out.println(clazz.getPackage());
        //得到类的父类
        System.out.println(clazz.getSuperclass());
    }

}
class Person{
    public static String identification="学生";
    public Person(){

    }
    public Person(String identification){
        Person.identification =identification;
    }
}
class Student extends Person  {
    public int high;
    private String name;
    private int age;
    private char sex;
    public Student(){

    }
    public Student(String name,int age,char sex){
        this.age=age;
        this.name=name;
        this.sex=sex;
    }
    public void introduce(String name,int age,char sex){
        System.out.println("My name is"+name+",I am"+age+",I am a"+sex);
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                '}';
    }

    public int getHigh() {
        return high;
    }

    public void setHigh(int high) {
        this.high = high;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public char getSex() {
        return sex;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }
}
```

## lambda表达式

```java
public class lambda {

    public static void main(String[] args) {
        If1 if1=()->{
            System.out.println("这是一个无参方法");
        };
        if1.test();
        If2 if2=(int a)->{
            System.out.println("这是一个有参构造"+a);
        };
        if2.test(3);
        If3 if3=(int a)->{
            int b=3;
            return (int)(Math.pow(a,3));
        };
        System.out.println(if3.test(2));
    }

}
@FunctionalInterface//函数式接口的注解（可加科不加）
interface If1{
    void test();
}
interface If2{
    void test(int a);
}
interface If3{
    int test(int a);
}
```

## 面向对象（oop）

1、面向过程是具体化的，流程化的，解决一个问题，你需要一步一步的分析，一步一步的实现。

2、面向对象是模型化的，你只需抽象出一个类，这是一个封闭的盒子，在这里你拥有数据也拥有解决问题的方法。需要什么功能直接使用就可以了，不必去一步一步的实现，至于这个功能是如何实现的，管我们什么事？我们会用就可以了。

3、联系：面向对象的底层其实还是面向过程，把面向过程抽象成类，然后封装，方便我们使用的就是面向对象了。

4、面向过程和面向对象的区别

面向过程：优点：性能比面向对象好，因为类调用时需要实例化，开销比较大，比较消耗资源。
缺点：不易维护、不易复用、不易扩展。

面向对象：优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统 更加灵活、更加易于维护
缺点：性能比面向过程差。

### 一、三大特性

1、封装
隐藏对象的属性和实现细节，仅对外提供公共访问方式，将变化隔离，便于使用，提高复用性和安全性。

2、继承
提高代码复用性；继承是多态的前提。

3、多态
父类或接口定义的引用变量可以指向子类或具体实现类的实例对象。提高了程序的拓展性。

### 二、五大基本原则

1、单一职责原则SRP(Single Responsibility Principle)
类的功能要单一，不能包罗万象，跟杂货铺似的。

2、开放封闭原则OCP(Open－Close Principle)
一个模块对于拓展是开放的，对于修改是封闭的，想要增加功能热烈欢迎，想要修改，哼，一万个不乐意。

3、里式替换原则LSP(the Liskov Substitution Principle LSP)
子类可以替换父类出现在父类能够出现的任何地方。比如你能代表你爸去你姥姥家干活。哈哈~~

4、依赖倒置原则DIP(the Dependency Inversion Principle DIP)
高层次的模块不应该依赖于低层次的模块，他们都应该依赖于抽象。抽象不应该依赖于具体实现，具体实现应该依赖于抽象。就是你出国要说你是中国人，而不能说你是哪个村子的。比如说中国人是抽象的，下面有具体的xx省，xx市，xx县。你要依赖的抽象是中国人，而不是你是xx村的。

5、接口分离原则ISP(the Interface Segregation Principle ISP)
设计时采用多个与特定客户类有关的接口比采用一个通用的接口要好。就比如一个手机拥有打电话，看视频，玩游戏等功能，把这几个功能拆分成不同的接口，比在一个接口里要好的多。

## 集合

### 一、Collection

1、list:有序(元素存入集合的顺序和取出的顺序一致)，元素都有索引。元素可以重复。	

List的主要实现：ArrayList， LinkedList， Vector。

|              |                ArrayList                 |         LinkedList         |         Vector         |
| ------------ | :--------------------------------------: | :------------------------: | :--------------------: |
| 底层实现     |                   数组                   |          双向链表          |          数组          |
| 同步性及效率 | 不同步，非线程安全，效率高，支持随机访问 | 不同步，非线程安全，效率高 | 同步，线程安全，效率低 |
| 特点         |              查询快，增删慢              |       查询慢，增删快       |     查询快，增删慢     |
| 默认容量     |                    10                    |             /              |           10           |
| 扩容机制     |                  1.5 倍                  |             /              |          2 倍          |



![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTklOUIlODYlRTUlOTAlODglRTYlQTElODYlRTYlOUUlQjYvTGlzdCVFNSVCOCVCOCVFNyU5NCVBOCVFNiU5NiVCOSVFNiVCMyU5NS5wbmc)

```java
public class Main {//使用迭代器遍历时可以用迭代器删除其中元素，用加强for会报错
    public static void main(String[] args) {
       List<Integer> list=new ArrayList<>();
       list.add(1);
       list.add(2);
       list.add(3);
       Iterator it=list.iterator();
       while (it.hasNext()){
           int num=(int)it.next();
           if(num==2){
               it.remove();
           }
       }
        System.out.println(list);
    }
}
```

2、set:无序(存入和取出顺序有可能不一致)，不可以存储重复元素。必须保证元素唯一性。

Set的主要实现类：HashSet， TreeSet

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTklOUIlODYlRTUlOTAlODglRTYlQTElODYlRTYlOUUlQjYvU2V0JUU1JUI4JUI4JUU3JTk0JUE4JUU2JTk2JUI5JUU2JUIzJTk1LnBuZw)

|            |                      HashSET                      |                         **TreeSet**                          |                        LinkedHashSet                         |
| :--------: | :-----------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|  底层实现  |                      HashMap                      |                            红黑树                            |                        LinkedHashMap                         |
|   重复性   |                    不允许重复                     |                          不允许重复                          |                          不允许重复                          |
|   有无序   |                       无序                        | 有序，支持两种排序方式，自然排序和定制排序，其中自然排序为默认的排序方式。 |           有序，以元素插入的顺序来维护集合的链接表           |
| 时间复杂度 | add()，remove()，contains()方法的时间复杂度是O(1) |     add()，remove()，contains()方法的时间复杂度是O(logn)     | LinkedHashSet在迭代访问Set中的全部元素时，性能比HashSet好，但是插入时性能稍微逊色于HashSet，时间复杂度是 O(1)。 |
|   同步性   |                不同步，线程不安全                 |                      不同步，线程不安全                      |                      不同步，线程不安全                      |
|   null值   |                    允许null值                     | 不支持null值，会抛出 java.lang.NullPointerException 异常。因为TreeSet应用 compareTo() 方法于各个元素来比较他们，当比较null值时会抛出 NullPointerException异常。 |                          允许null值                          |
|    比较    |                     equals()                      |                         compareTo()                          |                           equals()                           |

### 二、Map

Map 是一种把键对象和值对象映射的集合，它的每一个元素都包含一对键对象和值对象。 Map没有继承于Collection接口，从Map集合中检索元素时，只要给出键对象，就会返回对应的值对象。
Map 的常用实现类：HashMap、TreeMap、HashTable、LinkedHashMap、ConcurrentHashMap
![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTklOUIlODYlRTUlOTAlODglRTYlQTElODYlRTYlOUUlQjYvTWFwJUU1JUI4JUI4JUU3JTk0JUE4JUU2JTk2JUI5JUU2JUIzJTk1LnBuZw)

|          |                         **HashMap**                          |                 **HashTable**                 |                           TreeMap                            |
| :------: | :----------------------------------------------------------: | :-------------------------------------------: | :----------------------------------------------------------: |
| 底层实现 |                     哈希表（数组+链表）                      |              哈希表（数组+链表）              |                            红黑树                            |
|  同步性  |                          线程不同步                          |                     同步                      |                          线程不同步                          |
|  null值  | 允许 key 和 Vale 是 null，但是只允许一个 key 为 null，且这个元素存放在哈希表 0 角标位置 |           不允许key、value 是 null            | value允许为null。当未实现 Comparator 接口时，key 不可以为null当实现 Comparator 接口时，若未对 null 情况进行判断，则可能抛 NullPointerException 异常。如果针对null情况实现了，可以存入，但是却不能正常使用get()访问，只能通过遍历去访问。 |
|   hash   | 使用hash(Object key)扰动函数对 key 的 hashCode 进行扰动后作为 hash 值 | 直接使用 key 的 hashCode() 返回值作为 hash 值 |                                                              |
|   容量   |                 容量为 2^4 且容量一定是 2^n                  |          默认容量是11，不一定是 2^n           |                                                              |
|   扩容   |           两倍，且哈希桶的下标使用 &运算代替了取模           |       2倍+1，取哈希桶下标是直接用模运算       |                                                              |

集合里面都是可以存储null值的

### 三、集合工具类

Collections

常用方法：max（最大值）,min（最小值）,reverse（颠倒）,swap（交换）,sort（排序）

```java
public static void main(String[] args) {
    String[] arr = {"abc", "kk", "qq"};
    List<String> list = Arrays.asList(arr);
    // 添加一个元素,抛出异常UnsupportedOperationException
    list.add("bb");
```

}

## IO流

```java
import org.junit.Test;

import java.io.*;

public class IO流 {
    //FileInputStream和FileOutputStream都是对字节进行操作
    @Test
    public void  FileInputStream()throws IOException{
		//FileInputStream fis=new FileInputStream("C:\\Users\\20680\\Desktop\\data.txt");
        //绝对路径
        FileInputStream fis=new FileInputStream("./src/a.txt");
        //相对路径，其中.代表当前Java项目的根目录
        int b;
        byte[] bytes=new byte[1024];//一个汉字两个字节
        while ((b=fis.read(bytes))!=-1){//得到的是对应字符的ASCII
            System.out.print(new String(bytes,0,b));
        }
        fis.close();//关闭资源
    }
    @Test
    public void FileOutputStream()throws IOException{
        FileOutputStream fos=new FileOutputStream("./src/a.txt",true);
        //加true是允许续写，否则写入的话会清空文件,并且在父级目录正确的前提下若文件不存在会自行创建
        fos.write("\n迎接你们的王！！！".getBytes());//\r或\n都可以实现换行，因为Java会自动补成\r\n
        fos.close();
    }
    @Test
    public void copyFile()throws IOException{
        FileInputStream fis=new FileInputStream("./src/a.txt");
        FileOutputStream fos=new FileOutputStream("./src/b.txt");
        byte[] buffer=new byte[4];//缓冲区
        int length;
        while ((length=fis.read(buffer))!=-1){
            fos.write(buffer,0,length);
        }
        fis.close();
        fos.close();
    }
    //FileReader和FileWriter都是对字符进行操作
    @Test
    public void FileReader() throws IOException{
        int ch;
        FileReader fr=new FileReader("./src/a.txt");
        while ((ch=fr.read())!=-1){
            System.out.print((char) ch);
        }
        fr.close();
    }
    @Test
    public void FileWriter()throws IOException{
        FileWriter fw=new FileWriter("./src/b.txt",true);//要开启true才允许续写，否则会覆盖
        fw.write("\n6666");
        fw.close();
    }
    @Test
    public void BufferedReader() throws IOException{
        BufferedReader br=new BufferedReader(new FileReader("./src/a.txt"));
        String line;
        while ((line=br.readLine())!=null){
            System.out.println(line);
        }
    }
    @Test
    public void BufferedWriter()throws IOException{
        BufferedWriter bw=new BufferedWriter(new FileWriter("./src/b.txt",true));
        bw.newLine();//可实现换平台换行
        String s="这真的太酷了！！！!";
        bw.write(s);
        bw.close();
    }
}
```

### File

1、创建文件

```java
public static void main(String[] args) throws IOException {
    String fileName="a.txt";
    String path="E:\\demo1\\"+fileName;
    File file=new File(path);
    File parentFile=file.getParentFile();
    if (!parentFile.exists()){
        parentFile.mkdirs();
    }
    if (!file.exists()){
        file.createNewFile();
    }
    System.out.println(file.getAbsoluteFile());
}
```

2、删除文件或文件夹

`file.delete`

3、判断是否是文件或文件夹

`file.isFile()` `parentFile.isDirectory()`

4、返回路径下的文件或文件夹

以字符串的形式返回该文件夹下的所有文件（夹）`file.list` 

以文件的形式返回该文件夹下所有的文件（夹） `file.listFile`

5、文件重命名

`file.renameTo(file1)`  file1必须要和file同一个父路径才能成功，如果该文件存在则不能改名成功，并且如果该文件不存在且未改名成功将会自动生成file1文件。

## 网络编程

### 一、常见的软件架构

1、BS：Browser/Server(浏览器/服务器)，只需要一个浏览器，用户通过不同的网住，客户访问不同的服务器。

优点：不需要开发客户端，只需要页面+服务端；用户不需要下载，打开浏览器就能使用。

缺点：如果应用过大，用户体验受到影响。

2、CS：Client/Server(客户端/服务器)，在用户本地需要下载并安装客户端程序，在远程有一个服务器的程序。

优点：画面可以做的非常精美，用户体验好。

缺点：需要开发客户端，夜需要开发服务端；用户需要下载和更新的时候太麻烦。

### 二、网络编程三要素

#### 1、IP

IP（Internet Protocol）是互联网协议地址，也称IP地址。是分配给上网设备的数字标签。是设备在网络中的地址，是唯一标识。

常见的IP分类：IPv4(Internet Protocol version 4)，IPv6(Internet Protocol version 6)  互联网通信协议第xx版

##### IPv4

IPv4采用32位地址长度，分为4组，但由于不方便使用，又用点十进制表示法表示，变成如今我们见到的192.168.1.66但后来IP不够用了（2019年11月26日全部分配完毕）。

IPv4分为公网地址（万维网使用）和私有地址（局域网使用）。

192.168.开头的就是私有地址，范围即为192.168.0.0--192.168.255.255，专门为组织机构内部使用，以此节省IP。

特殊IP地址：127.0.01，也可以是localhost:是回送地址也称本地回环地址，也称本机IP，永远只会寻找当前所在本机

常用cmd命令：ipconfig（查看电脑IP）ping+网站/IP（查看网速）

##### IPv6

IPv6采用128位地址长度，分为8组（还未大规模使用），用冒分十六进制表示法

```java
public static void main(String[] args) throws UnknownHostException {
    InetAddress address=InetAddress.getByName("fangjj");
    System.out.println(address);
    System.out.println(address.getHostAddress());  //获得IP
    System.out.println(address.getHostName());    //获得主机名
}
```

#### 2、端口号

端口号是应用程序在设备的唯一标识。

端口号由两个字节表示的整数，取范围：0到65535，其中0到1023之间的端口号用于一些知名的网络服务或应用。我们自己使用1024以上的端口号。（一会端口号只能被一个应用程序使用）

#### 3、协议

协议是数据在网络中传输的规则，常见的协议有：UDP,TCP,http,https,ftp。

OSI参考模型：世界互联网协议标准，全球通信规范，单模型过于理想化，未能在英特网上进行广泛推广

TCP/IP参考模型（或TCP/IP协议）：事实上的国际标准。

<img src="C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231204172119252.png" alt="image-20231204172119252" style="zoom:150%;" />

##### UDP协议

1、用户数据协议（User Datagram Protocol）

2、UDP是面向无联通通信协议。

3、速度快，由大小限制，一次最多发送64K，数据不安全，已丢失数据

```Java
public void sendMessageUDP() throws IOException {//UDP协议发送信息
    //绑定端口，空参的话就随机赵一个能用的端口号，夜可以直接指定端口号。
    DatagramSocket ds=new DatagramSocket();
    String str="你好！！！";//数据
    byte[] bytes = str.getBytes();
    InetAddress address=InetAddress.getByName("fangjj");//IP
    int port=8082;//端口号
    DatagramPacket dp=new DatagramPacket(bytes,bytes.length,address,port);//数据打包
    ds.send(dp);//发送
    ds.close();//关闭
}
```

```java
public void receiveMessageUDP() throws IOException {
    //绑定端口，在接收时要手动写入发送的端口号，要保持一致。
    DatagramSocket ds=new DatagramSocket();
    byte[] bytes=new byte[1024];
    DatagramPacket dp=new DatagramPacket(bytes,bytes.length);
    ds.receive(dp);//接收数据
    byte[] data=dp.getData();//获得数据
    int len=dp.getLength();//获得数据长度
    InetAddress address=dp.getAddress();//获取IP
    int port=dp.getPort();//获取端口号
    System.out.println(new String(data,0,len));
    System.out.println(address+" "+port);
    ds.close();
}
```

这两个代码要一块运行，且接收时，发送一定要正在运行才行。

4、发送方式有三种：单播，组播，广播。组播地址：224.0.0.0到224.0.0.255  广播地址：25	5.255.255.255

##### TCP协议

1、传输控制协议（Transmission Control Protocol）

2、TCP协议是面向连接的通信协议。一般用于网络会议，语音通话，在线视频。

3、速度慢，没有大小限制，数据安全。一般用于下载软件，文字聊天，发送邮件。

4、通信之前要保证连接已经建立。

5、通过Socket产生IO流来进行网络通信。

```java
public static void main(String[] args) throws IOException {
    Socket socket=new Socket("127.0.0.1",10000);//连接不上服务器会报错（三次握手原则）
    OutputStream outputStream = socket.getOutputStream();
    outputStream.write("你好你好".getBytes());//发送数据
    outputStream.close();
    socket.close();//（四次挥手原则）
}
```

```java
public static void main(String[] args) throws IOException {
        ServerSocket serversocket=new ServerSocket(10000);
        Socket socket=serversocket.accept();//尝试连接，连接不上就一直卡着
        InputStream inputStream = socket.getInputStream();//获取字节输入流
        InputStreamReader isr=new InputStreamReader(inputStream);//字节流转字符流
        int b;
        while ((b=isr.read())!=-1){
            System.out.print((char)b);
        }
        socket.close();
        inputStream.close();
    }
```

## 函数

### 一、Math

abs（绝对值）,ceil（向上取整）,floor（向下取整）,round（四舍五入）,max（最大值）

min（最小值）,pow（次方运算）,random（随机数）

注意：1、round四舍五入时是先+0.5再floor。

2、在使用pow函数时，底数必须是常量（double型），结果才不会出现偏差。或者用(long)(Math.pow(x, t) + 0.5)

3、random是生成[0，1)的随机数。

### 二、System

java的时间原点是1970年1月1日8:00(C语言的生日)

1、System.exit( );括号中是0表示正常停止，非0表示异常停止。

2、System.currentTimeMillis( );表示从时间原点到现在所过的毫秒数。

3、System.arraycopy(int[] arr1,int start1,int[] arr2,int start2,int length );复制数组

### 三、Runtime

```java
Runtime.getRuntime().exec(s)//s是字符串，运行的cmd命令
```

### 四、Object

1、toString 返回的是一个字符串:包名+类名+@+地址

### 五、Date

```java
public static void main(String [] args) throws IOException {
    Date date=new Date();
    System.out.println(date);//返回当前时间
    Date date1=new Date(0L);
    System.out.println(date1);//返回距时间原点0ms的时间
    date.setTime(1000L);
    System.out.println(date);//返回距时间原点1000ms的时间
    Date date2=new Date();
    System.out.println(date2.getTime());//返回当前时间距时间原点的ms值
}
```



### 六、SimpleDateFormat

- > | Letter | Date or Time Component                           | Presentation                           | Examples                                    |
  > | ------ | ------------------------------------------------ | -------------------------------------- | ------------------------------------------- |
  > | `G`    | Era designator                                   | [Text](#text)                          | `AD`                                        |
  > | `y`    | Year                                             | [Year](#year)                          | `1996`; `96`                                |
  > | `Y`    | Week year                                        | [Year](#year)                          | `2009`; `09`                                |
  > | `M`    | Month in year (context sensitive)                | [Month](#month)                        | `July`; `Jul`; `07`                         |
  > | `L`    | Month in year (standalone form)                  | [Month](#month)                        | `July`; `Jul`; `07`                         |
  > | `w`    | Week in year                                     | [Number](#number)                      | `27`                                        |
  > | `W`    | Week in month                                    | [Number](#number)                      | `2`                                         |
  > | `D`    | Day in year                                      | [Number](#number)                      | `189`                                       |
  > | `d`    | Day in month                                     | [Number](#number)                      | `10`                                        |
  > | `F`    | Day of week in month                             | [Number](#number)                      | `2`                                         |
  > | `E`    | Day name in week                                 | [Text](#text)                          | `Tuesday`; `Tue`                            |
  > | `u`    | Day number of week (1 = Monday, ..., 7 = Sunday) | [Number](#number)                      | `1`                                         |
  > | `a`    | Am/pm marker                                     | [Text](#text)                          | `PM`                                        |
  > | `H`    | Hour in day (0-23)                               | [Number](#number)                      | `0`                                         |
  > | `k`    | Hour in day (1-24)                               | [Number](#number)                      | `24`                                        |
  > | `K`    | Hour in am/pm (0-11)                             | [Number](#number)                      | `0`                                         |
  > | `h`    | Hour in am/pm (1-12)                             | [Number](#number)                      | `12`                                        |
  > | `m`    | Minute in hour                                   | [Number](#number)                      | `30`                                        |
  > | `s`    | Second in minute                                 | [Number](#number)                      | `55`                                        |
  > | `S`    | Millisecond                                      | [Number](#number)                      | `978`                                       |
  > | `z`    | Time zone                                        | [General time zone](#timezone)         | `Pacific Standard Time`; `PST`; `GMT-08:00` |
  > | `Z`    | Time zone                                        | [RFC 822 time zone](#rfc822timezone)   | `-0800`                                     |
  > | `X`    | Time zone                                        | [ISO 8601 time zone](#iso8601timezone) | `-08`; `-0800`; `-08:00`                    |

```java
public static void main(String [] args) throws IOException, ParseException {
        Date date=new Date();
        SimpleDateFormat sdf=new SimpleDateFormat();//无参构造为默认格式
        SimpleDateFormat sdf1=new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss E");//有参构造自己输入格式
        String str=sdf.format(date);
        String str1=sdf1.format(date);
        System.out.println(str);
        System.out.println(str1);
        String s="2023-11-11 11:11";//字符串形式的日期
        SimpleDateFormat sdf2=new SimpleDateFormat("yyyy-MM-dd hh:mm");//解析格式
        Date parse = sdf2.parse(s);
        System.out.println(sdf1.format(parse));
    }
```

### 七、Calender

```java
public static void main(String [] args) throws IOException, ParseException {
    /*
     *月份中0代表1月----11代表12月
     *在老外眼中周日是一个星期的开始，故1代表周日---7代表周六
     */
    Calendar calendar=Calendar.getInstance();//Calender会把纪元，年，月，日，时，分，秒等放入一个数组中
    System.out.println(calendar);
    Date date=new Date(0L);
    calendar.setTime(date);//更新日历中存储的日期
    calendar.set(Calendar.YEAR, 2005);//更改日历中的年
    calendar.set(Calendar.MONTH, 11);//更改日历中的月

}
```

## 算法

### 一、BigInteger

BigInteger类型的数字范围较Integer，Long类型的数字范围要大得多，它支持任意精度的整数，也就是说在运算中 BigInteger 类型可以准确地表示任何大小的整数值而不会丢失任何信息。

1、读入：BigInteger m = scanner.nextBigInteger();

2、基本运算：

```java
//add(),subtract(),multiply(),divide(),mod(),remainder(),pow(),abs(),negate()
	@Test
	public void testBasic() {
		BigInteger a = new BigInteger("13");
		BigInteger b = new BigInteger("4");
		int n = 3;
    //1.加
	BigInteger bigNum1 = a.add(b);			//17
	//2.减
	BigInteger bigNum2 = a.subtract(b);		//9
	//3.乘
	BigInteger bigNum3 = a.multiply(b);		//52
	//4.除
	BigInteger bigNum4 = a.divide(b);		//3
	//5.取模(需 b > 0，否则出现异常：ArithmeticException("BigInteger: modulus not     positive"))
	BigInteger bigNum5 = a.mod(b);			//1
	//6.求余
	BigInteger bigNum6 = a.remainder(b);	//1
	//7.平方(需 n >= 0，否则出现异常：ArithmeticException("Negative exponent"))
	BigInteger bigNum7 = a.pow(n);			//2197
	//8.取绝对值
	BigInteger bigNum8 = a.abs();			//13
	//9.取相反数
	BigInteger bigNum9 = a.negate();		//-13
}
```

3、比较大小：

```Java
//比较大小:compareTo(),max(),min()
@Test
public void testCompare() {
	BigInteger bigNum1 = new BigInteger("52");
	BigInteger bigNum2 = new BigInteger("27");

	//1.compareTo()：返回一个int型数据（1 大于； 0 等于； -1 小于）
	int num = bigNum1.compareTo(bigNum2);			//1

	//2.max()：直接返回大的那个数，类型为BigInteger
	//	原理：return (compareTo(val) > 0 ? this : val);
	BigInteger compareMax = bigNum1.max(bigNum2);	//52

	//3.min()：直接返回小的那个数，类型为BigInteger
	//	原理：return (compareTo(val) < 0 ? this : val);
	BigInteger compareMin = bigNum1.min(bigNum2);	//27
}
```

### 二、取余和取模的区别

通常取模运算也叫取余运算，它们返回结果都是余数 **.rem** 和 **mod** 唯一的区别在于:

当 x 和 y 的正负号一样的时候，两个函数结果是等同的；当 x 和 y 的符号不同时，rem 函数结果的符号和 x 的一样，而 mod 和 y 一样。

这是由于这两个函数的生成机制不同，rem 函数采用 fix 函数，而 mod 函数采用了 floor 函数（这两个函数是用来取整的，fix 函数向 0 方向舍入，floor 函数向无穷小方向舍入）。

## 字符串处理

###  一、substring

1、s.substring(int index):返回从索引开始后的字符串。

2、s.substring(int index1,int index2):返回俩个索引之间的字符串，不包括index2的字符。

### 二、trim

去除字符串开头和结尾的空格。

### 三、反转字符串

new StringBuilder(str).reverse().toString;

### 三、split

s.split(String  str1,String str2);

str1表示被替换的字符（串），str2表示用来替换的字符（串），并且str1可以为正则表达式。

## 正则表达式

### 一、基本语法

#### 1、普通字符

1. ？：代表前面的字符可以出现一次或零次
2. *：代表前面的字符可以出现零次或多次
3. {a,b}：代表前面的字符可以出现a到b次，其中b可以省略不写，代表字符可以出现a次以上，a不可省略
4. +：代表前面的字符可以出现一次或多次
5. |：代表选择，只能我‘|’左右两边的其中一个
6. []:代表的是一定的范围，例如：[abc]，表示只能取自abc的其中一个或多个；[a-z],表示取自所有的小写字母
7. ^：代表取反，取与该符号后不同的字符
8. .：代表任意字符，但不包括换行符
9. ^：代表匹配行首
10. $：代表匹配行尾




#### 2、元字符

1、\d：代表所有的数字            

2、\w：代表所有的单词字符，包括数字，字母，下划线      

3、\s：代表空白符，包括tab键和换行符    

4、 \b：代表匹配隐式位置
上述的表达式的字母如果大写就代表与原来的相反 

### 二、用法

```java
String s = "theskyisblue   ";
String pattern="[a-z]*\\s";
Pattern r=Pattern.compile(pattern);
Matcher m=r.matcher(s);
if(m.find()){
    System.out.println(m.group(0)+"|");
}
```



### 三、常用正则表达式

^\d+$ ：非负整数（正整数 + 0）

^[0-9]*[1-9][0-9]*$ ：正整数

^((-\d+)|(0+))$ ：非正整数（负整数 + 0）

^-[0-9]*[1-9][0-9]*$ ：负整数

^-?\d+$ ：整数

^\d+(\.\d+)?$ ：非负浮点数（正浮点数 + 0）

^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$ ：正浮点数

^((-\d+(\.\d+)?)|(0+(\.0+)?))$ ：非正浮点数（负浮点数 + 0）

^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$ ：负浮点数

^(-?\d+)(\.\d+)?$ ：浮点数

^[A-Za-z]+$ ：由26个英文字母组成的字符串

^[A-Z]+$ ：由26个英文字母的大写组成的字符串

^[a-z]+$ ：由26个英文字母的小写组成的字符串

^[A-Za-z0-9]+$ ：由数字和26个英文字母组成的字符串

^\w+$ ：由数字、26个英文字母或者下划线组成的字符串

^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$ ：email地址

^[a-zA-z]+://(\w+(-\w+)*)(\.(\w+(-\w+)*))*(\?\S*)?$ ：url

/^(d{2}|d{4})-((0([1-9]{1}))|(1[1|2]))-(([0-2]([1-9]{1}))|(3[0|1]))$/ ：年-月-日

/^((0([1-9]{1}))|(1[1|2]))/(([0-2]([1-9]{1}))|(3[0|1]))/(d{2}|d{4})$/ ：月/日/年

^([w-.]+)@(([[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.)|(([w-]+.)+))([a-zA-Z]{2,4}|[0-9]{1,3})(]?)$ ：Emil

/^((\+?[0-9]{2,4}\-[0-9]{3,4}\-)|([0-9]{3,4}\-))?([0-9]{7,8})(\-[0-9]+)?$/ ：电话号码

^(d{1,2}|1dd|2[0-4]d|25[0-5]).(d{1,2}|1dd|2[0-4]d|25[0-5]).(d{1,2}|1dd|2[0-4]d|25[0-5]).(d{1,2}|1dd|2[0-4]d|25[0-5])$ ：IP地址

匹配中文字符的正则表达式： [\u4e00-\u9fa5]

匹配双字节字符(包括汉字在内)：[^\x00-\xff]

匹配空行的正则表达式：\n[\s| ]*\r

匹配HTML标记的正则表达式：/<(.*)>.*<\/\1>|<(.*) \/>/

匹配首尾空格的正则表达式：(^\s*)|(\s*$)

匹配Email地址的正则表达式：\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*

匹配网址URL的正则表达式：^[a-zA-z]+://(\\w+(-\\w+)*)(\\.(\\w+(-\\w+)*))*(\\?\\S*)?$

匹配帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$

匹配国内电话号码：(\d{3}-|\d{4}-)?(\d{8}|\d{7})?

匹配腾讯QQ号：^[1-9]*[1-9][0-9]*$

