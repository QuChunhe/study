
[Memory Models for C/C++ Programmers](https://arxiv.org/pdf/1803.04432.pdf)

[Linux Perf 性能分析工具及火焰图浅析](https://zhuanlan.zhihu.com/p/54276509)

[Profiling Software Using perf and Flame Graphs](https://www.percona.com/blog/2019/11/20/profiling-software-using-perf-and-flame-graphs/)


```
#include <stdio.h>
int main() {
   printf("Hello, World!");
   return 0;
}

$ gcc hello.c -o hello
$ strace ./hello
```

 Linux 执行系统调用的三种方法：
* 使用软件中断（Software interrupt）触发系统调用；
* 使用 SYSCALL / SYSENTER 等汇编指令触发系统调用；
* 使用虚拟动态共享对象（virtual dynamic shared object、vDSO）执行系统调用；
