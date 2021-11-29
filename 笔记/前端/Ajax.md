# 全局刷新和局部刷新

全局刷新：整个浏览器都被新的数据覆盖，在网络中传输大量数据，浏览器需要加载渲染页面

局部刷新：在浏览器内部发起请求，获取数据，改变页面中的部分内容，其余的页面无须加载和渲染，网络中数据传输量少，给用户的感受好

通过点击按钮改变div文本的方式也可以做局部刷新，然而这并不能实现与后端通信进而与数据库交互的功能，所以意义不大；而通过ajax的局部刷新则能做到

ajax是做局部刷新的，局部刷新使用的和新对象是异步对象(XMLHttpRequest)，这个异步对象是存在浏览器内存中的，使用JS语法创建和使用XMLHttpRequest对象

# Ajax

Asynchronous JavaScript and XML(异步的JavaScript和XML)

ajax是一种做局部刷新的方法，不是一种语言，包含技术主要有js、dom、css、xml等等

js负责创建异步对象，发送请求，更新页面的DOM对象

xml是网络中传输数据的格式，ajax请求需要服务器端数据

# AJAX异步实现步骤

## 创建对象方式

```javascript
var xmlHttp = new XMLHttpRequest();
//XMLHttpRequest是核心对象
```

## 给异步对象绑定事件

onreadystatechange：当异步对象发起请求，获取了数据都会触发这个事件，这个事件需要指定一个函数，在函数中处理状态的变化

```javascript
xmlHttp.onreadystatechange = function(){
    
}
```

异步对象的属性 readyState 表示异步对象请求的状态变化:

0. 创建异步对象时，new  XMLHttpRequest()

1. 初始异步请求对象，xmlHttp.open()

2. 发送请求，xmlHttp.send()

3. 从服务器端获取了最原始的数据，异步对象内部在处理数据
4. 异步对象把接收的数据处理完成后，开发人员在此时处理数据，更新当前页面

异步对象的属性 status 表示网络请求的状况:

200,404,500等，即Http状态码

## 初始异步请求对象

异步的方式open()

xmlHttp.open(请求方式，访问地址，默认是true(true表示异步，false是同步), (ftp服务器)用户名, 密码)

## 使用异步对象发送请求

xmlHttp.send()

获取服务器端返回的数据，使用异步对象的属性 responseText

# 与json

在服务器内部通信时：如果是普通请求(请求转发，重定向)，那么没必要使用json，用java对象在servlet和jsp中传来传去就可以了；然而对于ajax请求，不用json格式传递数据而用普通java对象传递必出bug

