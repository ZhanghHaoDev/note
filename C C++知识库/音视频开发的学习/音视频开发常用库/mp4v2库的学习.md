# mp4v2库的学习

# 1. 简介

mp4v2库是一个用于操作MPEG-4 Part 14（通常被称为MP4）文件的开源库。它提供了一组API，可以用于创建、读取、修改和删除MP4文件。

mp4v2库支持MP4文件中的多种元素，包括：

- 视频轨道（包括H.264和MPEG-4 Part 2视频）
- 音频轨道（包括AAC和MP3音频）
- 文字轨道（包括字幕和章节）
- 元数据（包括标题、艺术家、专辑等）

mp4v2库的API设计得非常直观，使得操作MP4文件变得非常简单。例如，你可以使用MP4Create函数创建一个新的MP4文件，使用MP4AddH264VideoTrack函数添加一个H264视频轨道，使用MP4WriteSample函数写入视频数据，然后使用MP4Close函数关闭MP4文件。

mp4v2库是跨平台的，可以在Windows、Linux和macOS上使用。它是用C++编写的，但也提供了C语言的API，因此可以在C和C++项目中使用

项目地址

[https://github.com/enzo1982/mp4v2](https://github.com/enzo1982/mp4v2)

# 2. 安装

1. Windows

```
# 下载mp4v2的源码，打开vstudio/mp4v2.sln
直接用vs打开vstudio/mp4v2.sln编译就可以
```

1. Linux

```
# 可以使用cmake
cmake . && make
```

1. macos

```
xcode/mp4v2.xcodeproj
```

# 3. demo

输出mp4v2的版本，验证安装成功

```cpp
#include <iostream>
#include <mp4v2/mp4v2.h>

int main() {
    std::cout << "mp4v2 version: " << MP4V2_PROJECT_version << std::endl;
    return 0;
}
```