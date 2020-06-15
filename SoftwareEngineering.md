

针对复杂工程问题的通用思路是通过模块化来简化简化问题
* 逐步分解为细粒度的、相对独立的模块
* 通过简单的接口集成模块所提供的功能


modular programming,



[What Is Design Pattern?](http://www.vishalchovatiya.com/what-is-design-pattern/)

The SOLID principles comprise of these five principles:
* SRP – Single Responsibility Principle
* OCP – Open/Closed Principle
* LSP – Liskov Substitution Principle
* ISP – Interface Segregation Principle
* DIP – Dependency Inversion Principle


架构风格（architecture style)


![The Software Design & Architecture Stack](https://github.com/QuChunhe/study/blob/master/pics/Software-Design-Architecture-Stack.png)


John Ousterhout, A Philosophy of Software Design

松耦合低内聚的手段就是模块化，目标是隔离复杂性。分层模式，流水线和过滤器模式，Pipes and Filters

奥卡姆剃刀定律（Occam's Razor, Ockham's Razor）又称“奥康的剃刀”，它是由14世纪英格兰的逻辑学家、圣方济各会修士奥卡姆的威廉（William of Occam，约1285年至1349年）提出。这个原理称为“如无必要，勿增实体”，即“简单有效原理”。正如他在《箴言书注》2卷15题说“切勿浪费较多东西去做，用较少的东西，同样可以做好的事情。”

简无可简时，采用模块。虽然需要满足的需求越来越多，需要

CPU很复杂，通过指令系统提供其功能，操作系统很复杂，通过系统调用，提供其功能。

David Parnas’classic paper “On the Criteria to be used in Decomposing Systems into Modules” appeared in 1971, but the state of the art in software design has not progressed much beyond thatpaper in the ensuing 45 years.

The most fundamental problem in computer science is problem decomposition : how to take a complex problem and divide it up into pieces that can be solved independently.

The largerthe program, and the more people that work on it, the more difficult it is to managecomplexity.

There are two general approaches to fighting complexity. The first approach is to eliminate complexity by making codesimpler and more obvious. For example, complexity can be reduced by eliminatingspecial cases or using identifiers in a consistent fashion.
The second approach to complexity is to encapsulate it, so that programmers can workon a system without being exposed to all of its complexity at once. This approach iscalled modular design . In modular design, a software system is divided up intomodules , such as classes in an object-oriented language. The modules are designed tobe relatively independent of each other, so that a programmer can work on one modulewithout having to understand the details of other modules.



降低复杂性的基本方法，就是把复杂性隔离。“如果能把复杂性隔离在一个模块，不与其他模块互动，就达到了消除复杂性的目的。”

    Isolating complexity in places that are rarely interacted with is roughly equivalent to eliminating complexity.

改变软件设计的时候，修改的代码越少，软件的复杂性越低。

    Reduce the amount of code that is affected by each design decision, so design changes don’t require very many code modifications.

复杂性尽量封装在模块里面，不要暴露出来。如果多个模块耦合，那就把这些模块合并成一个。

    When a design decision is used across multiple modules, coupling them together.


[阮一峰：如何降低软件的复杂性](https://www.techug.com/post/a-philosophy-of-software-design.html?from=singlemessage)

[五年磨一剑,服务端团队呕心力作之稳定性规范](https://mp.weixin.qq.com/s/gVNKibDQ6UsX_q8_CHvg1A)
