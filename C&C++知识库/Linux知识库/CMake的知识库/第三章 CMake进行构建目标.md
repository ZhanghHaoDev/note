### 目标的概念
在 CMake 中，目标（target）是构建系统的一个核心概念，代表最终要生成的可执行文件、库文件或其他自定义输出。

### 目标类型
- **可执行文件**：使用 `add_executable()` 指令创建。
- **库文件**：使用 `add_library()` 指令创建，可以是静态库（STATIC）、动态库（SHARED）或模块库（MODULE）。
- **自定义目标**：使用 `add_custom_target()` 指令创建，用于执行非编译任务。

### 构建可执行文件
使用 `add_executable()` 指令，可以指定目标名称和源文件列表：
```cmake
add_executable(app1 a.cpp b.cpp)
```

### 定义库
使用 `add_library()` 指令，可以指定库名称、库类型和源文件列表：
```cmake
add_library(mylib STATIC source1.cpp source2.cpp)
```

### 连接目标
使用 `target_link_libraries()` 指令，可以链接库到目标：
```cmake
target_link_libraries(myapp PRIVATE mylib)
```

### 链接项属性
- `PUBLIC`：链接项会被添加到目标的链接依赖项中，并传递给依赖该目标的其他目标。
- `PRIVATE`：链接项只会被添加到目标的链接依赖项中，不会传递给其他目标。
- `INTERFACE`：链接项只用于目标的消费者，不会添加到目标本身的链接过程中。

### CMake 中的表达式
- **生成器表达式**：用于在构建阶段根据目标属性生成值。
- **条件表达式**：用于在配置阶段根据条件生成不同的值。

### CMake 编译 C++
- CMake 管理 C++ 编译过程，包括预处理、编译、优化和链接。
- 可以通过 CMake 指定不同的编译优化级别。

### 优化级别
- `-O0`：不进行优化（默认）。
- `-O1`：启用基本优化。
- `-O2`：进一步优化，提高性能。
- `-O3`：最高级别的优化。
- `-Os`：空间优化，减少程序大小。

### 配置优化器
在 CMake 中，可以通过设置变量来配置优化器标志：
```cmake
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
```

### 管理目标源
使用 `file(GLOB ...)` 指令可以收集文件列表，但通常不推荐这种做法，因为它可能导致构建系统在文件列表未变更时不触发重新构建。

### 总结
CMake 提供了强大的机制来定义和管理构建目标，包括可执行文件、库文件和自定义目标。通过使用 `add_executable()`、`add_library()` 和 `target_link_libraries()` 指令，可以轻松地构建和管理复杂的项目。生成器表达式和条件表达式为构建系统提供了灵活性，使得可以根据不同的构建环境和需求生成不同的输出。优化器配置允许开发者根据开发阶段（如 Debug 或 Release）调整编译器的优化行为。
