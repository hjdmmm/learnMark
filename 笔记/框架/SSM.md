# SSM编程

SpringMVC+Spring+MyBatis整合，是当前最流行的JavaEE开发技术架构，其实SSM整合实质，仅仅是将MyBatis整合入Spring，因为SpringMVC原本就是Spring的一部分

也叫SSI(IBatis是MyBatis的前身)

SpringMVC：视图层，界面层，负责接收请求，显示处理结果

Spring：业务层，管理service，dao，工具类对象的

MyBatis：持久层，访问数据库

用户发起请求--SpringMVC接收--Spring中的Service对象--MyBatis处理数据

需要做的是把用到的对象交给适当的容器创建，管理。把Controller还有web开发的相关对象交给SpringMVC容器，这些web对象写在SpringMVC配置文件中；service，dao对象定义在Spring的配置文件中，让Spring管理这些对象

SpringMVC容器是Spring容器的子容器，子可以访问父的内容，在子容器中的Controller可以访问父容器中的Service对象，就可以实现Controller使用Service对象

# 容器

1. springMVC的容器：使用中央调度器DispatcherServlet来创建
2. spring容器对象：使用监听器ContextLoaderListener来创建

# 配置文件

1. springmvc的配置文件
2. spring配置文件
3. mybatis主配置文件
4. 数据库的属性配置文件