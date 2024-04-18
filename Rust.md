[快速配置 Rust 开发环](https://www.rust-lang.org/zh-CN/learn/get-started)

```shell
sudo apt install rust-src rustc


sudo rustup component add rust-src
# sudo rustup component add rust-docs
```


```shell
rustc hello.rs

cargo new hello
cargo run

cargo run
cargo help command

cargo run --quiet --bin true

cargo test -- --test-threads=1
```

https://zhuanlan.zhihu.com/p/218098514


https://rustwiki.org/zh-CN/rust-by-example/attribute/crate.html

Rust libraries are called crates, and they are expected to use semantic version numbers in the form major.minor.patch


clap (command-line argument parser) crate


shadowed and overwritten

In Rust jargon, such an abort operation is named panic, and the action of aborting the current thread is named panicking.


[Rust Cargo使用指南 | 第十七篇 | 构建脚本 build.rs](https://zhuanlan.zhihu.com/p/477949743)


Sizedness。确定大小类型(sized type)可以通过传值(by value)或者传引用(by reference)的方式来传递。如果一个类型的大小不能在编译期确定，那么它就被称为不确定大小类型(unsized type)或者DST，即动态大小类型(Dynamically-Sized Type)。因为不确定大小类型(unsized type)不能存放在栈上，所以它们只能通过传引用(by reference)的方式来传递。
[Rust中的Sizeness](https://mp.weixin.qq.com/s/5eRaXMewRqdyrnwhYU3HIg)

```shell
cargo install flamegraph

cargo flamegraph --bin tectonic -- texfile.tex
```