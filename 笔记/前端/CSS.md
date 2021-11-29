# 学什么

1. CSS是什么
2. CSS怎么用
3. CSS选择器
4. 美化网页
5. 盒子模型
6. 浮动
7. 定位
8. 网页动画

# CSS是什么

Cascading Style Sheet 层叠级联样式表

在浏览器中编译并执行的编程语言

用来修饰HTML页面，设置HTML页面中的某些元素的样式，让HTML页面更好看，是HTML的化妆品

HTML还是主体，CSS依赖HTML，CSS的存在就是修饰HTML，所以新建的文件还是xx.html文件

# 掌握程度

常见的CSS样式要求会写，别人写的CSS样式要能看懂

# CSS的三种导入方式

## 1.外部样式,链入外部样式表文件(最常用)

将样式写到一个独立的CSS文件，在需要的网页上直接引入css文件

<link type="text/css" rel="stylesheet" href="css文件的路径"/>

这种方式易维护，维护成本较低

   1. 链接式：html
   2. 导入式：CSS2.1

## 2.内部样式，样式块方式

在head标签中使用style块

<head>
    <style type="text/css">
        选择器 {
            样式名:样式值;
            样式名:样式值;
            ...
        }
        选择器 {
            样式名:样式值;
            样式名:样式值;
            ...
        }
    </style>
</head>



## 3.行内样式，内联定义方式

   <标签 style="样式名:样式值;样式名:样式值;..."></标签>

# 选择器

选择页面上的某一个或某一类元素

方便更改多个相同样式的标签

## 基本选择器(重点)

1. 标签选择器：标签名{}
2. 类选择器：.类名{}
3. id选择器：#id名{}

id选择器>类选择器>标签选择器

---

了解即可

## 层次选择器

HTML标签之间只有两种关系：父子关系、兄弟关系



``` html
<body>
    <div>1</div> <!--大哥-->
    <p>2</p> <!--二哥-->
    <span>3</span> <!--三哥-->
</body>
<tr>
	<td>
    	<input type="text"/>	
    </td>
</tr>
```

父子关系即为包含关系：td标签是tr标签的子标签，input标签是td标签的子标签

兄弟关系：一组标签拥有相同的父标签，并且彼此之间没有任何任何包含关系，还按从上到下的顺序分辈分

层级选择器：通过标签之间的父子或兄弟关系定位标签

1. 后代选择器：在某个元素的后面全部，包括子的，格式：body 
2. 子选择器：在某个元素的后面全部，不包括子的，格式：body>
3. 相邻弟弟选择器：+
4. 所有弟弟选择器：~

```html
<head>
    <style type="text/css">
        /*后代选择器*/
        #one p{
            font-size:30;
            color:blue;
        }
    </style>
</head>
<body>
    <div id=one>
        <p>
            这是第一个段落标签
        </p>
        <p>
            这是第二个段落标签
        </p>
        <span>span1</span>
    </div>
</body>
```



## 结构伪类选择器(垃圾)

1. first-child
2. last-child
3. nth-child
4. nth-of-type

## 属性选择器(常用)

属性可以用正则

# 美化网络元素

## 为什么要美化

1. 有效的传递页面信息
2. 吸引客户
3. 突出网页主题
4. 提高用户体验

##  文本样式

1. 颜色 color rgb rgba
2. 文本对齐的方式 text-align = center
3. 首行缩进 text-indent: 2em
4. 行高 line-height:
5. 装饰 text-decoration:
6. 文本图片水平对齐: vertical-align: middle
