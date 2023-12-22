

CPU
* 执行指令
* 处理数据

两个指标
* CPI(Clock cycles Per Instruction) 每条指令的时钟数
* 时钟周期


指令级并行 ILP(instruction-level parallelism)

GPU 性能指标
* 核心数
* GPU显存容量
* GPU计算峰值
* 显存带宽

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
```

smi(System Management Interface )


Perf列表示的是当前的GPU性能状态（Performance State），通常简写为"P-State"。P-State是一个数字，表示GPU的运行模式，其中较低的数字表示更高的性能状态，而较高的数字表示更低或节能的性能状态。

NVIDIA的GPU通常有多种P-States，从P0（最大性能）到P12（最小性能，最低功耗）


Persistence-M (Persistence Mode). persistence mode 持续模式默认关闭。persistence mode 能够让 GPU 更快响应任务，待机功耗增加。关闭 persistence mode 同样能够启动任务。

Disp.A: Display Active,表示GPUS是否初始化

Memory-Usage:显存使用率

Volatile GPU-UTil: GPU使用率

ECC:是否开启错误检查和纠错技术

Compute M:计算模式


__global__ 核函数(Kernel function)
* 限定词__global__ 修饰
* 返回值必须是void
* 只能访问GPU内存
* 不能使用变长参数
* 不能使用静态变量
* 不能使用指针函数
* 具有异步性
* 不支持C++的iostream

定义了一个异步函数,表示这个函数在CPU中调用,并在GPU上并行执行


__device__ 函数是在GPU中调用,并在GPU上执行

__host__ 在CPU上调用和执行的函数