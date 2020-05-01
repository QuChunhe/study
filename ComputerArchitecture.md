
“Power Wall + Memory Wall + ILP Wall = Brick Wall”
* The Power Wall means faster computers get really hot.
* The Memory Wall means 1000 pins on a CPU package is way too many.
* ILP Wall means a deeper instruction pipeline really means digging a deeper power hole. (ILP stands for instruction level parallelism.)

[The future of computers – Part 1: Multicore and the Memory Wall](https://www.edn.com/the-future-of-computers-part-1-multicore-and-the-memory-wall/)

[The future of computers - Part 2: The Power Wall](https://www.edn.com/future-of-computers-part-2-the-power-wall/)

[The future of computing - Part 3: The ILP Wall and pipelines](https://www.edn.com/future-of-computing-part-3-the-ilp-wall-and-pipelines/)

四十年来CPU发展的推动力
* 半导体工艺：更高的频率、更多的晶体管
* 体系结构

摩尔定律
* 集成电路芯片上所集成的电路的数目，每隔18个月就翻一番；
* 微处理器的性能每隔18个月提高一倍，而价格下降一半

摩尔定律说的是半导体工艺的发展，其本质上是在技术可能性的前提下实现商业利益的最大化
* 技术的可能性
* 商业利益的最大化

* 周期间隔太小，厂家收不回成本
* 周期间隔太大，面对更多竞争以及更少的需求，也会造成利润下降

相对固定的周期，有利于上下游厂商的协同
* 为更快的CPU，设计开发操作系统和系统软件
* 根据摩尔周期清理库存，避免压货

[什么是CPU Die](https://zhuanlan.zhihu.com/p/51354994)   

Die或者CPU Die指的是处理器在生产过程中，从晶圆（Silicon Wafer）上切割下来的一个个小方块（这也是为啥消费者看到的CPU芯片为什么都是方的的原因），在切割下来之前，每个小方块（Die）都需要经过各种加工，将电路逻辑刻到该Die上面.

对于主流的CPU厂商Intel和AMD而言，他们会将1个或者N个CPU Die封装起来形成一个CPU Package，有时候也叫作CPU Socket.

而对于AMD的EYPC CPU而言，它的每个CPU Socket由4个CPU Die组成，每个CPU Die中包含有4个CPU内核

CPU Die之间通过片外总线（Infinity Fabric）互联，并且不同CPU Die上的CPU内核不能共享CPU缓存，而单个Die的Xeon处理器内和所有CPU内核其实是可以共享CPU的第三级缓存（L3 Cache）的。

CPU Socket(NUMA Node)--> CPU Die --> CPU Core (Physic CPU)--> HyperThread (logic CPU)

* socket ⇄ node

socket是一个物理上的概念，指的是主板上的cpu插槽。node是一个逻辑上的概念，对应于socket。

* core ⇄ 物理cpu

core就是一个物理cpu,一个独立的硬件执行单元

* thread ⇄ 逻辑cpu

socket就是主板上的CPU插槽; Core就是socket里独立的一组程序执行的硬件单元，比如寄存器，计算单元等; Thread：就是超线程hyperthread的概念，逻辑的执行单元，独立的执行上下文，但是共享core内的寄存器和计算单元。

# Memory

[Memory Hierarchy Design – Part 1. Basics of Memory Hierarchie](https://www.edn.com/memory-hierarchy-design-part-1-basics-of-memory-hierarchies/)

[ Memory Hierarchy Design – Part 2. Ten advanced optimizations of cache performance](https://www.edn.com/memory-hierarchy-design-part-2-ten-advanced-optimizations-of-cache-performance/)

[Memory Hierarchy Design – Part 3. Memory technology and optimizations](https://www.edn.com/memory-hierarchy-design-part-3-memory-technology-and-optimizations/)

[Memory Hierarchy Design – Part 4. Virtual memory and virtual machines](https://www.edn.com/memory-hierarchy-design-part-4-virtual-memory-and-virtual-machines/)

[Memory Hierarchy Design – Part 5. Crosscutting issues and the memory design of the ARM Cortex-A8](https://www.edn.com/memory-hierarchy-design-part-5-crosscutting-issues-and-the-memory-design-of-the-arm-cortex-a8/)

[Memory Hierarchy Design – Part 6. The Intel Core i7, fallacies, and pitfalls](https://www.edn.com/memory-hierarchy-design-part-6-the-intel-core-i7-fallacies-and-pitfalls/)



[What Every Programmer Should Know About Memory](https://people.freebsd.org/~lstewart/articles/cpumemory.pdf)



[Modern Microprocessors:A 90-Minute Guide!](http://www.lighterra.com/papers/modernmicroprocessors/)

关键技术
* pipelining (superscalar, OOO, VLIW, branch prediction, predication)
* multi-core and simultaneous multi-threading (SMT, hyper-threading)
* SIMD vector instructions (MMX/SSE/AVX, AltiVec, NEON)
* caches and the memory hierarchy

**Pipelining & Instruction-Level Parallelism**
* Fetch
* Decode
* Execute
* Writeback
Modern processors overlap these stages in a pipeline, like an assembly line. 

D**eeper Pipelines – Superpipelining**

Since the clock speed is limited by (among other things) the length of the longest, slowest stage in the pipeline, the logic gates that make up each stage can be subdivided, especially the longer ones, converting the pipeline into a deeper super-pipeline with a larger number of shorter stages. Then the whole processor can be run at a higher clock speed! Of course, each instruction will now take more cycles to complete (latency), but the processor will still be completing 1 instruction per cycle (throughput), and there will be more cycles per second, so the processor will complete more instructions per second (actual performance).




**Multiple Issue – Superscalar(超标量)**

Since the execute stage of the pipeline is really a bunch of different functional units, each doing its own task, it seems tempting to try to execute multiple instructions in parallel, each in its own functional unit. To do this, the fetch and decode/dispatch stages must be enhanced so they can decode multiple instructions in parallel and send them out to the "execution resources".

The number of instructions able to be issued, executed or completed per cycle is called a processor's width.

**Explicit Parallelism – VLIW(very long instruction word)**


**Instruction Dependencies & Latencies**


**Branches & Branch Prediction**

**Eliminating Branches with Predication**

**Instruction Scheduling, Register Renaming & OOO(out-of-order execution)**

The instructions in the program must be reordered so that while one instruction is waiting, other instructions can execute. Not surprisingly, this is called out-of-order execution, or just OOO for short (sometimes written OoO or OOE).


Another approach to the whole problem is to have the compiler optimize the code by rearranging the instructions. This is called static, or compile-time, instruction scheduling. The rearranged instruction stream can then be fed to a processor with simpler in-order multiple-issue logic, relying on the compiler to "spoon feed" the processor with the best instruction stream. 

A question that must be asked is whether the costly out-of-order logic is really warranted, or whether compilers can do the task of instruction scheduling well enough without it. This is historically called the brainiac vs speed-demon debate. 

**The Power Wall & The ILP Wall**

功耗和散热问题(power and heat issures)限制了时钟频率。And while power increases linearly with clock frequency, it increases as the square of voltage, making for a kind of "triple whammy" at very high clock speeds (f*V*V).

It gets even worse, because in addition to the normal switching power, there is also a small amount of leakage power, since even when a transistor is off, the current flowing through it isn't completely reduced to zero. And just like the good, useful current, this leakage current also goes up as the voltage is increased. If that wasn't bad enough, leakage generally goes up as the temperature increases as well, due to the increased movement of the hotter, more energetic electrons within the silicon.


The power and heat problems become unmanageable, because it's simply not possible to provide that much power and cooling to a silicon chip in any practical fashion, even if the circuits could, in fact, operate at higher clock speeds. This is called the power wall.

Pursuing more and more ILP also has definite limits, because unfortunately, normal programs just don't have a lot of fine-grained parallelism in them, due to a combination of load latencies, cache misses, branches and dependencies between instructions. This limit of available instruction-level parallelism is called the ILP wall.
* 通常的程序没有很多细粒度的并行性
* 读取（内存）的时延。CPU和内存的速度失配。
* ache未命中
* 指令的分支和依赖


**Threads – SMT(Simultaneous multi-threading), Hyper-Threading & Multi-Core**

Simultaneous multi-threading (SMT) is a processor design technique which exploits exactly this type of thread-level parallelism.

在Intel　CPU中被成为超线程(hyper-threading)

**More Cores or Wider Cores?**

 One key problem is that the complex multiple-issue dispatch logic scales up as roughly the square of the issue width, because all n candidate instructions need to be compared against every other candidate.8-issue more than 4 times larger than 4-issue (for only 2 times the width).In addition, a very wide superscalar design requires highly multi-ported register files and caches, to service all those simultaneous accesses. Both of these factors conspire to not only increase size, but also to massively increase the amount of longer-distance wiring at the circuit-design level, placing serious limits on the clock speed. 


**Data Parallelism – SIMD Vector Instructions**

In addition to instruction-level parallelism and thread-level parallelism, there is yet another source of parallelism in many programs – data parallelism. Rather than looking for ways to execute groups of instructions in parallel, the idea is to look for ways to make one instruction apply to a group of data values in parallel.

This is sometimes called SIMD parallelism (single instruction, multiple data). More often, it's called vector processing. Supercomputers used to use vector processing a lot, with very long vectors, because the types of scientific programs which are run on supercomputers are quite amenable to vector processing.

[Gallery of Processor Cache Effects](http://igoro.com/archive/gallery-of-processor-cache-effects/)

# Intel
The processor uses three interdependent mechanisms for carrying out locked atomic operations:
* Guaranteed atomic operations
* Bus locking, using the LOCK# signal and the LOCK instruction prefix
* Cache coherency protocols that ensure that atomic operations can be carried out
on cached data structures (cache lock)
These mechanisms are interdependent in the following ways. Certain basic memory transactions (such as reading or writing a byte in system memory) are always guaranteed to be handled atomically. That is, once started, the processor guarantees that the operation will be completed before another processor or bus agent is allowed access to the memory location. The processor also supports bus locking for performing selected memory operations (such as a read-modify-write operation in a shared area of memory) that typically need to be handled atomically, but are not automatically handled this way. Because frequently used memory locations are often cached in a processor’s L1 or L2 caches, atomic operations can often be carried out inside a processor’s caches without asserting the bus lock. Here the processor’s cache coherency protocols ensure that other processors that are caching the same memory locations are managed properly while atomic operations are performed on cached memory locations.
<<Intel 64 and IA-32 Architectures Software Developer’s Manual Volume 3 (3A, 3B & 3C): System Programming Guide>> Chater 8 Mutiple-Processor Managment






#ARM

[ARM Manul](http://infocenter.arm.com/help/index.jsp?topic=/com.arm.doc.ddi0198e/Cacghbij.html)
