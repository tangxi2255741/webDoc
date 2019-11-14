@Configuration把一个类作为一个IoC容器，它的某个方法头上如果注册了@Bean，就会作为这个Spring容器中的Bean。

# @Lazy(true) 

表示延迟初始化

# @Service

用于标注业务层组件、 

# @Controller

用于标注控制层组件（如struts中的action）

# @RestController

Spring4之后加入，默认返回json格式，不需要再加@ResponseBody注解了；

# @Repository

用于标注数据访问组件，即DAO组件。

# @Component

泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注。

# @Scope

用于指定scope作用域的（用在类上）

1、singleton（默认）:单例模式,全局有且仅有一个实例

2、prototype:原型模式,每次获取Bean的时候会有一个新的实例

3、request:表示该针对每一次HTTP请求都会产生一个新的bean，同时该bean仅在当前HTTP request内有效

4、session:表示该针对每一次HTTP请求都会产生一个新的bean，同时该bean仅在当前HTTP session内有效

5、global session:只在portal应用中有用，给每一个 global http session 新建一个Bean实例。

# @PostConstruct

被@PostConstruct修饰的方法会在服务器加载Servlet的时候运行，并且只会被服务器执行一次。PostConstruct

在构造函数之后执行,init()方法之前执行

# @PreDestory

被@PreDestroy修饰的方法会在服务器卸载Servlet的时候运行，并且只会被服务器调用一次，类似于Servlet的

destroy()方法。被@PreDestroy修饰的方法会在destroy()方法之后运行，在Servlet被彻底卸载之前

@DependsOn：定义Bean初始化及销毁时的顺序

@Primary：自动装配时当出现多个Bean候选者时，被注解为@Primary的Bean将作为首选者，否则将抛出异常

# @Resource

默认按名称装配，当找不到与名称匹配的bean才会按类型装配。

**装配顺序:**

1. 如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常;

2. 如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常

3. 如果指定了type，则从上下文中找到类型匹配的唯一bean进行装配，找不到或者找到多个，都会抛出异常

4. 如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则回退为一个原始类型进行匹配，如果匹配则自动装配；

# @Autowired

默认按类型装配，如果我们想使用按名称装配，可以结合@Qualifier注解一起使用，如下：

`@Autowired @Qualifier("personDaoBean") `

# @PostConstruct

初始化注解

# @PreDestroy

摧毁注解 默认 单例  启动就加载？？



# @RequestMapping

类定义处: 提供初步的请求映射信息，相对于 WEB 应用的根目录。

方法处: 提供进一步的细分映射信息，相对于类定义处的 URL。

# @RequestParam

用于将请求参数区数据映射到功能处理方法的参数上

如果接口传过来的参数名和定义的不一致，则需要指定

```java
public String test(@RequestParam(value="userName") String name){
	XXX
}
```

# @ModelAttribute

接收参数，并自动放到Model对象中

一、标记在方法上：

有返回值

```java
@ModelAttribute(value="userName") // 类似于model.addAttribute("userName", name);
// @ModelAttribute // 类似于model.addAttribute("name", name);
public String test(@RequestParam(value="userName") String name){
	return name;
}
```

没有返回值，则需要手动去`model.addAttribute("userName", name)`

二、标记在方法参数上：





