
[Memory Models for C/C++ Programmers](https://arxiv.org/pdf/1803.04432.pdf)

[Linux Perf 性能分析工具及火焰图浅析](https://zhuanlan.zhihu.com/p/54276509)

[Profiling Software Using perf and Flame Graphs](https://www.percona.com/blog/2019/11/20/profiling-software-using-perf-and-flame-graphs/)

掌握如下三个方面就应对95%的C/C++实际编程问题
* 高效的文件读写
  * 机械硬盘
  * 固态硬盘
* 高效的网络操作
  * 服务端
  * 客户端
* 高效的并发处理
  * 锁的使用
  * 并发数据结构
  * 并发编程模式

[李浩: 再谈 volatile 关键字](https://blog.csdn.net/21cnbao/article/details/114362308?spm=1001.2014.3001.5501)



C -std
* ANSI C Standard (referred to as ANSI C and C89)
* C90 (official name: ISO/IEC 9899:1990; it is the ANSI C Standard adopted by ISO; the C89 and C90 are the same things)
* C99 (ISO/IEC 9899:1999)
* C11 (ISO/IEC 9899:2011)
* C17 (ISO/IEC 9899:2018)
* The upcoming standard informally named C2x


# GCC

GCC（英文全拼：GNU Compiler Collection）

```
gcc [options] file...
```

选项：
* -pass-exit-codes ：从一个阶段以最高错误代码退出。
* --target-help ：显示特定于目标的命令行选项。
* --help={common|optimizers|params|target|warnings|[^]{joined|separate|undocumented}}[,...] ：显示特定类型的命令行选项（使用 -v --help 显示子进程的命令行选项）。
* -dumpspecs ：显示所有内置规范字符串。
* -dumpversion ：显示编译器的版本。
* -dumpmachine ：显示编译器的目标处理器。
* -print-search-dirs ：显示编译器搜索路径中的目录。
* -print-libgcc-file-name ：显示编译器配套库的名称。
* -print-file-name=<lib> ：显示库 <lib> 的完整路径。
* -print-prog-name=<prog> ：显示编译器组件 <prog> 的完整路径。
* -print-multiarch ：显示目标的规范化 GNU 三元组，用作库路径中的一个组件。
* -print-multi-directory ：显示 libgcc 版本的根目录。
* -print-multi-lib ：显示命令行选项和多个库搜索目录之间的映射。
* -print-multi-os-directory ：显示操作系统库的相对路径。
* -print-sysroot ：显示目标库目录。
* -print-sysroot-headers-suffix ：显示用于查找标题的 sysroot 后缀。
* -Wa,<options> ：将逗号分隔的 <options> 传递给汇编器（assembler）。
* -Wp,<options> ：将逗号分隔的 <options> 传递给预处理器（preprocessor）。
-Wl,<options> ：将逗号分隔的 <options> 传递给链接器（linker）。
-Xassembler <arg> ：将 <arg> 传递给汇编器（assembler）。
-Xpreprocessor <arg> ：将 <arg> 传递给预处理器（preprocessor）。
-Xlinker <arg> ：将 <arg> 传递给链接器（linker）。
-save-temps ：不用删除中间文件。
-save-temps=<arg> ：不用删除指定的中间文件。
-no-canonical-prefixes ：在构建其他 gcc 组件的相对前缀时，不要规范化路径。
-pipe ：使用管道而不是中间文件。
-time ：为每个子流程的执行计时。
-specs=<file> ：使用 <file> 的内容覆盖内置规范。
-std=<standard> ：假设输入源为 <standard>。
--sysroot=<directory> ：使用 <directory> 作为头文件和库的根目录。
-B <directory> ：将 <directory> 添加到编译器的搜索路径。
-v ：显示编译器调用的程序。
-### ：与 -v 类似，但引用的选项和命令不执行。
-E ：仅执行预处理（不要编译、汇编或链接）。
-S ：只编译（不汇编或链接）。
-c ：编译和汇编，但不链接。
-o <file> ：指定输出文件。
-pie ：创建一个动态链接、位置无关的可执行文件。
-I ：指定头文件的包含路径。
-L ：指定链接库的包含路径。
-shared ：创建共享库/动态库。
-static ：使用静态链接。
--help ：显示帮助信息。
--version ：显示编译器版本信息。



```
c99 -Wall -o getting-started getting-started.c -lm
```




 


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


 Michael J. Donahoo and Kenneth L. Calvertm, TCP/IP Sockets in C: Practical Guide for Programmers, 2nd Edition, Morgan Kaufmann, 2009 [source code](http://cs.ecs.baylor.edu/~donahoo/practical/CSockets2/textcode.html)



# C

declarations, definitions, and statements.

All identifiers in a program have to be declared.

keywords are predefined by the language and must not be declared or redefined.

```shell
apropos printf
man printf
man 3 printf
```


```c
int main(int argc, char *argv[])
```
argc表示参数个数（argument count），而argc表示参数向量（argument vector）.

第一个参数argc是传递的参数数量加1，包括了执行程序的名字。因此，args总是大于0，而argv[0]是正在持续程序的名字（包括了路径）




操作符的优先级
> ++ -- postfix increment and decrement
> () function call operator
> [] array subscript
> . structure member access
> -> structure member access through a pointer
> ++ -- prefix increment and decrement
> + - unary plus and minus
> ! logical NOT
> (type_name) cast operator
> * dereference operator
> & address-of
> * / % multiplication, division, and remainder
> + - addition and subtraction
> << >> bitwise left shift and right shift
> < <= relational operators
> >= relational operators
> == != equality operators
> && logical AND
> || logical OR
> ?: ternary conditional operator
> = assignment operator
> += -= compound assignments


&和*
* definition：用于定义数据类型
  * 指针: *
  * 引用: & 
* operator：用于运算符
  * 取值(解引用): *，当变量所代表内存空间存储的是一个内存地址时，通过取值符获得这个内存地址所存储的值。
  * 取址: &，当变量代表一个变量时，通过取址符获得这个变量数据所在的内存地址。

[var arg](https://www.tutorialspoint.com/c_standard_library/c_macro_va_arg.htm)

```c
#include <stdarg.h>

va_list arg_ptr;

type va_arg(
   va_list arg_ptr,
   type 
);
void va_end(
   va_list arg_ptr 
);
void va_start(
   va_list arg_ptr,
   prev_param 
);
```

>va_list  建参数列表
>va_start(ap, num_args) 初始化列表为传入的可变长参数
>va_arg(ap, int) 依次读取参数列表中的参数。ap指参数列表，type指转换类型
>va_end(ap) 放参数列表。


But the pointer of type void* can point to any type. All pointer types are implicitly convertible to type void*. The void* type is also called a pointer to void or a generic pointer type.

When a pointer has a value of NULL, it does not point to any other object.

The p[i] expression is equivalent to *(p+i). Using a subscript operator with an index on a pointer as in p[i] means increment a pointer by i places and dereference it.


 # Courses

 [南科大课堂原版 - C/C++：从基础语法到优化策略（2021年秋季版本）](https://www.bilibili.com/video/BV1Vf4y1P7pq?p=1)

 https://github.com/ShiqiYu/CPP



[黑马程序员-Linux系统编程](https://www.bilibili.com/video/BV1KE411q7ee?p=1)

[Linux系统编程（李慧琴）](https://www.bilibili.com/video/BV1yJ411S7r6?from=search&seid=13482678134358786324&spm_id_from=333.337.0.0)