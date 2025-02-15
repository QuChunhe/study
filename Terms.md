

# Time

Coordinated Universal Time (UTC)

Greenwich Mean TIM (GMT)

Internaltional Atomic Time (TAI)

UTC is TAI with corrections to account for Earch rotation.

Time zones and daylight saving time are offsets to UTC.

Two most common representationi
* Unix time
* ISO 8601: 2020-11-09T09:05:00+08:00

leap second: A leap second is a second added to Coordinated Universal Time (UTC) in order to keep it synchronized with astronomical time. 

闰秒，是指为保持协调世界时接近于世界时时刻，由国际计量局统一规定在年底或年中（也可能在季末）对协调世界时增加或减少1秒的调整。由于地球自转的不均匀性和长期变慢性（主要由潮汐摩擦引起的），会使世界时（民用时）和原子时之间相差超过到±0.9秒时，就把协调世界时向前拨1秒（负闰秒，最后一分钟为59秒）或向后拨1秒（正闰秒，最后一分钟为61秒）； 闰秒一般加在公历年末或公历六月末。

# Code

ASCII(American Standard Code for Information Interchange)

UNIVERSAL CHARACTER SET (UCS) - 

Universal Multiple-Octet Coded Character Set 通用多八位编码字符集

Unicode 只是一个符号集，它只规定了符号的二进制代码，却没有规定这个二进制代码应该如何存储.

UTF-8、UTF-16、UTF-32 中的 "UTF" 是 "Unicode Transformation Format" 的缩写，意思是"Unicode 转换格式"，后面的数 字表明至少使用多少个比特位来存储字符, 比如：UTF-8 最少需要8个比特位也就是一个字节来存储

Little endian 和 Big endian

bps（bit per second），也就是bit/s

“KBps”（ 千 字 节/ 秒）  或“MBps” （ 兆 字 节/ 秒） 

重载 (overload)覆盖 (override)

*[Write Amplification](https://en.wikipedia.org/wiki/Write_amplification) -

[Object-Oriented Programming vs. Procedural Programming](https://study.com/academy/lesson/object-oriented-programming-vs-procedural-programming.html)   
Programming Paradigms: fundamentally different approaches to building solutions to specific types of problems

* Procedural Programming: list of instrunctions to tell the computer what to do step by step.
   * procedures
   * routines
   * sub-routines   
 imperative programming
* Object-oriented programming：approach to problem solving where all computations are carried out using objects.
   * Object： component of a program that knows how to perform certain actions and how to ineract with other elements of the program. property and method
   * Class   
   OOP的核心特性
   * Abstraction
   * Encapsulation
   * Inheritance
   * Polymorphism
   
   
* Functional Programming


Object-oriented  programming
* Object-oriented programming collects information into single entities called objects.
* Each object is a single instance of a class.
* Abstraction hides the inner workings of an object when it’s not necessary to see them.
* Encapsulation stores related variables and methods within objects and protects them.
* Inheritance allows sub-classes to use attributes from parent classes.
* Polymorphism allows objects and methods to deal with multiple different situations with a single interface

命令式编程
* 命令式编程（Imperative programming）：详细的命令机器怎么（How）去处理一件事情以达到你想要的结果（What）；
* 声明式编程（ Declarative programming）：只告诉你想要的结果（What），机器自己摸索过程（How）


* commodity hardware 商品化硬件
* 定制化硬件


 multi-tier architecture 多级架构
 
  multi-layer architecture　多层架构

认证 (authentication) 和授权 (authorization)

第一性原理（First principle thinking）
第一性原理指的是，回归事物最基本的条件，将其拆分成各要素进行解构分析，从而找到实现目标最优路径的方法。
该原理源于古希腊哲学家亚里士多德提出的一个哲学观点：“每个系统中存在一个最基本的命题，它不能被违背或删除。” 

Bayes’ rule or the Bayes–Price–Laplace rule
>>‘causes and effects are discoverable, not by reason, but by
>>experience’


* 本地化：Localization，通常缩写为“L10N”。将产品或软件针对特定国际语言和文化进行加工，使之符合特定区域市场的过程。真正的本地化要考虑目标区域市场的语言、文化、习俗、特征和标准。通常包括改变软件的书写系统（输入法）、键盘使用、字体、日期、时间和货币格式等。
* 国际化：Internationalization，通常缩写为“I18N”。使产品或软件具有不同国际市场的普遍适应性，从而无需重新设计就可适应多种语言和文化习俗的过程。真正的国际化要在软件设计和文档开发过程中，使产品或软件的功能和代码设计能处理多种语言和文化习俗，具有良好的本地化能力。
* 全球化：Globalization，通常缩写为“G11N”。使产品或软件进入全球市场而进行的有关的商务活动。包括正确的国际化设计，本地化集成，以及在全球市场进行的市场推广、销售和支持的全部过程。


一、首先从数据多语上分析设计：目前将数据分为四类：基础数据、业务数据、提示数据、日志数据。

* 数据格式：国家、地区、时间、地址、货币
* 多币种：公司本位币、集团本位币、全球统一币种
* 多时区：UTC、多时区协同应用、多时区业务处理
* 多会计制度：多账簿机制、支持中国、GAAP多会计制度
* 多支持本地化：分层设计机制：客户级、伙伴级、行业级、本地化级、领域级




Headroom is available usable resources. 余量可剩余可用的资源。
* Total Capacity minus Peak Utilization and Margin

Utilization
* Utilization is the proportion of busy time
* Always defined over a time interval

# 时间

https://www.huxiu.com/article/2744458.html


State 和 Status 的核心区别，就是它们的枚举值之间是否有依赖关系，没有依赖关系的用 State，有依赖关系的用 Status。

区分点就在于一个房间当用State 描述时，它是个彼此独立的枚举值，可以没有前后顺序的在婚房、普通房、豪华总统房之间来回转换。而当使用 Status 时，是存在前后状态依赖关系的一个变化量，不能没有做设计就施工，也不能没施工就验收。

“state”通常指的是系统或程序在某一特定时刻的内部状态。这个状态包括了程序运行时的所有变量值、内存使用情况、文件状态等。它是一个更为宽泛且深入的概念，用于描述系统或程序在整体上或某个具体功能点上的当前状况。例如，在一个用户登录的系统中，“state”可能指的是用户当前是否已登录、用户的权限级别等。此外，“state”还常用于描述对象的状态，如一个对象可能处于“可用”或“不可用”的状态。

而“status”则更侧重于描述某个操作、请求或事件的结果或状态。它通常是一个更为具体的、用于表示某个特定操作是否成功、失败或处于其他某种特定状态的标识。例如，在网络通信中，一个HTTP请求可能返回一个状态码（status code），如200表示成功，404表示未找到资源。在这个语境下，“status”提供了一个关于请求结果的明确信息。



>> ! 叹号 exclamation mark/bang  /ˌekskləˈmeɪʃn mɑːk/
>>  ? 问号 question mark
>>  , 逗号 comma英 /ˈkɒmə/ 美 /ˈkɑːmə/ 
        . 点号 dot/period/point
        : 冒号 colon英 /ˈkəʊlən; ˈkəʊlɒn/
        ; 分号 semicolon 英 /ˌsemiˈkəʊlən; ˌsemiˈkəʊlɒn/
        ” 双引号 quotation marks/double quote 英 /kwəʊˈteɪʃn mɑːks/ 
        ‘ 单引号/撇号 apostrophe/single quote 英 /əˈpɒstrəfi/
        ` 重音号 backquote/grave accent美 /ɡreɪv ˈæksent/
        * 星号 asterisk/star英 /ˈæstərɪsk/ 
        + 加号 plus sign
        - 减号/横线 hyphen/dash/minus sign/ 英 /ˈhaɪfn/
        = 等号 equal sign
        / 斜线 slash
        \ 反斜线 backslash/escape英 /ɪˈskeɪp/
        | 竖线 bar/pipe/vertical bar
        _ 下划线 underline/underscore
        $ 美元符号 dollar sign
        @ at at sign
        # 井号 crosshatch/sharp/hash
        % 百分号 percent sign/mod英 /mɒd/ 
        & and/和/兼 and/ampersand英 /ˈæmpəsænd/ 
        ^ 折音号 circumflex/caret 英 /ˈsɜːkəmfleks/  英 /ˈkærət/
        ~ 波浪号 tilde 英 /ˈtɪldə/ 
        {} （左右）花括号/大括号 (left/right|open/close) braces英 /ˈbreɪsɪz/
        [] （左右）方括号/中括号 (left/right|open/close) brackets 美 /ˈbrækɪts/ 
        () （左右）圆括号/小括号 (left/right|open/close) parentheses英 /pəˈrenθəsiːz/
        <> 尖括号 angle brackets
        < 大于号 less than
        > 小于号 greater than

# 杂项

所谓“黑天鹅”和“黑水母”都是情景规划（Scenario Planning）的模型。“情景规划”是美国未来学家赫尔曼·卡恩（Herman Kahn）在上世纪四五十年代开创的一种战略管理和决策分析方法，通过构建多个可能的未来情境，帮助组织或企业在不确定的环境中制定更具弹性的策略。1970年代，蚬壳（Shell）公司进一步完善情景规划的企业战略应用，预测了1973年石油危机，使它比竞争对手更好地适应市场变化。这一成功使蚬壳声名大噪，成为情景规划的领跑者，也促使情景规划在商业战略中被广泛采用。

简单地说，“黑天鹅事件”指极不可能发生，但一旦发生会带来巨大影响的事件，通常难以预测（如2008年金融危机）；“灰犀牛事件”指大概率会发生、影响深远但因被长期忽视而最终爆发的风险（如2024年网络安全公司CrowdStrike软件更新引发全球大范围宕机）；“黑水母事件”指长期存在、影响范围广泛，但因其分散性和缓慢性而难以察觉的系统性风险（如冠病疫情和迟早将暴发的另一场“大流行病”）