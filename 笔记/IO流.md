# IO流分类

多种分类方式：

1. 按照流的方向分类

   参照物是内存

   从硬盘到内存是输入，读，输入流

   从内存到硬盘是输出，写，输出流

2. 按照读取方式分类

   有的流按照字节的方式读取数据，一次读取1个byte，等同于一次读取8个bit，万能流

   有的流按照字符方式读取数据，这种流只能读取普通文本文件，不能读取声音、视频、word文档等

# 包和接口

在java.io包下

所有流都实现了java.io.Closeable接口，都是可关闭的，用完流都应该用close()方法关闭流

所有的输出流都实现了java.io.Flushable接口，输出流在最终输出之后，一定要记得flush()，将管道中未输出的内容强行输出

# IO流四大家族

java.io.InputStream字节输入流

java.io.OutputStream字节输出流

java.io.Reader字符输入流

java.io.Writer字符输出流

四大家族首领都是抽象类

# 16个流

## 文件专属

java.io.FileInputStream

java.io.FileOutputStream

java.io.FileReader

java.io.FileWriter

## 转换流（将字节流转换为字符串）

java.io.InputStreamReader

java.io.OutputStreamWriter

## 缓冲流专属

java.io.BufferedReader

java.io.BufferedWriter

java.io.BufferedInputStream

java.io.BufferedOutputStream

---

readLine()方法读一行但不带换行符

## 数据流专属

java.io.DataInputStream

java.io.DataOutputStream

## 标准输出流

java.io.DataInputStream

java.io.DataOutputStream

不需要手动close()关闭

## 对象专属流

java.io.ObjectInputStream

java.io.ObjectOutputStream

# 节点流和包装流

当一个流的构造方法需要一个流时，被传进来的流叫节点流

外围的流叫包装流

# File类

1. File类和四大家族没有关系，故不能完成读写
2. File对象是文件名或路径的抽象表示形式

# 序列化和反序列化

序列化：Serialize java对象存储到文件中，将java对象的状态保存下来

反序列化：DeSerialize 将硬盘上的数据重新恢复到内存，恢复成java对象

类要实现Serializable接口，标志接口，JVM会默认提供序列化版本号

# transient

游离的，不参与序列化操作

# Java区分类

1. 首先是类名
2. 序列化版本号

# IO + Properties

经常改变的数据可以单独写到一个文件——配置文件，使用程序动态读取

属性配置文件建议以.properties结尾

属性配置文件中#是注释

不建议使用: 用=

最好不要有空格
