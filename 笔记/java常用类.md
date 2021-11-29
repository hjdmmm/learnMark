# API

应用程序编程接口

每一套API一般都有一套API英文接口

# Object

JDK类库的根类

老祖宗类，任何一个类都直接或间接继承Object

方法：

- protected Object clone() 负责对象克隆
- int hashcode() 获取对象哈希值
- boolean equals(Object obj) 判断两个对象是否相等
- String toString() 将对象转换成字符串形式
- protected void finalize() 垃圾回收器负责调用的方法



## toString()

源代码的默认实现是：类名@内存地址十六进制

目的是：通过调用这个方法可以将一个java对象转换为字符串

SUN公司建议所有的子类都重写该方法，重写后越简单、越明了越好



## equals()

源代码的默认实现是：用==比较两对象

目的是：验证两个对象是否相等

引用数据类型用==是比较内存地址是否相等，一般不满足目的

注意方法重写必须满足方法名、返回值、参数列表全都相同，故要重写equals()方法，经常会需要将obj强转，可用obj instance 要转的Class判断是否能强转

判断基本数据类型是否相等用==，引用数据类型是否相等用.equals()

## finalize()

这个方法不需要程序员手动调用，由GC负责调用

该方法在一个对象即将被GC回收时执行

如果程序员想要在对象销毁时执行一段代码，可以重写finalize()方法，但不用手动调用

项目开发中有记录对象释放时间的要求，就可以重写finalize()

提示：java中的GC不是轻易启动的

# Arrays

数组的工具类

所有方法都是静态的

## sort()

## binarySearch()

# String

在JDK中双引号括起来的字符串，都是直接存储在方法区的字符串常量池中，因为在开发中字符串太常用，可以提高效率

双引号括起来的内容是不可变的

---

如果直接s1 = "abc"，则栈中的s1直接指向常量池中的"abc"

如果s1 = new String("abc")，则栈中的s1指向堆中的String对象，堆中的String对象指向常量池中的"abc"

## String(byte[] bytes)

byte[] bytes = {97, 98, 99};

String s1 = new String(bytes);

会得到"abc"

## String(char[] chars)

## charAt(int index)

输出相应索引的char

## compareTo(String s)

用字符串第一个字符与另一个字符串第一个字符比较，以此类推知道能找到区别或判断完全相等为止

## contains(CharSequence s)

CharSequence是一个接口

String、StringBuffer、StringBuilder实现了这个接口

## endsWith(String s)

## equalsIgnoreCase(String s)

## getBytes()

## indexOf(String s)

判断某个子字符串在当前字符串中第一次出现的索引

## length()

数组长度是length属性

字符串长度是length()方法

## lastIndexOf(String s)

## replace(CharSequence target, CharSequence replacement)

## split(String s)

以s为分隔符拆分，返回String[]

## startsWith(String prefix)

## substring(int beginIndex, int endIndex)

包含begin，不包含end

## toCharArray()

## toLowerCase()

## toUpperCase()

## trim()

去除前后空白，但不去除中间空白

## valueOf(各种)

String中唯一一个static，

对于抽象数据类型的对象，实际上调用该对象的toString()方法

# StringBuffer & StringBuilder

String本质是final byte[] value

StringBuffer和StringBuilder是byte[] value

垃圾回收器不能扫有final修饰的常量，所以用StringBuffer更节约空间

StringBuffer中的方法都有synchronized，保障其线程安全

StringBuilder非线程安全，局部变量用

## append()

# 八种包装类

八种基本数据类型的包装类

为了将基本数据类型抽象成类，便于传参等操作

---

八种包装类其中6个都是数字对应的包装类，它们的父类都是Number，Number是一个抽象类，无法实例化

## intValue()等

拆箱，将引用数据类型转换为基本数据类型

new Integer()为装箱

在JDK1.5后可以自动拆装箱，如Integer i = 3，因此Number类的方法已废弃

## Integer.MAX_VALUE等

常量，可快速获取最值

## parseInt(String s)

转换为int基本数据类型

## valueOf(int或String)

转换为Integer包装类

## toBinaryString(int i)

转换为二进制字符串

## toHexString(int i)

转换为十六进制字符串

## toOctalString(int i)

转换为八进制字符串

# 时间有关的类

## Date

在java.util包下

### Date()

无参构造，获取系统当前时间，精确到毫秒

### Date(long date)

date指自1970年1月1日0时以来的毫秒数

## SimpleDateFormat

在java.text包下

- yyyy年
- MM月
- dd日
- HH时
- mm分
- ss秒
- SSS毫秒

除了y M d H m s S以外的字符，可以随便写

### SimpleDateFormat(String s)

s = "yyyy-MM-dd HH:mm:ss SSS"

### format(Date date)

将一个Date时间格式化

### parse(String s)

将s按照格式转化为Date对象

## System

### currentTimeMillis()

获取自从1970年1月1日0点到现在时间的毫秒数



# System

## out

out是一个PrintStream静态变量

println()是PrintStream类的方法

## gc()

建议启动垃圾回收器

## exit(int i)

退出JVM

## currentTimeMillis()

获取自从1970年1月1日0点到现在时间的毫秒数

# DecimalFormat

- #代表任意数字
- , 代表千分位
- . 代表小数点
- 0代表不够时补0

## DecimalFormat(String s)

## format(double等)

将数字转化为格式化字符串

# BigDecimal

## BigDecimal(int等)

## add(BigDecimal b)

## divide(BigDecimal b)

# Random

## Random()

产生int范围内的随机数

## nextInt(int i)

产生一个[0,i) 之间的int随机数

