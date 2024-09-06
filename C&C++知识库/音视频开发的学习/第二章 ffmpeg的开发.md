# 第二章 ffmpeg的开发

# 1. ffmpeg 的简介

`FFmpeg` 是一个开源的多媒体框架，可以用来录制、转换和流式传输音视频。它支持几乎所有已知的音视频格式，并且提供了丰富的工具和库来处理多媒体数据。以下是 `FFmpeg` 的一些关键特性和常用工具的简介：

### 关键特性

1. 多格式支持：支持几乎所有的音视频格式，包括但不限于 MP4、AVI、MKV、MP3、AAC、FLAC 等。
2. 高效编码和解码：提供高效的编码和解码功能，支持硬件加速。
3. 多媒体处理：支持视频剪辑、合并、滤镜、字幕、音频处理等多种操作。
4. 跨平台：支持多种操作系统，包括 Windows、Linux、macOS 等。

### 常用工具

1. ffmpeg：主要的命令行工具，用于录制、转换和流式传输音视频。
2. ffplay：一个简单的媒体播放器，用于播放音视频文件。
3. ffprobe：一个多媒体流分析工具，用于获取音视频文件的详细信息。
4. ffmepg 的安装

# 2. Linux 上的安装

建议直接源码安装

源码安装完了以后，省事的话，可以将 ffmpeg 的安装目录添加到环境变量，没有权限的情况下，需要在 cmake 当中指定 ffmpeg 的头文件和库文件的路径

```makefile
# 安装依赖
sudo apt update
sudo apt install yasm

# 下载ffmpeg的源码
git clone https://git.ffmpeg.org/ffmpeg.git ffmpeg
cd ffmpeg

# 配置和编译
./configure
# 编译
make -j
sudo make install

# 验证安装成功
ffmpeg -version
```

# 2.1. 验证安装

```c
#include <stdio.h>

#include <libavcodec/avcodec.h>
#include <libavformat/avformat.h>
#include <libavutil/avutil.h>

int main(int argc, char* argv[]) {
    printf("Hello, FFmpeg!\n");
    printf("FFmpeg version: %s\n", av_version_info());

    return 0;
}
```

```
cmake_minimum_required(VERSION 3.20)
project(demo)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_executable(demo main.c)

target_link_libraries(demo PUBLIC
    avcodec
    avformat
    avutil
    swscale
)
```

[2.1 ffmpge命令](2%201%20ffmpge命令%20e5e5aea21e23497788af4c55a92f5449.md)

[2.2 ffmpeg的基础开发](2%202%20ffmpeg的基础开发%208a4ef1b47d9e4f378f66532c1d9e31e8.md)

[2.3 AAC编码格式分析](2%203%20AAC编码格式分析%20876fadfe666b47db8f08bac501e1a8ad.md)

[2.4 H264编码格式分析](2%204%20H264编码格式分析%2036ea6269880e4a0986c852a7061ee255.md)

[2.5 FLV格式分析](2%205%20FLV格式分析%204fae9d56685644d9b066ba68b099e48e.md)

[2.6 FLV解复用实战](2%206%20FLV解复用实战%203fea0486b80d423d94664f71f0bc7f63.md)