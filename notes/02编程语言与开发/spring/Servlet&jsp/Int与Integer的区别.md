# [Int与Integer的区别](https://www.cnblogs.com/bigdata-stone/p/10560759.html)

## 一、区别：

1.Integer是int的包装类，int则是java的一种基本的数据类型；

2.Integer变量必须实例化之后才能使用，而int变量不需要实例化；

3.Integer实际是对象的引用，当new一个Integer时，实际上生成一个指针指向对象，而int则直接存储数值

4.Integer的默认值是null，而int的默认值是0。

## 二、Integer和int的比较

　　1.由于Integer实际是对一个Integer对象的引用，所以两个通过new生成的Integer变量永远是不相同的，因为New生成的是两个不同的对象，其内存地址不同。下面运行的结果为false

![img](https://img2018.cnblogs.com/blog/1441368/201903/1441368-20190319192633131-196666942.png)

　　2.Integer变量和int变量进行比较时，只要两个变量的值相等，则结果就为True，(因为包装类Integer和基本数据类型比较的时候，java会自动拆箱为int，然后进行比较，实际上就是两个int变量进行比较)，下面运行的结果为true

![img](https://img2018.cnblogs.com/blog/1441368/201903/1441368-20190319192919592-1360610694.png)

　　3.非new生成的Integer变量和new Integer生成的Integer变量比较的时候，结果为false(因为非new生成的Integer变量指向的是Java常量池中的对象，而new出来的对象指向的是堆中新建的对象，两者内存地址不同)，下面返回的是false

![img](https://img2018.cnblogs.com/blog/1441368/201903/1441368-20190319193216197-198126027.png)

　　4.两个非new出来的Integer对象，进行比较的时候，如果两个变量的值区间在-127~128之间的时候，则返回的结果为true，如果两个变量的变量值不在这个区间，则比较的结果为false。下面返回的是true

 ![img](https://img2018.cnblogs.com/blog/1441368/201903/1441368-20190319193415007-1534025617.png)

　　下面返回的是false

![img](https://img2018.cnblogs.com/blog/1441368/201903/1441368-20190319193501663-1862596945.png)

## 三、java 基本类型与引用类型的区别：

　　1.基本数据类型保存原始值，引用数据类型保存的是引用值(引用值就是指在对象中所处的地理位置)