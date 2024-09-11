### add_subdirectory 命令
- **作用**：将子目录添加到CMake项目中，执行子目录中的CMakeLists.txt文件。
- **语法**：`add_subdirectory(<source_dir> [binary_dir] [EXCLUDE_FROM_ALL])`
  - `source_dir`：子目录的路径，必须包含CMakeLists.txt文件。
  - `binary_dir`（可选）：指定生成的目标文件的输出目录。
  - `EXCLUDE_FROM_ALL`：表示该目录从默认构建中排除。

#### 作用域规则
- 子目录的作用域是独立的，对变量的修改不会影响到父作用域。
- 子目录可以访问父作用域中的变量，但修改的变量只在子作用域中有效。

### include 命令
- **作用**：在CMake脚本中包含其他CMake脚本。
- **语法**：`include(<file|module> [OPTIONAL] [RESULT_VARIABLE <var>] [NO_POLICY_SCOPE])`
  - `file`：CMake脚本文件。
  - `module`：CMake模块文件。
  - `OPTIONAL`：文件不存在时不报错。
  - `RESULT_VARIABLE`：将包含结果存储在指定变量中。
  - `NO_POLICY_SCOPE`：不使用当前目录的策略。

#### 与 add_subdirectory 的区别
- `include` 引入的是文件，而 `add_subdirectory` 引入的是目录。
- `include` 不引入新的变量范围，而 `add_subdirectory` 引入新的变量范围。
- 默认情况下，`include` 和 `add_subdirectory` 都引入新的策略范围，可以通过 `NO_POLICY_SCOPE` 选项来避免。

### 示例项目结构
假设项目结构如下：
```
myproject/
├── CMakeLists.txt
├── src/
│   ├── main.cpp
│   └── CMakeLists.txt
└── lib/
    ├── mylib.cpp
    ├── mylib.h
    └── CMakeLists.txt
```
在 `myproject/CMakeLists.txt` 文件中：
```cmake
# 添加 src 目录
add_subdirectory(src)

# 添加 lib 目录
add_subdirectory(lib)
```
在 `myproject/src/CMakeLists.txt` 文件中：
```cmake
# 将 main.cpp 文件添加到可执行文件的构建中
add_executable(myapp main.cpp)
```
在 `myproject/lib/CMakeLists.txt` 文件中：
```cmake
# 将 mylib.cpp 文件添加到库的构建中
add_library(mylib mylib.cpp)

# 将包含目录添加到库的构建中
target_include_directories(mylib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# 将库链接到可执行文件的构建中
target_link_libraries(myapp mylib)
```

### 总结
- 使用 `add_subdirectory` 来组织项目中的子目录和模块。
- 使用 `include` 来共享和重用CMake脚本中的代码。
- 注意作用域和策略范围的变化，以确保变量和设置的正确性。

