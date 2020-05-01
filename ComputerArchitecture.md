
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
