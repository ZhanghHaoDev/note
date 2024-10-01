# avio_read_callback

## 1. avio_read_callback的简介

1. 主要功能：使用 FFmpeg 的 AVIOContext API 通过自定义读取回调函数从内存缓冲区中读取数据，并解析媒体文件的格式信息
2. 使用方法：./avio_read_callback sample.mp4

## 2. 项目函数解析
1. main函数：初始化和参数检查，读取文件到内存，设置自定义读取回调，打开输入文件并解析格式，打印格式信息，清理资源，关闭输入文件
2. read_packet 函数是自定义的读取回调函数，用于从内存缓冲区中读取数据。
3. 结构体 buffer_data 的内容 uint8_t *ptr：指向内存缓冲区的指针，用于存储文件数据。 size_t size：缓冲区中剩余的数据大小。

