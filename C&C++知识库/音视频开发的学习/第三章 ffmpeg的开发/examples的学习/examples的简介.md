# examples的学习

1. 原项目路径：[https://github.com/FFmpeg/FFmpeg/tree/master/doc/examples]
2. 仓库路径：ffmpeg_stu/examples_model
3. 测试路径：ffmpeg_stu/test/examples_model_test
4. 这个笔记主要是对ffmpeg项目的examples的解析，用于ffmpeg库的入门

## 1. 项目模块

1. avio_list_dir.c 使用 FFmpeg 库中的 AVIOContext API 列出目录内容
2. avio_read_callback.c：展示如何使用自定义读取回调函数从内存缓冲区中读取数据。
3. decode_audio.c：解码音频文件，演示如何使用 FFmpeg 解码音频流。
4. decode_filter_audio.c：解码并过滤音频数据，展示如何使用 FFmpeg 的过滤器 API。
5. decode_filter_video.c：解码并过滤视频数据，展示如何使用 FFmpeg 的过滤器 API。
6. decode_video.c：解码视频文件，演示如何使用 FFmpeg 解码视频流。
7. demux_decode.c：解复用并解码音视频文件，展示如何使用 FFmpeg 进行解复用和解码。
8. encode_audio.c：编码音频数据，演示如何使用 FFmpeg 编码音频流。
9. encode_video.c：编码视频数据，演示如何使用 FFmpeg 编码视频流。
10. extract_mvs.c：提取视频文件中的运动矢量，展示如何使用 FFmpeg 提取视频编码信息。
11. filter_audio.c：对音频数据应用滤镜，展示如何使用 FFmpeg 的音频滤镜功能。
12. hw_decode.c：硬件加速解码，演示如何使用 FFmpeg 进行硬件加速解码。
13. mux.c：复用音视频流，展示如何使用 FFmpeg 进行复用操作。
14. qsv_decode.c：使用 Intel Quick Sync Video (QSV) 进行解码，展示如何使用 FFmpeg 的 QSV 支持。
15. qsv_transcode.c：使用 Intel Quick Sync Video (QSV) 进行转码，展示如何使用 FFmpeg 的 QSV 支持。
16. remux.c：重新复用音视频流，展示如何使用 FFmpeg 进行重新复用操作。
17. resample_audio.c：重采样音频数据，展示如何使用 FFmpeg 进行音频重采样。
18. scale_video.c：缩放视频数据，展示如何使用 FFmpeg 进行视频缩放。
19. show_metadata.c：显示媒体文件的元数据，展示如何使用 FFmpeg 读取和显示元数据。
20. transcode.c：转码音视频文件，展示如何使用 FFmpeg 进行转码操作。
21. transcode_aac.c：转码音频文件为 AAC 格式，展示如何使用 FFmpeg 进行音频转码。
22. vaapi_encode.c：使用 VAAPI 进行视频编码，展示如何使用 FFmpeg 的 VAAPI 支持。
23. vaapi_transcode.c：使用 VAAPI 进行视频转码，展示如何使用 FFmpeg 的 VAAPI 支持。