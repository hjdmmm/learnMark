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

使用两个注解

1. @ExceptionHandler
2. @ControllerAdvice

# 拦截器

拦截器需要实现HandlerInterceptor接口

拦截器是全局的，可以对多个Controller做拦截

拦截器执行时间：

1. 在请求处理之前，也就是Controller类中的方法执行之前先被拦截
2. 在控制器方法执行之后也会执行拦截器
3. 在请求处理完毕后也会执行拦截器

```java
//有返回值，返回值为真才会进入处理器方法
@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    System.out.println("拦截器的preHandler()");

    return true;
}


//在处理器方法之后执行，能够获取到处理器方法的返回值ModelAndView，可以对其修改
@Override
public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
    HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
}

//最后执行的方法，在请求处理完后执行，即对视图执行了forward后，一般做资源回收工作
@Override
public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
    HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
}
```

多个拦截器按照web.xml中的声明顺序执行

## 拦截器和过滤器

1. 过滤器是Servlet中的对象，拦截器是SpringMVC框架中的对象
2. 过滤器实现Filter接口中的对象，拦截器是实现HandlerInterceptor接口的对象
3. 过滤器是用来设置request，response的参数和属性的，侧重对数据过滤，用来设置字符编码等；拦截器用来验证请求，能截断请求，用来登录验证，权限检查等
4. 过滤器是在拦截器之前执行的
5. 过滤器是Tomcat服务器创建的对象，拦截器是SpringMVC容器创建的对象
6. 过滤器是一个执行时间点，拦截器有三个执行时间点
7. 过滤器可以处理jsp，js，html等，拦截器是侧重拦截Controller的对象，如果请求不能被中央调度器接收，不会执行拦截器内容

# SpringMVC请求处理流程

## 用户发起请求

## 中央调度器

作用：把请求转交给处理器映射器，并将完成接下来的各个对象之间的大部分传递工作(所以称为调度器)

## 处理器映射器

SpringMVC框架中的一种对象，框架把实现了HandlerMapping接口的类都叫映射器

作用：根据请求，从SpringMVC容器对象中获取处理器对象，框架把找到的处理器对象放到一个叫做处理器执行链的类(HandlerExecutionChain)保存

## 处理器执行链

类中保存着处理器对象，拦截器对象

作用：把处理器对象交给处理器适配器对象(多个)

## 处理器适配器

实现了HandlerAdapter接口

作用：执行处理器方法，即调用Controller对象的方法，得到返回值ModelAndView，将ModelAndView交给视图解析器

## 视图解析器

实现了ViewResolver接口，可以有多个

作用：组成视图完整路径，添加前缀后缀(如果需要的话)，并创建View对象(View对象指实现View接口的对象，框架中使用它表示视图)

## 视图类

如InternalResourceView类用来表示jsp文件，视图解析器遇到jsp后缀的文件时，就会创建一个InternalResourceView类对象，对象内有一个属性url存储着实际地址

## forward

以中央调度器为首的很多对象一起完成，调用视图类自己的方法，把Model数据放入request作用域，然后执行视图的forward()方法，请求处理完毕
