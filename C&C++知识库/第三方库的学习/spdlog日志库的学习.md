### spdlog日志库的学习

#### 简介
- **spdlog**：一个高效的C++日志库，支持多线程、异步日志记录，以及多种日志级别。
- **特点**：作为头文件库，易于使用和集成。

#### 获取和安装
- **下载**：
  ```bash
  git clone https://github.com/gabime/spdlog.git
  ```
- **构建和安装**：
  ```bash
  cmake -DCMAKE_INSTALL_PREFIX=/path/to/install ..
  make
  sudo make install
  ```

#### 学习资源
- **官方Wiki**：[spdlog Wiki](https://github.com/gabime/spdlog/wiki)

#### 使用实例
- **main.cpp**：
  ```cpp
  #include <iostream>
  #include "spdlog/spdlog.h"
  #include "spdlog/sinks/basic_file_sink.h"
  #include "spdlog/sinks/daily_file_sink.h"
  #include "spdlog/sinks/rotating_file_sink.h"
  #include "spdlog/sinks/stdout_color_sinks.h"

  int main() {
      // example spdlog output info
      spdlog::info("Welcome to spdlog!");

      // example spdlog output info to file
      auto file_logger = spdlog::basic_logger_mt("basic_logger", "logs/basic-log.txt");
      file_logger->info("Welcome to spdlog!");

      // example spdlog file name as current date
      auto daily_logger = spdlog::daily_logger_mt("daily_logger", "logs/daily-log.txt");
      daily_logger->info("Welcome to spdlog!");

      // example spdlog output log to file, file name as current date, suffix is .log
      auto rotating_logger = spdlog::rotating_logger_mt("rotating_logger", "logs/rotating-log.log", 1024 * 1024 * 5, 3);
      rotating_logger->info("Welcome to spdlog!");

      return 0;
  }
  ```

#### CMake配置
- **CMakeLists.txt**：
  ```cmake
  cmake_minimum_required(VERSION 3.20)
  project(spdlog_demo)

  # 设置语言标准
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_C_STANDARD 11)

  # 设置构建类型
  set(CMAKE_BUILD_TYPE Debug)
  # set(CMAKE_BUILD_TYPE Release)

  # 设置编译选项
  if(CMAKE_BUILD_TYPE STREQUAL "Debug")
      message(STATUS "Debug mode")
      set(CMAKE_C_FLAGS_DEBUG "$ENV{CFLAGS} -O0 -Wall -g")
      set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g")
  elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
      message(STATUS "Release mode")
      set(CMAKE_C_FLAGS_RELEASE "$ENV{CFLAGS} -O3 -Wall")
      set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
  endif ()

  # 设置spdlog库位置
  set(SPDLOG_DIR /Users/zhanghao/code/SDK/spdlog)

  # 设置spdlog头文件路径
  include_directories(${SPDLOG_DIR}/include)

  # 设置生成的可执行文件
  add_executable(spdlog_demo main.cpp)

  # 设置spdlog链接库
  target_link_libraries(spdlog_demo ${SPDLOG_DIR}/lib/libspdlog.a)
  ```