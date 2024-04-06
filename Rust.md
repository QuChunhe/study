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


Rust libraries are called crates, and they are expected to use semantic version numbers in the form major.minor.patch


clap (command-line argument parser) crate