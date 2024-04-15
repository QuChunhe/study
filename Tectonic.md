

更改代码集成方案
* 采用JNI，速度最快，问题集成麻烦
* 采用服务，耦合性地，文件数据通过网卡链路，比较慢
* 采用文件，以命令方式调用，并将输入文件和结果文件都在本地文件中

两种数据
* 元数据：外接矩形大小
* pdf数据：

# 代码

```
git clone --recursive 
git submodule update --init



```

windows
```
set TECTONIC_DEP_BACKEND vcpkg
set RUSTFLAGS "-Ctarget-feature=+crt-static"


sudo apt-get install libfontconfig1-dev libgraphite2-dev libharfbuzz-dev libicu-dev libssl-dev zlib1g-dev

cargo build --release
```

'''
set TECTONIC_DEP_BACKEND=pkg-config
set RUSTFLAGS=-Ctarget-feature=+crt-static
cargo build --release
'''

https://blog.csdn.net/qq_42679415/article/details/122510120

```

git pull origin master

.\bootstrap-vcpkg.bat

.\vcpkg update
.\vcpkg upgrade
.\vcpkg upgrade --no-dry-run



vcpkg install fontconfig freetype "harfbuzz[graphite2]" icu --triplet=x64-windows
```


https://zhuanlan.zhihu.com/p/649819420

https://blog.csdn.net/m0_63230155/article/details/132216971

https://packages.msys2.org/search