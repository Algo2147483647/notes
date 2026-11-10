# Domain Driven Design 

[TOC]

## Define
Domain-driven design is predicated on the following goals:
- placing the project's primary focus on the *core domain* and domain logic.
- basing complex designs on a model of the domain.
- initiating a creative collaboration between technical and domain experts to iteratively refine a conceptual model that addresses particular domain problems.

## Concept

<img src="assets/100-explicit-architecture-svg.png" alt="100-explicit-architecture-svg"  />

### Domain

### Subdomain

### Bounded Context

指的是具有明确边界的特定责任领域，在这个边界内部，模型是一致且完整的。边界上下文帮助开发人员划分系统的不同部分，每个部分内部都维护着自己的领域模型，上下文之间通过明确定义的接口或者共享模型来通信。

### Domain Model

指反映领域或子域业务概念的抽象模型，这个模型包括了业务对象、业务规则、策略以及业务逻辑。领域模型通常通过实体（Entities）、值对象（Value Objects）、服务（Services）、聚合（Aggregates）等DDD的模式来构建。

1. **实体 (Entity)**：
   - 实体是领域模型中的一个对象，它有一个唯一标识符（通常是ID）。
   - 实体在其生命周期内可以更改属性，但其标识不会改变。
   - 举例来说，用户账户可以是一个实体，因为它有一个唯一的账户号码。

2. **值对象 (Value Object)**：
   - 值对象是用来描述领域中的某些特性或者属性，但它没有唯一标识。
   - 值对象应该是不可变的，它的属性被创建后不应该更改。
   - 例如，一个地址可以是一个值对象，因为它描述了一个属性但不需要唯一标识。

3. **聚合 (Aggregate)**：
   - 聚合是一组相关的实体和值对象的集合，它们被视为数据修改的一个单元。
   - 聚合定义了一个明确的边界，用来保证业务规则和数据的一致性。

4. **聚合根 (Aggregate Root)**：
   - 每个聚合有一个根实体，称为聚合根。
   - 外部对聚合的引用只能通过聚合根，聚合根负责保持聚合内部的一致性。

5. **领域事件 (Domain Event)**：
   - 领域事件是在领域模型中发生的有意义的业务事件，通常表示了某些业务行为的发生。
   - 事件驱动的架构常用领域事件来进行不同聚合或边界上下文之间的通信。

6. **服务 (Service)**：
   - 在DDD中，服务是执行不属于实体或值对象的领域逻辑的一个对象。
   - 服务通常表现为无状态，并且其操作是函数式的。

7. **领域服务 (Domain Service)**：
   - 领域服务包含特定于领域的逻辑，这些逻辑不自然属于实体或值对象。

8. **应用服务 (Application Service)**：
   - 应用服务协调领域对象来执行特定的用例或者应用逻辑。
   - 它们负责应用流程的控制，而不包含业务逻辑。

9. **基础设施服务 (Infrastructure Service)**：
   - 基础设施服务提供非业务的技术能力，如数据持久化、消息传递等。

10. **仓储 (Repository)**：
    - 仓储用于封装存储逻辑，提供领域对象的检索和持久化。
    - 它抽象了数据源的细节，使得领域模型可以不依赖于特定的数据持久化机制。

11. **工厂 (Factory)**：
    - 工厂用于创建复杂的对象和聚合，封装了实例化逻辑。
    - 它提供一个清晰的界面来创建领域中的对象，而不需要暴露对象创建的细节。

## Reference

- [领域驱动设计在互联网业务开发中的实践 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2017/12/22/ddd-in-practice.html)
