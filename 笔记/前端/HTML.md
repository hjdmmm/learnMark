# HTML概述

## 系统架构

B/S架构：主要是这个，Browser/Server(浏览器/服务器交互形式)

Browser支持的语言：HTML、CSS、JavaScript，写这些语言的人叫WEB前端开发工程师，Java程序员目前来看也要会一些前端的东西

前端页面上的图片需要UI设计师完成

服务器端的语言有很多：C、C++、Java、Python

缺点：速度慢、界面不炫酷、体验不好

优点：升级方便，只升级服务器端代码即可，维护成本低

企业内部的解决方案都是采用B/S架构的系统

C/S架构：Client/Server

缺点：升级麻烦，维护成本较高

优点：速度快，体验号，界面炫酷

## 什么是HTML

Hyper Text Markup Language，超文本标记语言，超文本：流媒体、图片、声音

由大量标签组成

## 规范制定者

W3C，万维网联盟

制定了HTML的规范，浏览器生产厂家和HTML程序员都会遵守这个规范

HTML目前最高版本是HTML5.0，简称H5

W3C标准：

- 结构化标准语言
- 表现标准语言
- 行为标准

w3school，中文互联网HTML学习网站

## 常见IDE

- 记事本
- Dreamweaver
- IDEA
- WebStorm

## HTML基本结构

头部，主体

成对的开放标签闭合标签

自闭合标签，独目标签

```html
<!--
注释在此
-->
<!doctype html>

<html>
    <head>
        <title>网页的标题</title>
    </head>
    <body>
        网页的主体部分
    </body>
</html>
```



## 语法特点

HTML语法松散不严格，不区分大小写

所有命令都是声明在标签中

HTML开发时主要通过对命令中属性进行赋值实现开发目的，属性赋值时内容包含在""或''，也可以省略但此时属性之间必须有空格隔离

# 网页基本标签

- 标题标签，<h1~h6></h1~/h6>
- 段落标签，<p></p>
- 换行标签，<br>
- 水平线标签，<hr>
- 预留格式，<pre></pre>
- 字体样式标签<font color="" size=""></font>
- 右上角的字<sup></sup>
- 右下角的字<sub></sub>
- 各种特殊的字

```html
<!doctype html>
<html>
    <head>
        <title>网页基本标签</title>
    </head>
    <body>
        <p>
            段落标签
        </p>
        
        <h1>标题字</h1>
        <h2>标题字</h2>
        <h3>标题字</h3>
        <h4>标题字</h4>
        <h5>标题字</h5>
        <h6>标题字</h6>
        
        <!--换行标记，是独目标签-->
        <br>
        <!--水平线标记，是独目标签，color和width是hr标签的属性-->
        <hr color="red" width="50%">
        <!--语法太松散了-->
        <hr color='red' width=50%>
        
        <pre>
        预留格式
        </pre>
        
        <del>删除字</del>
        <ins>插入字</ins>
        <b>粗体字</b>
        <i>斜体字</i>
        
        <sup>10</sup>
        <sub>2</sub>
        
        <!--实体符号-->
        小于号&lt;大于号&gt;空格&nbsp;
    </body>
</html>
```

# HTML标签属性分类

1. 基本属性：id、name(允许一组标签拥有相同name)、...
2. 样式属性：style="background-color:red;color:green..."
3. 工作状态属性：只存在于表单域标签中
   1. checked：存在于radio与checkbox中，表示标签是否被选中
   2. disabled：表示标签处于不可用状态
   3. readonly：表示标签处于只读状态
   4. selected：存在option中，表示是否被选中
4. 监听属性：js的事件句柄

# 实体符号

以&开始，以;结束

```html
小于号&lt;大于号&gt;空格&nbsp;
```

# 表格

```html
<!doctype html>
<html>
    <head>
        <title>表格</title>
    </head>
    <body>
        <!--border属性设置表格的边框为1像素宽度，width和height属性设置格子大小-->
        <table border="1px" width="60%" align="center">
            <tr>
                <!--th标签也是单元格标签，比td多的是居中，加粗-->
            	<th>员工编号</th>
            	<th>员工姓名</th>
            	<th>员工薪资</th>
            </tr>
            <tr align="center">
            <!--align属性，对齐方式-->
            	<td>a</td>
                <td>b</td>
                <td>c</td>
            </tr>
        </table>
    </body>
</html>
```

## 单元格合并

吞并下面一格，删掉下面的格，在上面的格上加上属性rowspan="2"

吞并右面一格，删掉右面的格，在上面的格上加上属性colspan="2"

## 标签

thead

tbody

tfoot

# 背景颜色背景图片

```html
<body bgcolor="red" background=""></body>
```

# 图像标签

```html
<img src="" width="" height="" title="" alt=""/>
```

设置宽度时，高度会自动等比例缩放，不用手动设置，否则会失真

title属性，鼠标悬停到图片上显示的文字

alt属性，图片找不到时显示的文字提示

# 超链接

```html
<a href="https://www.baidu.com"></a>
<a href="https://www.baidu.com"><img src=""/></a> <!--图片超链接-->
```

href：hot reference热引用

target属性:

_blank:新窗口

_self:当前窗口(默认)

_top:顶级窗口

_parent:父窗口

超链接的作用：通过超链接可以从浏览器向服务器发送请求，浏览器向服务器发送数据(请求：request，必须使用get请求方式)，服务器向浏览器发送数据(相应：response)。B/S结构的系统，每一个请求都会对应一个响应

# 列表

type属性来指定样式

## 无序列表

```html
<ul>
    <li>中国
        <ul>
            <li>北京
                <ul>
                    <li>东城区</li>
                    <li>西城区</li>
                </ul>
            </li>
            <li>天津</li>
        </ul>
    </li>
    <li>美国</li>
</ul>
```

## 有序列表

```html
<ol>
    <li>水果</li>
    	<ol>
            <li>桃子</li>
    	</ol>
    <li>蔬菜</li>
    <li>甜点</li>
</ol>
```

# 表单语法

浏览器发送请求时携带的请求参数来源

1. 通过超链接标签命令指定请求参数
2. 通过表单域标签命令指定请求参数
3. 不包括form标签的action属性的?

表单作用：收集用户信息。表单展示后，用户填写表单，点击提交按钮提交数据给服务器。

表单提交的格式：action?name=value&name=value...

表单项没有写name属性的，该项不会提交给服务器

对于大多数表单域标签，value属性没有写的时候，默认值为空字符串""，会将其提交给服务器

对于radio与checkbox来说，value属性默认值为'on'字符串

```html
<form action=""></form>
<input type="submit"/>
<input type="button" value="设置按钮上显示的文本"/> <!--普通按钮，不具有提交表单的能力-->

<form action="">
    <table>
        <tr>
        	<td>用户名</td>
            <td><input type="text" name="username"/></td>
        </tr>
        <tr>
        	<td>密码</td>
            <td><input type="password" name="userpwd"></td>
        </tr>
        <tr align="center">
        	<td colspan="2">
            	<input type="submit" value="登录"/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <input type="reset" value="清空"/>
            </td>
        </tr>
    </table>
</form>
```

action属性：用来指定数据提交给哪个服务器

method属性：get(默认)，post

表单域标签分类：

```
1. <input />
2. <select></select>
3. <textarea></textarea>
```

## input控件

```html
<input type="text" name="username"/>
<input type="password" name="password"/>
<input type="radio" name="sex" value="man"/>
<input type="radio" name="sex" value="woman"/> <!--name相同识别为单选框-->
<input type="checkbox" name="habit" value="java"/>
<input type="checkbox" name="habit" value="c++"/> <!--多选框-->
<input type="file" name="myfile"/>
<input type="submit"/>
<input type="reset"/> <!--将表单所有value恢复为初始值-->
```

### input标签的属性

readonly属性和disabled属性

readonly和disabled相同点：都是只读不能修改

但readonly可以选中复制，还能提交给服务器，disabled选都不能选中，而且不会提交给服务器(即使写了name)

maxlength属性，最多输入的字符

id属性，给js拿到该元素

## select控件

下拉列表

```html
<select name="home">
    <option value="beijing">北京</option>
    <option value="tianjin">天津</option>
</select>
```

## textarea控件

多行文本框

```html
<textarea name="tt" rows=10 cols=30> <!--展示出10行,30宽-->
	
</textarea>
```

## hidden控件

隐藏域，网页上看不到，但是表单提交的时候数据会提交

# 浏览器请求方式

有七种

## get

用户提交的信息会显示在地址栏上，不安全，效率高，携带的请求参数数量不能超过4K，必须将请求参数信息保存在Http请求协议包中(请求头)，在接收到返回的资源文件内容后，必须将资源文件内容保存在浏览器的缓存

## post

用户提交的信息不会显示在地址栏上，安全，传输大文件，可以携带任意数量的请求参数，必须将请求参数信息保存在Http请求协议包中(请求体)，禁止浏览器将服务器返回资源文件内容进行保存

## 适用场景

1. 考虑到POST请求方式，用户可以将病毒文件内容发送到服务器上进行攻击，因此绝大多数门户级网站拒绝接收POST请求，日常开发过程绝大多数请求都是GET
2. 在某些特殊场景下必须使用POST
   1. 文件上传
   2. 发起登录验证请求
   3. 索要服务器中实时变化数据(股票价格、车票数量……)



# div标签和span标签

div和span都可以称为图层，保证页面可以灵活布局

最早网页是采用table布局，不灵活太死板

现代网页中div布局使用最多

div和span是可以定位的，只要定下div左上角坐标即可

div独自占用一行(默认情况下)，span不会独自占用一行



# 其他页面结构

- header：头部区域
- footer：脚部内容
- section：独立区域
- article：独立文章内容
- aside：相关内容（侧边栏）
- nav：导航类辅助内容

# frame标签系列

利用frameset和frame可以把网页制作成所需要的不同大小的框架，用来布局。

iframe则是把一些网页嵌入到当前网页中，达到所需要的效果。

```html
<head>
    <!--frameset标签只能放在head标签中-->
    <framset cols="25%,*">
        <frameset rows="30%,*">
            <frame src="http://www.baidu.com"></frame>
        	<frame src="http://www.126.com"></frame>
        </frameset>
		<frame src="http://www.163.com"></frame>
    </framset>"
</head>
<body>
    <iframe src="xxx.html"></iframe>
</body>
```

