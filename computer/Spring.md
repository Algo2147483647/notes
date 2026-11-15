# Spring

[TOC]

## Bean 的生命周期

实例化 -> 属性赋值 -> 初始化 -> 销毁

<img src="assets/format,png.png" alt="img" style="zoom: 30%;" />



## Architecture of MVC (Model-View-Controller)

* Model
  * Entity: represent the data objects in the application. They typically correspond to database tables or other data sources, and they encapsulate the data and business logic associated with those entities.
  * Data access objects (DAO): responsible for data access and provide an abstraction layer for interacting with the underlying data storage, such as a database. They encapsulate the logic for querying, inserting, updating, and deleting data.
  * Service: implement the business logic and act as intermediaries between the controllers and the DAO layer. They coordinate multiple DAO operations and apply business rules on the data.
  * Utility: provide helper methods or utility functions used by the Model components.
* Controller  
  The Controller acts as an intermediary between the Model and the View. 
* View

## Annotations
1. `@SpringBootApplication` - 组合注解，用于启动Spring应用程序的自动配置等。

2. `@Component` - 表示一个类作为组件类，并告诉Spring需要为这个类创建bean。

3. `@Service` - 标记服务层的组件。用于将一个类标记为服务层组件，表示该类负责处理业务逻辑、协调数据访问和执行其他服务操作。

4. `@Repository` - 标记数据访问层组件，即DAO层组件。

5. `@Controller` - 标记控制层组件，如Spring MVC控制器。

6. `@RestController` - 用于创建RESTful控制器，它结合了`@Controller`和`@ResponseBody`。

7. `@RequestMapping` - 用于映射web请求到Spring Controller的方法上。

8. `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping` - 这些是`@RequestMapping`的专化版本，用于处理HTTP GET, POST, PUT, DELETE, PATCH请求。

9. `@Autowired` - 自动装配依赖关系。

10. `@Qualifier` - 当有多个相同类型的bean时，用于指定需要装配哪一个。

11. `@Value` - 用于注入属性文件中的值。

12. `@Configuration` - 表示一个类定义了一个或多个`@Bean`方法，并且可能会被Spring容器用来构建bean定义，初始化Spring环境。

13. `@Bean` - 表示一个方法产生一个bean要由Spring容器管理。

14. `@Profile` - 指定某些bean只有在特定的profile被激活时才会注册。

15. `@Scope` - 定义bean的作用域。

16. `@Lazy` - 标记在bean的懒加载时使用。

17. `@Required` - 表明bean的属性必须在配置时设置，通过一个显式的bean属性值或通过自动装配。

18. `@Transactional` - 声明事务的边界。

19. `@EnableAutoConfiguration` - 告诉Spring Boot自动配置你的应用程序。

20. `@Import` - 用于导入其他配置类。

21. `@Aspect` - 标记一个类为切面类。

22. `@EnableAspectJAutoProxy` - 开启AspectJ自动代理。

23. `@ExceptionHandler` - 用于定义方法处理异常。

24. `@PathVariable` - 用于将请求URL中的模板变量映射到方法的参数上。

25. `@RequestParam` - 用于将请求参数区数据映射到方法的参数上。

26. `@RequestBody` - 允许将HTTP请求体绑定到方法的参数上。

27. `@ResponseBody` - 告诉Spring使用消息转换器返回数据作为HTTP响应体。

28. `@Valid` - 用于验证标注了约束条件的Bean属性。


# $Spring\ Boot$

[TOC]

- `@SpringBootApplication`
  - `@Sconfiguration`
  - `@ComponetnScan`
  - `@EnableAutoConfiguration`

# Bean

## Life cycle

<img src="./assets/640-1692084908072-9.jpeg" alt="Image" style="zoom: 50%;" />

- 1.**「实例化」**，实例化该 Bean 对象

  - Bean 容器找到配置文件中 Spring Bean 的定义。
  - Bean 容器利用 Java Reflection API 创建一个Bean的实例。

- 2.**「填充属性」**，给该 Bean 赋值

  - 如果涉及到一些属性值 利用 `set()`方法设置一些属性值。

- 3.**「初始化」**

- - 如果实现了 Aware 接口，会通过其接口获取容器资源
  - 如果实现了 BeanPostProcessor 接口，则会回调该接口的前置和后置处理增强
  - 如果配置了 init-method 方法，会执行该方法

- 4.**「销毁」**

- - 如果实现了 DisposableBean 接口，则会回调该接口的 destroy 方法
  - 如果配置了 destroy-method 方法，则会执行 destroy-method 配置的方法

## Scope

1. **单例作用域（Singleton Scope）**：
   - 默认情况下，Spring中的beans都是单例的。这意味着Spring IoC容器在启动时会创建一个单例bean的实例，并缓存它。
   - 后续当有其他bean或代码需要该单例bean时，Spring容器不会创建新的实例，而是返回之前创建并缓存的实例。
   - 因此，对于单例作用域，不管你需要多少次注入，它都使用同一个实例。
2. **原型作用域（Prototype Scope）**：
   - 如果bean的作用域被定义为原型，则每次请求bean时，Spring容器都会创建一个新的实例。
   - 对于原型作用域的bean，每次注入都会有一个新的bean实例被创建。
3. **其他作用域**：
   - Spring还提供了其他作用域，如`request`、`session`和`application`，它们在web应用程序上下文中使用。
   - 对于这些作用域，bean的实例化取决于具体的作用域。例如，对于`session`作用域，每个用户会话都会有自己的bean实例，但在同一个会话中的多次注入将使用相同的实例。

总结：并不是每次依赖注

# Configuration Method

- **XML配置**
- **基于注解的配置**
- **基于Java API的配置**



# Annotations

1. `@Component`及其派生注解：
   - `@Component`: 通用的组件注解，标识一个类为Spring容器的组件。
   - `@Service`: 用于标识业务逻辑层的组件。
   - `@Repository`: 用于标识数据访问层的组件。
   - `@Controller`: 用于标识控制器层的组件。
2. 依赖注入相关注解：
   - `@Autowired`: 自动装配（自动注入）一个Bean到另一个Bean中。
   - `@Qualifier`: 指定使用哪个具体的Bean进行装配，结合`@Autowired`使用。
   - `@Value`: 注入一个外部属性值到Bean的字段或方法参数中。
3. AOP相关注解：
   - `@Aspect`: 声明一个切面。
   - `@Pointcut`: 声明切入点，用于指定在哪些连接点上应用切面逻辑。
   - `@Before`: 在方法调用之前执行切面逻辑。
   - `@After`: 在方法调用之后执行切面逻辑。
   - `@Around`: 在方法调用前后执行切面逻辑，包围方法的执行。
4. 事务管理相关注解：
   - `@Transactional`: 声明方法或类需要事务管理。可以应用在方法或类级别，控制方法的事务行为。
5. Web相关注解：
   - `@RequestMapping`: 映射HTTP请求到方法处理。
   - `@RestController`: 结合`@Controller`和`@ResponseBody`，表示一个控制器返回JSON响应。
   - `@PathVariable`: 用于提取URI模板变量的值。
   - `@RequestParam`: 用于提取请求参数的值。
6. 其他常见注解：
   - `@Configuration`: 声明一个配置类，替代XML配置文件。
   - `@Bean`: 在配置类中声明一个Bean。
   - `@ComponentScan`: 配置Spring扫描组件的基础包路径。
   - `@Conditional`: 根据条件条件化地创建Bean。
   - `@Profile`: 基于配置文件的条件化激活Bean。

# Dependency Injection

Dependency injection reduces the coupling among components by moving the dependencies of objects from within the code to external management. In dependency injection, the object is no longer responsible for creating or managing the objects it depends on, but instead provides these dependencies through an external container. The purpose of this pattern is to promote loose coupling, testability and maintainability.

- **Constructor Injection**
- **Setter Injection**
- **Field Injection**

## Constructor Injection

**recommended**

```
public class TextEditor {
   private SpellChecker spellChecker;

   public TextEditor(SpellChecker spellChecker) {
      this.spellChecker = spellChecker;
   }
   // ...
}

public class SpellChecker {
   // ...
}
```



```
<bean id="textEditor" class="com.example.TextEditor">
   <constructor-arg ref="spellChecker"/>
</bean>

<bean id="spellChecker" class="com.example.SpellChecker"/>
```



## Setter Injection

```
public class TextEditor {
   private SpellChecker spellChecker;

   public void setSpellChecker(SpellChecker spellChecker) {
      this.spellChecker = spellChecker;
   }
   // ...
}

public class SpellChecker {
   // ...
}
```



```
<bean id="textEditor" class="com.example.TextEditor">
   <property name="spellChecker" ref="spellChecker"/>
</bean>

<bean id="spellChecker" class="com.example.SpellChecker"/>
```

## Field Injection

** Field injection is not recommended.*

Injection is performed directly on fields by using the `@Autowired` annotation.

```
public class TextEditor {
   @Autowired
   private SpellChecker spellChecker;
   // ...
}
```

underlying principle:



## *Q: How does spring solve circular dependencies?*

<img src="./assets/circular_dependencies.png" alt="circular_dependencies" style="zoom: 40%;" />

循环依赖就是说两个对象相互依赖，形成了一个环形的调用链路

spring 使用三级缓存去解决循环依赖的，其**「核心逻辑就是把实例化和初始化的步骤分开，然后放入缓存中」**，供另一个对象调用

- **「第一级缓存」**：用来保存实例化、初始化都完成的对象
- **「第二级缓存」**：用来保存实例化完成，但是未初始化完成的对象
- **「第三级缓存」**：用来保存一个对象工厂，提供一个匿名内部类，用于创建二级缓存中的对象

当 A、B 两个类发生循环引用时 大致流程

- 1.A 完成实例化后，去**「创建一个对象工厂，并放入三级缓存」**当中

- - 如果 A 被 AOP 代理，那么通过这个工厂获取到的就是 A 代理后的对象
  - 如果 A 没有被 AOP 代理，那么这个工厂获取到的就是 A 实例化的对象

- 2.A 进行属性注入时，去**「创建 B」**

- 3.B 进行属性注入，需要 A ，则**「从三级缓存中去取 A 工厂代理对象」**并注入，然后删除三级缓存中的 A 工厂，将 A 对象放入二级缓存

- 4.B 完成后续属性注入，直到初始化结束，将 B 放入一级缓存

- 5.**「A 从一级缓存中取到 B 并且注入 B」**, 直到完成后续操作，将 A 从二级缓存删除并且放入一级缓存，循环依赖结束

------

spring 解决循环依赖有两个前提条件：

- 1.**「不全是构造器方式」**的循环依赖(否则无法分离初始化和实例化的操作)
- 2.**「必须是单例」**(否则无法保证是同一对象)

## Process

Spring的依赖注入是其核心功能之一，它使我们能够实现控制反转（IoC）模式，从而达到松耦合的目的。以下是Spring依赖注入的基本运行流程和相关概念的详细描述：

1. **配置阶段**:
   - 在传统的基于XML的配置中，你会在XML文件中定义beans和它们之间的依赖关系。
   - 在基于注解的配置中，你可以使用`@Component`, `@Service`, `@Repository`等注解来标记一个类作为bean。依赖关系可以通过`@Autowired`或者`@Inject`来定义。
2. **启动阶段**:
   - 当Spring应用上下文初始化时，它会读取配置（无论是XML文件还是注解）。
   - Spring的BeanFactory或ApplicationContext负责解析这些配置并创建bean定义。
   - Class加载是在bean实例化的时候发生的。Spring会使用Java的反射机制来实例化对象。
3. **实例化与依赖注入**:
   - 当一个bean被请求，Spring容器开始bean的实例化过程。
   - 如果这个bean依赖于其他beans，Spring容器会先解析这些依赖。
   - 使用反射，Spring会查找类的构造函数、setter方法或字段，然后注入所需的依赖。
   - 如果bean的作用域是单例（默认），则bean会被缓存，并且所有对该bean的请求都会返回同一个实例。
4. **关于Java对象与Bean的关系**:
   - 在Spring上下文中，所有的bean都是Java对象。但并不是所有的Java对象都是Spring bean。
   - Spring bean是Spring容器管理的对象，意味着它们的生命周期、依赖等都由Spring控制。
   - 一个普通的Java对象（非Spring bean）的生命周期和依赖必须由开发人员手动管理。
5. **后处理阶段**:
   - Spring提供了一个接口`BeanPostProcessor`，允许在bean初始化之后进行一些处理。例如，可以实现额外的配置或初始化。
   - 一些内部的Spring功能（如AOP代理或事务管理）也使用这个机制来对bean进行增强。
6. **销毁阶段**:
   - 当Spring容器关闭时，它会清理所有的单例bean。
   - 如果bean实现了`DisposableBean`接口或定义了自定义的destroy方法，Spring会在关闭时调用这些方法。

总的来说，Spring的依赖注入流程涉及了从配置读取、解析bean定义、实例化对象、解决依赖、后处理等一系列步骤。这些都确保了Spring应用中的组件之间的松耦合和高度的模块化。

# Process

<img src="./assets/6ba8bf5c8177430b8f462f35948d1c74tplv-k3u1fbpfcp-zoom-in-crop-mark4536000.webp" alt="spring_running.png" style="zoom: 60%;" />


Spring Boot是一个用于简化Spring应用程序开发的框架，它提供了一种快速、简单的方式来创建独立运行的、基于Spring的应用程序。下面是Spring Boot项目的运行流程，详细介绍了从项目启动到运行的各个阶段：

1. **项目配置和依赖管理：** 开发人员首先需要创建一个Spring Boot项目。项目可以使用Spring Initializr进行初始化，选择所需的依赖项，例如Web、数据库、安全等。生成的项目基础结构包括主应用程序类、配置文件等。
2. **主应用程序类：** Spring Boot应用程序的入口点是主应用程序类（通常带有`@SpringBootApplication`注解）。这个类初始化Spring应用程序上下文并启动应用程序。
3. **自动配置：** Spring Boot通过自动配置机制尝试根据项目的依赖和配置来自动设置应用程序。它基于约定大于配置的原则，减少了开发人员的手动配置工作。
4. **应用程序上下文初始化：** 主应用程序类会创建Spring应用程序上下文。应用程序上下文是一个IoC容器，负责管理Bean的创建、依赖注入和生命周期管理。
5. **依赖注入：** Spring Boot使用依赖注入来管理Bean之间的关系。开发人员通过注解（如`@Autowired`）将需要的组件注入到其他组件中，从而建立起整个应用程序的组件协作。
6. **运行时属性加载：** Spring Boot使用属性文件（如`application.properties`或`application.yml`）来配置应用程序的行为。这些属性可以在运行时被加载，影响应用程序的各个方面，如数据库连接、端口号等。
7. **组件扫描：** Spring Boot会自动扫描主应用程序类所在的包及其子包，找到被Spring管理的组件（Bean）。可以使用`@Component`及其派生注解来标记组件。
8. **Web服务器初始化：** 如果应用程序具有Web部分，Spring Boot会自动初始化嵌入式Web服务器（如Tomcat、Jetty）。它会根据配置的端口号和路径来监听HTTP请求。
9. **请求处理：** 当收到HTTP请求时，嵌入式Web服务器将请求传递给Spring MVC框架。Spring MVC根据请求的URL、HTTP方法等信息，将请求映射到相应的Controller方法。
10. **Controller处理：** Controller方法处理请求，执行业务逻辑，可能会涉及数据库查询、业务计算等操作。Controller方法返回数据、视图名或重定向信息。
11. **视图解析：** 如果Controller方法返回的是视图名，Spring Boot会根据配置的视图解析器将视图名解析为实际的视图模板，如Thymeleaf、FreeMarker、JSP等。
12. **模型数据渲染：** 视图模板会根据Controller方法传递的模型数据进行渲染，生成最终的HTML内容。
13. **HTTP响应：** 渲染后的视图内容作为HTTP响应返回给客户端，客户端浏览器解析渲染页面并显示。
14. **应用程序关闭：** 当应用程序关闭时，Spring Boot会执行一些清理工作，如关闭数据库连接、释放资源等。

# Application

## Spring MVC

 Service层（处理业务）、Dao层（数据库操作）、Entity层（实体类）、Controller层(控制层，返回数据给前台页面)。

## @Controller 

<img src="./assets/640-1692084442023-3.png" alt="Image" style="zoom: 67%;" />

## @RestController 

@Controller + @ResponseBody = @RestController

<img src="./assets/640-1692084584291-6.png" alt="Image" style="zoom:67%;" />

`@ResponseBody` 注解的作用是将 `Controller` 的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到HTTP 响应(Response)对象的 body 中，通常用来返回 JSON 或者 XML 数据，返回 JSON 数据的情况比较多。



# *Q: What design patterns are used in the Spring framework?*

- **工厂设计模式** : Spring使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。
- **代理设计模式** : Spring AOP 功能的实现。
- **单例设计模式** : Spring 中的 Bean 默认都是单例的。
- **模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
- **包装器设计模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
- **观察者模式:** Spring 事件驱动模型就是观察者模式很经典的一个应用。
- **适配器模式** :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring M
