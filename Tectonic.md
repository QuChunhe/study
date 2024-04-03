
```
git clone --recursive 
git submodule update --init



```

windows
```
set TECTONIC_DEP_BACKEND vcpkg
set RUSTFLAGS "-Ctarget-feature=+crt-static"
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