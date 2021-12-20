
凡事预（豫）则立，不预（豫）则废。言前定，则不跲；事前定，则不困；行前定，则不疚；道前定，则不穷。——《礼记·中庸》。

居安思危，思则有备，有备无患，敢以此规。——《左传·襄公十一年》

万物之始，大道至简，衍化至繁 --中国道家思想

不谋万世者，不足谋一时；不谋全局者，不足谋一域。--《寤言二·迁都建藩议》

坐而言，不如起而行 --《荀子。性恶》

子贡问：“师与商也孰贤?”
子曰：“师也过，商也不及。”
曰：“然则师愈与?”
子曰：“过犹不及。”   --《论语·先进》

子曰：“工欲善其事，必先利其器。居是邦也，事其大夫之贤者，友其士之仁者。” --《论语·卫灵公》


measure twice and cut once 三思而后行

“季文子三思而后行。《南齐书·公冶度》

阿尔伯特 爱因斯坦说：凡事应该尽量简单，直到不能再简单为止。
 

针对复杂工程问题的通用思路是通过模块化来简化简化问题
* 逐步分解为细粒度的、相对独立的模块
* 通过简单的接口集成模块所提供的功能

产品管理的两大革命
* 标准化
* 流水线

传统的工厂流水线，比如汽车或者手机制造工厂
* 过程可分解。整个产品的生产过程可以分解为若干个相互衔接的阶段。
* 零件标准化，零件是标转化的，最终产品是标转化的，产品线上的生产是过程也是高度标准化的
* 操作固定化，每个人的工作是固定不变，也就是说，在一个流水线一个特定环节的工作是重复性，从上一个流程输出何种半成品
* 质量可衡量，产品质量和每个人的工作是可以衡量的，通过最终质检能够
* 工作协同化，一个流水线上众多的环节和工人能够以并行方式相互协同生产
流水线的优势
* 生产效率高
* 规模可扩展
* 员工要求低

管理中最为成功的发明非流水线莫属了，在很多大型工厂中广泛采用流水线生产，其优势是：1）生产效率高；2）质量可测量；3）规模可扩展。然而，流水线方式很难在大型软件开发中使用，这是因为流水线方式依赖于：1）零件标准化；2）过程可分解；3）工作重复性。软件的边际成本为零，面对相同需求，直接拷贝和应用就行，根本无需重复开发。因此，开发软件往往面临不同需求、场景和环境，差异性造成协作困难，成功高昂

modular programming,

类似于战略、战术和战场不同层级的划分，软件工程中
* 业务
* 架构
* 模块
模块遵循架构的要求，而架构服务于业务。


可以通过如下几个方面分解或者划分系统
* 用户
* 功能
* 数据

如果用户相同，但是功能和数据完全不同，可以将这些功能划分为不同的系统，并通过单点登录使得用户可以在多个系统之前切换

如果部分功能完全系统或者大部分相同，可以采用将这部分功能构建为独立的库或者包

对于系统划分的粒度，在功能上参考如下几个方面
* 系统角色
* 地理位置

对于系统划分的粒度，在功能上参考如下几个方面
* 吞吐需求
* 处理时间
* 耦合程度

对于系统划分的粒度，在数据上参考如下几个方面
* 数据规模
* 相互关系


软件设计的核心能力
* 分解，庖丁解牛，把大功能或大模块分解为更小的子功能或者子模块
* 抽象，分解后的子功能或者子模块具有较少的对外接口


一些软件设计原则：
* Don’t Repeat Yourself (DRY)。
  DRY 系统的每一个功能都应该有唯一的实现，即不能重复开发相同的功能。因此，也被称为"一次且仅一次原则"(Once and Only Once)。《The Pragmatic Programmer》首次提出，在遇到相似或者相同的代码时，需要抽象出公共的解决方案，避免相同的或相似的代码。
  \href{http://en.wikipedia.org/wiki/KISS_principle}{DRY}

* Keep It Simple, Stupid (KISS)
  把一个事情搞复杂是一件简单的事，但要把一个复杂的事变简单，这是一件复杂的事。
  \href{http://en.wikipedia.org/wiki/KISS_principle}{KISS}

* Program to an interface, not an implementation。
  这是设计模式中最根本的哲学，与 Composition over inheritance（喜欢组合而不是继承）原则一起被称为23个经典设计模式中的设计原则。模块之间依赖于接口，而不是实现。接口是抽象的和稳定的，而实现则是多种多样的。该原则可以认为是依赖倒置原则的另一种描述形式。，就是这个原则的的另一种样子。还有一条原则叫。

* Command-Query Separation (CQS) – 命令-查询分离原则。
  查询：当一个方法返回一个值来回应一个问题的时候，它就具有查询的性质；
  命令：当一个方法要改变对象的状态的时候，它就具有命令的性质；
  通常，一个方法可能是纯的Command模式或者是纯的Query模式，或者是两者的混合体。在设计接口时，如果可能，应该尽量使接口单一化，保证方法的行为严格的是命令或者是查询，这样查询方法不会改变对象的状态，没有副作用，而会改变对象的状态的方法不可能有返回值。也就是说：如果我们要问一个问题，那么就不应该影响到它的答案。实际应用，要视具体情况而定，语义的清晰性和使用的简单性之间需要权衡。将Command和Query功能合并入一个方法，方便了客户的使用，但是，降低了清晰性，而且，可能不便于基于断言的程序设计并且需要一个变量来保存查询结果。在系统设计中，很多系统也是以这样原则设计的，查询的功能和命令功能的系统分离，这样有则于系统性能，也有利于系统的安全性。
  \href{http://en.wikipedia.org/wiki/Command-query_separation}{COS}

* 接口隔离原则（ISP）	1.使用多个专门的接口比使用单一的总接口总要好。换而言之，从一个客户类的角度来讲：一个类对另外一个类的依赖性应当是建立在最小接口上的。2．过于臃肿的接口是对接口的污染。不应该强迫客户依赖于它们不用的方法。

* You aren't gonna need it (YAGNI)。
  除了最核心的功能，其他功能一概不要部署，这样可以大大加快开发，其背后的指导思想，就是尽可能快、尽可能简单地让软件运行起来（do the simplest thing that could possibly work）。
  这个原则简而言之为——只考虑和设计必须的功能，避免过度设计。只实现目前需要的功能，在以后您需要更多功能时，可以再进行添加。如无必要，勿增复杂性。软件开发先是一场沟通博弈。我们的程序员或是架构师在设计系统的时候，会考虑很多扩展性的东西，导致在架构与设计方面使用了大量折衷，最后导致项目失败。这是个令人感到讽刺的教训，因为本来希望尽可能延长项目的生命周期，结果反而缩短了生命周期。
  \href{http://en.wikipedia.org/wiki/You_Ain%27t_Gonna_Need_It}{YAGNI}

* Law of Demeter – 迪米特法则.
  迪米特法则(Law of Demeter)，又称“最少知识原则”（Principle of Least Knowledge），其来源于1987年荷兰大学的一个叫做Demeter 的项目。Craig Larman把Law of Demeter 又称作“不要和陌生人说话”。在《程序员修炼之道》中讲LoD的那一章叫作“解耦合与迪米特法则”。

  \item Single Responsibility Principle (SRP) – 职责单一原则.
  单一职责原则的核心思想为：一个类仅负责一项职责，只做一件事并将其做好。单一职责原则可以看作是低耦合、高内聚在面向对象原则上的一个应用。如果一个类负责的职责过多，就使得多个职责在一个类中高度耦合，当其中一个职责变化或者改动时，可能会导致其他职责的故障。单一职责，通常意味着单一的功能，为类之间和模块之间划分清晰的职责和边界。
* Open/Closed Principle (OCP) – 开闭原则.
  开发封闭的核心思想是：Software entities should be open for extension,but closed for modification，即软件模块对扩展是开放的，但对修改是封闭的。换而言之年，模块是可扩展的，而不可修改的。对扩展开放，意味着有新的需求或变化时，可以对现有代码进行扩展，以适应新的情况。对修改封闭，意味着类一旦设计完成，就可以独立完成其工作，而不要对类进行任何修改。开闭规则的核心好处：1) 弹性扩展已有的系统,增加新的功能,以满足新的需求。这使得软件系统具有一定的适应性和灵活性；2)不用修改已有的软件模块，这使得系统具有一定的稳定性和延续性。
  \item Liskov substitution principle (LSP) – 里氏代换原则.
  软件工程大师Robert C. Martin把里氏代换原则最终简化为一句话：“Subtypes must be substitutable for their base types”。也就是，子类必须能够替换成它们的基类。即：子类应该可以替换任何基类能够出现的地方，并且经过替换以后，代码还能正常工作。另外，不应该在代码中出现if/else之类对子类类型进行判断的条件。里氏替换原则LSP 是使代码符合开闭原则的一个重要保证。正是由于子类型的可替换性才使得父类型的模块在无需修改的情况下就可以扩展。
* Interface Segregation Principle (ISP) – 接口隔离原则.
  接口隔离原则意思是把功能实现在接口中，而不是类中，使用多个专门的接口比使用单一的总接口要好。
* Dependency Inversion Principle (DIP) – 依赖倒置原则.
  高层模块不应该依赖于低层模块的实现，而是依赖于高层抽象。
  \item Common Closure Principle（CCP）– 共同封闭原则.
  一个包中所有的类应该对同一种类型的变化关闭。一个变化影响一个包，便影响了包中所有的类。一个更简短的说法是：一起修改的类，应该组合在一起（同一个包里）。如果必须修改应用程序里的代码，我们希望所有的修改都发生在一个包里（修改关闭），而不是遍布在很多包里。CCP原则就是把因为某个同样的原因而需要修改的所有类组合进一个包里。如果2个类从物理上或者从概念上联系得非常紧密，它们通常一起发生改变，那么它们应该属于同一个包。
* Common Reuse Principle (CRP) – 共同重用原则.
  包的所有类被一起重用。如果你重用了其中的一个类，就重用全部。换个说法是，没有被一起重用的类不应该被组合在一起。CRP原则帮助我们决定哪些类应该被放到同一个包里。依赖一个包就是依赖这个包所包含的一切。当一个包发生了改变，并发布新的版本，使用这个包的所有用户都必须在新的包环境下验证他们的工作，即使被他们使用的部分没有发生任何改变。因为如果包中包含有未被使用的类，即使用户不关心该类是否改变，但用户还是不得不升级该包并对原来的功能加以重新测试。
* Hollywood Principle – 好莱坞原则.
  好莱坞原则就是一句话——“don’t call us, we’ll call you.”。意思是，好莱坞的经纪人们不希望你去联系他们，而是他们会在需要的时候来联系你。也就是说，所有的组件都是被动的，所有的组件初始化和调用都由容器负责。组件处在一个容器当中，由容器负责管理。
  简单的来讲，就是由容器控制程序之间的关系，而非传统实现中，由程序代码直接操控。这也就是所谓“控制反转”的概念所在：

  1.不创建对象，而是描述创建对象的方式。

  2.在代码中，对象与服务没有直接联系，而是容器负责将这些联系在一起。

  控制权由应用代码中转到了外部容器，控制权的转移，是所谓反转。好莱坞原则就是IoC（Inversion of Control）或DI（Dependency Injection ）的基础原则。这个原则很像依赖倒置原则，依赖接口，而不是实例，但是这个原则要解决的是怎么把这个实例传入调用类中？你可能把其声明成成员，你可以通过构造函数，你可以通过函数参数。但是 IoC可以让你通过配置文件，一个由Service Container 读取的配置文件来产生实际配置的类。但是程序也有可能变得不易读了，程序的性能也有可能还会下降。
* High Cohesion \& Low/Loose coupling  – 高内聚， 低耦合
  这个原则是UNIX操作系统设计的经典原则，把模块间的耦合降到最低，而努力让一个模块做到精益求精。
  内聚：一个模块内各个元素彼此结合的紧密程度
  耦合：一个软件结构内不同模块之间互连程度的度量
  内聚意味着重用和独立，耦合意味着多米诺效应牵一发动全身

* Convention over Configuration（CoC）– 惯例优于配置原则
  简单点说，就是将一些公认的配置方式和信息作为内部缺省的规则来使用。例如，Hibernate的映射文件，如果约定字段名和类属性一致的话，基本上就可以不要这个配置文件了。你的应用只需要指定不convention 的信息即可，从而减少了大量convention 而又不得不花时间和精力啰里啰嗦的东东。配置文件很多时候相当的影响开发效率。
  Rails 中很少有配置文件（但不是没有，数据库连接就是一个配置文件），Rails 的fans号称期开发效率是 java 开发的 10 倍，估计就是这个原因。Maven也使用了CoC原则，当你执行mvn -compile命令的时候，不需要指源文件放在什么地方，而编译以后的class文件放置在什么地方也没有指定，这就是CoC原则。

* Separation of Concerns (SoC) – 关注点分离.
  SoC 是计算机科学中最重要的努力目标之一。这个原则，就是在软件开发中，通过各种手段，将问题的各个关注点分开。如果一个问题能分解为独立且较小的问题，就是相对较易解决的。问题太过于复杂，要解决问题需要关注的点太多，而程序员的能力是有限的，不能同时关注于问题的各个方面。实现关注点分离的方法主要有两种，一种是标准化，另一种是抽象与包装。标准化就是制定一套标准，让使用者都遵守它，将人们的行为统一起来，这样使用标准的人就不用担心别人会有很多种不同的实现，使自己的程序不能和别人的配合。Java EE就是一个标准的大集合。每个开发者只需要关注于标准本身和他所在做的事情就行了。就像是开发镙丝钉的人只专注于开发镙丝钉就行了，而不用关注镙帽是怎么生产的，反正镙帽和镙丝钉按标来就一定能合得上。不断地把程序的某些部分抽像差包装起来，也是实现关注点分离的好方法。一旦一个函数被抽像出来并实现了，那么使用函数的人就不用关心这个函数是如何实现的，同样的，一旦一个类被抽像并实现了，类的使用者也不用再关注于这个类的内部是如何实现的。诸如组件，分层，面向服务，等等这些概念都是在不同的层次上做抽像和包装，以使得使用者不用关心它的内部实现细节。

* Design by Contract (DbC) – 契约式设计

* Acyclic Dependencies Principle (ADP) – 无环依赖原则.
  包之间的依赖结构必须是一个直接的无环图形，也就是说，在依赖结构中不允许出现环（循环依赖）。如果包的依赖形成了环状结构，怎么样打破这种循环依赖呢？有2种方法可以打破这种循环依赖关系：第一种方法是创建新的包，如果A、B、C形成环路依赖，那么把这些共同类抽出来放在一个新的包D里。这样就把C 依赖A变成了C依赖D以及A依赖D，从而打破了循环依赖关系。第二种方法是使用DIP （依赖倒置原则）和ISP （接口分隔原则）设计原则。
  无环依赖原则（ADP）为我们解决包之间的关系耦合问题。在设计模块时，不能有循环依赖。

*  Encapsulate What Changes -封装经常修改的代码
在软件领域永远不变的是“变化”，所以把您认为或怀疑将来要被修改的代码封装起来。这种面向对象设计模式的优点是：易于测试和维护恰当封装的代码。

* Rule Of Three。Rule of three 称为"三次原则"，指的是当某个功能第三次出现时，才进行"抽象化"

*  Favor Composition over Inheritance -优先使用组合而非继承。

  如果可以的话，要优先使用组合而非继承。





单一职责原则（SRP）	就一个类而言，应该仅有一个引起它变化的原因。

”开放－封闭”原则(OCP)	在软件设计模式中，这种不能修改，但可以扩展的思想也是最重要的一种设计原则。即软件实体（类、模板、函数等等）应该可以扩展，但是不可修改。

里氏代换原则（LSP）一个软件实体如果使用的是一个父类的话，那么一定适用于该子类，而且他觉察不出父类对象和子类对象的区别。也就是说，在软件里面，把父类都替换成它的子类，程序的行为没有变化。

依赖倒置原则(DIP)	高层模块不应该依赖于底层模块。两个都应该依赖抽象。2.抽象不应该依赖于细节，细节依赖于抽象。针对接口编程，不要针对实现编程。



合成/聚合复用原则（CARP）	尽量使用合成/聚合，尽量不要使用类继承。聚合：表示一种弱的拥有关系，体现的是A 对象可以包含B对象，但B 对象不是A对象的一部分。合成：一种强的拥有关系，提现了严格的部分和整体的关系，部分和整体的生存周期一致。

迪米特法则（LoD）强调类之间的松耦合。即：如果两个类不必彼此直接通信，那么着两个类就不应当发送直接的相互作用。如果其中一个类需要调用另一个类的某一个方法的话，可以通过第三者转发这个调用。

SOLID中的字母“O”指的是打开/关闭设计原则。单一职责原则是另外一个SOLID设计原则，SOLID中的字母“S”指的就是它
SOLID中的字母“D”指的就是Dependency Injection or Inversion principle。SOLID中的字母“L”指的就是 LSP设计原则


《The Art of Unix Programming》总结了下面这些哲学，都是至理名言啊。
* Rule of Modularity: Write simple parts connected by clean interfaces.
* Rule of Clarity: Clarity is better than cleverness.
* Rule of Composition: Design programs to be connected to other programs.
* Rule of Separation: Separate policy from mechanism; separate interfaces from engines.
* Rule of Simplicity: Design for simplicity; add complexity only where you must.
  简单原则：设计要简单；如无必要，切勿增加复杂性
* Rule of Parsimony: Write a big program only when it is clear by demonstration that nothing else will do.
* Rule of Transparency: Design for visibility to make inspection and debugging easier.
* Rule of Robustness: Robustness is the child of transparency and simplicity.
* Rule of Representation: Fold knowledge into data so program logic can be stupid and robust.
* Rule of Least Surprise: In interface design, always do the least surprising thing.
* Rule of Silence: When a program has nothing surprising to say, it should say nothing.
* Rule of Repair: When you must fail, fail noisily and as soon as possible.
* Rule of Economy: Programmer time is expensive; conserve it in preference to machine time.
* Rule of Generation: Avoid hand-hacking; write programs to write programs when you can.
* Rule of Optimization: Prototype before polishing. Get it working before you optimize it.
  优化原则：在打磨之前先有原型，在优化之前先能工作
* Rule of Diversity: Distrust all claims for “one true way”.
* Rule of Extensibility: Design for the future, because it will be here sooner than you think.


传统软件开发过程划分为相互衔接但泾渭分明的若干阶段，分别为需求分析、系统设计、代码开发和测试验收等。之所以称为敏捷开发，是相对于传统开发的迟钝而言，其敏捷性主要体现在：1）设计、编码和测试更加紧密地揉合一起，相关的人员和过程没有清晰的分割，因此可以更加地进入代码开发；2）设计、编码和测试是相互不断迭代的过程，出现问题或者偏差可以更快地优化设计和重构代码。


[Open–closed principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle)

In object-oriented programming, the open–closed principle states "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"; that is, such an entity can allow its behaviour to be extended without modifying its source code. 

[Single-responsibility principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)

The single-responsibility principle (SRP) is a computer-programming principle that states that every module, class or function in a computer program should have responsibility over a single part of that program's functionality, which it should encapsulate. All of that module, class or function's services should be narrowly aligned with that responsibility.

[Cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science))

In computer programming, cohesion refers to the degree to which the elements inside a module belong together.

迪米特法则（Law of Demeter）又叫作最少知识原则（Least Knowledge Principle 简写LKP），就是说一个对象应当对其他对象有尽可能少的了解

[KISS](https://en.wikipedia.org/wiki/KISS_principle)

[DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

[SLA](http://www.principles-wiki.net/principles:single_level_of_abstraction)

[“You aren’t gonna need it!” (YAGNI)](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it)

[What Is Design Pattern?](http://www.vishalchovatiya.com/what-is-design-pattern/)

The SOLID principles comprise of these five principles:
* SRP – Single Responsibility Principle
* OCP – Open/Closed Principle
* LSP – Liskov Substitution Principle
* ISP – Interface Segregation Principle
* DIP – Dependency Inversion Principle

[SOLID](https://en.wikipedia.org/wiki/SOLID)

架构风格（architecture style)


[10 Coding principles and acronyms demystified!](https://areknawo.com/10-coding-principles-and-acronyms-demystified/)


![The Software Design & Architecture Stack](https://github.com/QuChunhe/study/blob/master/pics/Software-Design-Architecture-Stack.png)

高内聚，松耦合

对于高内聚低耦合，很多人即熟悉又陌生。说熟悉，是因为软件工程中最为常见的准则，说陌生，是因为大多数说不清楚何时，类似于道，只可意会，不可言传。不利于设施，也不利于。难以找到相关指标的数据支撑，考核过程中非理性因素难以控制，

虽然工程师都在谈论，但是实际上却无从下手，甚至判断一个是否是高内聚松耦合时，还会争论不休

需要明确和简单的指标衡量，这个指标很好地反映了高内聚和松耦合性

耦合性

依赖性，依赖性越高，其内聚程度越低。代码规模越大。

软件工程既然称之为工程，那么就类似其他工程，例如建桥、修路和制造分解

1）满足工程目标和业务需求，一系列的衡量指标，在业务上满足那些功能和流程，每个流程的数据要求等。在性能上，满足可靠性、吞吐量和响应时间等要

2）收到各种条件约束，例如预算、人员、开发周期、硬件设施和继承遗留系统等等

设计的目的在满足1）和2）的情况，给出一个可实施的方案：a）要尽可能简单，使得复杂性最小化；b)指导和协同后续的开发、多人并行开发，能够将会集成起来，满足1）


minimize their complexity



Charles Perrow’s Normal Accident Theory 

Charles Perrow, Normal Accidents (Princeton, NJ: Princeton University Press, 1999).

[Todd R. LaPorte and Paula M. Consolini, “Working in Practice but Not in Theory: Theoretical Challenges of ‘High-Reliability Organizations,’” Journal of Public Administration Research and Theory, Oxford Journals](https://polisci.berkeley.edu/sites/default/files/people/u3825/LaPorte-WorkinginPracticebutNotinTheory.pdf)

考虑考量上面的条件约束继承上，实现工程目标和业务需求。运行在高性能的小型机上，与运行在三个普通商用刀片服务器上，系统设计就可能会不同。每天响应一百万和每天响应一百亿个服务请求。99%的可靠性，99.999%的可靠性，硬件设施、软件架构和代码质量等方面的要求就会非常不同。


横看成岭侧成峰，远近高低各不同。不同角色，不同任务的参与者看到的系统是不同的，需要不同的视图，便于参与者理解系统，

大量程序员的困境

IT行业的特点
zhid
IT行业技术演进快，新技术、新概念和新方法层出不穷。知识和技能的老化程度很快，

在参加工作后，缺乏动力系统的和持续的学习，难以跟上技术进步的步伐。投入生活的时间更多，缺乏工作的冲进和主动性。

面向年轻客户，需要年轻的员工和开发人员；

成本考量，年轻程序员的薪水较低，


中国的产业结果和中国企业在产业链中的位置有关


面向业务应用，应用软件开发，缺乏基础软件，工具软件，缺乏软件产品的

代码规模较小，团队也小，很多大公司，也是小团队独立作战。

软件质量不高

性能要求较低

功能实现简单，虽然大量工具和开源系统的涌现，大大降低了开发的难度，使得程序员的准入门槛不高，无须复杂的计算机知识和专业领域支持，

产品利润较低，在某一个方面和领域，长期投入人力和物力，进行研究和开发。往往短平快，缺乏技术的积累和沉淀



管理方面的考虑，年轻程序员，尤其是刚刚进入职场的程序员，职业可塑性更强，便于管理

公司的历史较段，大部分是年轻程序员，

软件系统分类
* 服务器端软件系统
  * 软件产品：通用需求，第三方运维和管理
  * 软件服务：通用需求，自己运维和管理
  * 软件应用：定制开放，自己运维和管理
* 客户端软件系统


### John Ousterhout, A Philosophy of Software Design

松耦合低内聚的手段就是模块化，目标是隔离复杂性。分层模式，流水线和过滤器模式，Pipes and Filters

奥卡姆剃刀定律（Occam's Razor, Ockham's Razor）又称“奥康的剃刀”，它是由14世纪英格兰的逻辑学家、圣方济各会修士奥卡姆的威廉（William of Occam，约1285年至1349年）提出。这个原理称为“如无必要，勿增实体”，即“简单有效原理”。正如他在《箴言书注》2卷15题说“切勿浪费较多东西去做，用较少的东西，同样可以做好的事情。”

简无可简时，采用模块。虽然需要满足的需求越来越多，需要。模块化，实现功能的分装和复杂性的隔离

CPU很复杂，通过指令系统提供其功能，操作系统很复杂，通过系统调用，提供其功能。

David Parnas’classic paper “On the Criteria to be used in Decomposing Systems into Modules” appeared in 1971, but the state of the art in software design has not progressed much beyond thatpaper in the ensuing 45 years.

The most fundamental problem in computer science is problem decomposition : how to take a complex problem and divide it up into pieces that can be solved independently.

The largerthe program, and the more people that work on it, the more difficult it is to managecomplexity.

There are two general approaches to fighting complexity. The first approach is to eliminate complexity by making codesimpler and more obvious. For example, complexity can be reduced by eliminatingspecial cases or using identifiers in a consistent fashion.
The second approach to complexity is to encapsulate it, so that programmers can workon a system without being exposed to all of its complexity at once. This approach iscalled modular design . In modular design, a software system is divided up intomodules , such as classes in an object-oriented language. The modules are designed tobe relatively independent of each other, so that a programmer can work on one modulewithout having to understand the details of other modules.


 Software systemsare intrinsically more complex than physical systems; it isn’t possible tovisualize the design for a large software system well enough to understand all of itsimplications before building anything. As a result, the initial design will have manyproblems. The problems do not become apparent until implementation is well underway. However, the waterfall model is not structured to accommodate major design changes atthis point (for example, the designers may have moved on to other projects). Thus,developers try to patch around the problems without changing the overall design. Thisresults in an explosion of complexity.

Beautiful designs reflect a balance between competing ideas and approaches.

to minimize their complexity。Exactly what is “complexity”? How can youtell if a system is unnecessarily complex? What causes systems to become complex?


使得复杂性最小化：确定去说复杂性是什么？如何评估一个系统不该如此复杂？什么造成系统变得复杂？
如果一味追求简单性，那么只能使得人类退回到石器时代。

Complexity is anything related to the structure of a software system thatmakes it hard to understand and modify the system.

复杂性可以是与一个软件系统结构相关的任何东西，只要其使得该系统难以理解和难以更改。




降低复杂性的基本方法，就是把复杂性隔离。“如果能把复杂性隔离在一个模块，不与其他模块互动，就达到了消除复杂性的目的。”

Isolating complexity in places that are rarely interacted with is roughly equivalent to eliminating complexity.

改变软件设计的时候，修改的代码越少，软件的复杂性越低。

Reduce the amount of code that is affected by each design decision, so design changes don’t require very many code modifications.

复杂性尽量封装在模块里面，不要暴露出来。如果多个模块耦合，那就把这些模块合并成一个。

 When a design decision is used across multiple modules, coupling them together.





[阮一峰：如何降低软件的复杂性](https://www.techug.com/post/a-philosophy-of-software-design.html?from=singlemessage)

[五年磨一剑,服务端团队呕心力作之稳定性规范](https://mp.weixin.qq.com/s/gVNKibDQ6UsX_q8_CHvg1A)

[IEEE Std 729-1983, IEEE Standard Glossary of Software Engineering Terminology](http://www.informatik.htw-dresden.de/~hauptman/SEI/IEEE_Standard_Glossary_of_Software_Engineering_Terminology%20.pdf)

architectural design. (1) The process of defining a collection of hardware and software components and their interfaces to establish the framework for the development of a computer system. See also: functional design. (2) The result of the process in (1).

architecture. The organizational structure of a system or component. See also: component; module; subprogram; routine.

cohesion. The manner and degree to which the tasks performed by a single software module are related to one another. Types include coincidental, communicational, functional,logical, procedural, sequential, and temporal. Syn: module strength. Contrast with: coupling.

component. One of the parts that make up a system. A component may be hardware or software and may be subdivided into other
components. Note: The terms “module,” “component,” and “unit” are often used interchangeably or defined to be subelements of one another in different ways
depending upon the context. The relationship of these terms is not yet standardized.

coupling. The manner and degree of interdependence between software modules. Types include common-environment coupling,content coupling, control coupling, data coupling, hybrid coupling, and pathological coupling. Contrast with: cohesion.

decoupling. The process of making software modules more independent of one another to decrease the impact of changes to, and errors in, the individual modules. See also: Coupling.

encapsulation. A software development technique that consists of isolating a system function o r a set of data and operations on
those data within a module and providing precise specifications for the module. See also: data abstraction; information hiding.

modular. Composed of discrete parts. See also:modular decomposition; modular programming.

modular decomposition. The process of breaking a system into components to facilitate design and development; an element of modular programming. Syn: modularization. See also: cohesion; coupling; demodularization; factoring; functional decomposition; hierarchical decomposition; packaging.


modular programming. A software development technique in which software is developed as a collection of modules.

modularity. The degree t o which a system or computer program is composed of discrete components such that a change to one component has minimal impact on other components. See also: cohesion; coupling.

module. (1) A program unit that is discrete and identifiable with respect to compiling,combining with other units, and loading; for example, the input to, or output from, an assembler, compiler, linkage editor, or executive routine.(2) A logically separable part of a program.


https://en.wikipedia.org/wiki/Bertrand_Meyer

five criteria for modularity:
* Decomposability of the problem into sub-problems
* Composability of modules to produce new systems
* Understandability of a module in isolation
* Continuity - small changes have localized effects
* Protection - fault isolation


[Modularity of Mind](https://plato.stanford.edu/entries/modularity-mind/)


[Modularity:Guidelines for design in any programming language](https://www.eecs.yorku.ca/course_archive/2013-14/F/3311/slides/14-Modularity.pdf)

Modular software ==> maintainable software:Uses divide and conquer principle

三种编程范式Three Programming Styles： procedural programming/structured programming（过程式编程/结构化编程）, object-oriented programming（面向对象编程）, and functional programming（函数式编程）. 


[HOW DO COMMITTEES INVENT?](http://www.melconway.com/Home/pdf/committees.pdf)



[康威定律](https://www.jianshu.com/p/ba2d444c89d2)

Conway’s law 最初来自于Conway在1967年发表的论文《How Do Committees Invent?》，之后在《人月神话》
这本书中引用了论文的结论，并命名为康威定律（Conway’s law）得以推广。
>Conway’s law: Organizations which design systems (in the broad sense used here) are constrained to produce designs which are copies of the communication >structures of these organizations. - Melvin Conway(1967)
>设计系统的组织其产生的设计等价于组织间的沟通结构。

>a design effort should be organized according to the need for communication.

Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure.

任何设计系统的组织，必然会产生以下设计结果：即其结构就是该组织沟通结构的写照。简单来说： 产品必然是其组织沟通结构的缩影。 

反向理解起来也是成立的。
>Conway’s law reversed：You won’t be able to successfully establish an efficient organizational structure that is not supported by your system architecture >design.
>如果系统架构不支持，你无法建立一个高效的组织。

[Conway’s Four Laws](www.amundsen.com/talks/2016-07-restfest-conway/2016-07-restfest-conway.pdf)

Communication dictates design.-- Mel Conway, 1967

Brooks’ Law “Adding manpower to a late software project makes it later.” -- Fred Brooks, 1975

Intercommunication formula n(n − 1) / 2  -- Fred Brooks, 1975

Dunbar's Number: the max number of relationships a person can maintain

**Conway’s (first) Law**: tells us TEAM SIZE is important

so... Make the teams as small as necessary.

“There is never enough time to do something right, but there is always enough time to do it over.” -- Mel Conway, 1967

Increasing Intractability -- Eric Hollnagel, 2009
1. Systems grow too large
2. Rate of change increases
3. Overall expectations keep rising


**Conway’s Second Law**: tells us PROBLEM SIZE is important.

so...Make the solution as small as necessary.

Homomorphism  “There is a homomorphism from the linear graph of a system to the linear graph of its design organization” -- Mel Conway, 1967

**Conway’s Third Law** : tells us CROSS-TEAM INDEPENDENCE is important.

So...
Make each team fully independent.


Disintegration  “The structures of large systems tend to disintegrate during development, qualitatively more so than with small systems.” -- Mel Conway, 1967


**Conway’s Fourth Law**: tells us TIME is against LARGE teams.

So...
Make release cycles short and small.


Conway’s First Law: A system’s design is a copy of the organization’s communication structure. Actively manage communications within the
teams and across teams.

Conway’s Second Law: There is never enough time to do something right, but there is always enough time to do it over. Remember the process is
continually repeating.

Conway’s Third Law: There is a homomorphism from the linear graph of a system to the linear graph of its design organization. Organize teams in order to
achieve desired system.

Conway’s Lessons from 1967
1. Increase communications
2. Support continuous process
3. Organize teams by products
4. Make teams small as necessary





Mike Amundsen 归纳了如下四个核心观点:

**第一定律**

>Communication dictates the design
>组织沟通方式会通过系统设计表达出来

**第二定律**

>There is never enough time to do something right, but there is always enough time to do it over
>时间再多一件事情也不可能做的完美，但总有时间做完一件事情


**第三定律**

>There is a homomorphism from the linear graph of a system to the linear graph of its design organization
>线型系统和线型组织架构间有潜在的异质同态特性



**第四定律**

>The structures of large systems tend to disintegrate during development, qualitatively more so than with small systems
>大的系统组织总是比小系统更倾向于分解



**Murphy's law**

[Murphy's law](https://en.wikiquote.org/wiki/Murphy%27s_law)
>Murphy's law is a popular adage that states that "things will go wrong in any given situation, if you give them a chance." or more commonly, "whatever can go >wrong, will go wrong."

如果事情可能出錯，它最終一定會出錯。


**Brook’s Law**

[Brook’s Law](https://www.techopedia.com/definition/18085/brooks-law)


Brooks’ Law refers to a well-known software development principle coined by Fred Brooks in "The Mythical Man-Month". 
>"Adding manpower to a late software project makes it later,” 
states that when a person is added to a project team, and the project is already late, the project time is longer, rather than shorter.

Brooks' law may be applied for two key reasons:
* "Ramp up" time, which is required by new project members for productivity because of the complex nature of software projects are complex. This takes existing resources (personnel) away from active development and places them in training roles.
* An increase in staff drives communication overhead, including the number and variety of communication channels. 


**Hofstadter's law** 

Douglas Hofstadter, a cognitive scientist and author, introduced the law in his 1979  book Gödel, Escher, Bach: An Eternal Golden Braid.

Hofstadter’s law is the observation that “It always takes longer than you expect, even when you take into account Hofstadter's Law.” In other words, time estimates for how long anything will take to accomplish always fall short of the actual time required -- even when the time allotment is increased to compensate for the human tendency to underestimate it.


Hofstadter’s law illustrates one element of optimism bias, which leads people to overestimate the benefits of some proposed system and underestimate the drawbacks, as well as the time required for completion. It’s also closely related to the ninety-ninety rule proposed by Tom Cargill of Bell Labs: The first 90 percent of the code accounts for the first 90 percent of the development time. The remaining 10 percent of the code accounts for the other 90 percent of the development time.

**Conway’s Law**

**帕累托法则（Pareto Principle）或 80/20法则**

**Moore’s Law**


[Who is Solution Architect: Processes, Role Description, Responsibilities, and Outcomes](https://www.altexsoft.com/blog/engineering/solution-architect-role/)

[Software Architect Role, Skills, and Impact on Product Success](https://www.altexsoft.com/blog/software-architect-role/)

[How Enterprise Architects Close the Gap between Technology and Business](https://www.altexsoft.com/blog/business/how-enterprise-architects-close-the-gap-between-technology-and-business/)


D. L. Parnas, On the Criteria To Be Used in Decomposing Systems into Modules

A well-defined segmentation of the project effort ensures system modularity. Each task forms a separate, distinct program module. At implementation time each module
and its inputs and outputs are well-defined, there is no confusion in the intended interface with other system modules. At checkout time the integrity of the module is tested independently; there are few scheduling problems in synchronizing  the completion of several tasks before checkout can begin. Finally, the system is maintained in modular fashion; system errors and deficiencies can be traced to specific system modules, thus limiting the scope of detailed error searching.
对于项目工作定义明确的分工确保系统的模块化。每个任务形成一个分离的、清晰的程序模块。在实现期间，每个模块以及其输入和输出会被明确的定义，使得在打算通过接口集成其他系统模块时不会产生任何混淆。在检测期间，集成的模块可以独立测试。最后，系统能够以模块化的方式被维护，系统错误和缺陷能够被跟踪定位到特定的系统模块，因此限制记录错误搜索的范围

The major progress in the area of modular programming has been the development of coding techniques and assemblers which (1) allow one module to be written with little knowledge of the code used in another module and, (2) allow modules to be reassembled and replaced without reassembly of the whole system.
在模块化变成领域主要的进展是编码技术和装配器的发展：1）其许可在对另一个使用的模块知之甚少的情况下编写一个模块；2）许可模板被重新装配和替换而无需整个系统进行重新组装，


The expected benefits of modular programming fall into three classes: (1) managerial -- development time could be shortened because separate groups would work on each module with little need for communication (and little regret afterward that there had not been more communication); (2) product flexibility — it was hoped that it would be possible to make quite drastic changes or improvements in one module without changing others; (3) comprehensibility -- it was hoped that the system could be studied a module at a time with the result that the whole system could be better designed because it was better understood.
模块化编程所期望的好处可以划归为三类：（1）管理上——因为分开的多个组需要较少的交流就可以开发对应的模块，从而缩短开发时间；（2）产品的灵活性——期望可以在不改变其他模块的情况针对一个模块实现巨大的更新或者改进；（3）可理解性——期望能够在一个时间仅仅研究系统的一个模块，由于系统能够更好地理解，从而够更好地设计系统。

In the first decomposition the criterion used was make each 'major step' in the processing a module. One might say that to get the first decomposition one makes a flowchart. Figure 1 is a flowchart. This is the most common approach to decomposition or modularization.
在第一个分解中所使用的标准是使得处理过程中的每个主要步骤成为一个模块。有人可能会说，为了得到第一个分解可以制作了一个流程图。图1是一个流程图。这是最常见的分解或模块化方法。

The second decomposition was made using "information hiding"  as a criteria. The modules no longer correspond to steps in the processing. 
在第二次分解中采用了信息隐藏作为标准。模块不再对应于处理中的步骤

Every module in the second decomposition is characterized by its knowledge of a design decision which it hides from all others. Its interface or definition was chosen to reveal as little as possible about its inner workings.
第二个分解中每个模块都以其对设计决策的知识为特征，而模块对其他所有模块隐藏这些知识。所选择的接口或定义暴露尽可能少的其内部工作情况。

另种方式的区别
* 第一种分解方式采用动词分解过程
* 第二种分解方式采用名称分解实体




伯斯塔尔法则 Postel’s Law

接受多变，输出保守。

理论背景

该原理也被称为鲁棒性原理（Robustness Principle），1980 年，Jonathan Bruce Postel 在他编写的最早期的 TCP 协议规范中有提到：

    Be conservative in what you send, be liberal in what you accept.
    对发送的内容保持谨慎，对接收的内容保持自由。（直译）

至此之后，该原理便被称为伯斯塔尔法则（Postel’s Law），广泛应用于计算机协议以及系统控制理论中。虽然最近几年计算机界中出现了一些质疑伯斯塔尔法则的声音，但这并不妨碍其核心思想被应用于 UI/UX 的领域。

[让设计更有说服力的20条经典原则：伯斯塔尔法则、系列位置效应](https://www.uisdc.com/postels-law-serial-position-effect)

[The Full-stack Software Design & Architecture Map](https://khalilstemmler.com/articles/software-design-architecture/full-stack-software-design/)
Understanding how to:
* Architect a system to serve the needs of its users
* Write code that's easy to change
* Write code that's easy to maintain
* Write code that's easy to test

First Principles Thinking： 第一性原则

A first principle is a basic assumption that cannot be deduced any further. Over two thousand years ago, Aristotle defined a first principle as “the first basis from which a thing is known.”

Many of the most groundbreaking ideas in history have been a result of boiling things down to the first principles and then substituting a more effective solution for one of the key part. 
历史上许多最具开创性的想法都是结果，将事情简化为第一条原则，然后用更有效的解决方案替代其中一个关键部分。

One of the primary obstacles to first principles thinking is our tendency to optimize form rather than function. 
第一性原则思考的一个主要障碍是我们倾向于优化形式而不是功能。

The goal of software is to continually produce something that satisfies the needs of its users, while minimizing the effort it takes to do so.

Stage 1: Clean code

Stage 2: Programming Paradigms
* Object-Oriented Programming is the tool best suited for defining how we cross architectural boundaries with polymorphism and plugins
* Functional programming is the tool we use to push data to the boundaries of our applications
* Structured programming is the tool we use to write algorithms



Stage 3: Object-Oriented Programming

Functional programming can seem like the means to all ends in this scenario, but I'd recommend getting acquainted with model-driven design and Domain-Driven Design to understand the bigger picture on how object-modelers are able to encapsulate an entire business in a zero-dependency domain model.

https://khalilstemmler.com/articles/software-design-architecture/full-stack-software-design/





产品经理能够从软件工程中学到的
* 尽可能地使用商品化硬件/系统，而不是定制化的硬件/系统。大规模的生产不仅能够大大降低成本，而且有助于协同的、快速的技术演进。更多的产量往往意味着更多的利润，能够促进上下游厂商投入更多资源参与，从而促进相关技术、组件和产品的进步。产品进步往往又会促进产品的更新换代和使用，形成产品进步和产品产量之间的正向促进。超级计算机和商品化服务器搭建的集群，前者是定制化的设计和制造，甚至需要专门地改造软件系统，用以适配不同的超算，在大型数值计算等领域，超算还是有其用武之地，因此集群不能完全替代超算的位置，但是在很多领域，例如网络服务和数据数据等领域，
* 帕瓦罗原理，二八定律
* 


[Enterprise Integration Patterns](https://www.enterpriseintegrationpatterns.com/patterns/conversation/toc.html)


[隔舱模式](https://docs.microsoft.com/zh-cn/azure/architecture/patterns/bulkhead)



幂等这个概念，是一个数学上的概念，即：f……(f(f(x))) = f(x)。用在计算机领域，指的是系统里的接口或方法对外的一种承诺，使用相同参数对同一资源重复调用某个接口或方法的结果与调用一次的结果相同


The situation where the number of classes increases to an unmanageable extent is called a class explosion and the java.io package is a good example of that.
