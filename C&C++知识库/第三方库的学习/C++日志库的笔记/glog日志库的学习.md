# glog 日志库

## 1. 简介
glog（Google Logging Library）是Google开发的一个C++日志库，提供了简单而强大的日志记录功能。它支持多种日志级别（INFO、WARNING、ERROR、FATAL），并且可以将日志输出到控制台、文件或其他自定义输出目标。glog还支持日志文件轮转、日志格式化、条件日志记录等高级功能。

### 主要特点
- **多级别日志记录**：支持INFO、WARNING、ERROR和FATAL四种日志级别。
- **日志文件轮转**：支持按大小或时间进行日志文件轮转，防止日志文件过大。
- **条件日志记录**：支持条件日志记录，可以根据条件选择性地记录日志。
- **线程安全**：glog是线程安全的，可以在多线程环境中安全使用。
- **丰富的日志格式**：支持自定义日志格式，便于日志分析和调试。

### 典型应用场景
- **服务器日志**：记录服务器运行状态、错误信息和性能数据。
- **应用程序调试**：记录应用程序的运行过程，便于调试和分析。
- **数据分析**：记录数据处理过程中的关键信息，便于后续分析和处理。

+ 默认输出文件和行号
+ 默认输出文件进程等信息

## 2. 安装

1. Linux

```shell
sudo apt install libgoogle-glog-dev
```

2. macos

```shell
brew install glog
```

3. 源码构建

glog的安装依赖gflags，需要先安装gflags

```shell
# Linux 
sudo apt install cmake libgflags-dev
# macOS
brew install cmake gflags

git clone https://github.com/google/glog.git
cd glog
mkdir build
cd build
cmake ..
make
sudo make install
```

## 3. glog与cmake

默认链接的库为：glog::glog

cmake的FetchContent模块

glog需要配合gflags使用，所以需要两个cmake文件

```cmake
# glog的FetchContent模块
include(FetchContent)

FetchContent_Declare(
  glog
  GIT_REPOSITORY https://github.com/google/glog.git
  GIT_TAG master
)

FetchContent_MakeAvailable(glog)
include_directories(${glog_SOURCE_DIR}/src ${glog_BINARY_DIR})
```

```cmake
# gflags的模块
include(FetchContent)

FetchContent_Declare(
  gflags
  GIT_REPOSITORY https://github.com/gflags/gflags.git
  GIT_TAG master  
)

FetchContent_MakeAvailable(gflags)
include_directories(${gflags_SOURCE_DIR}/src ${gflags_BINARY_DIR})
```

## 4. 遇到的错误

1. 使用glog的时候，需要先把glog初始化
2. 使用glog完毕，需要释放资源操作

```cpp
// glog初始化
google::InitGoogleLogging("avformat_model");
google::SetStderrLogging(google::INFO); 
google::InstallFailureSignalHandler();  
```

``` cpp
// glog 释放资源
google::ShutdownGoogleLogging();
```