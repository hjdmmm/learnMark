# 概述

## 计算机网络

是指地理位置不同的具有独立功能的多台计算机及其外部设备，通过通信线路连接起来，在网络操作系统、网络管理软件及网络通信协议的管理和协调下，实现资源共享和信息传递的计算机系统

javaweb：网页编程

TCP/IP：网络编程

## 互联网通信

角色划分：

1. 客户端计算机：用于发送请求，来索要资源的计算机
2. 服务端计算机：用于接收请求，并提供对应的资源文件的计算机

互联网通信模型：

1. C/S通信模型：client software客户端软件，专门安装在客户端上，帮助客户端计算机向指定服务端计算机发送请求，索要资源文件，解析服务器发送的二进制数据为各种类型文件；server software服务器软件，专门安装在服务端上，接收来自于特定客户端软件发送请求，定位被访问的资源文件，将其内容解析为二进制数据，通过网络发送回客户端。使用场景：个人娱乐市场、企业办公应用较少。优点：安全性较高、有效降低服务端；缺点：增加客户获得服务的成本、更新较为繁琐
2. B/S通信模型：Browser浏览器，安装在客户端，可以向任意的服务器发送请求索要资源文件，将服务器返回的二进制数据解析为各种文件；server software服务器软件，同上。使用场景：既适用于个人娱乐市场、又广泛适用于企业日常活动。优点：不会增加用户获得服务的成本、几乎不需要更新的浏览器；缺点：几乎无法有效对服务端计算机资源文件进行保护、服务器计算机工作压力巨大

## 共享资源文件

可以通过网络进行传输的文件，也就是所有文件

Http下服务器对于共享资源文件分类：静态动态文件、动态资源文件

### 静态动态文件

文件内容是固定的：文档、图片、视频

文件中存放的是命令：.html、.css、.js

### 动态资源文件

文件中存放的是命令，并且命令不能在浏览器中执行，只能在服务端计算机编译执行

.class

### 区别

静态文件被索要时，Http服务器直接通过输出流，将静态文件中内容或命令以二进制方式推送给发起请求的服务器

动态文件被索要时，Http服务器需要创建当前class文件的实例对象，通过实例对象调用对应的方法处理用户请求，Http服务器负责将方法运行结果以二进制形式推送回发送请求服务器

## 控制浏览器发送的请求地址(三要素)：

1. 控制浏览器发送的请求地址
2. 控制浏览器发送请求方式
3. 控制浏览器发送请求携带参数

## 控制浏览器接受结果行为：

1. 控制浏览器才用对应的"编译器"将接受的二进制数据解析为文字、视频、图片、命令
2. 控制浏览器将解析内容或命令进行执行或者展示(全局刷新展示/局部刷新展示)
3. 控制用户与浏览器之间交流(js--->Jqury)

# 网络协议包

1. 在网络中传递信息都是以二进制形式存在的
2. 接收方(浏览器/服务器)在收到信息后，第一件事就是将二进制数据进行编译[文字、图片、视频、命令]
3. 传递信息数据量往往巨大，导致接收方很难在一组连续的二进制中得到相应数据
4. 网络协议包是一组有规律的二进制数据，在这组数据存在了固定空间，每一个空间专门存放特定信息，这样接收方在接受网络协议之后，就可以到固定空间得到相应信息，网络协议包出现极大降低了接收方对接收二进制数据的编译难度

0000(ip地址)0000(端口号)0000(资源文件名)0000...

常见的网络协议包：FTP网络协议包、Http网络协议包

## Http网络协议包

在基于B/S结构下互联网通信过程中，所有在网络中传递信息都是保存在Http网络协议包

分类：Http请求协议包、Http相应协议包

### Http请求协议包

在浏览器准备发送请求时，负责创建(不准确，按此理解)一个Http请求协议包，浏览器将请求信息以二进制形式保存在Http请求协议包各个空间中，由浏览器负责将Http请求协议包推送到指定服务端计算机

#### 内部空间

按照自上而下划分有4个：

请求行：[url:请求地址 method:请求方法(post/get)]

请求头：[请求参数信息(用get时)]

空白行：[没有任何内容，起到隔离作用]

请求体：[请求参数信息(用post时)]

### Http响应协议包

Http服务器在定位到被访问的资源文件后，负责创建一个Http响应协议包，Http服务器将定位文件内容或文件命令以二进制形式写入到Http服务器负责将Http响应协议包推送回发起请求的浏览器上

#### 内部空间

按自上而下的顺序也有4个

状态行：[Http状态码]

响应头：[content-type:指定浏览器采用对应编译器对响应体二进制数据进行解析]

空白行：[没有任何内容，起到隔离作用]

响应体：[可能是被访问的静态资源文件内容、静态资源文件明令、动态资源文件运行结果，当然均以二进制形式存在]

# Http服务器

JBOSS服务器、Glassfish服务器、Websphere服务器(强大)、Tomcat服务器

# 网站内部结构

src文件夹：存放作为动态资源文件的Java文件

web文件夹：存放作为静态资源文件

# servlet规范

## 简介

servlet规范来自于JavaEE规范中的一种

作用：

1. 在servlet规范中，指定动态资源文件的开发步骤
2. 在servlet规范中，指定Http服务器调用动态资源文件的规则
3. 在servlet规范中，指定Http服务器管理动态资源文件实例对象规范

## servlet接口实现类

servlet接口来自于servlet规范下的一个接口，存在于Http服务器提供的jar包

Tomcat服务器下lib文件有一个servlet-api.jar存放servlet接口(javax.servlet.Servlet接口)

servlet规范中，Http服务器能调用的动态资源文件必须是一个Servlet接口的实现类

### 开发步骤

1. 创建一个Java类继承HttpServlet父类，使之成为一个Servlet接口实现类

   不直接实现Servlet接口，不用实现接口全部方法，体现抽象类降低接口实现类对接口实现过程中难度的功能，将接口中不需要使用抽象方法交给抽象类完成

   Servlet接口：

   ​	init()、getServlet()、getServletInfo()、destory()四个方法没用

   ​	Tomcat通过实例对象

2. 重写HttpServlet父类两个方法 doGet()或doPost()

   通过父类决定在何种情况下调用子类的方法，属于模板设计模式

   HttpServlet：service(){if(请求方式==get) this.doGet(); else if (请求方式==post){this.doPost();}}

   OneServlet：重写doGet()、doPost()

3. 将Servlet接口实现类信息注册到Tomcat服务器

   网站-->web-->WEB-INF-->web.xml

   ``` html
   <!--将Servlet接口实现类路径地址交给Tomcat-->
   <servlet>
   	<servlet-name>mm</servlet-name> <!--声明一个变量存储Servlet接口实现类路径-->
       <servlet-class>com.hjdmmm.controller.OneServlet</servlet-class> <!--存储Servlet接口实现类路径-->
   </servlet>
   <!--
   Tomcat就会String mm = "com.hjdmmm.controller.OneServlet";
   为了降低用户访问Servlet接口实现类难度，需要设置简短请求别名
   -->
   <servlet-mapping>
   	<servlet-name>mm</servlet-name>
       <url-pattern>/one</url-pattern> <!--设置简短请求别名，必须以/开头-->
   </servlet-mapping>
   <!--
   如果现在浏览器想要向Tomcat索要OneServlet地址时
   http://localhost:8080/myWeb/one
   -->
   ```


## Servlet对象生命周期

1. 网站中所有Servlet接口实现类的实例对象，只能由Http服务器负责创建，开发人员不能手动创建Servlet接口实现类的实例对象

2. 在默认情况下，Http服务器接收到对于当前Servlet接口实现类第一次请求时自动创建这个Servlet接口实现类的实例对象

   在手动配置情况下，要求Http服务器在启动时自动创建某个Servlet接口实现类的实例对象

   ```xml
   <sevlet>
   	<servlet-name></servlet-name>
       <servlet-class></servlet-class>
       <load-on-startup>写一个自然数，越小优先级越高</load-on-startup><!--加上这一句会让服务器在启动时就创建Servlet对象实例-->
   </sevlet>
   ```

   

3. 在Http服务器运行期间，一个Servlet接口实现类只能被创建出一个实例对象

4. 在Http服务器关闭时刻，自动将网站中所有Servlet对象销毁

## HttpServletResponse接口

HttpServletResponse接口来自于Servlet规范中，在Tomcat中存在于servlet-api.jar

实现类依然是由Http服务器负责提供

负责将doGet/doPost方法执行结果写入到响应体交给浏览器

开发人员习惯于将HttpServletResponse接口修饰的对象称为响应对象

### 主要功能

1. 将执行结果以二进制形式写入到响应体
2. 设置响应头中[content-type]属性值，从而控制浏览器使用对应编译器将响应体二进制数据编译为文字、图片、视频、命令
3. 设置响应头中[location]属性，将一个请求地址赋值给location，从而控制浏览器向指定服务器发送请求

## HttpServletRequest接口

HttpServletRequest接口来自于Servlet规范中，在Tomcat中存在于servlet-api.jar

实现类依然是由Http服务器负责提供

负责将doGet/doPost方法运行时读取Http请求协议包中信息

开发人员习惯于将HttpServletRequest接口修饰的对象称为请求对象

### 主要作用

1. 可以读取Http请求协议包中请求行的信息
2. 可以读取保存在Http请求协议包中请求头或请求体中请求参数信息
3. 可以代替浏览器向Http服务器申请资源文件调用

## 请求对象与响应对象的生命周期

1. 在Http服务器接收到浏览器发送的Http请求协议包之后，自动为当前的Http请求协议包生成一个请求对象和一个响应对象
2. 在Http服务器调用doGet()和doPost()方法时，负责将请求对象和响应对象作为实参传递到方法，确保doGet()和doPost()正确执行
3. 在Http服务器准备推送Http响应协议报之前，负责将本次请求关联的请求对象和响应对象销毁

请求对象和响应对象生命周期贯穿一次请求的处理过程

请求对象和响应对象相当于用户在服务端的代理人

# 欢迎资源文件

用户可以记住网站名，但是不会记住网站资源文件名

默认欢迎资源文件：

用户发送了一个针对某个网站的默认请求时，此时由Http服务器自动从当前网站返回的资源文件

(全局设置)Tomcat对于默认欢迎资源文件的定位规则，在conf/web.xml的welcome-file-list下

某一个的网站在网站文件夹/web/WEB-INF/web.xml下

# Http状态码

由三位数字组成的一个符号

Http服务器在推送响应包之前，根据本次请求处理情况，将Http状态码写入到响应包中状态行上

如果Http服务器针对本次请求，返回了对应的资源文件，通过Http状态码通知浏览器应该如何处理这个结果

如果Http服务器针对本次请求，无法返回对应的资源文件，通过Http状态码向浏览器解释不能提供服务的原因

组成：100-599之间

## 分类

1. 1XX：最有特征100：通知浏览器本次返回的资源文件并不是一个独立的资源文件，需要浏览器在接收到响应包之后，继续向Http服务器索要依赖的其他资源文件

2. 2XX：最有特征200：通知浏览器本次返回的资源文件是一个完整独立资源文件，浏览器在接收到之后不需要索要其他关联文件

3. 3XX：最有特征302：通知浏览器本次返回的不是一个资源文件内容，而是一个资源文件地址，需要浏览器根据这个地址自动发起请求来索要这个资源文件

4. 4XX：404：通知浏览器，由于在服务端没有定位到被访问的资源文件，因此无法提供帮助

   405：通知浏览器，在服务端已经定位到被访问的资源文件(Servlet)，但是这个Servlet对于发送的请求方式无法处理

5. 5XX：500：通知浏览器，在服务端已经定位到被访问的资源文件(Servlet)，这个Servlet可以接收浏览器采用请求方式，但是Servlet在处理请求期间，出现Java异常

# 多个Servlet之间调用规则

1. 前提条件：某些来自于浏览器发送请求，往往需要服务端中多个Servlet协同处理，但是浏览器一次只能访问一个Servlet，导致用户需要手动通过哦浏览器发起多次请求才能得到服务，这样增加用户获得服务难度，导致用户放弃访问当前网站
2. 提高用户使用感受规则：无论本次请求涉及到多少个Servlet，用户只需要手动通知浏览器发起一次请求即可
3. 多个Servlet之间的调用规则：重定向解决方案、请求转发解决方案

## 重定向解决方案

原理：用户第一次手动方式通知浏览器访问OneServlet，OneServlet工作完毕后，将TwoServlet地址写入到响应头location，并导致Tomcat将302状态码写入状态行；浏览器接收到响应包，读取到了302，立刻自动根据响应头中location属性地址发起第二次请求，访问TwoServlet去完成请求中剩余的任务

命令：response.sendRedirect("请求地址")

特征：

1. 请求地址：既可以把当前网站内部的资源地址发送给浏览器，又可以把其他网站资源文件地址发送给浏览器("https://baidu.com")
2. 请求次数：浏览器至少发送两次请求，但是只有第一次请求是用户手动发送的
3. 请求方式：重定向解决方案中，通过地址栏通知浏览器发起下一次请求，因此通过重定向解决方案调用的资源文件接收的请求方式一定是get
4. 缺点：重定向解决方案需要在浏览器与服务器之间进行多次往返，大量时间消耗在往返次数上，增加用户等待服务时间

## 请求转发解决方案

**转发使用的是一种特殊的绝对路径，这种绝对路径前面不加/项目名，这种路径也称之为内部路径；而重定向使用的是正常的绝对路径，需要加/项目名。这样设计的原因是重定向可以到容器任一个web应用的url，而请求转发只能到当前web应用下的url**

1. 原理：用户第一次通过手动的方式要求浏览器访问OneServlet，OneServlet工作完毕后，通过当前的请求对象代替浏览器，向Tomcat发送请求，申请调用TwoServlet，Tomcat在接收到这个请求之后，自动调用TwoServlet来完成剩余任务

2. 实现命令：请求对象代替浏览器向Tomcat发送请求

   ```java
   //1. 通过当前请求对象生成资源文件申请报告对象
   RequestDispatcher report = request.getRequestDispatcher("/资源文件名"); //一定要以/开头
   //2. 将报告对象发送给Tomcat
   report.forward(当前请求对象, 当前响应对象);
   ```

3. 优点：

   1. 无论本次请求涉及到多少个Servlet，用户只需要手动通过浏览器发送一次请求
   2. Servlet之间调用发生在服务端计算机上，节省服务端与浏览器之间往返次数，增加处理服务速度

4. 特征：

   1. 请求次数：在请求转发过程中，浏览器只发送一次请求

   2. 请求地址：只能向Tomcat服务器申请调用当前网站下资源文件的地址

      ```java
      request.getRequestDispatcher("/资源文件名")     //不要写网站名
      ```

   3. 请求方式：在请求转发过程中，浏览器只发送了一个Http请求协议包，参与本次请求的所有Servlet共享同一个请求协议包，因此，这些Servlet接受的请求方式与浏览器发送的请求方式保持一致


## 使用场景

若要在服务器通过request内部通信，必不能使用重定向，因为重定向会让浏览器重新发一次request，原来的request就会被销毁，你在1.servlet中存进request的文件必不能被2.jsp收到，这样2.jsp就没有东西展示了



# Servlet规范中提供四种数据共享方案

数据共享：OneServlet工作完毕后，将产生数据交给TwoServlet来使用

多个Servlet之间数据共享实现方案

## ServletContext接口
来自于Servlet规范中的一个接口，在Tomcat中存在servlet-api.jar
在Tomcat中负责提供这个接口实现类
如果两个Servlet来自于同一个网站，彼此之间通过网站的ServletContext实例对象实现数据共享
开发人员习惯于将ServletContext对象称为全局作用域对象
工作原理：每一个网站都存在一个全局作用域对象，这个全局作用域对象相当于一个Map，在这个网站中OneServlet可以将一个数据存入到全局作用域对象，当前网站中其他Servlet此时都可以从全局作用域对象得到这个数据进行使用
全局作用域对象生命周期：在Http服务器启动过程中，自动为当前网站在内存中创建一个全局作用域对象；在一个网站启动过程中，一个网站只有一个全局作用域对象；在Http服务器运行期间，全局作用域对象一直处于存活状态；在Http服务器准备关闭的时候，负责将当前网站中的全局作用域对象进行销毁处理。总而言之，全局作用域对象生命周期贯穿网站整个运行期间
命令实现：同一个网站OneServlet将数据共享给TwoServlet

``` java
OneServlet{
public void doGet(HttpServletRequest request, HttpServletResponse response){
           //1.通过请求对象向Tomcat索要当前网站中全局作用域对象
           ServletContext application = request.getServletContext();
           //2.将数据添加到全局作用域对象作为共享数据
           application.setAttribute("key1", value);
       }
   }
   
   TwoServlet{
       public void doGet(HttpServletRequest request, HttpServletResponse response){
           //1.通过请求对象向Tomcat索要当前网站中全局作用域对象
           ServletContext application = request.getServletContext();
           //2.从全局作用域对象得到指定关键字对应的数据
           Object o = application.getAttribute("key1");
       }
   }
```

## Cookie类

Cookie来自于Servlet规范中一个工具类，存在于Tomcat提供servlet-api.jar中

如果两个Servlet来自于同一个网站，并且为同一个浏览器/用户提供服务，此时借助于Cookie对象进行数据共享

Cookie存放当前用户的私人数据，在共享数据过程中提高服务质量

在现实生活场景中，Cookie相当于用户在服务端得到会员卡

原理：用户通过浏览器第一次向myWeb网站发送请求申请OneServlet，OneServlet在运行期间创建一个Cookie存储与当前用户有关的数据，OneServlet工作完毕后，将Cookie写入到响应头交还给当前浏览器，浏览器收到响应包之后，将Cookie存储在浏览器的缓存一段时间之后，用户通过同一个浏览器再次向myWeb网站发送请求申请TwoServlet时，浏览器需要无条件的将myWeb网站之前推送过来的Cookie，写入到请求头发送过去

实现命令：同一个网站OneServlet与TwoServlet借助于Cookie实现数据共享

```java
OneServlet{
	public void doGet(HttpServletRequest request, HttpServletResponse response){
           //1.创建一个Cookie对象，保存共享数据(当前用户数据)
           Cookie card = new Cookie("key1", "abc");
           Cookie card1 = new Cookie("key2", "efg");
           /*
           cookie相当于一个map
           一个coookie只能存放一个键值对
           这个键值对的key与value只能是String
           键值对的key不能是中文
           */
           //2.将Cookie写入到响应头，交给浏览器
           response.addCookie(card);
           response.addCookie(card1);
       }
   }
TwoServlet{
	public void doGet(HttpServletRequest request, HttpServletResponse response){
           //1.调用请求对象从请求头得到浏览器返回的Cookie
           Cookie cookieArray[] = request.getCookies();
           //2.循环遍历数据得到每一个Cookie的key与value
           for  (Cookie card : cookieArray){
               String key = card.getName();
               String value = card.getValue();
               //提供服务
           }
       }
   }

```

存活周期：默认情况下，Cookie对象存放在浏览器的缓存中，因此只要浏览器被关闭，Cookie对象就被销毁掉；但是在手动设置的情况下，Cookie可以存放在客户端计算机硬盘上，这需要指定存活时间cookie.setMaxAge(秒);

## HttpSession接口

介绍

1. HttpSession接口来自于Servlet规范下的一个接口，存在于Tomcat中servlet-api.jar，其实现类由Http服务器提供，Tomcat提供实现类存在于servlet-api.jar
2. 如果两个Servlet来自于同一个网站，并且为同一个浏览器提供服务，此时借助于HttpSession对象进行数据共享
3. 开发人员习惯于将HttpSession接口修饰对象称为会话作用域对象


与Cookie区别

1. 存储位置：一个在天上，一个在地上

   Cookie：存储在客户端计算器中；HttpSession：存放在服务端计算机内存

2. 数据类型：Cookie对象存储共享数据类型只能是String，HttpSession对象可以存储任意类型的共享数据Object

3. 数据数量：一个Cookie对象只能存储一个共享数据；HttpSession使用map集合存储共享数据，所以可以存储任意数量共享数据

4. 参照物：Cookie相当于客户在服务端会员卡；HttpSession相当于客户在服务端私人保险柜

命令实现：在同一个网站下OneServlet将数据传递给TwoServlet

```java
OneServlet{
    public void doGet(HttpServletRequest request, HttpServletResponse response){
        //1.调用请求对象向Tomcat索要当前用户在服务器的私人储物柜
        HttpSession session = request.getSession();
        //2.将数据添加到用户私人储物柜
        session.setAttribute("key1", 共享数据);
    }
}

//浏览器访问/myWeb中TwoServlet
TwoServlet{
    public void doGet(HttpServletRequest request, HttpServletResponse response){
        //1.调用请求对象向Tomcat索要当前用户在服务端的私人储物柜
        HttpSession session = request.getSession();
        //2.从会话作用域对象得到OneServlet提供的共享数据
        Object 共享数据 = session.getAttribute("key1");
    }
}
```

Http服务器通过Cookie将用户与HttpSession关联起来

getSession()与getSession(false)：

getSession(false)如果当前用户在服务端没柜子，就不接待了Tomcat返回null

HttpSession销毁时机：

1. 用户与HttpSession关联时使用的Cookie只能存放在浏览器缓存中

2. 在浏览器关闭时，意味着用户与他的HttpSession关系被切断

3. 由于Tomcat无法检测浏览器何时关闭，因此浏览器关闭时并不会导致Tomcat将浏览器关联的HttpSession进行销毁

4. 为了解决这个问题，Tomcat为每一个HttpSession对象设置空闲时间，这个空闲时间默认是30分钟，如果当前HttpSession对象空闲时间达到30分钟，此时Tomcat认为用户已经放弃了自己的HttpSession，此时Tomcat就会销毁掉这个HttpSession

5. 手动设置HttpSession空闲时间：在当前网站web.xml下

   ```xml
   <session-config>
   	<session-timeout>5</session-timeout><!--当前网站中每一个session最大空闲时间5分钟-->
   </session-config>
   ```

## HttpServletRequest接口

在同一个网站中，如果两个Servlet之间通过请求转发方式调用，彼此之间共享一个请求协议包，而一个请求协议包只对应一个请求对象，因此servlet之间共享同一个请求对象，此时可以利用这个请求对象在这两个servlet之间实现数据共享

在请求对象实现servlet之间数据共享功能时，开发人员将请求对象称为请求作用域对象

命令实现：OneServlet通过请求转发申请调用TwoServlet时，需要给TwoServlet提供共享数据

```java
OneServlet{
    public void doGet(HttpServletRequest request, HttpServletResponse response){
        //1.将数据添加到请求作用域对象中attribute属性
        request.setAttribue("key1", 数据); //数据类型为Object
        //2.向Tomcat申请调用TwoServlet
        request.getRequestDispatcher("/two").forward(request, response);
    }
}
TwoServlet{
    public void doGet(HttpServletRequest request, HttpServletResponse response){
        //从当前请求对象得到OneServlet写入到共享对象
        Object 数据 = request.getAttribute("key1");
    }
}
```

# 监听器接口

一组来自于Servlet规范下的接口，共有8个接口，在Tomcat存在servlet-api.jar包

监听器接口需要由开发人员亲自实现，Http服务器提供jar包并没有对应的实现类

监听器接口用于监控作用域对象生命周期变化时刻以及作用域对象共享数据变化时刻

## 作用域对象

在Servlet规范中，认为在服务端内存中可以在某些条件下为两个Servlet之间提供数据共享方案的对象

Servlet规范下作用域对象：

1. ServletContext：全局作用域对象，江湖人称application
2. HttpSession：会话作用域对象
3. HttpServletRequest：请求作用域对象

## 开发规范(三步)

1. 根据监听的实际情况，选择对应监听器接口进行实现
2. 重写监听器接口声明，监听事件处理方法
3. 在web.xml文件将监听器接口实现类注册到Http服务器

## ServletContextListenner接口

作用：合法地检测全局作用域对象被初始化时刻以及被销毁时刻

监听事件处理方法：

public void contextInitlized() : 在全局作用域对象被Http服务器初始化被调用

public void contextDestory() : 在全局作用域对象被Http服务器销毁被调用

## ServletContextAttributeListener接口

作用：通过这个接口合法地检测全局作用域对象共享数据变化时刻

监听事件处理方法：

public void contextAdd()：在全局作用域对象添加共享数据

public void contextReplace()：在全局作用域对象更新共享数据

public void contextRemove()：在全局作用域对象删除共享数据

全局作用域对象共享数据变化时刻：

ServletContext application = request.getServletContext();

application.setAttribute("key1", 100); //新增共享数据

application.setAttribute("key1", 200); //更新共享数据

application.removeAttribute("key1"); //删除共享数据

# 过滤器接口

Filter接口，来自于Servlet规范下接口，在Tomcat存在于servlet-api.jar包

Filter接口实现类由开发人员负责提供，Http服务器不负责提供

Filter接口在Http服务器调用资源文件之前，对Http服务器进行拦截

作用：

1. 拦截Http服务器，帮助Http服务器检测当前请求合法性
2. 拦截Http服务器，对当前请求进行增强操作

## 开发步骤

1. 创建一个java类，实现Filter接口
2.  重写Filter接口中的doFilter方法
3. 在web.xml将过滤器接口实现类注册到Http服务器

## doFilter()方法

```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain){
    //对请求进行过滤
    
    //执行下一个过滤器，如果没有过滤器了，执行最终的Servlet
    chain.doFilter(request, response);
    
    //对响应进行处理
    
}
```

## 拦截命令格式

filter-mapping的顺序决定了多个filter之间的优先级

```xml
<filter-mapping>
	<filter-name>oneFilter</filter-name>
    <url-pattern>拦截地址</url-pattern>
    <dispatcher>REQUEST</dispatcher> <!--缺省值就是REQUEST，过滤request和response-->
    <dispatcher>FORWARD</dispatcher> <!--加上这个才会过滤请求转发解决方案的servlet-->
</filter-mapping>
<!--拦截地址通知Tomcat在调用何种资源文件之前需要通过OneFilter过滤进行拦截-->
<!--要求Tomcat在调用某一个具体文件进行拦截，访问同一个资源文件，Filter优先级高于Servlet-->
<url-pattern>/具体地址</url-pattern>
<!--要求Tomcat在调用某个文件夹下所有文件进行拦截-->
<url-pattern>/img/*</url-pattern>
<!--要求Tomcat在调用任意文件夹下某种类型文件进行拦截-->
<url-pattern>*.jpg</url-pattern>
<!--要求Tomcat在调用任意文件夹下任何类型文件进行拦截-->
<url-pattern>/*</url-pattern>
```

## 生命周期

创建：Servlet第一次访问才创建(在web.xml的Servlet标签中加上load-on-startup可以让Servlet和Filter一样在服务器启动时就创建实例化对象)，而Filter服务器刚启动就创建了

请求过滤：在Servlet被创建和初始化以后才进行请求过滤

doFilter：执行完请求过滤以后，进入下一个过滤器(没有则进入最终的Servlet)，执行Servlet的service()[doGet()或doPost()]

响应过滤：执行完Servlet的service()后进行响应过滤

销毁：Filter和Servlet都只创建一次(都是单实例多线程环境下运行的组件)，都在服务器停止后才被销毁

# MVC开发规范

## 介绍

MVC开发规则制定了互联网通信开发过程中必须出现角色有哪些

MVC开发规则制定了互联网通信开发过程中必须出现角色担负职责

MVC开发规则制定了互联网通信开发过程中必须出现角色的出场顺序

## 角色

DAO对象：提供了某张表文件操作的细节，降低了对表文件操作难度，避免了反复开发表文件操作的代码，提高代码复用性

Service对象：服务对象，提供业务的具体解决方案，Service对象一个方法指定一个业务的解决方案，避免业务开发重复性开发行为，提供复用性，网站每一个业务都有一个独立标准解决方案

## 业务

浏览器向Http服务器发送请求，用户向网站发送请求

如：张三用户发送请求：要求在服务端实现将张三账户3000元钱转给李四账户

业务处理方案：

1. 判断"张三"是否是当前系统中用户
2. 判断"李四"是否是当前系统中用户
3. 读取"张三账户余额"，判断余额是否充足
4. 读取"李四账户余额"，背账
5. 更新"张三账户余额 - 3000"
6. 更新"李四账户余额 + 3000"

## 业务特征

1. 真实业务场景中，一个业务往往包含多个分支任务，因此解决业务开发工作量往往比较巨大
2. 真实业务场景中，只有所有分支任务都能顺利成功解决，才可以认为当前业务处理成功

## 解决业务开发困扰

1. 一个业务可能在网站的多个地方重复出现，如果不做封装，增加开发难度，进行业务解决代码重复性开发
2. 不同程序员面对同一个业务时，给出解决方案往往有偏差，导致最终解决数据会有偏差

## 必须出现的角色

有三个

C，controller object：控制层对象(servlet对象)

对于controller，前端开发和后端开发在控制器的概念上有一定的区别，对于前端开发而言，controller不仅仅只是用来接收并处理数据，更重要的是还要处理具体的业务逻辑。如果是对于后端开发，controller会继续细分成两块，controller只负责接收并处理数据，同时为终端提供相应，对于业务逻辑划分为service业务去处理。

M，model object：业务模型对象(Service对象)

V，view object：视图层对象(jsp or HttpServletResponse)

## MVC开发规则

互联网通信开发过程中必须出现角色担任职责

C(servlet对象)：

1. 可以调用请求对象读取请求包参数信息
2. 必须调用Service对象处理业务
3. 必须调用视图层对象将结果写入到响应体中

M(service对象)：

1. 处理业务中所有的分支业务
2. 根据分支任务的执行情况判断业务是否处理成功
3. 必须通过return将处理结果返回给控制层对象

V(jsp/HttpServletResponse)

1. 禁止参与业务处理
2. 唯一任务将处理结果写入到响应体中

## Model层

### dao层

Data Access Object，数据访问对象，和业务逻辑没有任何关系，不能有业务代码，只能完成CRUD操作

dao层方法名一般都是：insertXXX，deleteXXX，updateXXX，selectXXX

### service层

在业务层中只能写纯业务逻辑，不能编写JDBC代码

在service层中编写的方法名一般和业务逻辑有关

#### 事务机制

service层和业务紧密相关，当我们一个业务完全完成之后再提交数据，所以控制事务应该放在service层

事务的提交回滚和conn的关闭在service中处理，dao处理sql的异常要上抛给service来处理，因为只有service才能回滚事务

因为在service层中控制事务，必须保证service方法执行的连接对象和dao方法中的连接对象是同一个，保证一个线程一个连接对象(**原则**)，不能让多个线程共享一个连接对象，不然事务会混乱

方法：

1. 在service中方法创建conn，并在调用dao中方法时传入service创建的conn，缺点是在service引入了JDBC代码，十分丑陋
2. 使用ThreadLocal完成在同一个线程中conn的传递，缺点是仍然将控制事务的代码放在service的方法中编写，每一个方法中控制事务的代码都是相同的，事务代码没有得到复用(用动态代理机制解决)

# 通过浏览器往服务器发请求(传参数)

1. 表单form提交
2. 超链接
3. document.location
4. window.location
5. window.open(url)
6. 直接在浏览器地址栏上输入url，然后回车

以上所有的请求方式均可以携带数据给服务器，只有通过表单可以动态提交数据

后台一律使用request.getParameter("xxx")或request.getParameterValues("xxx")来接收参数

# 后台往前端发数据

