# SpringMVC概述

SpringMVC是基于spring的一个框架，实际上就是spring的一个模块，专门做web开发的，理解为是servlet的一个升级

web开发底层是servlet，SpringMVC底层也是servlet，框架是在servlet基础上加入一些功能

SpringMVC就是一个spring，spring是容器，ioo能够管理对象，使用bean标签，@Component，@Repository，@Service，@Controller

SpringMVC能够创建对象，放入到容器中，springMVC容器中放的是控制器对象

## Servlet

原生的spring的@Controller注解创建的是一个普通类对象，不是Servlet。但是SpringMVC赋予了控制器对象一些额外的功能

SpringMVC中有一个对象DispatcherServlet(中央调度器)是一个Servlet，用户把请求发给

DispatcherServlet之后，它把请求转发给我们自己创建的Controller对象，最后Controller对象处理请求

# web.xml

```xml
<servlet>
    <!--声明中央调度器，它初始化会执行init()方法，创建容器读取配置问卷，并把容器对象放入ServletContext中-->
    <servlet-name>myweb</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    
    <!--springmvc配置文件的位置-->
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:springmvc.xml</param-value>
    </init-param>
    
    <!--在tomcat启动后，创建Servlet对象-->
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>myweb</servlet-name>
    <!--设置需要应用的资源地址-->
    <url-pattern>*.do</url-pattern>
</servlet-mapping>
```

# 视图解析器

视图解析器，帮助开发人员设置视图文件的路径

```xml
<!--spring配置文件-->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view/"/>
    <property name="suffix" value=".jsp"/>
</bean>
```

# @RequestMapping

重要注解，加在方法上

value属性：{"/some.do", "/other.do"}，Servlet映射地址

method属性：RequestMethod.GET等，用于指定接收哪种方式的请求

# 处理器方法的参数

HttpServletRequest request, HttpServletResponse response, HttpSession session

这三种常见的

还可以继续接用户提交的参数，如String name, Integer  age，保证方法参数名和用户提交参数名一致

实际上框架是进行了request.getParameter("name"), Integer.valueOf(request.getParameter("age"))

## @RequestParam

当请求中参数名和处理器方法的形参名不一样时，使用@RequestParam，用在处理器方法形参类型的前面，如@RequestParam("stu_name") String stuName

value属性：请求参数名

required属性：请求中必须包含该参数

## 对象接收参数

逐个接收在参数多的时候不好

创建一个vo类，类中的属性名与请求参数名一致，在处理器方法参数中创建对象

支持有多个不同类的对象，springMVC会按照对象属性名和参数名同名的原则赋值

# 解决post乱码

```xml
<filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceRequestEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
    <init-param>
        <param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>

<filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

# 处理器方法的返回值

## ModalAndView

处理器方法处理完后，需要跳转到其他资源，而且又要在跳转资源间传递数据，就用ModalAndView

常用方法addObject()，setViewName()

## Spring

只跳转视图，不涉及数据传递

可以是逻辑名称(配置了视图解析器时)，也可以是完整视图路径(未配置了视图解析器时)

```java
return "/WEB-INF/view/show.jsp"
```

---

也可以只传递数据，不跳转视图

区分就是这时有@ResponseBody注解，有@ResponseBody就是数据，没有就是视图

## void

既不传递数据，也不跳转视图

一般用来处理ajax请求，ajax返回结果需要通过HttpServletResponse的对象response借一个PrintWriter来输出结果

## Object

返回的Object表示数据，与视图无关

一般用来返回json对象，比void写法更好：

1. 加入json工具库依赖，springmvc默认使用jackson
2. springmvc配置文件中加入mvc:annotation-driven标签(注解驱动)，作用是转换为将java对象转换为json对象
3. 在处理器方法的上面加入@ResponseBody，作用是向response输出json对象

json数组返回值为List即可

# 静态资源

如果设置中央调度器的url-pattern是"/"，将导致禁用Tomcat的DefaultServlet，使得静态资源(图片，js，html等)404，因为中央调度器没有能力处理静态资源

两种解决方法：

1. 在springmvc配置文件中，加上mvc:default-servlet-handler和mvc:annotation-driven两个标签，这种方式依赖于服务器自带的Servlet
2. mvc:resources标签，mapping属性是访问静态资源的uri地址，通常使用通配符**，location属性静态资源在项目中的目录位置

# 重定向和请求转发

```java
//视图解析器此时失效
//缺省时默认是请求转发
mv.setViewName("forward:/WEB-INF/view/show.jsp"); //转发

//下面的实际上浏览器地址栏会出现.../WEB-INF/view/show.jsp?1=1&2=2，参数是框架提供的额外功能
mv.addObject("1", 1);
mv.addObject("2", 2);
mv.setViewName("redirect:/WEB-INF/view/show.jsp"); //重定向
```

# 异常处理

springmvc采用的是统一全局的异常处理，把controller中所有的异常处理都集中到一个地方，采用的是aop思想
