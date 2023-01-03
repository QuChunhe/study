
Michael Huth and Mark Ryan, Logic in Computer Science: Modelling and Reasoning about Systems 2ed, Cambridge University Press, 2004.

数理逻辑17.flv

Completeness Compactness consistency  

 induction on the complexity of the formula, or induction on the structure of the formula

 Free variables are the variables upon which the truth value of a formula may depend.


 形式语义（formal semantics）以及可靠（sound）和完备（完备）的推理规则。

[陆钟万 数理逻辑](https://www.bilibili.com/video/av9936866?from=search&seid=14344028886371409819)　

数理逻辑的四个分支
* 模型论   
* 集合论   
* 递归论   
* 证明论   

用数学的方法研究数据推理

前提 结论 命题(是确定的，非真即假)


前提正确，结论正确。推理正确，有可推导关系。

数理逻辑
* 演绎逻辑，研究可推导关系
* 归纳逻辑，

命题包括
* 内容：决定命题的真或假
* 逻辑形式，简称形式。决定前提和结论之间的可推导性关系的是它们的逻辑形式

形式语言：人工构造的符号语言
＊　语义：符合和符号表达式的含义
＊　语法：符号表达式的形式结构

形式语言：对象语言

研究形式语言的语言，称为元语言

Leibniz

Frege:弗雷格(德语:Friedrich Ludwig Gottlob Frege，1848年11月8日-1925年7月26日)，德国数学家、逻辑学家和哲学家。他是数理逻辑和分析哲学的奠基人，代表作为《概念演算--一种按算术语言构成的思维符号语言》。

归纳定义和归纳证明

* R(0)基始
* R(n)归纳步骤
* R(n')归纳假设

串值归纳法

递归等义

经典命题逻辑(Classical propositional logic)


形式语言　自然语言

联结词，五个是常用的联接词 简单命题　复合命题

可兼容的或，不相容的或


在命题逻辑中，以简单命题作为基本单位，由简单命题出发，经过使用联结词，构成复合命题。

n元真假值函数


Lp，L代表语言，p代表proposition

命题符号，r，p，r

联结符号 五个

标点符号，两个左括号和右括号

表达式的相等　　表达式的并列

原子公式Atom(Lp)　公式Form(Lp)


逻辑推论和形式推演是不同的事情，前者属于语义，而后者属于语法。

范式是具有标准形式的公式。公式可以经过变换成为范式。析取范式，合取范式

[数理逻辑（Mathematical Logic）](https://yiqinnju.github.io/course/MathLogic/MathLogic.html)

[Insights into Mathematics](https://www.youtube.com/user/njwildberger)  -->A Grief history of Logic


逻辑学：研究“有效推理”和“证明的原则与标准”的一门学科

亚里士多德的三段论：大前提、小前提和结论

扬·卢卡西维茨： “波兰表示法”和“逆波兰表示法”

* 符号逻辑
* 语义＋语法

伽罗华：开创研究抽象的公理化代数系统的抽象代数

布尔：建立描述人类思维代数规律的布尔代数（1847-1854）

康托：建立集合论，可用于表达整个数学的形式语言（1872-1874）

弗雷格：严格建立第一个人工的形式语言概念文字（1879）

皮亚诺：建立算术的形式语言皮亚诺算术（1889）

策梅洛: 建立第一个公理化集合论策梅洛集合论（1908）


罗素：《数学原理》（1910-1913）表述所有数学真理在一组数理逻辑内的公理和推理规则下，原则上都是可以证明的

希尔伯特：《几何基础》，《数学基础》，建立几何和数学的形式语言

哥德尔：哥德尔不完备定理

邱奇：什么是可计算的：基于λ演算定义的可计算函数

图灵：可对输入进行运算的理论机器模型图灵机

命题逻辑

语法（Syntax）与语义（Semantics）是符号逻辑的两个基本要素


* 程序正确性证明：霍尔逻辑
* 可执行文件正确性验证：软件测试

两者直接的关系
* Soundness(可靠性)：程序执行正确--> 程序正确
* Completeness(完备性)：程序正确-->程序执行正确
* Compactness(紧致性）： 有限次执行 --> 程序执行全正确


字母表 ： PS
* 命题符
* 连接符
* 辅助符

命题符，　联结词，辅助符

命题

命题集

用Bacus-Naur Form定义

括号引理（Parenthesis Lemma）:结构归纳

构造序列

命题符对应于赋值，而命题对应于解释

联接词定义的布尔代数，联接词看作函数


命题与真值函数

析合范式 合析范式

逻辑等价

Semantic Consequence 语义推论

G推理系统，此系统最早是由逻辑学家Gentzen给出（Gentzen 1969），Gallier的符号

推理规则的可靠性（soundness）

推理规则的完全性（completeness）


In our attempt to falsify A, the tree is constructed in such a way that we are trying to find a valuation that makes every proposition occurring in the first component of a pair labeling a node true, and all propositions occurring in the second component of that pair false. Hence, we are naturally led to deal with pairs of finite sequences of propositions called sequents.

sequent， 前提（antecedent），结论（succedent）

deduction trees



Gentzen system G

inference rules:premises,conclusion

Falsifiable and Valid Sequents






Propositional logic

natural deduction

Rules for natural deduction
* The rules for conjunction
   * and-introduction
   * and-elimination
* The rules of double negation
   * double negation-introduction
   * double negative-elimination
* The rule for eliminating implication
   * modus ponens肯定前件式；假言推理, implies-elimination (sometimes also referred to as arrow-elimination)
   * modus tollens, or MT否定后件律
* The rule implies introduction
   * implies-introduction
* The rules for disjunction
   * or-introduction
   * or-elimination
* The rules for negation
   * bottom-elimination
   * not-elimination
   
   
Jean H. Gallier,  Logic For Computer Science: Foundations of Automatic Theorem Proving, Harper & Row, New York, 1986.

all propositions in PROP
* Associativity rules
* Commutativity rules:
* Distributivity rules:

BeiJing21