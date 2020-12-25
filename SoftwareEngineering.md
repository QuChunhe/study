
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

针对复杂工程问题的通用思路是通过模块化来简化简化问题
* 逐步分解为细粒度的、相对独立的模块
* 通过简单的接口集成模块所提供的功能

产品管理的两大革命
* 标准化
* 流水线

传统的工厂流水线，比如汽车或者手机制造工厂
* 标准化，流水线的生产是高度标准化的
* 固定化，每个人的工作是固定不变，也就是说，在一个流水线一个特定环节的工作是重复性，从上一个流程输出何种半成品
* 可衡量，产品质量和每个人的工作是可以衡量的
* 协同化，一个流水线上众多的环节和工人能够以并行方式相互协同生产

modular programming,


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

三种编程范式Three Programming Styles： procedural programming, object oriented programming, and functional programming. 


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
