### 构建类型
- **Debug**：禁用优化，包含调试信息，适合开发和调试。
- **Release**：启用优化，不包含调试信息，适合发布产品。
- **RelWithDebInfo**：启用优化，包含调试信息，适合发布同时需要调试的场景。
- **MinSizeRel**：启用优化，目标是最小化可执行文件大小，适合发布最小化部署。

### 设置构建类型
- 使用 `CMAKE_BUILD_TYPE` 变量来指定构建类型。

#### 示例
```cmake
# 指定构建类型为Debug
set(CMAKE_BUILD_TYPE Debug)

# 根据构建类型设置编译选项
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
  target_compile_options(myTarget PRIVATE -g)
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
  target_compile_options(myTarget PRIVATE -O3)
endif()
```

### 编程语言标准
- 使用 `CMAKE_<LANG>_STANDARD` 变量来设置C/C++语言的标准。

#### 示例
```cmake
# 设定C语言标准为C11
set(CMAKE_C_STANDARD 11)

# 设定C++语言标准为C++11
set(CMAKE_CXX_STANDARD 11)
```

### 注意事项
- 确保在CMakeLists.txt文件的顶部设置 `CMAKE_BUILD_TYPE`，这样它就可以影响整个项目的配置。
- 可以在命令行中设置构建类型：`cmake -DCMAKE_BUILD_TYPE=Debug ..`
- `CMAKE_<LANG>_STANDARD` 需要与 `target_compile_features()` 命令一起使用，以确保目标正确地使用指定的语言标准。

### 完整的CMakeLists.txt示例
```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

# 指定构建类型
set(CMAKE_BUILD_TYPE Debug)

# 添加可执行文件
add_executable(myTarget main.cpp)

# 根据构建类型设置编译选项
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
  target_compile_options(myTarget PRIVATE -g)
  message(STATUS "Debug build: Debugging symbols enabled")
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
  target_compile_options(myTarget PRIVATE -O3)
  message(STATUS "Release build: Optimizations enabled")
endif()

# 设定C++语言标准为C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 确保目标使用指定的语言标准
target_compile_features(myTarget PRIVATE cxx_std_11)
```
