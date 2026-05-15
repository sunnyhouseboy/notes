EL（Expression Language）表达式     用于简洁jsp中的Java代码

一、主要功能：获取数据

二、语法：1、${expression}

​                    2、< <c:if>>:相当于if语句

```
<c:if test="true">
  <h1>true</h1>
</c:if>
```

​                   3、<<c:forEach>>相当于for循 环

<c:forEach items="${brands}" var="brand">

​     <tr align="center">

​         <td>${brand.id}</td>

​        <td>${brand.brandName}</td>

​        <td>${brand.companyName}</td>

​        <td>${brand.description}</td>

​     </tr>

<<c:forEach>>