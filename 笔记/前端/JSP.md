# JSP简介

JSP规范来自于JAVAEE规范中的一种

JSP规范制定了如何开发JSP文件代替响应对象将处理结果写入到响应体的开发流程

JSP规范制定了Http服务器应该如何调用管理JSP文件

## 响应对象存在弊端

适合将数据量较少的处理结果写入到响应体

如果处理结果数量过多，使用响应体增加开发难度

## JSP优势

降低将处理结果写入到响应体开发工作量，降低处理结果维护难度

# 在JSP中写Java

```jsp
<%
	//在执行标记中写声明变量，表达式，控制语句
	int num1 = 10;
	int num2 = num1 - 10;
	if (num2 >= num1){
        
    }
	for (int i = 0; i < 10; i++){
        
    }
%>
<%=num1%> <!--输出标记-->
```

# Servlet与JSP分工

Servlet：负责处理业务并得到处理结果

JSP：不负责业务处理，不写复杂逻辑判断，只负责输出，主要任务将Servlet中处理结果写入到响应体

## 调用关系

Servlet工作完毕后，一般通过请求转发方式，向Tomcat申请调用JSP

## 数据共享

Servlet将处理结果添加到请求作用域对象，JSP文件在运行时从请求作用域对象得到处理结果

# Http服务器调用JSP文件步骤

1. Http服务器将JSP文件内容编辑为一个Servlet接口实现类(.java)
2. Http服务器将Servlet接口实现类编译成class文件(.class)
3. Http服务器负责创建这个class的实例对象，这个实例对象就是Servlet实例对象
4. Http服务器通过Servlet实例对象调用jsp_service方法，将jsp文件内容写入到响应体

# JSP四大作用域对象

1. ServletContext application 全局作用域对象
2. HttpSession session 会话作用域对象
3. HttpServletRequest request 请求作用域对象
4. PageContext pageContext 当前页作用域对象，这是JSP文件独有的作用域对象，Servlet中不存在，在当前页作用域对象存放的共享数据只能在当前JSP文件中使用，不能共享给其他Servlet或其他JSP文件，真实开发过程，主要用于JSTL标签与JSP文件之间数据共享

# JSP九大内置对象

包含四大作用域对象

| JSP九大内置对象 | 完整java类名                          |
| --------------- | ------------------------------------- |
| application     | javax.servlet.ServletContext          |
| pageContext     | javax.servlet.jsp.PageContext         |
| request         | javax.servlet.http.HttpServletRequest |
| session         | javax.servlet.http.HttpSession        |
| response        | javax.servlet.ServletContext          |
| out             | javax.servlet.jsp.JspWriter           |
| exception       | java.lang.Throwable                   |
| page            | this                                  |
| config          | javax.servlet.ServletConfig           |

# EL工具包

由Java技术开发的一个jar包

作用降低JSP文件开始时Java命令的开发强度

Tomcat服务器本身自带了EL工具包(Tomcat安装目录/lib/el-api.jar)

## .

EL表达式中的.xxx

有时是.getXxx()，如emp.xxx时

有时是.get("xxx")，如一个List/Map集合.xxx时

有时是.getParameter("xxx")，如param.xxx时

有时是.getAttribute("xxx")，如四个内置对象requestScope.xxx时

### 造成的误会

```html
<base href="${requestScope.scheme}://${requestScope.serverName}:${requestScope.serverPost}${requestScope.contextPath}/">
<!--实质上是执行了request.getAttribute("scheme")，与想要执行的getScheme()不一致-->

<!--应该用page当前页对象得到request对象，让el表达式将request当成一个对象处理使得执行 对象.xxx时，转为对象.getXxx()方法-->
<!--而这里又出现了同一个问题，page对象获得request对象需要调用getRequest()方法，但如果用pageScope就会调用getAttribute("request")，与我们想要的又不一致，所以我们转为使用pageContext-->
<base href="${pageContext.request.scheme}://${pageContext.request.serverName}:${pageContext.request.serverPost}${pageContext.request.contextPath}/">
```



## 命令格式

${作用域对象别名.共享数据}

作用：

1. EL表达式是EL工具包提供一种特殊命令格式(表达式命令格式)
2. EL表达式在JSP文件上使用
3. EL表达式负责在JSP文件上从作用域对象读取指定的共享数据并输出到响应体

EL表达式的特点：没有取到任何数据(包括数组越界时)则输出""(空字符串)

```jsp
<%//严格上说,下面${requestScope.usercode}等价于%>
<%=request.getAttribue("usercode") == null ? "" : request.getAttribute("usercode")%>
```

## 作用域对象别名

1. application ${applicationScope.共享数据名}
2. session ${sessionScope.共享数据名}
3. request ${requestScope.共享数据名}
4. pageContext ${pageScope.共享数据名}

pageContext < request < session < application

pageScope < requestScope < sessionScope < applicationScope

PS：这里的pageScope相当于pageContext的阉割版，只能执行getAttribute("xxx")方法

## 引用对象的属性

${作用域对象别名.共享数据名.属性名}

从作用域对象读取指定共享数据关联的引用对象的属性值，并自动将属性的结果写入到响应体

属性名一定要与引用对象属性名完全一致(大小写也要一致)

本质上是调用了getXxx()方法，底层肯定运用了反射机制，也就是说如果你的属性名叫a，但是写了getB(return A;)方法，也要${empObj.b}才能拿到A，这启示我们Java一些约定俗成的命名规范是必须遵守的

EL表达式没有提供遍历集合方法，因此无法从作用域对象读取集合内容输出(其实这样说是错的，比如下面的List和Map中取值就打脸了)

## EL表达式简化版

${共享数据名}

EL表达式允许开发人员开发时省略作用域对象别名

首先到pageContext，然后到request，再到session，再到application，都没有返回null

缺点：容易降低程序执行速度，容易导致数据定位错误

设计目的：简化从pageContext读取共享数据并输出难度

## 从请求包中读取参数



**区分从域对象中取值，and，拿请求包中的参数内容**



${param.请求参数名}，param不能省

从通过请求对象读取当前请求包中请求参数内容，并将请求参数内容写入到响应体

代替一长串命令：

```jsp
index.jsp 发送请求：http://localhost:8080/myWeb/index.jsp?userName=mike&password=123

<%
	String userName = request.getParameter("userName");
	String password = request.getParameter("password");
%>
<%=userName%>
<%=password%>
```

---

${paramValues.请求参数名[下标]}

如果浏览器发送的请求参数是一个请求参数关联多个值，此时可以通过paramValues读取请求参数下指定位置的值并写入到响应体

代替命令：

```jsp
<!--
http://localhost:8080/myWeb/index_2.jsp?pageNo=1&pageNo=2&pageNo=3
此时pageNo请求参数在请求包中以数组形式存在
pageNo:[1,2,3]
-->
<%
	String array[] = request.getParameterValues("pageNo");
%>
第一个值:<%=array[0]%> ...
```

## List和Map集合中读取

```jsp
<%
List<emp> empList new ArrayList<>();
empList.add(e1);
empList.add(e2);
request.setAttribute("empList", empList);
%>
${empList[0].empno}
${empList[1].empno}

<%
Map<string,Emp> empMap = new HashMap<>();
empMap.put("a", e1);
empMap.put("b", e2);
request.setAttribute("empMap", empMap);
%>
<%//本质上是empMap.get("a").getEmpno%>
${empMap.a.empno}
${empMap.b.empno}
```

## 常见运算
### +

```jsp
${1+1} <!--2-->
${"1"+1} <!--2-->
${1+"1"} <!--2-->
${"1"+"1"} <!--2-->
${"abc" + "1"} <!--报错-->
```

EL表达式中的加号只能做加法运算，加号两边会强制转为数字，不会字符串拼接

### ==(eq)

EL中调用equals()方法，与java中直接比较内存地址不一样

### empty

判断是否为空，EL认为"没有"就是空

```jsp
<%
List<String> myList = ArrayList<>();
request.setAttribute("myList", myList);
%>

${empty myList} <!--输出true-->
${not empty myList} <!--输出false-->
```

## 常见异常

PropertyNotFoundException

# JSTL

Jsp Standard Tag Library jsp标准标签库

作用是使用标签代替java语句，解决了纯EL表达式不能遍历集合等问题，用EL+JSTL基本可以替代jsp中的纯java语句

JSTL标准是sun制定的，apache实现了，sun收录了apache的实现

JavaEE5.0版本后，jstl相关jar包自带

JSTL使用的变量一般都放在pageContext中

## 步骤

1. 在项目中(web-INF/lib)引入jstl相关jar包

2. ```jsp
   <%@taglib prefix="c" uri="http://java.sun.com.jsp/jstl/core"%>
   ```

## 常见标签

c:choose，模拟else if

```jsp
<c:choose>
	<c:when test="${param.age < 5}">婴幼儿</c:when>
    <c:when test="${param.age < 18}">少年</c:when>
    <c:when test="${param.age < 35}">青年</c:when>
    <c:otherwise>老年</c:otherwise>
</c:choose>
```



c:forEach，模拟for循环

```jsp
<c:forEach begin="1" end="10" step="1" var="i">${i}</c:forEach>

<!--将以上代码翻译为jsp语句-->
<%
for (int i = 1; i <= 10; i++){
    pageContext.setAttribute("i", i);
%>
	<%=pageContext.getAttribute("i")%> <!--或${i}-->
<%
}
%>
```
模拟数组和集合的foreach循环

```jsp
<c:forEach items="${empList}" var="emp" varStatus="empStatus">
	${empStatus.count}<!--从1开始-->, ${emp.empno}, ${emp.ename}<br/>
</c:forEach> 
```

c:forTokens，字符串切割变成数组

```jsp
<c:forTokens items="${initParam.ips}" delims="," var="ip">
	${ip}<br/>
</c:forTokens>
```

## 函数

函数是对EL表达式的补充，属于JSTL的一部分，对应fn.tld文件

函数也是联合EL表达式来代替JSP中的java代码

导入

```jsp
<%@taglib prefix="fn" uri="http://java.sun.com.jsp/jstl/functions"%>
```

内置函数使用
```jsp
fn:contains("hello.java", "hello")
```

### 自定义标签

1. 在WEB-INF下新建xxx.tld

2. 编写配置文件

   ```html
   <desciption>EGOV 1.0 functions library</desciption>
   <display-name>EGOV functions</display-name>
   <tlib-version>1.0</tlib-version>
   <uri>http://www.hjdmmm.com/jsp/jstl/jstl/functions</url>
   
   <function>
       <name>getTextByCode</name>
       <function-class>com.hjdmmm.egov.util.StringUtil</function-class>
       <function-signature>java.lang.String getTextByCode(java.lang.String)</function-signature>
   </function>
   ```

3. 编写对应类，在该类中编写对应的public方法

