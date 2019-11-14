## SpringMVC中的几个组件

1. 前端控制器（DispatcherServlet）：接收请求，响应结果，相当于电脑的CPU。
2. 处理器映射器（HandlerMapping）：根据URL去查找处理器
3. 处理器（Handler）：需要程序员去写代码处理逻辑的
4. 处理器适配器（HandlerAdapter）：会把处理器包装成适配器，这样就可以支持多种类型的处理器，类比笔记本的适配器（适配器模式的应用）

5. 视图解析器（ViewResovler）：进行视图解析，多返回的字符串，进行处理，可以解析成对应的页面



## Spring框架的7个模块？

1. Spring Core

​	框架最基础部分，提供IOC和依赖注入的特性；

2. Spring Context:

   提供了一种框架式的对象访问方法，有些象JNDI注册器。

3. Spring DAO:
   DAO (Data Access Object)进一步简化DAO开发步骤，能以一致的方式使用数据库访问技术，用统一的方式调用事务管理，避免具体的实现侵入业务逻辑层的代码中。

4. Spring ORM:
   ORM 封装包提供了常用的“对象/关系”映射APIs的集成层。 其中包括JPA、JDO、hibernate 和 iBatis 。利用ORM封装包，可以混合使用所有spring提供的特性进行“对象/关系”映射，如前边提到的简单声明性事务管理。

5. Spring AOP:

   spring的 AOP 封装包提供了符合AOP Alliance规范的面向方面的编程实现，让你可以定义，例如方法拦截器（method-interceptors）和切点（pointcuts），从逻辑上讲，从而减弱代码的功能耦合，清晰的被分离开。而且，利用source-level的元数据功能，还可以将各种行为信息合并到你的代码中。

6. Spring Web:
   Spring中的 Web 包提供了基础的针对Web开发的集成特性，例如多方文件上传，利用Servlet listeners进行IOC容器初始化和针对Web的ApplicationContext。当与WebWork或Struts一起使用Spring时，这个包使Spring可与其他框架结合。

7. Spring Web MVC:
   Spring中的MVC封装包提供了Web应用的Model-View-Controller（MVC）实现。Spring的MVC框架并不是仅仅提供一种传统的实现，它提供了一种清晰的分离模型，在领域模型代码和Web Form之间。并且，还可以借助Spring框架的其他特性。



## Spring中自动装配的方式有哪些？

- no：不进行自动装配，手动设置Bean的依赖关系。
- byName：根据Bean的名字进行自动装配。
- byType：根据Bean的类型进行自动装配。
- constructor：类似于byType，不过是应用于构造器的参数，如果正好有一个Bean与构造器的参数类型相同则可以自动装配，否则会导致错误。
- autodetect：如果有默认的构造器，则通过constructor的方式进行自动装配，否则使用byType的方式进行自动装配。

## Spring工作原理？

 	1. 用户提交请求，包含url还可能带有表单等其他信息
	2. 请求到达spring的前端控制器（DispatcherServlet）
	3. DispatcherServlet将请求分发给springMvc控制器（查询一个或多个处理映射器映射并根据url信息来决策到哪个控制器）
	4. 找到控制器后，DispatcherServlet将用户提交的信息传给控制器，控制器很少处理业务逻辑，一般委托给一个或多个服务对象。
	5. 控制器在完成逻辑处理后需要将产生的信息（model）返回给用户。但将原始信息返回给用户不好，需要进行格式化，所以信息需要发送给一个视图（view，如list.vm），一般是jsp。
	6. 控制器将模型数据打包，将请求连同模型和视图名称发送回DispatcherServlet。
	7. 视图将使用模型数据渲染输出，并通过这个输出将响应对象传给客户端
