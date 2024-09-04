# spdlog日志库的学习

spdlog是一个高效的C++日志库，它提供了丰富的日志记录功能，包括多线程和异步日志记录，以及格式化和多种日志级别。它是一个头文件库，所以使用起来非常方便。你可以在你的项目中包含spdlog，然后在你的代码中使用它来记录日志信息。2023.11.09

下载：git clone [https://github.com/gabime/spdlog.git](https://github.com/gabime/spdlog.git)

构建（指定位置）：cmake -DCMAKE_INSTALL_PREFIX=/path/to/install ..

编译：make

安装：make install

如何学习使用该库：https://github.com/gabime/spdlog/wiki

使用实例：

main.cpp

#include <iostream>

// spdlog

#include"spdlog/spdlog.h"

#include"spdlog/sinks/basic_file_sink.h"

#include"spdlog/sinks/daily_file_sink.h"

#include"spdlog/sinks/rotating_file_sink.h"

#include"spdlog/sinks/stdout_color_sinks.h"

int main()

{

// example spdlog 输出信息

spdlog::info("Welcome tospdlog!");

// example spdlog 输出信息到文件

auto file_logger =spdlog::basic_logger_mt("basic_logger", "logs/basic-log.txt");

file_logger->info("Welcome tospdlog!");

// example spdlog 文件名称为当前日期

auto daily_logger =spdlog::daily_logger_mt("daily_logger", "logs/daily-log.txt");

daily_logger->info("Welcome tospdlog!");

// example spdlog 输出日志到文件，文件名称为当前日期，后缀名为.log

auto rotating_logger =spdlog::rotating_logger_mt("file_logger", "logs/rotating-log.log", 1024 * 1024 * 5, 3);

rotating_logger->info("Welcome tospdlog!");

return 0;

}

---

cmake

cmake_minimum_required(VERSION3.20)

project(spdlog_demo)

#设置语言标准

set(CMAKE_CXX_STANDARD17)

set(CMAKE_C_STANDARD11)

#设置构建类型

set(CMAKE_BUILD_TYPEDebug)

#set(CMAKE_BUILD_TYPE Release)

#设置编译选项

if(CMAKE_BUILD_TYPE STREQUAL "Debug")

message(STATUS "Debug mode")

set(CMAKE_C_FLAGS_DEBUG"$ENV{CFLAGS} -O0 -Wall -g")

set(CMAKE_CXX_FLAGS_DEBUG"$ENV{CXXFLAGS} -O0 -Wall -g")

elseif(CMAKE_BUILD_TYPE STREQUAL "Release")

message(STATUS "Release mode")

set(CMAKE_C_FLAGS_RELEASE"$ENV{CFLAGS} -O3 -Wall")

set(CMAKE_CXX_FLAGS_RELEASE"$ENV{CXXFLAGS} -O3 -Wall")

endif ()

#设置sodlog库位置

set(SPDLOG_DIR/Users/zhanghao/code/SDK/spdlog)

#设置spdlog头文件路径

include_directories(${SPDLOG_DIR}/include)

#设置生成的可执行文件

add_executable(spdlog_demomain.cpp)

#设置spdlog链接库

target_link_libraries(spdlog_demo${SPDLOG_DIR}/lib/libspdlog.a)

---