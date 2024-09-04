# libsndfile库的学习

1. 简介

libsndfile 是一个用于读取和写入音频文件的 C 语言库。它支持许多不同的音频文件格式，包括 WAV、AIFF、AU、FLAC、Ogg/Vorbis 等。

libsndfile 提供了一组简单的 API，可以用来打开音频文件、读取或写入音频数据、获取和设置音频文件的元数据等。这使得它成为处理音频文件的一个非常有用的工具。

1. 安装

GitHub：https://github.com/libsndfile/libsndfile

1. libsndfile 在Windows上安装

可以使用vcpkg来安装

**代码**

---

vcpkg install libsndfile

---

也可以直接在GitHub上对应系统的安装包

|  |  |
| --- | --- |
| **🛈** | **信息**
[https://github.com/libsndfile/libsndfile](https://github.com/libsndfile/libsndfile) |
1. libsndfile 在Linux上的安装

**代码**

---

sudo apt-get install libsndfile1-dev

---

1. libsndfile 在macos上的安装

**代码**

---

brew install libsndfile

---

1. libsndfile 源码构建

**代码**

---

# 下载源码

git clone [https://github.com/libsndfile/libsndfile.git](https://github.com/libsndfile/libsndfile.git)

# 进入目录

cd libsndfile

# 构建

mkdir build

cd build

cmake ..

# 安装

make

sudo make install

---

1. libsndfile 与cmake

**代码**

---

cmake_minimum_required(VERSION 3.10)

project(SndFileExample)

set(CMAKE_CXX_STANDARD 14)

find_package(PkgConfig REQUIRED)

pkg_check_modules(SNDFILE REQUIRED sndfile)

add_executable(SndFileExample main.cpp)

target_include_directories(SndFileExample PRIVATE ${SNDFILE_INCLUDE_DIRS})

target_link_libraries(SndFileExample ${SNDFILE_LIBRARIES})

---