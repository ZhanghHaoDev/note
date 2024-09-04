# 2.3 AAC编码格式分析

[AAC ADTS格式分析.pdf](https://www.yuque.com/attachments/yuque/0/2024/pdf/23087967/1718522812791-b5fb1408-1ea5-49fe-a7ec-c1217a24b22b.pdf)

# 1. 基础知识

1. 一个视频文件或者音频文件是存在三层的，分别是封装，编码，基础数据
2. AAC（Advanced Audio Coding，高级音频编码）**是一种有损音频压缩格式**，旨在提供比 MP3 更高的音质和更高的压缩效率。它是由 MPEG（Moving Picture Experts Group，动态图像专家组）开发的，作为 MPEG-2 和 MPEG-4 标准的一部分。
3. AAC 默认：采样率 8KH~6KHz，采样个数 1024，码率：根据具体采样率也有对应的限制
4. 主要特点
- 高压缩效率：在相同的比特率下，AAC 通常比 MP3 提供更好的音质。
- 多声道支持：支持多达 48 个声道，适用于立体声和环绕声系统。
- 频带划分：使用更细致的频带划分，提高了音频编码的精度。
- 灵活性：支持多种采样率和比特率，适用于不同的应用场景。
1. 应用场景
- 流媒体：广泛应用于在线音乐和视频流媒体服务，如 Apple Music、YouTube 和 Netflix。
- 移动设备：由于其高效的压缩和解码性能，AAC 被广泛应用于智能手机、平板电脑和其他移动设备。
- 广播：在数字广播中，如 DAB（Digital Audio Broadcasting）和 DRM（Digital Radio Mondiale），AAC 也是常用的音频编码格式。

# 2. AAC 编码技术

1. 编码算法：AAC 使用基于 MDCT（Modified Discrete Cosine Transform，修正离散余弦变换）的编码算法，结合了时域和频域的处理方法。
2. 量化和编码：采用自适应量化和熵编码技术，提高了编码效率。
3. 频带划分：将音频信号划分为多个频带，分别进行处理，以提高编码精度。

# 3. AAC 文件格式

1. AAC 是一种音频文件的编码格式，ADIF 和 ADTS 分别是上层的封装格式（类似 h264 和 mp4）
2. 我们可以使用命令行来查看 aac 文件的封装格式

```bash
ffprobe -v error -show_format -show_streams output.aac
```

输出：

```json
format_long_name=raw ADTS AAC (Advanced Audio Coding)
```

1. 这两种封装格式有什么区别

ADIF：音频数据交换格式，这种格式的特点是可以确定的找到这个音频数据的开始，不需进展在音频数据流中间开始的解码，即他的解码必须在明确定义的开始处进展，常用在磁盘文件中

ADTS：是 AAC 音频的传输流格式。AAC 音频格式在 MPEG-2 中有定义，AAC 后来又被采用到 MPEG-4 标准当中，这种格式的特征是他是一个同步字的比特流，解码可以在这个流中任何位置开始，特征类似于 MP3 数据流格式

简单的说：**ADTS 可以在任意帧解码，也就是说他的每一帧都有头信息，ADIF 只有一个统一的头，所以必须得到所有的数据后解码**

ffmpeg 命令行将音频文件转换为 aac 编码的文件

```bash
ffmpeg -i input.mp3 -c:a aac output.aac
```

1. ADIF 的头信息

ADIF 的头信息包含：比特率，采样率，声道数，编码配置，其他参数

1. ADTS 的头信息

ADTS 的头文件包含：采样率，声道，帧长度等信息

1. 验证音频文件的格式，两种封装格式都可以

```bash
ffprobe -v error -show_format -show_streams test.mp3
```

- `ffprobe`：调用 FFmpeg 的 `ffprobe` 工具。
- `v error`：设置日志级别为 `error`，只显示错误信息，隐藏其他日志信息。
- `show_format`：显示文件的格式信息。
- `show_streams`：显示文件中所有流（音频、视频、字幕等）的信息。
- `test.mp3`：指定要分析的输入文件

使用代码输出音频文件的格式信息

```c
#include <stdio.h>
#include <libavcodec/avcodec.h>
#include <libavformat/avformat.h>
#include <libavutil/avutil.h>

void print_stream_info(AVFormatContext *fmt_ctx) {
    // 打印格式信息
    printf("格式: %s, 时长: %lld 微秒, 比特率: %lld kb/s\n",
           fmt_ctx->iformat->name,
           fmt_ctx->duration,
           fmt_ctx->bit_rate / 1000);

    // 打印每个流的信息
    for (unsigned int i = 0; i < fmt_ctx->nb_streams; i++) {
        AVStream *stream = fmt_ctx->streams[i];
        AVCodecParameters *codecpar = stream->codecpar;
        printf("流 #%u:\n", i);
        printf("  编解码器: %s (%s)\n",
               avcodec_get_name(codecpar->codec_id),
               av_get_media_type_string(codecpar->codec_type));
        printf("  时长: %lld 微秒\n", stream->duration);
        printf("  比特率: %lld kb/s\n", codecpar->bit_rate / 1000);
        printf("  采样率: %d\n", codecpar->sample_rate);
        printf("  声道数: %d\n",codecpar->ch_layout.nb_channels);
    }
}

int main(int argc, char *argv[]) {
    if (argc < 2) {
        fprintf(stderr, "用法: %s <输入文件>\n", argv[0]);
        return 1;
    }

    const char *input_filename = argv[1];

    AVFormatContext *fmt_ctx = NULL;
    if (avformat_open_input(&fmt_ctx, input_filename, NULL, NULL) < 0) {
        fprintf(stderr, "无法打开输入文件 '%s'\n", input_filename);
        return 1;
    }

    if (avformat_find_stream_info(fmt_ctx, NULL) < 0) {
        fprintf(stderr, "无法找到流信息\n");
        avformat_close_input(&fmt_ctx);
        return 1;
    }

    print_stream_info(fmt_ctx);

    avformat_close_input(&fmt_ctx);
    return 0;
}
```

1. AAC 音频文件的每一帧由 ADTS Header 和 AAC AUdio Data 组成。

ADTS 头部通常由 7 或 9 个字节组成，具体结构如下：

- 同步字（12 bits）：固定为 `0xFFF`，用于标识帧的开始。
- ID（1 bit）：MPEG 标识符，0 表示 MPEG-4，1 表示 MPEG-2。
- Layer（2 bits）：固定为 `00`。
- 保护位（1 bit）：表示是否有 CRC 校验，0 表示有 CRC 校验，1 表示无 CRC 校验。
- Profile（2 bits）：表示 AAC 的级别，如 Main、LC（Low Complexity）、SSR（Scalable Sample Rate）。
- 采样率索引（4 bits）：表示采样率。
- 私有位（1 bit）：私有数据。
- 声道配置（3 bits）：表示声道数。
- 原始拷贝（1 bit）：固定为 0。
- 家庭副本（1 bit）：固定为 0。
- 帧长度（13 bits）：表示整个帧的长度，包括 ADTS 头部和 AAC 音频数据。
- 缓冲区满度（11 bits）：表示固定码率时的缓冲区状态。
- 帧计数（2 bits）：表示当前帧在一个 AAC 片段中的位置。
- CRC 校验（16 bits，可选）：如果保护位为 0，则包含 CRC 校验。

# 4. 编码标准

HE-AAC（High-Efficiency Advanced Audio Coding，高效高级音频编码）是 AAC 的一种增强版本，旨在提供更高的压缩效率和更好的音质，特别是在低比特率下。HE-AAC 主要有两个版本：

- HE-AAC v1：在 AAC 的基础上增加了 SBR（Spectral Band Replication，频谱带复制）技术，通过复制和调整高频部分来提高音质。
- HE-AAC v2：在 HE-AAC v1 的基础上增加了 PS（Parametric Stereo，参数立体声）技术，通过参数化的方式处理立体声信号，进一步提高了压缩效率。

# 5. 从视频文件当中分离出 aac 音频

大体的思路为：检查视频文件当中是否存在 aac 音频，然后写 aac 音频的头（因为视频当中没有带 aac header），再然后写文件，最后写尾

```cpp
#include <stdio.h>
#include <libavformat/avformat.h>

int main(int argc, char *argv[]) {
    if (argc < 3) {
        printf("Usage: %s <input_flv_file> <output_aac_file>\n", argv[0]);
        return -1;
    }

    const char *input_filename = argv[1];
    const char *output_filename = argv[2];

    AVFormatContext *input_format_context = NULL;
    AVFormatContext *output_format_context = NULL;
    AVOutputFormat *output_format = NULL;
    AVPacket packet;
    // 打开输入文件
    if (avformat_open_input(&input_format_context, input_filename, NULL, NULL) < 0) {
        fprintf(stderr, "Could not open input file '%s'\n", input_filename);
        return -1;
    }

    // 获取输入文件的流信息
    if (avformat_find_stream_info(input_format_context, NULL) < 0) {
        fprintf(stderr, "Could not find stream information\n");
        return -1;
    }

    // 打开输出文件
    avformat_alloc_output_context2(&output_format_context, NULL, NULL, output_filename);
    if (!output_format_context) {
        fprintf(stderr, "Could not create output context\n");
        return -1;
    }

    output_format = output_format_context->oformat;

    // 查找音频流
    int audio_stream_index = -1;
    for (unsigned int i = 0; i < input_format_context->nb_streams; i++) {
        if (input_format_context->streams[i]->codecpar->codec_type == AVMEDIA_TYPE_AUDIO) {
            audio_stream_index = i;
            break;
        }
    }

    if (audio_stream_index == -1) {
        fprintf(stderr, "Could not find audio stream in the input file\n");
        return -1;
    }

    // 创建输出音频流
    AVStream *input_stream = input_format_context->streams[audio_stream_index];
    AVStream *output_stream = avformat_new_stream(output_format_context, NULL);
    if (!output_stream) {
        fprintf(stderr, "Failed allocating output stream\n");
        return -1;
    }

    if (avcodec_parameters_copy(output_stream->codecpar, input_stream->codecpar) < 0) {
        fprintf(stderr, "Failed to copy codec parameters\n");
        return -1;
    }

    output_stream->codecpar->codec_tag = 0;

    // 打开输出文件
    if (!(output_format->flags & AVFMT_NOFILE)) {
        if (avio_open(&output_format_context->pb, output_filename, AVIO_FLAG_WRITE) < 0) {
            fprintf(stderr, "Could not open output file '%s'\n", output_filename);
            return -1;
        }
    }

    // 写文件头
    if (avformat_write_header(output_format_context, NULL) < 0) {
        fprintf(stderr, "Error occurred when opening output file\n");
        return -1;
    }

    // 读取输入文件的音频数据并写入输出文件
    while (av_read_frame(input_format_context, &packet) >= 0) {
        if (packet.stream_index == audio_stream_index) {
            packet.stream_index = output_stream->index;
            if (av_interleaved_write_frame(output_format_context, &packet) < 0) {
                fprintf(stderr, "Error muxing packet\n");
                break;
            }
        }
        av_packet_unref(&packet);
    }

    // 写文件尾
    av_write_trailer(output_format_context);

    // 关闭输入和输出文件
    avformat_close_input(&input_format_context);
    if (output_format_context && !(output_format->flags & AVFMT_NOFILE)) {
        avio_closep(&output_format_context->pb);
    }
    avformat_free_context(output_format_context);

    printf("Audio extracted successfully to '%s'\n", output_filename);
    return 0;
}
```