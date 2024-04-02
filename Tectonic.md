
```
git submodule update --init



```

windows
```
set TECTONIC_DEP_BACKEND vcpkg
set RUSTFLAGS "-Ctarget-feature=+crt-static"
cargo build --release
```

'''
set TECTONIC_DEP_BACKEND=vcpkg
set RUSTFLAGS=-Ctarget-feature=+crt-static
cargo build --release
'''