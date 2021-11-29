# 初识MySQL
## 为什么学习数据库

1. 岗位需求
2. 大数据时代
3. 数据库是所有软件体系中最核心的存在

## 数据库分类

关系型数据库(SQL)：Excel，MySQL，Oracle，SQL Server

管理的表文件之间往往具有隶属关系特征，可以完整描述一段数据，但是查询时由于涉及数据较多，查询速度较慢

非关系型数据库(nosql, no just sql)：MongoDB

管理表文件都是独立，无法描述一段完整的数据 ，由于每次查询的大数据较少，因此查询速度较快

## 概念区分

1. DB，数据库，以文件形式在硬盘上存在，一个数据库一般存储500W以下的数据
2. DBMS，管理数据库的系统，MySQL，Oracle，DB2
3. SQL：结构化查询语言，是一门标准通用的语言，标准SQL适用于所有的数据库产品，属于高级语言，语句会编译

## 表

table，数据库的基本组成单元，所有的数据都以表格的形式组织，目的是增强可读性

一个表包括：行(数据/记录/data)，列(字段/column)

## 存储引擎

Oracle中叫"表的存储方式"

INNODB 默认使用，支持行级锁安全性高，支持事务，多表多用户操作,

MYISAM 早期使用，可被压缩节约空间， 可以转换为只读表查询速度较快，但不支持事务

MEMORY 不能包含TEXT或BLOB字段，结构存储在磁盘中，数据和索引存储在内存中，查询速度最快，以前叫HEPA引擎

|              | MYISAM | INNODB | MEMORY       |
| ------------ | ------ | ------ | ------------ |
| 事务支持     | 不支持 | 支持   | 不支持       |
| 数据行锁定   | 不支持 | 支持   | 支持         |
| 外键约束     | 不支持 | 支持   | 不支持       |
| 全文索引     | 支持   | 不支持 | 支持         |
| 表空间的大小 | 较小   | 较大   | 存储在内存中 |

## 安装MySQL

1. 解压
2. 配置环境变量path下新建MySQL的bin
3. 新建my.ini配置文件
4. 管理员模式运行cmd执行命令
5. 安装MySQL服务
6. 初始化数据库
7. 启动MySQL修改密码

登录mysql账户，-p后不能加空格，否则会认为是密码的一部分

## 安装SQLyog

SQLyog可视化管理

# MySQL命令行指令

use 数据库名;		切换数据库，可不用 ; 结尾

show databases;		列出所有的数据库

show tables;		列出数据库内所有的表

select database();

select version();

\c		终止一条语句

exit，\q

desc 表名; 	查看表的结构

show create table 表名; 		查看创建表时的语句

(cmd的) ctrl+c	强行终止命令

show engines \G	了解当前有哪些可用的存储引擎

explain 语句;		查看指定语句的执行计划

# 通用SQL语句

注意区分通用SQL语句和MySQL的命令！！！

任何一条SQL语句都以 ; 结尾

window下SQL语句不区分大小写

字符串用单引号，避免使用双引号

表内字段除最后一个外结尾加 ,

``标识符在MySQL中可用其包裹，但其他语言不支持，不建议用

注释用 单行-- 	多行/**/

所有符号全部用英文

实际开发中不建议使用*通配符，因为效率较低



## 运算符

| 操作符        | 含义     |
| ------------- | -------- |
| =             | 等于     |
| <>或!=        | 不等于   |
| >等等         | 比较     |
| BETWEEN   AND | 闭合区间 |
| AND或&&       | 与       |
| OR或\|\|      | 或       |
| Not或！       | 非       |
| is null     |          |
| is not null |          |
| between and | 在范围内(包括边界)，结果为真       |
| like        | SQL匹配                            |
| in          | 等同于or，不是区间，是具体的值 |
| not in |  |

## 数据库字段的数据类型

### 数值

1. tinyint 1个字节
2. smallint 2个字节
3. mediumint 3个字节
4. **int 4个字节**
5. **bigint 8个字节**
6. **float 4个字节**
7. double 8个字节
8. decimal 字符串形式的浮点数

### 字符串

1. **char 定长不可变字符串 0~255** 不可变指char(3)时存储"ab"变成 a,b,[空格]
2. **varchar 定长可变字符串 0~65535**  定长指varchar(3)能输入3个字母或三个汉字；可变指存储空间可以**缩小**
3. tinytext 微型文本 2^8 - 1
4. text 文本串 2^16 - 1

针对char类型字段进行数据读取时，MySQL服务器自动将字符串结尾处的空格去掉，因此如果插入字符串以空格结尾，不要添加到char类型字段中

### 时间日期

1. **date YYYY-MM-DD**
2. time HH:mm:ss
3. **datetime YYYY-MM-DD HH:mm:ss 最常用**
4. timestamp 时间戳 会根据当地时区自动转换
5. year 年份

### 大对象

1. BLOB 二进制大对象(图片视频等流媒体信息)
2. CLOB 字符大对象(较大的文本比如可以存储4G字符串)

### null

- 没有值
- 不要用null运算



## DML

DML语言：数据操作语言，对表中数据增删改

关键字：insert，delete，update

### 添加

insert into 表名(字段1,字段2) values('插入内容1','插入内容2'), ('插入内容1','插入内容2')

1. 字段和字段之间用英文逗号隔开
2. 可以同时插入多条数据
3. 字段可以省略，但后面的值必须与字段创建顺序一一对应

### 修改

update 表名 set 字段 = 值 where 条件

注意：没有条件整张表数据全部更新

### 删除

delete from 表名 where 条件

**删除大表中的数据(DDL语句)  TRUNCATE TABLE 表名**

DELETE删除的问题，重启数据库时

- innodb的自增列是存在内存中的断电即失去
- myisam继续从上一个自增开始，存在内存中

## DQL

Data Query Language 数据查询语言

- 所有的查询操作都用它
- 简单的查询，复杂的查询都可以
- 数据库中最核心的语言，最重要，使用频率最高的语句

关键字：select

### 指定查询字段

select像切蛋糕一样，将指定字段下所有的数据读取出来，在内存中将读取数据组成一个全新的临时表，每一个查询语句在执行时，实际上操作的都是上一个查询命令生成的临时表，在当前查询命令执行完毕后，上一个查询命令生成的临时表将自动从内存中销毁

select 字段 from 表名

> as 别名

可以给字段和表起别名，当列的名字不能见名知意时，as关键字可以省略

> distinct 去重

去除select中重复的数据

select distinct 字段 from 表名

distinct只能出现在所有字段的最前面，表示多个字段联合去重



### 模糊查询

like中%代表任意多个字符，_代表任意一个字符

### 排序

> order by 字段 

以某个字段升序排列

asc升序，desc降序

### 执行顺序

1. from 表名
2. join 表 on 条件
3. where 条件
4. group by 字段
5. having 字段
6. 聚合函数
7. select 字段
8. order by 排序字段
9. limit 

### 写的顺序

1. select
2. from
3. join
4. on
5. where
6. group by
7. having
8. order by
9. limit

### 分组函数(多行处理函数)

输入多行，最终输出一行

分组函数自动忽略NULL

一般和group by联合使用

分组函数不能放在where，因为group by在where后执行

- count 计数
- sum 求和
- avg 平均值
- max 最大值
- min 最小值

### 单行处理函数

输入一行，输出一行

ifnull(可能为NULL的数据, 被当做什么处理)空处理函数

### group by和having

先用group by分组，再用having过滤

能用where过滤的优先用where，涉及平均值等where解决不了的用having

group by是唯一一个会生成多个临时表的命令

having负责将group by生成的临时表中不满足条件的临时表从内存里面删除，不生成新的临时表

select和group by联合使用时，只会读取临时表下指定字段下第一个数据，此时select抓取的数据应该是当前临时表所有数据行共有的特征，所以此时select抓取的字段应该是group by分组所用的字段

多字段分组：分组字段出现的顺序不影响结果，group by一次只能根据一个字段分组，从第二个分组字段开始，操作的是上一个分组字段生成的临时表

### 多表查询

#### 连接查询

首先确保两张表之间存在隶属关系，然后就可以将两张表中数据行沿着水平方向拼接

笛卡尔积现象：两个集合中的每个有关的字段都要配对

##### 内连接

###### 等值连接

92	 where 第一个表的字段=第二个表的字段

99	 join 第二个表 on 第一个表的字段=第二个表的字段

###### 自连接

一张表看做两张表，自己连接自己，通过取

##### 外连接(左副右主)

角色划分：

1. 需要被帮助的表
2. 不要被帮助的表

原理：如果需要被帮助表中某行数据与不需要被帮助表所有的数据行都无法拼接为合法数据，此时已将这个数据行作为一个独立的数据行存入到新的临时表

左外连接：from 需要被帮助的表(主表) left join 不需要被帮助的表(副表)

右外连接：from 不需要被帮助的表(副表) right join 需要被帮助的表(主表) 

#### union

联合查询

要求参与合并的两个临时表的字段结构必须保持一致(字段个数、字段类型顺序)

将两张表中数据行沿着垂直方向堆砌

生成的临时表字段只能来自于第一个临时表字段

union会自动将两个表内容相同数据行进行过滤，自动去重，用union all取消该功能

### 子查询

```sql
select * from emp where sal > (select avg(sal) from emp);
select t.* from (select deptno,avg(sal) as avgsal from emp group by deptno) t join salgrade s on t.avgsal between s.losal and s.hisal;
select e.ename,(select d.dname from dept d where e.deptno = d.deptno) as dname from emp e;
```
### limit

limit是mysql特有的，Oracle有一个相同的机制rownum

limit取结果集中的部分数据

limit (startIndex，不写为0),length

## DDL

DDL：数据定义语言，对表的结构进行增删改

一般使用工具即可，因为实际开发中设计好表以后再修改的情况很少，这意味着对之前设计的否定

修改表结构的语句不会出现在java中，出现在java代码中的sql包括insert，delete，update，select

增删改查有术语CRUD  create增，Retrieve检索，Update更新，Delete删除



关键字：create，drop，alter，truncate

---

创建数据库

``` mysql
create database [IF NOT EXISTS] base;
```

删除数据库

``` mysql
drop database [IF EXISTS] base;
```

使用数据库

``` mysql
USE `base`
-- 在table键上面，反单引号
```

修改数据库

``` mysql
ALTER TABLE teacher RENAME AS teacher1 --修改表名
ALTER TABLE teacher1 ADD age int(3) --增加字段
ALTER TABLE teacher1 MODIFY age VARCHAR(3) --修改字段约束
ALTER TABLE teacher1 CHANGE age age1 int(3) --修改字段约束加上重命名字段
ALTER TABLE teacher1 DROP age1 --删除字段
DROP TABLE IF EXISTS teacher1 --删除表
alter database <数据库名> character set utf8; --改变编码
```

## TCL

transaction control language 事务控制语言

关键字：commit，rollback

## DCL

数据控制语言

关键字：grant，revoke

# 约束

非空约束(not null)：约束的字段不能为null

唯一约束(unique)：约束字段不能重复，但可以为NULL

主键约束(primary key，简称PK)：约束的字段既不能为NULL，也不能重复

外键约束(foreign key，简称FK)：

检查约束(check)：Oracle数据库才有，MySQL没有

---

唯一性约束分为列级约束和表级约束，列级约束指单个字段不能重复，表级约束指多个字段联合约束

但是可以有很多个null，因为两个null不能用=比较是否相等

```mysql
usercode varchar(255) unique,
username varchar(255) unique
#列级约束

usercode varchar(255),
username varchar(255),
unique(usercode,username)
#表级约束
```

---

主键可以分为单一主键和复合主键，复合主键违背三范式，不建议使用

还可以分为自然主键和业务主键(身份证号等)，最好不要拿和业务有关的字段做主键，否则耦合度高，不好

一张表的主键约束只能有一个

自增：自动在上一条记录的基础上+1，通常用来设定为唯一的主键，必须为整数类型

---

外键约束

被引用字段的表是父表，引用了别人字段的表是子表

被引用的字段不一定是主键，但必须具有unique约束，但一般都是引用主键

外键字段值可以为NULL

```mysql
foreign key(classno) references t_class(cno)
```

物理外键，数据库级的外键，不建议使用

数据库就是单纯的表，只用来存数据，只有行和列

我们想使用多张表的数据，想使用外键，应该用程序去实现



---

了解即可

Unsigned：无符号整数，即不能声明为正数

zerofill：不足的位数用0填充，如int(3) 005

AUTO_INCREMENT自增：自动在上一条记录的基础上+1，通常用来设定为唯一的主键，必须为整数类型

not null(非空)：如果设置为NOT NULL，不赋值就报错，如果设置为null，则默认值为null

默认：就是默认值

# 事务

## 什么是事务

一个事务是一个完整的业务逻辑单元，不可再分

比如：银行账户转账，从A账户向B账户转账10000，需要执行两条update语句

update t_act set balance = balance - 10000 where actno = 'act-001'

update t_act set balance = balance - 10000 where actno = 'act-002'

以上两条DML语句必须同时成功或同时失败，要保证就必须使用数据库的"事务机制"

和事务有关的语句只有DML语句(insert delete update)

## 事务机制

假设先执行一条insert，再执行一条update，最后执行一条delete

---

开启事务机制

1. 执行insert语句，执行成功之后，把这个执行记录到数据库的操作历史当中，不会真正修改硬盘中的数据
2. 执行update语句，这个执行也是记录一下历史操作，不会真正的修改硬盘上的数据
3. 执行delete语句，也不会真正修改硬盘上的数据

---

结束事务机制：提交事务或者回滚事务，清空历史操作记录

## 事务的特性

A.独立性：事务是最小的工作单元，不可再分

C.一致性：事务必须保证多条DML语句同时成功或者同时失败

I.隔离性：事务A与事务B之间无关

D.持久性：最终数据必须持久化到硬盘文件中，事务才算成功地结束

## 隔离性

Oracle默认是读已提交

MySQL默认是可重复读

必须重启数据库才能使更改隔离级别生效

### 第一级别：读未提交

read uncommitted

对方事务还未提交，我们当前事务可以读取到对方未提交的数据

存在脏读(Dirty Read)现象，读到脏的数据

### 第二级别：读已提交

read committed

对方事务提交了就可读

读已提交存在不可重复读的问题

### 第三级别：可重复读

repeatable read

解决了不可重复读的问题

存在问题：读取到的数据是幻读

### 第四级别：序列化读/串行化读

解决了上述问题，但是效率低

# 索引

## 什么是索引

索引相当于一本书的目录，通过目录可以快速的找到对应的资源

查询一张表有两种方式：全表扫描或者根据索引检索，索引缩小了扫描的范围

索引虽然可以提高检索效率，但不能随意添加索引，因为索引也是数据库当中的对象，也需要数据库不断地维护，是有维护成本的，当表中的数据经常被修改的时候，就不适合添加索引

## 什么时候加索引

1. 数据量庞大
2. 该字段很少DML操作
3. 该字段经常出现在where字句中

注意：主键约束和具有unique约束和外键约束的字段会自动添加索引

## 语句

create index 索引名称 on 表名(字段名);

drop index 索引名称 on 表名;

## 实现原理

底层的数据结构是B+树

通过B Tree缩小扫描范围，底层索引进行了排序，分区，索引关联了物理地址，最终通过索引检索到数据之后，获取物理地址，通过物理地址定位表中数据

事先对字段中内容进行排序，在where命令进行定位时，避免对表中所有的数据行进行遍历，提高效率

## 分类

- 单一索引：给单个字段添加索引

- 复合索引：给多个字段联合起来添加1个索引
- 主键索引：主键上会自动添加索引
- 唯一索引：有unique约束的字段上会自动添加索引

## 失效情况

模糊查询时第一个通配符使用的是% (like '%A%')

## 执行计划

explain select * from emp where ename = 'SMITH';

查询该语句的执行过程

通过执行计划判断执行效率：

1. 在执行计划中，通过type属性展示查询语句执行效率
2. 分类(慢--快)：all全部遍历；index也对所有数据遍历，在抓取字段内容时从索引中抓取，基本同all；range不会遍历，直接从索引得到定位的数据行行数；ref不会遍历，直接从索引得到定位的数据行行数，同时根据定位条件一次只能得到一个数据行；const根据主键字段上的索引进行定位，是执行效率最快的，但是实际基本不会用到
3. 如果从索引获得的数据行行数达到了表文件总行数的1/3时，此时考虑运行成本问题放弃使用索引

# 视图(view)

## 什么是视图

站在不同的角度去看数据

隐藏了表的实现细节，但还是可以进行CRUD，让开发人员不会知道其具体操作的表

相当于可以对原表进行CRUD的临时表，可以实现临时表的复用

## 语句

create view 视图名 from 表名;

create view 视图名 as 对原表的查询语句;

drop view 视图名;

# DBA命令

## 导出数据

在cmd中，不登录mysql

mysqldump 表名 (可指定表)>输出路径 -u账户 -p密码

## 导入数据

create database 新库;

use 新库;

source 导入的库

# 数据库设计三范式

隶属关系：一个老师培养多个学员，一个部门管理多个职员

一方表：存放一方数据，dept

多方表：存放多方数据，emp

## 表文件字段分类

1. 主键字段：用于存档主键编号的字段，每一个表都应该存在一个主键字段，既不能出现null，也不能出现重复值
2. 非主键字段：描述主键编号
3. 外键字段：只存在于多方表中，描述多方数据与一方数据之间的依赖关系，外键字段的值应该来自于一方表的主键值

## 设计范式

设计表的依据，按照这个三范式设计的表不会出现数据冗余

在实际开发中，以满足客户的需求为主，有的时候会拿冗余换执行速度

## 第一范式

每个表都应具有主键，且每一个字段原子性不可再分

## 第二范式

建立在第一范式的基础上，所有非主键字段完全依赖主键，不能产生部分依赖

多对多，三张表，关系表两个外键

## 第三范式

建立在第二范式的基础上，所有非主键字段直接依赖主键，不能产生传递依赖

一对多，两张表，多的表加外键

## 一对一设计

一个人一个身份证

杂糅：只用一张表存储，有时用此提高检索速度

主键共享：第二张表的主键作为外键关联第一张表的主键

外键唯一(最好的)：第二张表加一个既有外键又有唯一性约束的字段关联第一张表的主键(第一范式)

## 一对多设计

一个班级对应多个学生

两张表，多的表加外键(第三范式)

加外键，指外键关联，但实际开发的时候为了提高效率一般不加外键约束，通过其他方式关联

## 多对多设计

学生表，课程表

联合主键表中有两个字段：sno(fk)，cno(fk)，属于sno+cno联合fk

# 字段类型的设计

id：int/bigint

其他字段：varchar

当对日期等计算的需求不高的，在开发的时候一律用string，非常方便

