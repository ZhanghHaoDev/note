# CMake的简介

## 1. CMake的简介

CMake是一个跨平台的构建工具，可以用来管理软件的构建过程。它可以生成各种平台和编译器的构建文件，支持复杂的项目构建需求。

### CMake 的主要作用
- 生成可执行文件和库文件。
- 管理项目依赖，包括第三方库。
- 支持自动化测试。
- 支持软件的安装和打包

## 2. CMake的安装

1. **Windows**：通过官方网站下载安装包或使用包管理器（如 winget）。

2. Linux 下安装 CMake

```shell
sudo apt-get install cmake
```

3. macOS 下安装 CMake

```shell
brew install cmake
```

## 3. 构建系统

CMake的优点，主要在于他是一个跨平台的构建系统，可以生成多种构建系统的配置文件，比如Makefile、Ninja、Visual Studio等。

构建系统是自动化工具，用于编译、链接和打包源代码，生成可执行文件或库。它们处理依赖管理，确保只重新编译必要的文件，并支持跨平台编译。

### 常见的构建系统
- **Make**：在 Linux 上广泛使用的构建系统，通过 Makefile 控制构建过程。
- **CMake**：跨平台的高级构建系统，可以生成多种构建系统的配置文件。
- **Ninja**：专注于速度的小型构建系统，通常与 CMake 配合使用。
- **MSBuild**：用于 .NET 和 Visual Studio 的构建系统。
- **Gradle**：用于 Java 和 Android 的构建系统。

## 4. CMake的基本工作流程

1. 编写 CMakeLists.txt 文件，定义项目的构建规则。
2. 创建源文件，包括头文件和源文件。
3. 创建构建目录，用于存放生成的构建文件。
4. 运行 CMake，生成构建文件。
5. 使用构建系统编译源代码，生成可执行文件或库文件。

## 5. Hello World 示例

1. 创建一个源代码文件 `main.c`：

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

2. 创建一个 `CMakeLists.txt` 文件：

```cmake
cmake_minimum_required(VERSION 3.20)
project(hello_world)

add_executable(hello main.c)
```