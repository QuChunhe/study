

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


Promote Immutability

Prefer Expressions Over Statements

Design with Higher-Order Functions


external iterators

internal iteration
```
friends.forEach((final String name) -> System.out.println(name))

friends.forEach((name) -> System.out.println(name));

friends.forEach(name -> System.out.println(name));

friends.forEach(System.out::println);

```

Antoine de Saint-Exupéry: “Perfection is achieved not when there is nothing more to add, but when there is nothing left to take away.”

method reference:The Java compiler will take either a lambda expression or a reference to a method where an implementation of a functional interface is expected. With this feature, a short String::toUpperCase can replace name ->name.toUpperCase(),

Tell-Don't-Ask
[TellDontAsk](https://www.martinfowler.com/bliki/TellDontAsk.html)

Tell-Don't-Ask is a principle that helps people remember that object-orientation is about bundling data with the functions that operate on that data. It reminds us that rather than asking an object for data and acting on that data, we should instead tell an object what to do.
