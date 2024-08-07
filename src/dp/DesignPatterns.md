### 面向对象软件设计SOLID原则

#### 1、单一职责原则（Single responsibility principle，缩写为：SRP）

说明：一个类或者模块只负责完成一个职责（A class or module should have a singleresponsibility）。通俗来说就是，一个模块、类、方法不要承担过多的任务。

原则上来说，我们设计一个类的时候不应该设计成大而全的类，要设计粒度小，功能单一的类，如果一个类两个或者两个以上的不相干的功能，那我们就说它未被了单一职责原则，一个将他拆分成多个功能单一，粒度更细的类。

实际软件开发工作中，不必严格遵守原则，可以设计一个粗粒度的类，随着业务的发展，在进行重构。

实际开发中可以按照一下参考意见，进行代码的重构或者设计：

- 类依赖过多的其他类，或者代码直接依赖关系过于复杂时，不符合高内聚低耦合的设计思想时，就可以考虑对代码进行拆分。
- 类的名称和实际的功能关系不大或者没有任何关联性的时候，可以更加细粒度的拆分，把无关的功能独立出去。
- 类的代码函数过多影响可读性和代码维护时，可以对代码进行方法级别的拆分。

#### 2、开闭原则（Open-closed principle，缩写为：OCP）

说明：软件实体（模块、类、方法等）应该对扩展开放、对修改关闭（software entities （modules、classes、functions，etc.）should be open for extension,but closed for modification）。通俗来讲就是添加一个功能应该是在已有的代码基础上进行扩展，而不是修改已有代码。

开闭原则的目的是为了代码的可扩展，并且避免了对现有代码的修改给软件带来风险。可扩展的前提是需要了解到未来的扩展点，那实际软件开发中如何找到所有的可扩展点呢？一下提供了几种参考方案：

- 如果是业务驱动的系统，需要在充分了解了业务需求的前提下，才能找到对应的扩展点，如果不确定因素过多，需求变化过快，则可以对一些比较确定的，短期内就可会扩展，通过设计扩展点，能明显提升代码的稳定性和开发效率的地方就行设计。
- 如果是通用型的技术开发，比如开发通用的框架，组件，类库，你需要考虑技术框架将如何被用户使用，考虑功能的升级需要预留的扩展点以及版本之间的兼容问题。
- 即时对系统的业务或者技术框架有足够的了解，也不一定要设计所有的扩展点。为未来可能发生变化的每个地方都预留扩展点，也会个系统带来极大的复杂度，实现起来工作量也不可小觑。需要综合开发成本，影响范围，实际收益（包括时间和人员成本）等因素进行考虑。

#### 3、里氏替换原则（Liskvo substitution principle，缩写为：LSP）

说明：子类对象能够替换程序中父类对象的任何地方，并且保证原来的程序的逻辑行为不变及正确性不被破坏。

可以利用面向对象编程的多态性来实现，多态和里氏替换原则优点类似，但是他们的关注角度是不一样的，多态是面向对象编程的特性，而里氏替换是一种原则，用来指导继承关系中子类该如何设计，子类的设计要确保在替换父类的时候，不改变原有的程序的逻辑以及不破坏原有的程序的正确性。

具体的实现方式可以理解为，子类在设计的时候，要遵循父类的行为约定。父类定义了方法的行为，子类可以改变方法的内部实现逻辑，但不能改变方法原有的行为约定，如：接口、方法声明要实现的功能，对参数值、返回值、异常的约定，甚至包括注释中所罗列的任何特殊的说明。

#### 4、接口隔离原则（Interface segregation principle，缩写为：ISP）

说明：客户端不应该强迫依赖它不需要的接口。

接口隔离原则的时间可以参考如下方法：

1. 对于接口来说，如果某个接口承担了与它无关的接口定义，则说明接口违反了接口隔离原则。可以把无关的接口剥离出去。对胖而杂的接口瘦身。
2. 对于共通的功能来说，应该细分功能点，按需添加，而不是定义一个大而全的接口，让子类去被迫实现。

#### 5、依赖倒置原则（Dependency inversion principle，缩写为：DIP）

说明：高层模块不要依赖底层模块。高层模块和底层模块应该通过抽象来互相依赖。除此之外，抽象不要依赖具体实现细节，具体实现细节依赖抽象。

这个的高层模块，从代码的角度来说就是调用者，底层模块就是被调用者。即调用者不要依赖于具体的实现，而应该依赖抽象，如Spring中的各个Aware,框架依赖于Aware接口具体的实现增加功能，具体的实现通过实现接口来获得功能。而具体的实现与框架并没有直接耦合。

#### 6、迪米特法则（Law Of Demeter）

迪米特法则又称为 最少知道原则，它表示一个对象应该对其它对象保持最少的了解。通俗来说就是，只与直接的朋友通信。

首先来解释一下什么是直接的朋友：每个对象都会与其他对象有耦合关系，只要两个对象之间有耦合关系，我们就说这两个对象之间是朋友关系。耦合的方式很多，依赖、关联、组合、聚合等。其中，我们称出现成员变量、方法参数、方法返回值中的类为直接的朋友，而出现在局部变量中的类则不是直接的朋友。也就是说，陌生的类最好不要作为局部变量的形式出现在类的内部。

对于被依赖的类来说，无论逻辑多么复杂，都尽量的将逻辑封装在类的内部，对外提供 public 方法，不对泄漏任何信息。

#### 7、组合/聚合复用原则 (Composite/Aggregate Reuse Principle)

组合/聚合复用原则就是在一个新的对象里面使用一些已有的对象，使之成为新对象的一部分; 新的对象通过向这些对象的委派达到复用已有功能的目的。

在面向对象的设计中，如果直接继承基类，会破坏封装，因为继承将基类的实现细节暴露给子类；如果基类的实现发生了改变，则子类的实现也不得不改变；从基类继承而来的实现是静态的，不可能在运行时发生改变，没有足够的灵活性。于是就提出了组合/聚合复用原则，也就是在实际开发设计中，尽量使用组合/聚合，不要使用类继承。
