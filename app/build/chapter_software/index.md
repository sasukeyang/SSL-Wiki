---
icon: material/file-code
---

# 六大设计原则

> 最近在看一本关于设计模式的书，里面提到了六大设计原则，感觉对我们的项目有一些指向作用，在这里mark一下

## 关于六大设计原则

六大设计原则旨在使得构建出来的项目具有 **强健性，弱耦合，易维护** 等特点，具体包含以下几个原则：

* 单一职责原则
* 里氏替换原则
* 依赖倒置原则
* 接口隔离原则
* 迪米特法则
* 开闭原则

接下来我会简要介绍一下这几个原则的基本内容和实现借鉴

### 单一职责原则

 **单一职责原则** 的定义是 **应该有且只有一个原因引起类的变更** ，也即 **一个接口(java中的一种抽象类型)或类只有一个职责，只负责一件事情** 。
以 *Owl2* 中现在使用的 *optionobject* 为例，这个类实现了 *Socket* 通讯的管理与 *option* 这个 *message* 的管理，这是违反了单一职责原则的，可以考虑分成 *socket* 和 *option* 单独进行管理。

### 里氏替换原则

 **里氏替换原则** 主要体现在类之间的 **继承** 上，有如下两种定义：

* 如果对每一个类型为S的对象o1,都有类型为T的对象o2,使得以T定义的所有程序P在所有的对象o1都代换成o2时,程序P 的行为没有发生变化,那么类型S是类型T的子类型。
* 所有引用基类的地方必须能透明地使用其子类的对象

后一个定义比较清晰，即 **只要父类能出现的地方子类就可以出现，用子类替换父类不会出现任何错误或异常** 。
这一个定义中包含了四层含义：

* 子类必须完全实现父类的方法
* 子类可以有自己的个性（父类没有的成员）
* 子类覆盖或实现父类的方法时 **输入参数** 可以被放大
* 子类覆写或实现父类的方法时 **输出结果** 可以被缩小

这一原则可以增强 **程序的健壮性** ，不过在我所知道的范围内，我们的项目使用继承比较少，故可借鉴思路较少。

### 依赖倒置原则

 **依赖倒置原则** 主要包含一下三层含义：

* 高层模块不应该依赖低层模块（不可分割的原子逻辑）,两者都应该依赖其抽象
* 抽象不应该依赖细节
* 细节应该依赖抽象

这一原则是 **面向接口编程** 的精髓之一，主要体现在更多的使用 **抽象类** （java中的接口）来定义变量和实现逻辑，而不在依赖**实现类**来实现特定的逻辑。
这一原则可以 **减少类间的耦合，提高系统的稳定性** ，我认为在后续对rbk进行 **解耦** 或 **重写架构** 时可以尝试采用，不过和上一原则一样，抽象目前在我们的项目中使用不是很多，故不多加介绍。

### 接口隔离原则

 **接口隔离原则** 有如下两种定义：

* 客户端不应该依赖它不需要的接口
* 类间的依赖应该建立在最小的接口上

这一原则强调 **接口尽量细化，同时接口中的方法尽量少** ，尽量对不同的模块实现各自单独的接口，而不是建立一个庞大的臃肿接口。这一原则使用时有时会与 **单一职责原则** 有所冲突，应以 **单一职责原则** 为更高优先级来满足。
这一原则还强调接口的 **高内聚** 特性，即 **提高接口的处理能力吗，减少对外的交互** ，在代码中体现为尽量少公布*public*方法。

### 迪米特法则

 **迪米特法则** 也称为 **最少知识原则** ，其定义为 **一个对象应该对其他对象有最少的了解** ，实现中可以注意一下三点：

* 只和朋友（出现在成员变量、方法的输入输出参数中的类）交流，程序中不应含有非朋友类
* 注意朋友间的距离，尽量减少公开的*public*属性或方法
* 是自己的就是自己的，在不违反迪米特法则的前提下，优先把方法放在本类中

 **迪米特法则** 的核心观念就是 **类间解耦，弱耦合** ，这个法则在后续的项目构建中是可以广泛参考的，有助于项目的清洁。

### 开闭原则

 **开闭原则** 的定义是 **一个软件实体如类、模块和函数应该对扩展开放,对修改关闭** ，即一个软件实体应该更多的通过扩展来实现变化，而非修改已有的代码来实现。
这一原则可以显著减少 **测试工作** ， **提高复用性，可维护性** ，可以通过 **抽象约束** ， **元数据控制** 等来实现，
不过由于我们目前项目的可维护性本身就不高，加上抽象使用的较少，这一原则还得不到很好的体现。

## 关于出处

上面提到的概念来自于我在看的一本书《 *设计模式之禅* 》，因为还没有看完，可能在阅读的过程中会有不同的体会，仅是分享一下，另外个人感觉这本书的可读性还是不错的，有兴趣的朋友可以找来看一下，电子版的话找我要也可以：）