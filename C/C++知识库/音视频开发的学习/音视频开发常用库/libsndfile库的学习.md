# libsndfile库的学习

## 1. 简介
- **用途**：`libsndfile` 是一个用于读取和写入包含采样音频数据的音频文件的 C 语言库。
- **支持格式**：支持 WAV、AIFF、AU、FLAC、Ogg/Vorbis 等多种音频文件格式。
- **API**：提供简单易用的 API 接口，用于操作音频文件。

## 2. 安装

### GitHub 地址
- 源代码和更多信息：[https://github.com/libsndfile/libsndfile](https://github.com/libsndfile/libsndfile)

### 在Windows上安装
- **使用 vcpkg**：
  ```sh
  vcpkg install libsndfile
  ```
- **直接下载安装包**：可以从 GitHub 仓库中找到对应系统的预编译安装包。

### 在Linux上安装
- **使用 apt-get**：
  ```sh
  sudo apt-get install libsndfile1-dev
  ```

### 在macOS上安装
- **使用 Homebrew**：
  ```sh
  brew install libsndfile
  ```

## 3. 源码构建
- **步骤**：
  ```sh
  # 下载源码
  git clone https://github.com/libsndfile/libsndfile.git 
  
  # 进入目录
  cd libsndfile
  
  # 创建构建目录
  mkdir build
  cd build
  
  # 配置构建
  cmake ..
  
  # 编译安装
  make
  sudo make install
  ```

## 4. libsndfile 与 cmake
- **CMake 配置示例**：
  ```cmake
  cmake_minimum_required(VERSION 3.10)
  project(SndFileExample)
  
  set(CMAKE_CXX_STANDARD 14)
  
  find_package(PkgConfig REQUIRED)
  pkg_check_modules(SNDFILE REQUIRED sndfile)
  
  add_executable(SndFileExample main.cpp)
  
  target_include_directories(SndFileExample PRIVATE ${SNDFILE_INCLUDE_DIRS})
  target_link_libraries(SndFileExample ${SNDFILE_LIBRARIES})
  ```

### 使用示例
以下是一个简单的示例，展示如何使用 `libsndfile` 读取音频文件：

```c
#include <stdio.h>
#include <sndfile.h>

int main () {
    SF_INFO sfinfo;
    SNDFILE *infile;
    short *buffer;
    int readcount;
    
    // 打开音频文件
    infile = sf_open("input.wav", SFM_READ, &sfinfo);
    if (!infile) {
        printf("Not able to open input file.\n");
        return 1;
    }
    
    // 分配缓冲区
    buffer = (short*)malloc(sfinfo.channels * sfinfo.frames * sizeof(short));
    
    // 读取音频数据
    readcount = sf_readf_short(infile, buffer, sfinfo.frames);
    if (readcount < 0) {
        printf("Error reading audio file.\n");
        sf_close(infile);
        return 1;
    }
    
    // 处理音频数据
    // ...

    // 释放资源
    free(buffer);
    sf_close(infile);
    
    return 0;
}
```

### 总结
`libsndfile` 是一个功能强大的音频处理库，支持多种音频格式，提供了简单易用的 API。通过上述安装和配置步骤，你可以轻松地在你的项目中使用它。希望这些整理和补充对你有所帮助！如果你有更多问题或需要进一步的帮助，请随时告诉我。
