# Springboot

## Ⅰ、前后端参数交互注解

### 一、@RequestParam——获取传入参数的值

1、如果设置了该注解但是没有在请求头上设置value的值，那么将会报错，找不到页面。只有在后面设置了value的值才行。

![image-20231026195631384](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231026195631384.png)

![image-20231026195700931](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231026195700931.png)

2、如果设置了required的值未false，那么就和未加注解一样了。

![image-20231026195910527](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231026195910527.png)

![image-20231026195949925](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231026195949925.png)

3、设置defaultValue值可以让在参数为空时有个默认值。

### 二、@RequestBody——获取请求参数中的json字符串

1、@RequestBody主要用来接收前端传递给后端的json字符串中的数据的(请求体中的数据的)；而最常用的使用请求体传参的无疑是POST请求了，所以使用@RequestBody接收数据时，一般都用POST方式进行提交。在后端的同一个接收方法里，@RequestBody与@RequestParam()可以同时使用，@RequestBody最多只能有一个，而@RequestParam()可以有多个。

2、RequestBody 接收的是请求体里面的数据；而RequestParam接收的是key-value
    里面的参数；

3、json字符串中，如果value为""的话，后端对应属性如果是String类型的，那么接受到的就是""，如果是后端属性的类型是Integer、Double等类型，那么接收到的就是null。

json字符串中，如果value为null的话，后端对应收到的就是null。

如果某个参数没有value的话，在传json字符串给后端时，要么干脆就不把该字段写到json字符串中；要么写value时， 必须有值，null  或""都行。千万不能有类似"stature":，这样的写法。
### 三、@PathVariable—— 获取定义在路径中的参数值

![image-20231026202806319](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231026202806319.png)

![image-20231026202830583](C:\Users\20680\AppData\Roaming\Typora\typora-user-images\image-20231026202830583.png)

## Ⅱ、四种请求

### 一、POST

1、POST请求是向服务器端发送数据的，但是该请求会改变数据的种类等资源，就像数据库的insert操作一样，会创建新的内容。几乎目前所有的提交操作都是用POST请求的。

2、特点：

post提交数据相对于get的安全性高一些。（注意：抓包软件也会抓到post的内容，安全性要求高可以进行加密）

传递数据量大，请求对数据长度没有要求。

请求不会被缓存，也不会保留在浏览器的历史记录中。

用于密码等安全性要求高的场合，提交数据量较大的场合，如上传文件，发布文章等。

POST方式提交数据上限默认为8M（可以在PHP的配置文件post_max_size选项中修改）

### 二、GET

1、GET请求会向数据库发索取数据的请求，从而来获取信息，该请求就像数据库的select操作一样，只是用来查询一下数据，不会修改、增加数据，不会影响资源的内容，即该请求不会产生副作用。

2、**特点：**

get方式在url后面拼接参数，只能以文本的形式传递参数。

传递的数据量小，4kb左右（不同浏览器会有差异）。

安全性低，会将信息显示在地址栏。

速度快，通常用于对安全性要求不高的请求

### 三、PUT

1、PUT请求是向服务器端发送数据的，从而改变信息，该请求就像数据库的update操作一样，用来修改数据的内容，但是不会增加数据的种类等，也就是说无论进行多少次PUT操作，其结果并没有不同。

### 四、DELETE

1、DELETE请求顾名思义，就是用来删除某一个资源的，该请求就像数据库的delete操作。