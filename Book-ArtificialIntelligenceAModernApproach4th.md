

Stuart J. Russell and Peter Norvig, Artificial Intelligence: A Modern Approach,Fourth Edition, Perason, 2021.



# Chapter 2 Intelligent Agents


rational agents 理性主体

主体、环境和两者之间的耦合

An **agent** is anything that can be viewed as perceiving its environment through sensors and acting upon that environment through actuators. 一个主体可以是任何可以通过传感器感知其周围的环境并通过驱动器作用于环境的东西。

The **environment** could be everything—the entire universe! In practice it is just that part of the universe whose state we care about when designing this agent—the part that affects what the agent perceives and that is affected by the agent’s actions. 环境可以是所有东西——整个宇宙。实际上的环境仅仅是宇宙的一部分，在设计主体时我们关注其状态——这部分影响主体的感知并且受到主体行为的影响。

We use the term **percept** to refer to the content an agent’s sensors are perceiving. An agent’s **percept sequence** is the complete history of everything the agent has ever perceived. In general, an agent’s choice of action at any given instant can depend on its built-in knowledge and on the entire percept sequence observed to date, but not on anything it hasn’t perceived. 我们使用术语感知来指代一个主体的传感器所能感觉的内容。一个主体的感知序列是这个主体所感觉到的事情的完整历史。通常而言，在某个给定时刻主体所选择的动作依赖于其内置的知识以及到在当前时刻的整个感知序列，但是并不是任何的事情都能够被主体感知到。

Mathematically speaking, we say that an agent’s behavior is described by the **agent function** that maps any given percept sequence to an action. 从数学而言，我们说一个主体的行为被描述为主体函数，其将任何给定感知序列映射到一个动作。


Internally, the agent function for an artificial agent will be implemented by an **agent program**. It is important to keep these two ideas distinct. The agent function is an abstract mathematical description; the agent program is a concrete implementation, running within some physical system. 在内部，针对于一个智能主体的主体函数将会由主体程序来实现。将这两个术语区分开来是很重要的。主体函数是一种抽象的数据描述，而主体程序则是具体的实现，运行在一些物理系统上。