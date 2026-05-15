**会话控制Cookie和Session**

Cookie:
        1. 保存在浏览器本地
                2. 数据形式为键值对形式
                3. 有且只支持英文，并且不允许出现空格
                        4. 数据量存储有限制，一般浏览器允许最大Cookie个数为200，单一网站允许自带Cookie为90左右，单一Cookie数据占用空间，在2KB以内。
                        5.cookie大小时有限制的。通常 4096byte 。因为技术的更新可以存8192byt
            3. Session:
                        4. 数           1. 保存在服务器端内容
                        1. 、据保存形式是【属性键值对】形式
                                2. 数setAttribute(String name, Object obj);
                    Object getAttribute(String name);            
                    removeAttribute(String name);
                3. 对应的数据可以是任意类型，任意情况，不限大小，并且支持中文

        4. 数据量没有限制，但是在业务逻辑要求过程中，保存核心数据内容。
            用户名字。用户ID号，用户权限/等级ID、
            
            1.4 Session和Cookie对比
                1. 数据保存在服务器，对于浏览器压力较小，如果浏览器访问服务器想要使用对应的Session只要求保存对应sessionID即可
                2. cookie保存的数据类型单一，只能保存字符串类型的数据 ,Session可以保存任意类型数据，数据保存形式是键值对形式。
                3. cookie的大小时存在限制的
                4.cookie在浏览器中存的数据是有限制的，键值对300
                5. Session可以在服务器硬盘中保存，同时也可以在服务器内存中存储。
                6. Session也是一个【域对象】
            
            Session更有优势，但是session如果没有cookie的介入，就会显得很繁琐。
               1.使用session的时候一般要开启cookie
            
                2.如果浏览器没有开启cookie功能，咱们通过java url传入参数的形式来完成的session使用。

