# decode_audio

## 1. 项目简介

1. 主要功能：这个项目主要使用ffmpeg来进行音频解码，从一个MP2输入文件来解码音频，生成一个原始音频文件（PCM）
2. 使用方法：./decode_audio ./audio.mp2
3. MP2 文件介绍：MP2文件是一种有损音频压缩格式，主要用于广播和视频制作领域，MP2在音频广播中常见

## 2. 项目函数解析

### main()函数

av_packet_alloc 这里没有搞清楚为什么上了先申请这个了？

avcodec_find_decoder() 函数，查找编码器，这里是查找ffmpeg库当中是否有`AV_CODEC_ID_MP2`mp2的解码器
1. 函数原型：
```c
const AVCodec *avcodec_find_decoder(enum AVCodecID id);
```
2. 函数参数：enum AVCodecID id：编解码器的 ID，表示要查找的解码器类型。AVCodecID 是一个枚举类型，包含了所有支持的编解码器 ID，例如 AV_CODEC_ID_H264、AV_CODEC_ID_MP3 等。
3. 函数返回值：成功时返回指向 AVCodec 结构体的指针。如果找不到指定的解码器，返回 NULL。

av_parser_init() 是 FFmpeg 库中的一个函数，用于初始化一个解析器上下文。解析器用于将原始数据流解析成可以解码的数据包。它在处理音视频数据时非常有用，特别是在处理不包含完整帧的流时。

1. 函数原型
```c
AVCodecParserContext *av_parser_init(int codec_id);
```
2. 函数参数
int codec_id：编解码器的 ID，表示要初始化的解析器类型。codec_id 是一个 AVCodecID 枚举值，例如 AV_CODEC_ID_H264、AV_CODEC_ID_MP3 等。
3. 函数返回值：
    成功时返回指向 AVCodecParserContext 结构体的指针。
    如果找不到指定的解析器，返回 NULL。
4. AVCodecParserContext 结构体详解，用于解析编码数据流。它包含了多个字段，用于存储解析过程中需要的各种信息
   
avcodec_open2 是 FFmpeg 库中的一个函数，用于初始化一个编解码器上下文，以便进行解码或编码操作。它是 avcodec_open 的改进版本，因此带有数字 2
   
1. 函数原型：
```c
int avcodec_open2(AVCodecContext *avctx, const AVCodec *codec, AVDictionary **options);
```
2. 函数参数：
+ AVCodecContext *avctx: 指向需要初始化的编解码器上下文的指针。
+ const AVCodec *codec: 指向要使用的编解码器的指针。
+ AVDictionary **options: 一个指向字典的指针，用于传递编解码器的附加选项。可以为 NULL。

3. 函数返回值：成功返回0，失败返回错误码
4. 为什么ffmpeg库的很多函数后面带数字？这个数字可能是改进的版本
5. 编解码器：用于将数据或信号进行编码和解码，常用于音视频处理、数据压缩和传输。
6. 编解析器：用于将原始数据流解析成可以解码的数据包，特别适用于处理不包含完整帧的流。

main/while 这个循环的解释：

在这段代码中，data_size 表示从输入文件中读取的音频数据的大小。fread 函数返回的是实际读取的字节数。

data_size = fread(inbuf, 1, AUDIO_INBUF_SIZE, f);

这里，fread 从文件 f 中读取最多 AUDIO_INBUF_SIZE 字节的数据到缓冲区 inbuf 中。因为每个元素的大小为 1 字节，所以 fread 返回实际读取的字节数，并将其赋值给 data_size。

av_parser_parse2 是 FFmpeg 库中的一个函数，用于解析输入数据流并提取独立的帧。这个函数在处理不完整或分段的数据时非常有用，可以帮助将压缩数据流解析成独立的帧，以便进一步解码。这里是将文件分解为帧数据
1. 函数原型：
```c
int av_parser_parse2(AVCodecParserContext *s, AVCodecContext *avctx,
                     uint8_t **poutbuf, int *poutbuf_size,
                     const uint8_t *buf, int buf_size,
                     int64_t pts, int64_t dts, int64_t pos);
```

2. 函数参数：
+ AVCodecParserContext *s：指向解析器上下文的指针。
+ AVCodecContext *avctx：指向编解码器上下文的指针。
+ uint8_t **poutbuf：指向输出缓冲区的指针，用于存储解析后的数据。
+ int *poutbuf_size：指向输出缓冲区大小的指针。
+ const uint8_t *buf：指向输入缓冲区的指针，包含要解析的数据。
+ int buf_size：输入缓冲区的大小。
+ int64_t pts：输入数据的显示时间戳（Presentation Timestamp）。
+ int64_t dts：输入数据的解码时间戳（Decoding Timestamp）。
+ int64_t pos：输入数据在文件中的位置。

3. 函数返回值：成功时返回消耗的输入数据大小。失败时返回负值的错误码。
