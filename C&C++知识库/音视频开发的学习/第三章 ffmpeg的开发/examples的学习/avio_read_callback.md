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