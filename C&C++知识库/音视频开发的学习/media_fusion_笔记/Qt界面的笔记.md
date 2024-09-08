# Qt界面开发的笔记

## 1. 遇到的问题

1. 在make的时候，遇见一个虚函数的问题，导致链接错误，具体的错误
```bash
Undefined symbols for architecture arm64:
  "vtable for main_window", referenced from:
      main_window::main_window() in libqt_interface.a[2](main_window.cc.o)
   NOTE: a missing vtable usually means the first non-inline virtual member function has no definition.
ld: symbol(s) not found for architecture arm64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make[2]: *** [bin/media_fusion_app] Error 1
make[1]: *** [bin/CMakeFiles/media_fusion_app.dir/all] Error 2
make: *** [all] Error 2
```
解决方法：在cmake当中添加关于qt moc的内容
```cmake
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
```