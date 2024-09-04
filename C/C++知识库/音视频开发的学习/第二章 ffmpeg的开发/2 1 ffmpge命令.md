# 2.1 ffmpge命令

# 1. ffmpeg 的命令

这是一个非常强大的工具，可以用来录制、转换和流化音频和视频。它支持多种格式，并且提供了许多选项来调整输出的质量和格式。

1. 查看ffmpeg命令的帮助以及都有哪些命令

```makefile
ffmpeg -h
ffmpeg -h full
ffmpeg -h full long
```

1. 查看ffmpeg的版本

```bash
ffmpeg -version
```

1. 转化视频格式

```bash
ffmpeg -i input.mp4 output.avi
```

1. 提取音频

```bash
ffmpeg -i input.mp4 -vn output.mp3
```

1. 改变视频分辨率（分辨率改为1280x720）

```bash
ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4
```

1. 剪辑视频（从input.mp4的30秒处开始，剪辑出1分钟的视频）

```bash
ffmpeg -i input.mp4 -ss 00:00:30 -t 00:01:00 output.mp4
```

1. 添加水印

```bash
ffmpeg -i input.mp4 -i logo.png -filter_complex "overlay=W-w-10:H-h-10" output.mp4
```

1. 提取帧为图片（每帧保存为一个图片）

```bash
ffmpeg -i input.mp4 -vf fps=1 output_%04d.png
```

# 2. ffplay 的命令

这是一个简单的媒体播放器，使用SDL和FFmpeg库来播放多媒体文件。它可以播放各种格式的音频和视频文件，也可以播放网络流。

1. 查看ffplay的版本

```bash
ffplay -version
```

1. 查看ffplay的帮助

```bash
ffplay -h
```

1. 播放视频或者音频文件

```bash
ffplay filename.mp4
```

1. 播放网络流

```bash
ffplay http://example.com/stream
```

1. 播放网络流并且保存

```bash
ffplay -i http://example.com/stream -c copy output.mp4
```

1. 指定播放窗口大小

```bash
ffplay -x 640 -y 480 filename.mp4
```

1. 显示视频信息

```bash
ffplay -i filename.mp4 -showmode 1
```

1. 显示ffprobe的版本

```bash
ffprobe -version
```

1. 显示ffporbe的帮助

```bash
ffprobe -h
```

# 3. ffprobe

这是一个用来分析多媒体内容的工具，它可以提取有关音频和视频文件的元数据，如格式、编码、时长、帧率等

1. 显示音频或者视频信息：

```bash
ffprobe filename.mp4
```

1. 显示视频时长

```bash
ffprobe -v error -show_entries format=duration -of default=noprint_wrappers=1:nokey=1 filename.mp4
```

1. 显示视频帧率

```bash
ffprobe -v error -select_streams v -of default=noprint_wrappers=1:nokey=1 -show_entries stream=r_frame_rate filename.mp4
```

1. 显示音频采样率

```bash
ffprobe -v error -select_streams a -of default=noprint_wrappers=1:nokey=1 -show_entries stream=sample_rate filename.mp4
```

1. 显示视频分辨率

```bash
ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=s=x:p=0 filename.mp4
```