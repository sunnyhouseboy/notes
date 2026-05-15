filter:过滤器

​             *web中的过滤器：当访问服务器的资源是，过滤器可以将请求拦截下来，完成一些特殊的功能。

​            *过滤器的作用：一般用于完成通过的操作。如：登录验证、统一编码的处理，敏感字符过滤.....

​             1、步骤：

​                          Ⅰ、定义一个类，实现接口Filter

​                           Ⅱ、复写方法

​                           Ⅲ、配置拦截路径

​                                    1、注解编写

​                                     2、在web.xml文件中配置

```
<filter>
    <filter-name>demo1</filter-name>
    <filter-class>Filter1</filter-class>
</filter>
<filter-mapping>
    <filter-name>demo1</filter-name>
    <url-pattern>/index.jsp</url-pattern>
</filter-mapping>
```

​                                     3、可以用代码：chain.doFilter(request,response);取消拦截

​             2、过滤器执行过程

​                    Ⅰ、执行过滤器

​                    Ⅱ、执行放行后的资源

​                     Ⅲ、回来执行过滤器放行代码下面的代码

​            3、过滤器的生命周期方法

​                   Ⅰ、init：在服务器启动后，会创建Filter对象，然后调用init方法。只执行一次用于加载资源

​                    Ⅱ、doFilter:每一次请求被拦截资源时，会执行。执行多次

​                    Ⅲ、destroy：在服务器关闭后，Filter对象被销毁。如果服务器被正常关闭，则会执行                               

​                            destroy（）方法。只执行一次。用于释放资源。

​              4、过滤器配置详解

​                     *拦截路径配置：

​                        1、具体资源路径：   /index.jsp

​                        2、拦截目录：/user/*

​                        3、后缀名拦截： *.jsp

​                        4  、拦截所有资源：/*

​                      *拦截方式配置：资源访问方式

​                             *注解配置：

​                                  *设置dispatcherTypes属性

​                                         1、request:默认值。浏览器直接请求资源

​                                          2、forward:转发访问资源

​                                           3、include：包访问资源

​                                           4、error：错误跳转访问资源

​                                           5、async:异步访问资源

​                               *web.xml配置

​                                             设置标签<dispatcher></dispatcher>即可

​                             5、过滤器链（配置多个过滤器）

​                                    *执行顺序：如果有两个过滤器：过滤器1和过滤器2

​                                               过滤器1-->过滤器2-->资源执行-->过滤器2-->过滤器1

listener：监听器

​              *事件监听机制

​                      *事件：一件事件

​                       *事件源：事情发送的地方

​                        *监听器：一个对象

​                         *监听注册：将事件、事件源、监听器绑定在以前。当事件源上发送某给事件后，执行监听器代码。

​              *servletcontextListener：监听ServletContext对象的创建和销毁

​                  *方法：

​                            *void contextDestroyed(ServletContextEvent sce):ServletContext对象被消耗之前会调用该方法

​                             *void contextInitialized(ServletContextEvent sce) :ServletContext对象创建后会调用该方法

​                  *步骤：

​                            1、定义一个类，实现servletcontextListener的接口

​                             2、复写方法

​                             3、配置

​                                  1、web.xml

```
<listener>
    <listener-class>Listener1</listener-class>
</listener>
```

​                                   2、注解       @WebListener

​       