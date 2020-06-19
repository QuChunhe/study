

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

高内聚，松耦合

对于高内聚低耦合，很多人即熟悉又陌生。说熟悉，是因为软件工程中最为常见的，说陌生，是因为大多数说不清楚何时，类似于道，只可意会会，不可言传。不利于设施，也不利于。难以找到相关指标的数据支撑，考核过程中非理性因素难以控制，


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

minimize their complexity





降低复杂性的基本方法，就是把复杂性隔离。“如果能把复杂性隔离在一个模块，不与其他模块互动，就达到了消除复杂性的目的。”

Isolating complexity in places that are rarely interacted with is roughly equivalent to eliminating complexity.

改变软件设计的时候，修改的代码越少，软件的复杂性越低。

Reduce the amount of code that is affected by each design decision, so design changes don’t require very many code modifications.

复杂性尽量封装在模块里面，不要暴露出来。如果多个模块耦合，那就把这些模块合并成一个。

 When a design decision is used across multiple modules, coupling them together.





[阮一峰：如何降低软件的复杂性](https://www.techug.com/post/a-philosophy-of-software-design.html?from=singlemessage)

[五年磨一剑,服务端团队呕心力作之稳定性规范](https://mp.weixin.qq.com/s/gVNKibDQ6UsX_q8_CHvg1A)
