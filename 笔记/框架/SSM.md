# 系统框架

三层架构和MVC有联系但**不等价**

## 三层架构

视图层View Level(Servlet或Controller，JSP)：也叫Web层，用于接收用户提交请求的代码，

服务层Service Level：系统的业务逻辑主要在这里完成

持久层Dao Level：注解操作数据库的代码在这里编写

为了降低各层间的耦合度，在三层架构程序设计中，采用面向接口编程，即上层对下层的调用，是通过接口实现的，而下层对上层真正服务提供者是下层接口的实现类，实现了层间解耦合

## MVC

Model模型(Service和Dao和实体类)：承载数据，并对用户提交请求进行计算的模块，分为两类，一类称为数据承载Bean，一类称为业务处理Bean，所谓数据承载Bean是指实体类，业务处理Bean则是指Service或Dao对象

View视图(JSP)：为用户提供使用界面，与用户直接进行交互

Controller控制器(Servlet或Controller)：用于将用户请求转发给相应的Model进行处理，并根据Model的计算结果向用户提供相应响应

# SSM编程

SpringMVC+Spring+MyBatis整合，是当前最流行的JavaEE开发技术架构，其实SSM整合实质，仅仅是将MyBatis整合入Spring，因为SpringMVC原本就是Spring的一部分

也叫SSI(IBatis是MyBatis的前身)

SpringMVC：视图层(View)，负责接收请求，显示处理结果

Spring：业务层(Service)，并且统管全局，管理service，dao，工具类对象

MyBatis：持久层(Dao)，访问数据库

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