# avio_read_callback

## 1. avio_read_callback的简介

1. 主要功能：使用 FFmpeg 的 AVIOContext API 通过自定义读取回调函数从内存缓冲区中读取数据，并解析媒体文件的格式信息
2. 使用方法：./avio_read_callback sample.mp4

## 2. 项目函数解析
1. main函数：初始化和参数检查，读取文件到内存，设置自定义读取回调，打开输入文件并解析格式，打印格式信息，清理资源，关闭输入文件
2. read_packet 函数是自定义的读取回调函数，用于从内存缓冲区中读取数据。
3. 结构体 buffer_data 的内容 uint8_t *ptr：指向内存缓冲区的指针，用于存储文件数据。 size_t size：缓冲区中剩余的数据大小。


1. av_file_map 函数，需要的头文件libavutil/file.h libavutil/error.h 这个函数的作用：将文件内容映射到内存中，它的作用是读取文件并将其内容加载到内存缓冲区当中
    函数参数：filename 要映射的文件的路径，bufptr：指向内存缓冲器的指针。函数成功后，这个指针将指向映射的内存区域
              size：指向存储文件大小的变量的指针，函数成功以后，这个变量将包含映射的文件的大小
              log_offset ：日志偏移量，通常设置为0，log_ctx：日志上下文，通常设置为NULL
    返回值：成功返回0，失败返回负数的错误码
2. avformat_alloc_context 函数，这个函数的主要作用是： 用于分配并且初始化一个AVFormatContext 这个结构体，该结构体主要用于存放文件的格式信息
    这个函数需要配合 avformat_free_context 来使用，一个用于申请内存，一个用于释放内存
    但是也可以使用avformat_close_input 这个函数来关闭输入文件并释放相关资源的，并且close这个函数实际上会调用ferr这个函数来释放资源的
3. av_malloc 函数，这个函数是ffmpeg库当中的用来分配内存的函数，需要配合av_free 函数来使用
4. avio_alloc_context 这个函数是 用于分配并初始化一个AVIOContext 结构体，这个结构体用于自定义输入/输出操作
    函数原型：AVIOContext *avio_alloc_context(unsigend char *buffer,int buffer_size,int write_flag,void *opaque,
              int (*read_packet)(void *opaque ,uint8_t *buf,int buf_size),
              int (*write_packet)(void *opaque, uint8_t *buf,int buf_size),
              int64_t (*seek)(void *opaque, int64_t offset,int whence)
                );
    参数详解：
        buffer : 指向用于I/O操作的缓冲器
        buffer_size : 缓冲区的大小
        write_flag : 指示是读操作还是写操作，非0值表示写操作，0表示读操作
        opaque : 用户定义的数据指针，将传递给回调函数
        read_packet : 指向读取回调函数的指针，如果不需要设置为NULL
        write_packer : 指向写入回调函数的指针。如果不需要设置为NULL
        seek：指向seek回调函数的指针，如果不需要设置为NULL
    
    回调函数详解：
        int read_packet(void *opaque,uint8_t *buf, int buf_size);
        opaque ： 用户定义的数据指针
        buf ： 指向读取数据的缓冲区
        buf_siez : 缓冲区的大小
        返回值： 读取的字节数，错误返回负数

        int write_packet(void *opaque,uint8_t *buf,int buf_size);
        opaque : 用户定义的数据指针
        buf ： 指向写入数据的缓冲区
        buf_size ： 缓冲区的大小
        返回值：写入的字节数。错误返回负数

        int64_t seek(void *opaque,int64_t offset,int whence);
        opaque: 用户定义的数据指针
        offset：要seek的偏移量
        whence: seek的起始位置
        返回值：新的文件位置，错误返回负数

5. avformat_open_input 这个函数用于打开输入的文件，读取头部的信息
    函数原型：int avformat_open_input(AVFormatContext **ps,const char *filename ,AVInputFormat *fmt,AVDictionary **options);
    函数参数：
        AVFormatContext **ps 指向AVFormatContext 指针的指针，AVFormatContext是一个结构体，包含了媒体文件的格式信息，调用这个函数以后，*ps将指向一个已初始化的AVFormatContext结构体
        const char *filename 输入文件的路径，如果使用了AVIOContext，可以将这个设置为NULL
        AVInputFormat *fmt 指定输入格式，如果设置为NULL，会自动检测格式
        AVDictionary **options 一个字典，用于设置一些选项，可以设置为NULL
        返回值：成功0，失败负数
    【注意】：这个函数需要配合 avformat_close_input 配合使用，用来关闭文件

6. avformat_find_stream_info 这个函数用于读取媒体文件的流信息，分析文件的内容，然后填充AVFormatContext 结构体当中的流信息
    函数原型：
        int avformat_find_stream_info(AVFormatContext *ic,AVDictionary **options);

    函数参数：
        AVFormatContext *ic 指向AVFormatContext 结构体的指针，包含了文件的格式信息等
        AVDictionary **options 一个字典，设置一些选项，可以设置为NULL
    函数返回值：成功0，失败负数
7. av_dump_format 这个函数用于打印媒体文件的格式信息
    函数原型：
        void av_dump_format(AVFormatContext *ic,int index, const char *url,int is_output);
    函数参数：
        AVFormatContext *ic 指向AVFormatContext 结构体的指针，包含了媒体文件的格式信息
        int index 流的索引，如果想要打印整个文件的信息，设置为0
        const char *url 媒体文件的路径
        int is_output 指示输入文件还是输出文件，0:输入文件，1：输出文件
    【注意】：这个函数需要配合av_file_unmap这个函数来使用
        但是av_dump_format 这个函数并不能单独的使用，需要配合avformat_open_input 和 avformat_find_stream_info 这两个才可以
        并且这个函数的输出，日志等级设置为`AV_LOG_INFO`

8. avcodec_send_packet 这个函数用于将编码后的数据包发送给解码器，这个函数通常与`avcodec_receive_frame`配合使用
    函数原型：int avcodec_send_packet(AVCodecContext *avctx, const AVPacket *avpkt);
    函数参数：AVCodecContext *avctx：指向解码器上下文的指针。这个上下文包含了解码器的配置信息和状态。
            const AVPacket *avpkt：指向要发送的数据包的指针。这个数据包包含了编码后的数据。
    函数返回值：成功返回0，失败返回错误码

9. avcodec_receive_frame 这个函数用于从解码器（decoder）接收解码后的帧（frame）。这个函数通常与 avcodec_send_packet 函数配合使用，以实现完整的解码流程。
    函数原型：int avcodec_receive_frame(AVCodecContext *avctx, AVFrame *frame);
    函数参数：AVCodecContext *avctx：指向解码器上下文的指针。这个上下文包含了解码器的配置信息和状态。
            AVFrame *frame：指向要接收解码后帧的指针。这个帧结构体将包含解码后的数据。
    函数返回值：成功返回0，失败返回错误码

10. AVERROR(EAGAIN) 这个宏定义表示操作需要再次尝试，常在解码或编码过程中，当输入或输出缓冲区未准备好时，会返回这个错误码。
11. AVERROR_EOF 表示操作已经到达文件或数据流的末尾
12. av_get_bytes_per_sample() 这个函数用于获取指定音频采样格式的每个样本的字节数。这个函数在处理音频数据时非常有用，可以帮助你确定每个音频样本的大小，以便正确地处理和存储音频数据。
    函数原型：int av_get_bytes_per_sample(enum AVSampleFormat sample_fmt);
    函数参数：enum AVSampleFormat sample_fmt：音频采样格式。AVSampleFormat 是一个枚举类型，包含了所有支持的音频采样格式
    函数返回值：成功返回指定音频采样格式的每个样本的字节数，失败返回负数错误码

13. av_sample_fmt_is_planar 用于检查音频的格式是否为平面格式的函数
    函数原型：int av_sample_fmt_is_planar(enum AVSampleFormat sample_fmt);
    函数参数：这是一个 AVSampleFormat 枚举类型的值，它表示要检查的音频样本格式
    函数返回值：函数返回一个整型值（int），如果 sample_fmt 是平面格式，则返回非零值（通常为1），表示是平面格式；如果 sample_fmt 不是平面格式，则返回0。
    
    音频是否为平面格式：在音频数据处理中，音频样本的存储方式主要有两种：平面格式（Planar Format）和交错格式（Interleaved Format）。这两种格式在多声道音频数据的存储方式上有所不同。
    平面格式（Planar Format）在平面格式中，每个声道的数据是分开存储的。也就是说，所有的左声道样本存储在一个连续的内存块中，所有的右声道样本存储在另一个连续的内存块中，以此类推。
    交错格式（Interleaved Format）在交错格式中，所有声道的数据是交错存储的。也就是说，每个声道的样本依次存储在一个连续的内存块中。