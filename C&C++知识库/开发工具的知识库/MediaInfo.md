# MediaInfo
## MediaInfo工具简介

MediaInfo 是一个方便的工具，用于获取多媒体文件的技术和标签信息。它支持多种音频和视频文件格式，并提供详细的文件信息。

## 安装

### macOS
可以使用 Homebrew 安装 MediaInfo：
```sh
brew install mediainfo
```

### Windows
可以从 [MediaInfo官方网站](https://mediaarea.net/en/MediaInfo/Download) 下载并安装。

## 命令行版本的使用

### 基本用法
在命令行中运行以下命令来获取文件信息：
```sh
mediainfo <文件路径>
```

### 示例
```sh
mediainfo example.mp4
```

### 输出特定信息
可以使用 `--Output` 选项来指定输出格式，例如 JSON：
```sh
mediainfo --Output=JSON example.mp4
```

### 常用参数
- `--Full`: 显示所有可用的信息。
- `--Language=<语言>`: 设置输出语言，例如 `--Language=zh-CN`。
- `--LogFile=<文件路径>`: 将输出保存到指定文件。
- `--Cover_Data`: 显示封面图像数据（如果有）。
- `--Inform=<模板>`: 使用自定义模板格式化输出。

### 更多选项
查看所有可用选项：
```sh
mediainfo --Help
```

## 参考链接
- [MediaInfo 官方网站](https://mediaarea.net/en/MediaInfo)
- [MediaInfo 命令行文档](https://mediaarea.net/en/MediaInfo/Support/CommandLine)
