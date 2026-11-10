# Design Patterns

[TOC]

Design patterns are some solutions proposed to solve some specific problems in software development, and can also be understood as some ideas for solving problems. Design patterns can help us enhance code reusability, scalability, maintainability, and flexibility. The purpose is to achieve high cohesion and low coupling of the code.

# Design Principles

* **Single Responsibility Principle**: 对于一个类，只有一个引起该类变化的原因；该类的职责是唯一的，且这个职责是唯一引起其他类变化的原因。
* **Interface Segregation Principle**: 客户端不应该依赖它不需要的接口，一个类对另一个类的依赖应该建立在最小的接口上。
* **Dependency Inversion Principle**: 依赖倒转原则是程序要依赖于抽象接口，不要依赖于具体实现。简单的说就是要求对抽象进行编程，不要对实现进行编程，这样就降低了客户与实现模块间的耦合。
* **Liskov Substitution Principle**: 任何基类可以出现的地方，子类一定可以出现。里氏代换原则是继承复用的基石，只有当衍生类可以替换基类，软件单位的功能不受影响时，基类才能真正的被复用，而衍生类也能够在基类的基础上增加新的行为。里氏代换原则是对开闭原则的补充。实现开闭原则的关键步骤就是抽象化。而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。
* **Open-Closed Principle**
  * Open for extension: 这意味着模块的行为是可以扩展的。当应用的需求改变时，我们可以对模块进行扩展，使其具有满足那些改变的新行为。也就是说，我们可以改变模块的功能。
  * Closed for modification:对模块行为进行扩展时，不必改动模块的源代码或者二进制代码。模块的二进制可执行版本，无论是可链接的库、DLL或者.EXE文件，都无需改动。
* **Law of Demeter (Least Knowledge Principle)**: 一个对象应当对其它对象又尽可能少的了解，不和陌生人说话。
* **Composite/Aggregate Reuse Principle**: 合成复用原则要求在软件复用时，要尽量先使用组合或者聚合等关联关系来实现，其次才考虑使用继承关系来实现。如果要使用继承关系，则必须严格遵循里氏替换原则。合成复用原则同里氏替换原则相辅相成的，两者都是开闭原则的具体实现规范。

# Creational Patterns

The mode of object instantiation is used to decouple the instantiation process of objects.

* Singleton
* Factory 
  * Simple factory
  * Factory method
  * Abstract factory
* Builder
* Prototype


## Factory Pattern

The factory pattern is the abstraction of the process of obtaining objects.

- Simple Factory 
- Factory Method
- Abstract Factory

### Simple Factory 

Example

<img src="./assets/v2-374daced25d3f14c8c5d793f34cf8a1d_r.jpg" alt="img" style="zoom: 40%;" />

- Create a abstract product interface

  ```java
  public interface Product {
  	void use();
  }
  ```

- Create concrete entity classes that inherits the abstract class

  ```java
  public class ProductA implements Product {
      @override
      public void use() {
          // code
      }
  }
  ```

  ```java
  public class ProductB implements AbstructProduct {
      @override
      public void use() {
          // code
      }
  }
  ```

- Create a Product Factory

  ```java
  public class ProductFactory {
      public Product createProduct(string productType) {
          if (productType == null) {
              return null;
          }
          
          if (productType.equalsIgnoreCase("ProductA")) {
              return new ProductA();
          } else if (productType.equalsIgnoreCase("ProductB")) {
              return new ProductB();
          }
          
          return null;
      }
  }
  ```

- Test: Use factories to produce products of different types and use.

  ```java
  public class FactoryTest {
      public static void main(String[] args) {
      	ProductFactory productFactory = new ProductFactory();
          
          Product productA = productFactory.createProduct("ProductA");
          productA.use();
          
          Product productB = productFactory.createProduct("ProductB");
          productB.use();
      }
  }
  ```

Disadvantages: Poor scalability, which violates the principle of opening and closing (software implementation should be open to extension and closed to modification). When adding new products, you need to modify the factory class.

### Factory Method

Example

<img src="./assets/v2-d705bcb757fce334e251abb3c733bc1d_r.jpg" alt="img" style="zoom:50%;" />

- Create a abstract product interface

  ```java
  public interface Product {
  	void use();
  }
  ```

- Create concrete entity classes that inherits the abstract class

  ```java
  public class ProductA implements Product {
      @override
      public void use() {
          // code
      }
  }
  ```

  ```java
  public class ProductB implements AbstructProduct {
      @override
      public void use() {
          // code
      }
  }
  ```

- Create a Product Factory abstract class

  ```java
  public abstract class ProductFactory {
      public abstract createProduct();
  }
  ```
  
- Concrete Product Factory implementations

  ```java
  public class ProductAFactory extends ProductFactory {
      @Override
      public Product createProduct() {
          return new ProductA();
      }
  }
  ```
  
  ```java
  class ProductBFactory extends ProductFactory {
      @Override
      public Product createProduct() {
          return new ProductB();
      }
  }
  ```
  
- Test: Use factories to produce products of different types and use.

  ```java
  public class FactoryTest {
      public static void main(String[] args) {
      	ProductFactory productAFactory = new ProductAFactory();
          Product productA = productAFactory.createProduct();
          productA.use();
          
      	ProductFactory productAFactory = new ProductBFactory();
          Product productB = productBFactory.createProduct();
          productB.use();
      }
  }
  ```

Disadvantage: When we add new products, we also need to provide corresponding factory classes, which will multiply the number of classes in the system, equivalent to increasing the complexity of the system.

### Abstract Factory

Example

<img src="./assets/v2-981e27a93befe8436c8d98eca8e44911_r.jpg" alt="img" style="zoom:50%;" />


- Create abstract product interfaces

  ```java
  public interface Product_1 {
  	void use();
  }
  
  public interface Product_2 {
  	void use();
  }
  ```

- Create concrete entity classes that inherits the abstract classes

  ```java
  public class Product_1A implements Product_1 {
      @override
      public void use() {
          // code
      }
  }
  
  public class Product_1B implements Product_1 {
      @override
      public void use() {
          // code
      }
  }
  
  public class Product_2A implements Product_2 {
      @override
      public void use() {
          // code
      }
  }
  
  public class Product_2B implements Product_2 {
      @override
      public void use() {
          // code
      }
  }
  ```

- Create a Product Factory abstract class

  ```java
  public abstract class ProductFactory {
      public abstract Product createProduct_1();
      public abstract Product createProduct_1();
  }
  ```
  
- Concrete Product Factory implementations

  ```java
  public class ProductAFactory extends ProductFactory {
      @Override
      public Product createProduct_1() {
          return new Product_1A();
      }
      
      @Override
      public Product createProduct_2() {
          return new Product_2A();
      }
  }
  ```
  
  ```java
  public class ProductBFactory extends ProductFactory {
      @Override
      public Product createProduct_1() {
          return new Product_1B();
      }
      
      @Override
      public Product createProduct_2() {
          return new Product_2B();
      }
  }
  ```
  
- Test: Use factories to produce products of different types and use.

  ```java
  public class FactoryTest {
      public static void main(String[] args) {
      	ProductFactory productAFactory = new ProductAFactory();
          Product product_1A = productAFactory.createProduct_1();
          product_1A.use();
          Product product_2A = productAFactory.createProduct_2();
          product_2A.use();
          
      	ProductFactory productBFactory = new ProductBFactory();
          Product product_1B = productBFactory.createProduct_1();
          product_1B.use();
          Product product_2B = productBFactory.createProduct_2();
          product_2B.use();
      }
  }
  ```

Disadvantage: Difficulty in expanding new types of products. The abstract factory pattern requires us to determine in advance the types of products that may be needed in the abstract class of the factory to meet the needs of multiple products from different brands. But if the product type we need is not determined in advance in the factory abstract class, then we need to modify the factory abstract class. Once the factory abstract class is modified, all factory subclasses also need to be modified, which is obviously inconvenient for extension.




Difference:

- Simple Factory: A unique factory class, a product abstract class, whose creation method is determined based on input parameters and creates specific product objects. 
- Factory method: Multiple factory classes, one product abstract class, using polymorphism to create different product objects, avoiding a lot of if else judgments. 
- Abstract Factory: Multiple factory classes, multiple product abstract classes, grouping of product subclasses, and the same factory implementation class create different products in the same group, reducing the number of factory subclasses.

## *Q: factory vs builder pattern?*

> - Builder focuses on constructing a complex object step by step. Abstract Factory emphasizes a family of product objects (either simple or complex). Builder returns the product as a final step, but as far as the Abstract Factory is concerned, the product gets returned immediately.
> - Builder often builds a Composite.
> - Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.
> - Sometimes creational patterns are complementary: Builder can use one of the other patterns to implement which components get built. Abstract Factory, Builder, and Prototype can use Singleton in their implementations.
>
> [What is the difference between Builder Design pattern and Factory Design pattern? - Stack Overflow](https://stackoverflow.com/questions/757743/what-is-the-difference-between-builder-design-pattern-and-factory-design-pattern)

# Structural Patterns

把类或对象结合在一起形成一个更大的结构。
* Adapter: 将一个类的方法接口转换成客户希望的另一个接口。
* Decorator: 动态的给对象添加新的功能。
* Proxy: 为其它对象提供一个代理以便控制这个对象的访问。
* Bridge: 将抽象部分和它的实现部分分离，使它们都可以独立的变化。
* Composite: 将对象组合成树形结构以表示“部分-整体”的层次结构。
* Fasade: 对外提供一个统一的方法，来访问子系统中的一群接口。
* Flyweight: 通过共享技术来有效的支持大量细粒度的对象。

## Adapter

Adapter pattern allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code.

- Class Adapter Pattern
- Object Adapter Pattern

### Class Adapter Pattern

Example

<img src="./assets/W3sDesign_Adapter_Design_Pattern_UML.jpg" alt="img" style="zoom: 80%;" />

- Target Interface 

  ```java
  public interface Target {
      void operation();
  }
  ```

- Adaptee Class 

  ```java
  public class Adaptee {
  	public void specificOperation() {
  		// code
  	}
  }
  ```

- Adapter Class

  ```java
  public class Adapter extent Adaptee implements Rectangle {
  	@Override
      public void operation() {
          this.SpecificRequest();
      }
  }
  ```

- Test

  ```java
  public class AdapterTest {
      public static void main(String[] args) {
          // Using the Adaptee directly
          Adaptee adaptee = new Adaptee();
          adaptee.specificOperation();
  
          // Using the Adapter to adapt adaptee to the Target interface
          Target target = new Adapter();
          target.operation();
      }
  }
  ```

### Object Adapter Pattern

Example

- Target Interface & Adaptee Class as shown above

- Adapter

  ```java
  public class Adapter implements Rectangle {
      private Adaptee adaptee;
      
      public Adapter() {
          this.adaptee = new Adaptee();
      }
      
      public void operation() {
          this.adaptee.specificOperation();
      }
  }
  ```

- Test

  ```java
  public class AdapterTest {
      public static void main(String[] args) {
          // Using the Adaptee directly
          Adaptee adaptee = new Adaptee();
          adaptee.specificOperation();
  
          // Using the Adapter to adapt adaptee to the Target interface
          Target target = new Adapter(adaptee);
          target.operation();
      }
  }
  ```


## Decorator

Decorator allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class.



Example

<img src="./assets/400px-Decorator_UML_class_diagram.svg.png" alt="img" style="zoom: 80%;" />

- Component, The base interface

  ```java
  interface Component {
      void operation();
  }

- Concrete Component

  ```java
  class SimpleComponent implements Component {
      @Override
      public void operation() {
          // code
      }
  }
  ```

- Decorator: Abstract class for Component decorators

  ```java
  abstract class ComponentDecorator implements Component {
  	protected Component decoratedComponent;
      
      public ComponentDecorator(Component component) {
          this.decoratedComponent = component;
      }
      
      @Override
      public void operation() {
          return decoratedComponent.operation();
      }
  }
  ```

- Concrete Decorator: 

  ```java
  class ConcreteDecorator_1 extends ComponentDecorator {
      public ConcreteDecorator_1(Component component) {
          super(component);
      }
      
      @Override
      public void operation() {
          // modify based on the super.operation()
      }
  }
  
  class ConcreteDecorator_2 extends ComponentDecorator {
      public ConcreteDecorator_2(Component component) {
          super(component);
      }
      
      @Override
      public void operation() {
          // modify based on the super.operation()
      }
  }
  ```

- Test

  ```java
  public class DecoratorTest {
      public static void main(String[] args) {
          Component simpleComponent = new SimpleComponent();
          simpleComponent.opeation();
          
          Component component_1 = new ConcreteDecorator_1(simpleComponent);
          component_1.opeation();
          
          Component component_12 = new ConcreteDecorator_2(component_1);
          component_12.opeation();
      }
  }
  ```

  


# Behavioral Patterns

类和对象如何交互，及划分责任和算法。

* Strategy: 定义一系列算法，把他们封装起来，并且使它们可以相互替换。
* Template method: 定义一个算法结构，而将一些步骤延迟到子类实现。
* Command: 将命令请求封装为一个对象，使得可以用不同的请求来进行参数化。
* Iterator: 一种遍历访问聚合对象中各个元素的方法，不暴露该对象的内部结构。
* Observer: 对象间的一对多的依赖关系。
* Mediator: 用一个中介对象来封装一系列的对象交互。
* Memento: 在不破坏封装的前提下，保持对象的内部状态。
* Interpreter: 给定一个语言，定义它的文法的一种表示，并定义一个解释器。
* State: 允许一个对象在其对象内部状态改变时改变它的行为。
* Chain of responsibility: 将请求的发送者和接收者解耦，使的多个对象都有处理这个请求的机会。
* Visitor: 不改变数据结构的前提下，增加作用于一组对象元素的新功能。

# Concurrency Patterns

* Double-checked locking
* Reactor: A reactor object provides an asynchronous interface to resources that must be handled synchronously.
* Read-write lock: Allows concurrent read access to an object, but requires exclusive access for write operations. An underlying semaphore might be used for writing, and a Copy-on-write mechanism may or may not be used.
* Thread pool: A number of threads are created to perform a number of tasks, which are usually organized in a queue. Typically, there are many more tasks than threads. Can be considered a special case of the object pool pattern.
* CPU atomic operation

# Other Patterns

## Object Pool

The object pool pattern uses a set of initialized objects kept ready to use – a "pool" – rather than allocating and destroying them on demand. A client of the pool will request an object from the pool and perform operations on the returned object. When the client has finished, it returns the object to the pool rather than destroying it; this can be done manually or automatically.

<img src="./assets/1__odCuMsqO33z35l6yN0aURw.png" alt="The blog image" style="zoom:60%;" />

[Domain-Driven_Design](./Domain-Driven_Design.md)