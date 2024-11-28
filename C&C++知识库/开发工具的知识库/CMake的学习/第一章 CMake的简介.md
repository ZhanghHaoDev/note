# CMake的简介

## 1. CMake的简介

CMake是一个跨平台的构建工具，可以用来管理软件的构建过程。它可以生成各种平台和编译器的构建文件，支持复杂的项目构建需求。

### CMake 的主要作用
- 生成可执行文件和库文件。
- 管理项目依赖，包括第三方库。
- 支持自动化测试。
- 支持软件的安装和打包

### cmake推荐的书籍

1. [Modern CMake 简体中文版](https://modern-cmake-cn.github.io/Modern-CMake-zh_CN/)
2. CMake Cookbook
3. Mastering CMake（第七版）

## 2. CMake的安装

```shell
# Windows下的安装
访问官方网站，下载windows的二进制包，添加环境变量

# Linux下的安装
sudo apt-get install cmake

# macOS下的安装
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
