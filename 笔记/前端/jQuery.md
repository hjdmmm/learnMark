# 简介

jQuery是一款跨主流浏览器的JavaScript库，封装了JavaScript方法的调用，简化JS对HTML DOM操作

作用：可以处理dom对象，事件处理，动画，ajax

优点：

1. 写少代码，做多事情
2. 免费，开源，且轻量级的js库，容量很小
3. 兼容市面上主流浏览器：IE，Chrome，Firefox
4. 能够处理HTML/JSP/XML、CSS、DOM、事件、实现动画效果，也能提供异步AJAX功能
5. 文档手册很全，很详细
6. 成熟的插件可供选择，多种js组件
7. 出错后有一定的提示信息

# DOM对象和jQuery对象

## DOM对象

文档对象模型，是W3C组织推荐的处理可扩展性标志语言的标准编程接口，通过DOM对HTML页面的解析，可以将页面元素解析为元素节点、属性节点、文本节点，这些解析出的节点对象，即DOM对象，DOM对象可以使用JS中的方法

```javascript
var obj = document.getElementById("txt1"); //obj是dom对象，也叫作js对象
```

## jQuery对象

使用jQuery语法表示对象叫做jQuery对象，注意：jQuery对象都是数组，数组中的每个成员都是一个**dom对象**

```javascript
var jobj = $("#txt1"); //jobj就是使用jQuery语法表示的对象，也就是jQuery对象，他是一个数组，现在数组中就一个值
```

## 区分EL表达式

```jsp
<%
//EL表达式是用在jsp中的，作用是减少<百分号百分号>的出现
%>
${requestScope.ename}
```

```js
//jQuery是用在js中的，作用是简化JS对DOM对象的操作
var txt1Obj = ${"#txt1"};
```

## 互相转换

dom对象可以转为jQuery对象，语法：$(dom对象)

jQuery对象也可以转为dom对象，语法：从数组中获取第一个对象，第一个对象就是dom对象，使用[0]或者get(0)

为什么要进行dom和jQuery转换，目的是要使用对象的方法，或者属性，当你使用dom对象时，可以使用dom对象的属性或者方法，如果你想使用jQuery提供的函数，必须是jQuery对象才可以

# 选择器

与CSS中的选择器几乎相同

## id选择器

语法：$("#id值")

id在当前页面中是唯一值

## class选择器

语法：$(".class样式名")

class表示css中的样式，使用样式的名称定位dom对象

## 标签选择器

语法：$("标签名称")

一般返回多个对象组成的数组

## 全部选择器

语法：$("*")

## 组合选择器

语法：$("#one, span, .two, ...")

用, 间隔多个元素

## 表单选择器

在一个表单中常常会有很多input控件，我们可以一次性选择所有的某一类input控件，这与input是否在form中无关

语法：$(":type属性值")

## 属性选择器

某个标签的某种属性

语法：$("input[name=select]")

# 过滤器

过滤器需要和选择器一起使用

## 基本过滤器

即为CSS中的层次选择器，结构伪类选择器

1. $("选择器:first")
2. $("选择器:last")
3. $("选择器:eq(数组的下标)")
4. $("选择器:lt(下标)")
5. $("选择器:gt(下标)")

## 表单属性过滤器

根据表单中dom对象的状态情况，定位dom对象的

1. 选择可用的文本框：$(":text:enabled")
2. 选择不可用的文本框：$(":text:disabled")
3. 选择复选框选中的元素：$(":checkbox:checked")
4. 选择指定下拉列表被选中的元素：选择器>option:selected

# 绑定事件

**动态生成的元素(比如ajax分页查询时动态添加生成的元素)，不能用第一种，只能用第二种**

## 第一种

$(选择器).事件名称(事件处理函数)

事件名称，就是js中事件句柄去掉on，onclick-->click

## 第二种

on事件绑定

$(选择器).on(事件名称, 事件的处理函数)

```javascript
$("#btn").on("click", function(){})
```

对于动态生成的元素

$(需要绑定元素的有效的外层静态元素).on(事件名称, 需要绑定元素的jQuery对象, 事件的处理函数)

# 函数

## val()

操作数组中dom对象的value属性

相当于value

$(选择器).val()：无参调用，读取数组中每一个dom对象的value属性值

$(选择器).val(值)：有参调用，对数组中所有dom对象的value属性值进行统一赋值

## text()

相当于innerText

$(选择器).text()：无参调用，读取数组中所有dom对象的文字显示内容，将得到的内容拼接成一个字符串返回

$(选择器).text(值)：将数组中所有dom对象的文字显示内容进行统一的赋值操作

## attr()

对val，text之外的其他属性操作

$(选择器).attr("属性名")：获取dom数组第一个对象的属性值

$(选择器).attr("属性名", "值")：对数组中所有dom对象的属性设为新值

## remove()

将数组中所有dom对象及其子对象一并删除

select和option都删除

## empty()

将数组中所有dom对象添加子对象

select保留，option删除

## append()

为数组中所有dom对象添加子对象

## html()

设置或返回被选元素的内容

相当于innerHTML

$(选择器).html()：无参调用，获取dom数组第一个元素内容

$(选择器).html(值)：有参调用，用于设置dom数组中所有元素的内容

## each()

可以对数组，json，dom数组遍历处理，json中每个成员都会调用一次处理函数

$.each(要便利的对象, 处理函数)

$相当于类名，.each()就是类中的静态方法

处理函数: function(index, element)

index是循环的索引，element是数组的成员

处理jQuery对象 也可以用：jQuery对象名.each(function(){})

# 简化ajax

使用jQuery函数，实现ajax请求的处理

没有jQuery之前，使用XMLHttpRequest做ajax，有4个步骤，jQuery简化了ajax请求的处理

1. $.ajax()：jQuery实现ajax的核心函数
2. $.post()：使用post方式做ajax请求
3. $.get()：使用get方法发送ajax请求

$.post()和$.get()他们在内部都是调用$.ajax()

## $.ajax()

最标准形式，使用方便，应用广泛

函数的参数表示请求的url，请求方式，参数值等信息

参数是一个json结构，$.ajax({名称:值, 名称:值, 名称:值, 名称:值})

```javascript
$.ajax({ async:true, contextType:"application/json", data:{name:"lisi", age:20}, dataType:"json", error:function(){}, success:function(data){}, url:"oneAjax", type:"get" })
```



json结构的参数说明

1. async：布尔值，默认是true，表示是否进行异步请求
2. contextType：一个字符串，表示从浏览器发送服务器的参数的类型
3. data：可以是字符串，数组，json，表示请求的参数和参数值，常用的是json
4. dataType：期望从服务器端返回的数据格式，xml、html、text、json，当我们使用$.ajax()发送请求时，会把dataType的值发送给服务器，那我们的servlet能够读取dataType的值，让服务器返回你所需的内容
5. error：一个function，当请求发生错误时，执行的函数
6. success：一个function，请求成功了，从服务器返回了数据，就会执行这里的函数，相当于之前使用XMLHttpRequest时的readyState == 4 && status == 200；他可以接收一个参数，是responseText，是jQuery处理完后的数据
7. url：请求地址
8. type：请求方式，默认是get

主要用url，data，dataType，success

## $.get(), $.post()

参数不再是json结构，而是具体的值

简化了一些功能

(url, data, function(){}, dataType)

# prop()和attr()

相同点：都是设置标签的属性的，都是提供一个参数时返回参数值，提供两个参数为修改参数值

不同点：

```html
<input checked="checked"/>
<input checked=true/>
<!--以上两个prop("checked")返回true；attr("checked")返回checked-->

<input />
<!--这个prop("checked")返回false；attr("checked")返回undefined-->
<!--这个prop("href")返回""(空字符串)；attr("href")返回undefined-->
```

用法：

对于HTML元素本身具有的属性，如id，checked，selected，href等，处理时使用prop()

对于我们自定义的DOM属性，处理时使用attr()

具有true和false两个属性的属性，如checked，selected，disabled，处理时使用prop()
