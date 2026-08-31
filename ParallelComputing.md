https://hpc.llnl.gov/documentation/tutorials/introduction-parallel-computing-tutorial


```shell
sudo apt update
sudo apt upgrade
sudo apt install build-essential

sudo apt install openmpi-bin libopenmpi-dev

which mpirun
```


[](https://www.cs.cmu.edu/~guyb/paralg/paralg/parallel.pdf)

评估并行算法的三个指标
* Work：工作量/计算总量，通常记为$T_1$
* Span: 深度/关键路径长度，通常记为$T_{\infty}$
* Parallelism: 并行度，$T_1/T_\infty$

Brent 定理（Brent’s Theorem，由 Richard Brent 在 1974 年提出）
$\frac{T_1}{p} \le T_{p} \le \frac{T_1}{p} + T_\infty$


《Structured Parallel Programming Patterns for Efficient Computation》

算法的基础部分
* tasks
* data


策略
* data parallelism： 对于可扩展并行性，最好的综合策略
* functional decomposition

the degree of regularity in the dependencies between tasks
* Regular parallelism: The tasks are similar and have predictable dependencies.
* Irregular parallelism

Branch and bound optimizations on this tree 

机制
* thread parallelism： Hardware thread and Software thread
* vector parallelism：vector instructions

vectorization



Instruction Parallelism
* superscalar
* hardware multithreading
* vector instructions 
    * Streaming SIMD Extension (SSE)
    * Advanced Vector Extensions (AVX)