Requset:

​       一、Request和Response对象的原理

​               1、request和response对象都是有服务器创建的，我们来使用

​               2、request对象是来获取请求消息的，response对象是来设置响应消息的

​       二、request对象继承体系结构：

​               ServletRequest                    --接口

​                             |继承

​               HttpServletRequest             --接口

​                              |实现

​               org.apache.catalina.connector.RequestFacade 类（由tomcat创建）

​       三、request的功能：

​               1、获取请求消息数据

​                     Ⅰ、获取请求行数据

​                             *Get  /day14/demo1?name=zhangsan  HTTP /1.1

​                             *方法：

​                                    1、获取请求方式：GET

​                                          *String getMethod( )

​                                     2、获取虚拟目录：/day14             000

​                                           *String getContextPath( )
​                                     3、获取Servlet路径：/demo1
​                                           *String getServletPath( )

​                                      4、获取get方式请求参数：name=zhangsan

​                                           *String getQueryString( )

​                                      5、获取请求URI：/day14/demo1              0000

​                                           *String getRequestURI( );                       /day14/demo1

​                                           *StringBuffer  getRequestURL( )           :http://localhost/day14/demo1

​                                                  *URL:统一资源定位符

​                                                  *URI:统一资源标识符

​                                       6、获取协议及版本：HTTP/1.1

​                                            *String getProtocol( )

​                                        7、获取客户机的IP地址

​                                             *String getRemoteAddr( )

​                      Ⅱ、获取请求头数据

​                              *方法：

​                                       *String getGeader(String name):通过请求头的名称获取请求头的值           000	

​                                        *Enumeration<String> getHeaderNames( ):获取所有的请求头名称

​                        Ⅲ、获取请求体数据

​                                 *请求体：只有POST请求方式，才有请求体，在请求体中封装了POST请求的请求参数

​                                  *步骤：

​                                      1、获取流对象

​                                               *BufferedReader getReader( ):获取字符输入流，只能操作字符数据

​                                               *ServletInputStream getInputStream( ):获取字节输入流，可以操作所以类型数据

​                                        2、再从流对象中拿数据

​              2、其他功能：

​                    Ⅰ、获取请求参数的通用方式:不论get还是post都可以用下列方法请求参数

​                            1、String getParameter(String name):根据参数名称获取参数值       username=zs&password=123

​                            2、String[ ] getParameterValues(String name):根据参数名称获取参数的数组    hobby=xx&hobby=game

​                            3、Enumeration<String> getParameterNames( ):获取所以请求参数名称

​                             4、Map<String,String[ ]> getParameterMap( ):获取所以参数的map集合

​                                  *中文乱码问题：

​                                         *get方式:tomcat 8已经将get方式的乱码问题解决了

​                                          *post方式：会乱码   解决方法：

​                                             *在获取参数之前，设置request的编码req.setCharacterEncoding("utf-8");

​                     Ⅱ、请求转发：一种在服务器内部的资源跳转方式

​                             1、步骤

​                                    1、通过request对象获取请求器转发器对象：RequestDispatcher getRequestDispatcher(String path)

​                                    2、使用RequestDispatcher对象来进行转发：forward(ServletRequest request,ServletResponse response)

​                                                * 缩写：request.getRequestDispatcher("/body1").forward(request,response)

​                              2 、特点：

​                                     1、浏览器地址栏路径不发生变化

​                                     2、只能转发到当前服务器内资源中

​                                     3、转发是一次请求

​                      Ⅲ、共享数据：

​                              *域对象：一个有作业范围的对象，可以在范围内共享数据

​                               *request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据

​                               *方法：

​                                        1、void setAttribute(String name,Object obj);    存储数据

​                                         2、Object getAttribute(String name);     通过键获取值

​                                         3、void removeAttribute(String name);    通过建移除键值对

​                       Ⅳ、获取ServletContext

​                                *ServletContext getServletContext( );

​	