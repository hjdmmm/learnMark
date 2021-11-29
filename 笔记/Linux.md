# Linux概述

Linux：Linux is not unix，类unix

狭义的linux：linux kernel

广义的linux：linux kernel+软件包

## 发行版本

Linux发行版就是将Linux内核与应用软件做一个打包

RedHat，CentOS，Ubuntu

# Linux目录说明

bin->usr/bin：存放最常使用的命令

etc：这个目录存放所有的系统管理所需要的配置文件

opt：存放第三方软件，其实我们一般不用

var：存放日志

usr/local：存放第三方软件，并自动配置环境变量

home：普通用户的主目录

root：root用户的主目录

lib->usr/lib：存放着系统最基本的动态链接共享库，相当于DLL

mnt：光驱

tmp：临时文件

# 远程工具

XShell，SecureCRT，putty是远程工具

Xftp，WinSCP是文件管理工具

# Linux命令

## 磁盘管理

pwd：显示当前目录位置

ll：列出当前目录下目录及文件

ls：列出当前目录下目录及文件，但没有详细信息，只有名称

cd：切换文件夹

## 文件管理

mkdir 目录名：创建文件夹

---

rm 文件名：删除文件，不能删除文件夹，会询问

rm -rf 目录名：-rf中的r表示按递归(recursion)方式，因为文件夹里套有文件夹，f代表强制(force)删除，不询问

---

cp 被复制文件名 复制后文件名(只写目录，会在该目录创建同名文件)：覆盖时会询问

cp 被复制目录名 复制后的目录名

---

cat 文件名：查看文件全部内容

more 文件名：显示一屏内容，按空格翻页，按回车显示下一行，按ctrl+c强制退出

head -n 行数：显示从头数0~行数，默认是十行

tail -n 行数：显示从后数行数

---

grep -i(忽略大小写)w(以单词方式来搜索) 字符串 文件名：文件内按行搜索，展示含有指定字符串的行

echo 字符串 >(重定向) 文件名：创建含某个字符串的文本文件

## 系统命令

date

su 用户名：切换用户，root换普通用户不用输密码；普通用户换root要输密码

clear：清屏

shutdown -h 关机时间

reboot：重启

ps -ef：显示系统当前运行进程(程序)

kill -9(强制结束) 进程id：杀死某个进程

## 压缩解压

tar 参数(必须给) 要压缩或解压的文件或目录

常用参数：

z：压缩时表示用gzip压缩，生成xxx.tar.gz；解压时表示用gunzip解压

c：仅仅打包

v：显示压缩过程

f 名称：指定压缩文件名字

x：仅仅解压

t：查看压缩文件内部内容

C 目录：解压到指定目录

-zcvf 名称：压缩

-zxvf 名称 -C 解压到：解压

-tf 名称：查看压缩文件

##  网络通信

ifconfig：network interfaces configuring

ping ip

## 网络访问

curl ip： 用url语法在命令行方式下工作的开源文件传输工具，常用来测试网络访问，模拟用户访问

wget 资源地址：下载资源

# 权限管理

UGO模式，user(创建者)，group(创建者所属的组)，other(其他人)

用ll指令可以看到

![image-20211102141113462](C:\Users\hjdmm\AppData\Roaming\Typora\typora-user-images\image-20211102141113462.png)

读权限：4

写权限：2

执行权限：1

rwx=4+2+1=7

r-x=4+1=5

r--=4

常见644,755,777三种权限

## 权限命令

chmod xxx 文件：具体权限

chown 新的所有者账户 文件：更改文件所有者

# 管道和重定向

重定向覆盖：>

重定向换行追加：>>

管道：A|B，A的输出作为B的输入

# vi和vim编辑器

vi是linux下标配的一个纯字符界面的文本编辑器，由于不是图形界面，相关的操作都要通过键盘输入命令来完成

vim是vi的升级版本，完全兼容vi，vim是在vi的基础上增加一些功能，比如语法着色等

## 命令模式

按Esc键进入命令模式，无法编辑文件

:wq(冒号键，w键，q键)：保存退出

:q!：不保存退出

dd：删除光标所在行

yy：复制光标所在行到缓冲区

p：粘贴缓冲区中的内容

gg：光标回到文件第一行

GG：光标回到文件最后一行

^：光标移动到当前行行首

$：光标移动到当前行行尾

/关键字：搜索想要的的关键字，按n键定位下一条记录

## 编辑模式

按a或i键进入编辑模式，此时底部会出现insert

# 安装软件

yum：Yellow dog Updater, Modified，是一个在RedHat、Fedora、CentOS中的软件包管理器，能够从指定服务器自动下载软件包并且安装，可以自动处理软件包之间的依赖关系；并且一次安装所有依赖的软件包，无须繁琐地一次次下载安装

## 指令

yum search 安装包名称的关键字：查找软件包 

yum install 安装包名字

yum remove 安装包名字

yum list installed：列出所有安装的软件

yum clean all：清除已安装软件包的下载文件

# 安装jdk

1. 下载jdk.tar.gz文件
2. 解压缩 tar -zxvf jdk.tar.gz -C /usr/local
3. cd /etc目录下
4. 打开/etc/profile在结尾加上相关行

# 安装Tomcat

# 安装MySQL

详情见mysql笔记

# 将web项目部署到linux中

## war方式部署

把web应用打包为.war扩展名的文件，把xxx.war文件部署到tomcat的webapps目录，即可在tomcat中运行web应用

