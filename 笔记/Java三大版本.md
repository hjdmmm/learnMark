# Java三大版本

- JavaSE标准版
- JavaME嵌入式开发（凉了）
- JavaEE：企业级开发，在进行商业开发时遵守开发规则，在商业开发中，往往需要Java类与不同服务器进行沟通来解决当前业务，由于在商业开发过程中，Java需要与13种不同的服务器沟通，因此SUN公司根据13种服务器特征指定13套接口，统称为JAVAEE规范

# JDK,JRE,JVM

JDK: Java Development Kit

JRE: Java Runtime Environment

JVM: Java Virtual Machine

# Java开发环境搭建

## 卸载JDK

1. 删除安装目录
2. 删除JAVA_HOME
3. 删除Path下关于Java的目录
4. java -version

## 安装JDK

1. 搜索JDK8,

2. 同意协议
3. 下载对应版本
4. 安装EXE
5. （系统变量）新建JAVA_HOME
6. 在Path变量中加上%JAVA_HOME%\bin和%JAVA_HOME%\jre\bin
7. java -version

notepad++

# Hello world

1. 随便新建一个文件夹存放代码

2. 新建java文件

   文件后缀名为.java

   Hello.java

3. 编写代码

   ```java
   public class Hello{
       public static void main(String[] args){
           System.out.print("Hello,world!");
       }
   }
   ```

4. 在cmd用javac编译，生成class文件

5. 用java运行

# Java程序运行机制

编译型：翻译官把整本书翻译，不能实时更新		操作系统

解释性：一边翻一边读		网页

# IDEA安装

IDE集成开发环境，用来开发程序的程序

jetbrains捷克公司

WebStorm前端

菜单栏

src文件夹写代码