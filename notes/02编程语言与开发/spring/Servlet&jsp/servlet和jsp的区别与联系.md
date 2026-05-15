​                                           servlet和jsp的区别与联系
JSP更侧重于前端页面显示，Servlet更侧重于业务逻辑。

JSP经编译后就变成了Servlet。(JSP的本质就是Servlet，JVM只能识别java的类，不能识别JSP的代码,Web容器将JSP的代码编译成JVM能够识别的java类)

Servlet在Java代码中通过HttpServletResponse对象动态输出HTML内容
JSP在静态HTML内容中嵌入Java代码，Java代码被动态执行后生成HTML内容

Servlet的应用逻辑是在Java文件中，并且完全从表示层中的HTML里分离开来。
而JSP的情况是Java和HTML可以组合成一个扩展名为.jsp的文件。

JSP修改后可以立即看到结果，不需要编译；而Servelt缺需要编译。

JSP是动态网页开发技术，是运行在服务器端的脚本语言，而Servlet是web服务器端编程技术。所以JSP运行时就是转换为Servlet，也就是java程序来执行。