# HTML

超文本标记语言(程序员不能扩展)

HTML主要用途：做页面展示，不会做数据存储

HTML语法松散，不区分大小写

HTML还涉及到：CSS(修饰HTML)，DTD(Document Type Defined，约束HTML，约束HTML中能有那些标签，标签中应该有哪些属性)，schema(DTD的升级版，语法更新一些)

HTML不可以扩展，是因为程序员不能在HTML文件中随意编写标签，程序员不能干涉DTD文件，DTD文件是W3C制定的规范、约束，这个约束程序员只能用，不能改

# XML

可扩展的标记语言(程序员可对XML进行扩展)

主要用途是：数据存储和数据描述，是一个优良的配置文件，相当于一个小型的数据库

XML不依赖任何一种编程语言，是独立的W3C提供的规范，所以可以完成多种语言之间的数据交换。

XML还涉及到：XSL(等同于CSS，修饰XML文件)，DTD，schema

XML是可扩展的，因为XML中的DTD是程序员自己定义的，标签可以自定义

XML后缀名：.xml

DTD后缀名：.dtd

schema后缀名：.xsl

```xml
<?xml version="1.0" encoding="GB18030" ?>
<person-info>
	<xml_name/>
	<student>
		<id>001</id>
		<name><张三/></name>
		<age>10</age>
	</student>
	<teacher id="1" name="李四"/>
	<student id="11" name="王五">
		<desc>
			<![CDATA[<<Java编程思想>>]]>
		</desc>
	</student>
	<_student1/>
	<student/>
</person-info>
```



# XML文件解析

## DOM解析

原理：在开始解析XML文件的时候，将整个XML文件全部加载到内存中，在内存中编程语言将XML文件映射成一棵DOM树，这棵树就是一个对象，然后我们可以对这棵树上任何节点进行增删改查操作，由于这棵树全部都在内存中，解析过去的节点可以再次解析，比较灵活

优点：灵活，解析过去的节点，可以再次解析

缺点：如果XML文件比较大，可能会导致内存溢出，即使内存不溢出，也会消耗大量内存

使用场景：如果很灵活的操作每一个元素，选用DOM解析，但是注意文件要小一些

## SAX解析

原理：SAX解析是基于事件驱动的解析方式，他的解析不需要将整个XML文件全部装载到内存中，解析的时候是有顺序的，在XML文件中从上往下解析，遇到开始标签，表示发生了一个特定的事件，此时执行一段特定的程序，遇到结束标签表示又发生了一个特定的事件，此时执行一段特定的程序，遇到结束标签表示又发生了一个特定的事件，此时执行一段特定的程序完成解析

优点：不需要在内存中装载xml文件

缺点：解析过去的节点不能再次解析，除非从头开始

使用场景：大文件

## java解析XML文件

JDK自带了一套实现W3C规范的库org.w3c.dom. * ， org.xml.sax.*

常用 DOM4J(Dom for Java)，JDOM，...

为了提高解析XML文件的效率，涉及到XPATH(这是一种标签的匹配方式，类似正则表达式，方便程序快速定位xml文件的某个标签)

