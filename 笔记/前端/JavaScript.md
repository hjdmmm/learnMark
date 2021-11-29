# 什么是JavaScript

JavaScript是世界上最流行的脚本语言，运行在浏览器上

让浏览器更加生动，不再是单纯的静态页面，页面更具有交互性

Java运行在JVM当中，JS运行在浏览器内存中

JS程序不需要手动编译，编写完源代码之后，浏览器直接打开解释执行

JS的"目标程序"以普通文本形式保存，这种语言叫做"脚本语言"

Java目标程序以.class形式存在，不能使用文本编辑器打开，不是脚本语言

---

ECMAScript可以理解为是JavaScript的一个标准，最新到了es6版本，但是大部分浏览器还只能支持es5代码

---

JSP：JavaServer Pages，隶属于Java语言，运行在JVM中，和Servlet一起处理浏览器与Http服务器之间的请求问题

JS：JavaScript，运行在浏览器上，处理用户与浏览器之间的请求问题

# 语法

js中的字符串可以使用单引号，也可以使用双引号

js中的一条语句结束后可以用分号，也可以不用 

js脚本块在一个页面中可以出现多次，在页面哪个位置都可以

# 引入JavaScript

## 1.内联嵌入

```html
<input type="button" value="hello" onclick="window.alert('Hello, world.')">
```

## 2.脚本块方式

暴露在脚本块中的程序，在页面打开时执行，并且按照自上而下的顺序依次执行

```html
<script type="text/javascript">
	代码在这里写
</script>
```

## 3.外部引入方式

```js
<script type="text/javascript" src="">这里写的代码不会执行</script>
```

# 注释

```javas
//单行注释
/*多行注释*/
```

# 变量

js是弱类型语言，没有编译阶段，一个变量可以随便赋值

var 变量名;

变量名 = 值;

当一个变量没有手动赋值的时候，系统默认赋值undefined

当一个变量没有定义的时候，会报错 xx is not defined

## var和let

'use strict'; 严格检查模式，禁止全局变量，推荐都用

|      | 规范 | 重新定义 | 能否定义之前访问                    |
| ---- | ---- | -------- | ----------------------------------- |
| var  | es5  | 能       | 可以，因为var会把定义提前到函数头部 |
| let  | es6  | 不能     | 不行                                |

|      | 作用域                                                       |
| ---- | ------------------------------------------------------------ |
| var  | 函数作用域，在for循环中定义的var，在函数的其他地方也可以使用 |
| let  | 块作用域，在for循环中定义的let，出了for就不能再用了          |



## 全局变量和局部变量

在函数体外声明的变量就是全局变量，浏览器打开时声明，浏览器关闭时销毁，尽量少用，因为会占用浏览器内存

在函数体中声明的变量，包括形参，都是局部变量，生命周期为函数执行期间

如果一个变量声明时没有用var，即使在函数体内声明，也是全局变量

全局变量可以在当前HTML文件中所有的函数中使用

全局变量被声明时，自动分配给window对象作为其属性

## 变量作用域

---

从外到内查找，就近原则，全局变量和局部变量重名的，会优先访问本函数体内的局部变量

---

js中没有命名空间，所有全局变量实际上都会绑定到window对象上，使得不同js文件的全局变量极易出现冲突，建议使用自己的对象来绑定全局变量以减少冲突

---

var不能定义局部作用域的变量，如for循环的i，如果用var定义，出了循环体仍不会被销毁

建议使用let去定义局部作用域变量

const+名称大写来定义常量

# 数据类型

## 原始类型

### Number

js不区分浮点数和整数

123

123.1

1.241e3

NaN: not a number，运算结果本来应该是一个数字，但是结果不是一个数字，就是NaN，字符串拼接符(+)除外，非法数字

Infinity: 无穷大，除数为0的时候，结果为无穷大

尽量避免使用浮点数计算，避免精度损失

isNaN()判断是否为NaN，parseInt()将字符串转换为数字，还有舍弃小数的功能，parseFloat()将字符串转换为数字，Math.ceil()向上取整(进一法取整)

### String

'abc'，"abc"，单引号和双引号都行

字符串不可变

---

大String：var x = new String("abc")，String是一个内置类，继承Object，typeof x为object

小String：var y = "abc"，typeof y为string

---

常用属性和方法

length，indexOf()，split()

substr(startIndex, length)

substr(startIndex, endIndex)，注意不包括右边，即左闭右开

### Boolean

true, false

有就转换为true，没有就转换为false

Boolean(1)是true

Boolean(0)是false

Boolean("")是false

Boolean("abc")是true

Boolean(null)是false

Boolean(NaN)是false

Boolean(undefined)是false

Boolean(Infinity)是true

### Null和Undefined

Null是空，Undefined是没定义

Undefined类型只有一个值，就是undefined

Null类型只有一个值，就是null

Null表示对象引用了一个空内存，这个内存既不能读取也不能存储数据

### Symbol

ES6加的

## 引用类型

Function，Object和Object的子类

### Function

function在ES规范中不属于独立的数据类型，而属于object

然而typeof的返回值会出现function

JS中所有的函数都是function类型，所有通过构造函数生成的对象都是object类型

### 数组

js数组不需要相同类型

如果越界就是undefined

```javascript
var arr = [1, "s", 2.1]; //注意是[]，不是{}
```

1. 数组长度arr.length赋值，数组大小就会变化，数组长度可变，截短数组会造成数据丢失
2. indexOf，通过元素获取下表索引，数字1和字符串"1"不同
3. slice()，截取Array
4. push(), pop()，弹出压入尾部的一个元素
5. unshift()压入头部，shift()弹出头部的元素
6. sort()排序
7. reverse()元素反转
8. concat()拼接数组，并不会修改原数组，只是会返回一个新数组
9. join("-")，打印拼接数组，用特定的字符串连接

### 对象

若干个键值对

``` javascript
var 对象名 = {
    属性名: 属性值,
    属性名: 属性值,
    属性名: 属性值
}
```

1. 使用一个不存在的对象属性，不会报错，undefined

2. 动态的增添属性和方法

   ``` javascript
   delete person.name;
   person.haha = "haha";
   var s = "hehe";
   person[s] = "hehe";
   ```

3. 判断是否在对象中 in

4. 判断是否为对象自身而不是继承而来 hasOwnProperty()

### Map和Set

Map键值对

Set无序不重复的集合

# 标识符和关键字

标识符命名规则和规范按java执行

关键字不用刻意记

# 运算

## typeof

typeof 变量名

运算结果是以下6个字符串之一，注意字符串全部都是小写

null属于Null类型，但是typeof null结果是"object"

"undefined"

"number"

"string"

"boolean"

"object"

"function"

## 逻辑运算

&& || !

## 比较运算符

1. =
2. ==(等同运算符，类型无所谓，值一样为true)
3. ===(全等运算符，类型和值都相同才true)

坚持不使用==比较

NaN===NaN是false，NaN与所有数值包括自己不相等，只能用isNaN()判断

# 流程控制

1. if
2. switch
3. 各种循环
4. break
5. continue
6. for in语句
7. with语句

```javascript
for(var i in arr){
    alert(arr[i])//i是数组元素的下标
}
User = function(username, password){
    this.username = username;
    this.password = password;
}

var u = new User("张三", 123);
with(u){ //省略访问属性时的u.
    alert(username + ", " + password);
}
```



# 函数

``` javascript
function 函数名(形参列表){
    函数体
}
var 函数名 = function(形参列表){
    函数体
}
```

创建函数有两种方法：定义法和函数变量法

js没有函数重载，因为一个函数接收的形参可以为任意个数

js中函数若重名，代码按顺序结构执行，后面的会覆盖前面的

## arguments

JS中每一个函数都包含一个arguments属性

arguments属性是一个数组

在函数调用时，将实参输入到函数的arguments中，再由arguments将数据传递给形参

arguments属性存在，可以将JS中函数在调用时传递实参与形参进行隔离，增加函数调用的灵活性

arguments只能在函数内部使用，不能在函数外使用

## 创建时期

function类型对象创建时间：

浏览器在加载<script>时，共加载两次

第一次加载，将<script>标签所有以标准形式声明函数对象进行创建

第二次加载，将<script>标签所有命令行以自上而下顺序执行

# 方法

函数在对象里就叫方法

调用方法一定要有()

# 类

```javascript
function 类名(a, b){
    //属性
    this.a = a;
    this.b = b;
	//方法
    this.getPrice = function(){
        return this.price;
    }
}
类名 = function(){
    
}
//不用new就是函数，用new就是类
//声明类的同时制定了它的构造方法
```

普通函数与构造函数区分：

1. 函数没有调用之前，不能区分函数的身份，只能根据函数调用形式区分
2. 返回值，普通函数运行时需要通过return将执行结果返回，构造函数运行后，直接返回一个Object对象(即使写有return，也直接失效)

# 常用类

## Object

prototype用来给类动态扩展属性和方法

## Date

直接new是本地时间

toLocaleString()

getYear()返回21

getFullYear()返回2021

getMonth()得到的月份是0~11

getDate()获取天

getDay()获取星期几0~6

getTime()得到时间戳，1970.1.1 00:00:00 000到现在的毫秒数

## Array

join("-")返回一个字符串，将数组内的元素用-连接

push()在数组末尾加元素

pop()将数组末尾的元素弹出

reverse()翻转

## JSON

介绍：

- JSON是一种轻量级的数据交换语言

- 简洁和清晰的层次结构使其成为理想的数据交换语言

- 易于人阅读和编写，也便于及其解析和生成，并有效地提升网络传输效率

格式：

- 对象都用{}
- 数组都用[]
- 所有的键值对都用key:value

# 面向对象编程

类---原型对象

对象

## 原型继承

__po

## class继承

# 事件

JS是一门事件驱动型语言，依靠事件驱动，然后执行对应的程序

任何事件都会对应一个事件句柄，事件和事件句柄的区别是：事件句柄是在事件名称前加一个on。

事件句柄是以HTML标签的属性的形式存在的

## 常用事件

1. blur失去焦点
2. focus获得焦点
3. change下拉列表选中项改变，或文本框内容改变
4. click鼠标点击
5. dblclick鼠标双击
6. keydown键盘按下
7. keyup键盘弹起
8. load页面加载完毕
9. mousedown鼠标按下
10. mouseover鼠标经过
11. mousemove鼠标移动 
12. mouseout鼠标离开
13. mouseup鼠标弹起
14. reset表单重置
15. select文本被选定
16. submit表单提交

## 注册事件

### 直接在标签中使用事件句柄

回调函数：自己不调用，别人去调用的函数

```html
<input type="button" value="hello" onclick="seyHello()"/>
```

### 使用纯JS代码完成事件注册

```html
<script type="text/javascript">
    //第一步：获取按钮对象(document是全部小写，内置对象，代表整个HTML界面)
    var btnObj = document.getElementById("mybtn");
    //第二步：给按钮对象的onclick属性赋值
    btnObj.onclick = doSome;//注意不要加()，直接写函数名，这样不能传参
    //或匿名函数
    mybtn1.onclick = function(){
        
    };
    
</script>"
```

# DOM编程

Document Object Model，文档对象模型，对网页当中的节点进行增删改的过程，HTML文档被当成一棵树来看待。

## DOM对象

JS是不能直接操作HTML标签，只能通过HTML标签关联的DOM对象给HTML标签下指令

浏览器在接收到html文件之后，将html文件标签加载到浏览器缓存中，每当加载一个html标签对象的时候，自动为这个标签生成一个实例对象，这个实例对象就是DOM对象

在浏览器关闭之前或浏览器请求其他资源文件之前，本次生成的DOM对象一直存活在浏览器缓存中

在浏览器请求到新资源文件后，浏览器原有缓存的DOM对象会被覆盖

## document对象

document对象被称为文档对象

document对象用于在浏览器内存中根据定位条件定位DOM对象

生命周期：

1. 在浏览器将网页中所有标签加载完毕后，在内存中用树形结构，存储这些DOM对象，在树形结构生成完毕后由浏览器生成一个document对象管理这棵树(DOM树)

2. 浏览器运行期间，只会生成一个document对象

3. 在浏览器关闭时，负责将document对象进行销毁

## 定位方法

根据html标签的id属性值定位DOM对象

```javascript
var domObj = document.getElementById("one");
```

根据html标签的name属性值对位DOM对象

```javascript
var domArray = document.getElementsByName("deptNo");
//通知督document对象将所有name属性等于deptNO的标签关联的DOM对象进行定位并封装到一个数组进行返回，domArray就是一个数组存放本次返回的所有DOM对象
```

根据html标签类型定位DOM对象

```javascript
var domArray = document.getElementsByTagName("p");
//选中所有段落标签
```

## DOM对象对HTML标签属性操作

1. DOM对象对标签value属性进行取值与赋值

2. DOM对象对样式属性进行取值与赋值
3. DOM对象对标签中状态属性进行取值与赋值
4. DOM对象对标签中文字显示内容进行赋值与取值

```javascript
var domObj = document.getElementById("one");
//value取值赋值操作
var num = domObj.value;
domObj.value="abc";
//样式属性取值与赋值操作
var color = domObj.style.backgroundColor;
domObj.style.backgroundColor = red;
//状态属性的值都是boolean类型
var color = domObj.style.backgroundcolor;
domObj.style.backgroundcolor = red;
//DOM对象对标签中文字显示内容进行赋值与取值
var num1 = domObj.innerText;
domObj.innerText = "haha";
```

## innerHTML和innerText属性

都是用来设置元素内的内容

innerHTML会把后面的字符串当成一段HTML代码解释并执行

innerText全部视为普通文本

## 正则表达式

Regular Expression

主要用在字符串格式匹配方面，搜索方面等

最初使用在医学方面，用来表示神经符号

### 常见的正则表达式符号

. 匹配除换行符以外的符号

\w 匹配字母或数字或下划线或汉字

\s 匹配任意的空白符

\d 匹配数字

\b 匹配单词的开始或结束

^ 匹配字符串的开始

$ 匹配字符串的结束

---

*重复零次或多次

+重复一次或更多次

?重复零次或一次

{n}重复n次

{n,}重复n次或更多次

{n, m}重复n到m次

---

\W 匹配任意不是字母、数字、下划线

\S 匹配任意不是空白符的字符

\D 匹配任意非数字的字符

\B 匹配不是单词开头或结束的字符

[^x] 匹配除了x以外的任意字符

[^aeiou] 匹配除了aeiou这几个字母以外的任意字符

|表示或者

[A-Za-z0-9-]表示A-Z、a-z、0-9、-以上所有字符中任意1个字符

### 常见正则表达式

```
QQ号：^[1-9][0-9]{4,}$
email：^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
```

### 正则表达式使用方法

1. var regExp = /正则表达式/flags;
2. var regExp = new RegExp("正则表达式", "flags");

关于flags：

g：全局匹配

i：忽略大小写

m：多行搜索(ES规范之后才支持)，当前面是正则的时候不允许使用，普通字符串才可以 

# BOM编程

Browser Object Model，浏览器对象模型，关闭浏览器窗口，打开一个新的浏览器对象，后退前进，地址栏上的地址

## DOM和BOM关系

DOM顶级对象是document

BOM顶级对象是window

BOM实际上包括DOM

## window对象

```
open(1, 2)，1为url，2为方式：_self，_parent，_blank
close()，关闭当前窗口
alert()，消息框
confirm()，确认框，有返回值
```

## history对象

back()，go(-1)

## location对象

herf：地址栏

# JSON

JavaScript Object Notation，一种标准的数据交换格式，目前非常流行

标准的轻量级的数据交换格式，特点是：体积小、易解析

另一个使用较多的数据交换格式是XML，体积较大、解析麻烦、但是语法严谨、银行业务可用

```javascript
// 创建JSON对象，JSON也被称为无类型对象
var studentObj = {
    "sno" : "110",
    "sname" : "张三",
    "sex" : "男"
};
// 没有JSON时，定义类和创建对象
Student = function(sno,sname,sex){
    this.sno = sno;
    this.sname = sname;
    this.sex = sex;
};
var stu = new Student("111", "李四", "男");
//JSON数组
var student = {
    {"sno":"110","sname":"张三","sex":"男"},
    {"sno":"111","sname":"李四","sex":"男"}
}
```

## 语法格式

```javascript
var jsonObj = {
    "属性名": 属性值,
    "属性名": 属性值,
    "属性名": 属性值
};
```

## eval()函数

eval()是js的函数，经常用来将java传来的语句解析创建js对象

```javascript
var fromJava = "{\"name\": \"zhangsan\"}";
window.eval("var jsonObj = " + fromJava);
```

