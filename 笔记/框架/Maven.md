# Maven简介

传统项目的弊端：

1. 很多模块，手动管理模块间的关系很困难
2. 需要很多第三方功能，需要很多jar文件，需要手工从网络中获取各个jar
3. 需要手动管理jar版本
4. 手动管理jar文件之间的依赖

maven好处：

1. maven可以管理jar文件
2. 自动下载jar和它的文档，源代码
3. 管理jar直接的依赖
4. 管理你需要的jar版本
5. 帮你编译程序
6. 帮你测试代码
7. 帮你打包文件为jar和war
8. 帮你部署项目

maven生命周期：就是maven构建项目的过程：清理，编译，测试，报告，打包，安装，部署

## 构建

项目的构建是面向过程的，就是一些步骤，完成项目代码的编译，测试，运行，打包，部署等等

maven支持的构建包括：

1. 清理：把之前项目编译的东西删除掉
2. 编译：把.java编译为.class
3. 测试：maven可以执行测试程序代码，验证功能是否正确
4. 报告：生成测试结果的文件
5. 打包：把所有的class文件，配置文件等所有资源放到一个压缩文件中，java项目为.jar，web项目为.war
6. 安装：把5中生成的jar，war安装到本机仓库
7. 部署：把程序安装好可以执行

## maven使用

1. 独立使用maven：使用maven的各种命令
2. 结合IDEA使用

## maven安装

下载，解压，配置环境变量

# 核心概念

1. POM：一个文件，名称是pom.xml，项目对象模型，maven把一个项目当做一个模型来用，控制maven构建项目的过程，管理jar依赖
2. 约定的目录结构：maven项目的文件和目录的位置都是规定的
3. 坐标：是一个唯一的字符串，用来表示资源的
4. 依赖管理：管理项目可以使用的jar包
5. 仓库管理：资源存放的位置
6. 生命周期：maven构建项目的过程
7. 插件和目标：执行maven构建的时候用的工具
8. 继承
9. 聚合

# 约定目录结构

Hello/

​	---/src

​		---/main

​			---/java

​			---/resources

​		---/test

​			---/java

​			---/resources

​	---/pom.xml

# 仓库

仓库存放maven使用的jar包和我们项目使用的jar包

仓库分为本地仓库和远程仓库，远程仓库又分为中央仓库(中央仓库是最权威的)，中央仓库的镜像，私服(一般为公司内部的局域网)

仓库使用不需要人为参与

# pom文件

Project Object Model 项目对象模型

Maven把一个项目的结构和内容抽象成一个模型，在xml文件中进行声明，以方便进行构建和描述

groupId+artifactId+version称为坐标(gav)，在远程仓库中唯一地标识一个项目

| 信息                         | 作用                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| modelVersion                 | Maven模型的版本，一般为4.0.0                                 |
| groupId                      | 组织id，一般是域名倒写或+项目名，com.baidu; com.baidu.appolo |
| artifactId                   | 项目名称，对应groupId中项目的子项目                          |
| version                      | 项目的版本号，不稳定版本带-SNAPSHOT(快照)                    |
| packaging                    | 项目打包扩展名：jar，war，rar等                              |
| dependencies中嵌套dependency | 依赖                                                         |
| properties                   | 属性                                                         |
| build                        | maven在进行项目构建时配置信息                                |
| parent                       | 继承                                                         |
| modules                      | 聚合                                                         |

# Maven常用命令

执行命令必须在有pom.xml的目录下

mvn clean：清理target目录，即删除原来编译和测试的目录，但是已经install到仓库的包不会删除

mvn complie：编译主程序

mvn test-complie：编译test程序

mvn test：测试，生成surefire-reports目录保存测试结果

mvn package：打包主程序，会先进行编译主程序，编译测试程序，进行测试

mvn install：安装主程序，即打包并按照本工程坐标保存到本地仓库中

mvn deploy：部署主程序，即打包保存到本地仓库和远程仓库中，并且自动把项目部署到web容器中

# Maven常用依赖

## 单元测试

用的是junit，junit是一个专门测试的框架，测试的是类中的方法，每个方法都是独立测试的，方法是测试的基本单位(单元，指单个方法)

maven借助单元测试，批量的测试类中的大量方法是否符合预期

使用步骤：

1. 添加依赖

2. 在src/test/java创建测试类(Test+要测试的类名)

3. 在测试类中创建测试方法Test+要测试的方法名

   ```java
   //必须是public，必须没有返回值
   @Test
   public void testAdd(){
       //测试add()方法是否正确
   }
   ```

   

# Maven的插件

maven命令执行时，真正完成功能的是插件，插件就是一些jar文件

```xml
<!-- pom.xml中 -->
<build>
	<plugin>
    	
    </plugin>
</build>
```

# IDEA中使用Maven

idea中内置了maven，但是我们一般不用

使用自己安装的maven，需要覆盖idea中的默认设置

配置方法：进入settings中配置Maven Home directory，User Setting File，Local Repository

# 依赖应用范围

用scope标签

compile：只在编译阶段

test：只在测试阶段

provided：打包前的阶段，打包后不放进包内，由tomcat服务器提供

# Maven常用操作

## Maven属性设置

properties标签，设置maven的常用属性

## Maven全局变量

1. 在properties标签中通过自定义标签声明变量，标签名就是变量名
2. 在pom.xml文件中的其他位置使用$(标签名)使用变量值

自定义全局变量一般用来定义依赖版本号

## 资源插件

在build标签中的resources标签

1. 默认没有使用resources的时候，maven执行代码时，只拷贝src/main/resources目录的文件到target/classes目录中，对src/main/java目录的非java文件是不拷贝的
2. 若我们需要拷贝非src/main/resources目录的非java文件到target对应的文件夹中，就要用resources标签

比如应用mybatis时dao包下的.xml文件

