
Terms
* Graphics processing units (GPUs) 
* central processing unit (CPU)
* Compute Uniﬁed Device Architecture (CUDA)
* Message Passing Interface (MPI)
* high-performance computing (HPC)
* FLoating-point OPerations per Second (FLOPS) 


pixel-fragment processor

vertex processor


[CUDA C++ Programming Guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html)

[CUDA C++ Best Practices Guide](https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html)


[NVIDIA CUDA初级教程视频](https://www.iqiyi.com/v_19rrmjuw98.html)

[GPU Glossary](https://modal.com/gpu-glossary/readme)


[GPU 术语表](https://sodakeyeatsmush.notion.site/Smth-Smth-GPU-Related-27bf1129214e804ba217e8d5d08fc8b5)
[CMU 15-869Graphics and Imaging Architectures](https://www.cs.cmu.edu/afs/cs/academic/class/15869-f11/www/)

[NVIDIA Tesla: A Unified Graphics and Computing Architecture](https://www.cs.cmu.edu/afs/cs/academic/class/15869-f11/www/readings/lindholm08_tesla.pdf)


SIMD（Single Instruction Multiple Data）和 SIMT（Single Instruction Multiple Threads）
* 粒度差异：
  * SIMD以数据元素为单位，一条指令同时作用于多个数据元素。
  * SIMT以线程为单位，每个线程独立执行相同的指令，但可能处理不同的数据。
* 硬件实现：
  * SIMD通常由硬件的向量处理单元（例如SSE，AVX指令集）支持。
  * SIMT通常在GPU中实现，由硬件管理大量线程。
* 应用场景：
  * SIMD适用于数据级并行性较高的任务，如科学计算。
  * SIMT适用于大规模数据并行计算，尤其是在深度学习等领域



CPU
* 执行指令
* 处理数据

两个指标
* CPI(Clock cycles Per Instruction) 每条指令的时钟数
* 时钟周期

CPU和GPU
* CPU优化执行具有复杂控制和数据流机制的顺序任务
* GPU优先高吞吐的数据并行


指令级并行 ILP(instruction-level parallelism)

GPU用于并行地处理简单的数值计算任务。


GPU 性能指标
* 核心数
* GPU显存容量
* GPU计算峰值 每秒浮点数操作FLOPS(floating-point operation per second)
* 显存带宽

处理能力(processing power)

P = C * F * IPC 

C为时钟频率，IPC（Instrctions per cycle）为每个时钟周期能够执行的指令数，C为一个GPU中

GPU开发工具
* CUDA
* OpenCL
* OpenACC



* 指令流共享，多个程序片元共享指令流 Instruction stream sharing
* SIMD



算术逻辑单元(ALU, Arithmetic Logic Unit)


Nvidia
* Tesla：采用ECC内存(Error-correcting code momery)，科学计算
* Quadro：支持OpenGL(Open Graphics Library)渲染，专业绘图设计
* GeForce：游戏和娱乐
* Jetson：嵌入式

CPU和GPU各自都有DRAM(Dynamic random access memory),并且通过PCIe(Peripheral component interconnect express)总线连接

CPU称为Host,GPU称为Device,两者通过PCIe总线连接
* 驱动(driver)API
* 运行时(runtime)API

```shell
nvcc -V


nvidia-smi
nvidia-smi -h
nvidia-smi -q
nvidia-smi -q -i 0
nvidia-smi -q -i 0 -d MEMORY
nvidia-smi -i GPU_ID -c 0 # 默认模式
nvidia-smi -i GPU_ID -c 1 # 独占模式


sudo apt install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa-dev
```

smi(System Management Interface )


Perf列表示的是当前的GPU性能状态（Performance State），通常简写为"P-State"。P-State是一个数字，表示GPU的运行模式，其中较低的数字表示更高的性能状态，而较高的数字表示更低或节能的性能状态。

NVIDIA的GPU通常有多种P-States，从P0（最大性能）到P12（最小性能，最低功耗）


Persistence-M (Persistence Mode). persistence mode 持续模式默认关闭。persistence mode 能够让 GPU 更快响应任务，待机功耗增加。关闭 persistence mode 同样能够启动任务。

Disp.A: Display Active,表示GPUS是否初始化

Memory-Usage:显存使用率

Volatile GPU-UTil: GPU使用率

ECC:是否开启错误检查和纠错技术

Compute M:计算模式(compute mode)
* default：一个GPU许可存在多个计算进程
* E. Process (Exclusive process mode)：独占进程模式


\_\_global\_\_ 核函数(Kernel function)
* 限定词\_\_global\_\_ 修饰
* 返回值必须是void
* 只能访问GPU内存
* 不能使用变长参数
* 不能使用静态变量
* 不能使用指针函数
* 具有异步性
* 不支持C++的iostream

入口函数，定义了一个异步函数,表示这个函数在CPU中调用,并在GPU上并行执行


\_\_device\_\_ 函数是在GPU中调用,并在GPU上执行

\_\_host\_\_ 在CPU上调用和执行的函数

|    关键词    | 执行位置 | 调用位置 |
|:-------|-------:|:-------:|
| \_\_device\_\_ float deviceFunc() | device | device |
| \_\_global\_\_ void kernelFunc() | device | host |
| \_\_host\_\_ float hostFunc() | host | host |


线程模型
* grid 网格 
  * gridDim.x:2^31 -1
  * gridDim.y: 2^16 -1
  * gridDim.z: 2^16 -1
* block 线程块  :总的大小最大为1024
  * blockDim.x: 1024
  * blockDim.y: 1024
  * blockDim.z: 64



<<<grid_size, block_size>>>

线程分块是逻辑的划分,物理上线程不分块

gridDim.x: 为grid_size的值
blockDim.x: 为block_size的值

blockIdx.x:范围为0~gridDim.x

threadIdx.x:范围为0~blockDim.x

kernels是基于GPU的函数，由host（CPU）发起，并且在device（GPU）上运行。

The CUDA architecture is based on a scalable array of multithreaded Streaming Multiprocessors (SM). Each SM contains many CUDA cores.

Here is a high-level overview of the CUDA architecture:
* Host (CPU)
* Device (GPU): The graphics processor that executes the kernels.
* Global Memory
* Shared Memory
* Registers
* Streaming Multiprocessors (SMs)

每个流式多处理器包括
* CUDA Cores
* Warp Scheduler
* Instruction Cache
* Registration
* Shared Memory

Thread blocks and grids
1. Kernel Launch: When you launch a kernel, you define how many blocks there are in the grid and how many threads each block has.
2. Block Execution: Each block is performed individually, enabling scalable parallelism. Threads inside a block can interact and synchronize via shared memory and barrier synchronization.
3. Thread execution: Warps are formed by grouping threads within each block. Each warp performs the same command at the same time, which is required for optimal GPU efficiency.

 线程按照如下的层次进行组织
 * Threads
 * Blocks
 * Grids

一个warp包含32个并行thread，这些thread以不同数据资源执行相同的指令。
* 一个 Warp 由 32 个线程组成（对于大多数 NVIDIA 架构）。
* Warp 内的所有线程同步执行相同的指令（SIMT 模式）。
* Warp 是 GPU 执行的最小调度单位，GPU 不能单独调度一个线程，而是以 warp 为单位执行。
* 一个线程块（block）由多个 warp 组成，但 warp 内部线程的执行是同步的。


thread warp 线程束


warpSize大小为32

硬件的层次
* Core
* “32-core processing blocks”，曲速引擎(warp engine)
* symmetric multiprocessors or SMs.
* GPU

All threads in a warp execute the same instruction at the same time, therefore divergence (where threads in the same warp use separate execution pathways) can degrade performance.

Threads inside the same block can synchronize their execution by calling the '__syncthreads()' function.


An additional advantage of the GPU is that its internal memory is about 10 times faster than that of a typical PC, which is extremely helpful for problems limited by memory bandwidth rather than CPU power.

NVIDIA Software Development Kit (SDK)

CUDA

streaming processor (SP)

Streaming Multiprocessors (SMs)

streaming processor array (SPA)

raster operation processors (ROPs)

CUDA Memory Model
* Global memory
* Shared memory:Shared memory is fast on-chip memory that is shared by threads inside the same block.
* Local Memory:Accessible only to the thread that owns it.
* Constant memory: Constant memory is a read-only, cached memory region. It is optimized for scenarios in which all threads read the same data.


一个block内部的线程共享‘ Shared Memory’。可以同步‘_syncthreads()’

Kernel启动一个‘grid’，包含若干线程块。

线程和线程块具有唯一的标识。

There is a limit to the number of threads per block, since all threads of a block are expected to reside on the same streaming multiprocessor core and must share the limited memory resources of that core. On current GPUs, a thread block may contain up to 1024 threads.


* GPU Processing Cluster (GPC)
* Thread Block Clusters

The number of thread blocks in a cluster can be user-defined, and a maximum of 8 thread blocks in a cluster is supported as a portable cluster size in CUDA. 


```cpp
// Kernel definition
// Compile time cluster size 2 in X-dimension and 1 in Y and Z dimension
__global__ void __cluster_dims__(2, 1, 1) cluster_kernel(float *input, float* output)
{

}

int main()
{
    float *input, *output;
    // Kernel invocation with compile time cluster size
    dim3 threadsPerBlock(16, 16);
    dim3 numBlocks(N / threadsPerBlock.x, N / threadsPerBlock.y);

    // The grid dimension is not affected by cluster launch, and is still enumerated
    // using number of blocks.
    // The grid dimension must be a multiple of cluster size.
    cluster_kernel<<<numBlocks, threadsPerBlock>>>(input, output);
}
```

cudaOccupancyMaxPotentialClusterSize

```cpp
// Kernel definition
// No compile time attribute attached to the kernel
__global__ void cluster_kernel(float *input, float* output)
{

}

int main()
{
    float *input, *output;
    dim3 threadsPerBlock(16, 16);
    dim3 numBlocks(N / threadsPerBlock.x, N / threadsPerBlock.y);

    // Kernel invocation with runtime cluster size
    {
        cudaLaunchConfig_t config = {0};
        // The grid dimension is not affected by cluster launch, and is still enumerated
        // using number of blocks.
        // The grid dimension should be a multiple of cluster size.
        config.gridDim = numBlocks;
        config.blockDim = threadsPerBlock;

        cudaLaunchAttribute attribute[1];
        attribute[0].id = cudaLaunchAttributeClusterDimension;
        attribute[0].val.clusterDim.x = 2; // Cluster size in X-dimension
        attribute[0].val.clusterDim.y = 1;
        attribute[0].val.clusterDim.z = 1;
        config.attrs = attribute;
        config.numAttrs = 1;

        cudaLaunchKernelEx(&config, cluster_kernel, input, output);
    }
}
```

PTX(Parallel Thread Execution)

[vectorAdd CUDA sample](https://github.com/nvidia/cuda-samples)