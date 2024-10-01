# avio_list_dir
 
## 1. 项目简介

1. 主要功能：使用ffmpeg的api解析目录的文件，然后列举出目录下文件的参数
2. 使用方法：./avio_list_dir /home/user/videos

## 2. 项目函数解析
avio_list_dir 分为四个函数：
   1. main 主函数，程序入口
   2. usage 用法函数，函数打印程序的使用方法。(不是必须)
   3. list_op 列出目录内容的函数
   4. type_string 类型字符串函数

### main() 函数
```c
int main(int argc, char *argv[]){
    int ret;
    av_log_set_level(AV_LOG_DEBUG);
    if (argc < 2) {
        usage(argv[0]);
        return 1;
    }
    avformat_network_init();
    ret = list_op(argv[1]);
    avformat_network_deinit();

    return ret < 0 ? 1 : 0;
}
```
1. `int ret` 设置错误码和返回值
2. `av_log_set_level` 设置ffmpeg的日志等级
3. 判断main函数的参数，确保了提供了目录参数
4. `avformat_network_init`初始化网络组件
5. 执行list_op函数
6. 关闭ffmpeg的网络组件
7. 返回结果

### list_op() 函数
```c
static int list_op(const char *input_dir){
    AVIODirEntry *entry = NULL;
    AVIODirContext *ctx = NULL;
    int cnt, ret;
    char filemode[4], uid_and_gid[20];

    if ((ret = avio_open_dir(&ctx, input_dir, NULL)) < 0) {
        av_log(NULL, AV_LOG_ERROR, "Cannot open directory: %s.\n", av_err2str(ret));
        goto fail;
    }

    cnt = 0;
    for (;;) {
        if ((ret = avio_read_dir(ctx, &entry)) < 0) {
            av_log(NULL, AV_LOG_ERROR, "Cannot list directory: %s.\n", av_err2str(ret));
            goto fail;
        }
        if (!entry)
            break;
        if (entry->filemode == -1) {
            snprintf(filemode, 4, "???");
        } else {
            snprintf(filemode, 4, "%3"PRIo64, entry->filemode);
        }
        snprintf(uid_and_gid, 20, "%"PRId64"(%"PRId64")", entry->user_id, entry->group_id);
        if (cnt == 0)
            av_log(NULL, AV_LOG_INFO, "%-9s %12s %30s %10s %s %16s %16s %16s\n",
                   "TYPE", "SIZE", "NAME", "UID(GID)", "UGO", "MODIFIED",
                   "ACCESSED", "STATUS_CHANGED");
        av_log(NULL, AV_LOG_INFO, "%-9s %12"PRId64" %30s %10s %s %16"PRId64" %16"PRId64" %16"PRId64"\n",
               type_string(entry->type),
               entry->size,
               entry->name,
               uid_and_gid,
               filemode,
               entry->modification_timestamp,
               entry->access_timestamp,
               entry->status_change_timestamp);
        avio_free_directory_entry(&entry);
        cnt++;
    };

  fail:
    avio_close_dir(&ctx);
    return ret;
}
```
1. list_op 函数用于列出指定目录的内容。
2. 使用 avio_open_dir 打开目录。
3. 使用 avio_read_dir 读取目录中的每个条目。
4. 打印条目的类型、大小、名称、用户和组 ID、文件模式、修改时间、访问时间和状态更改时间。
5. 使用 avio_free_directory_entry 释放条目。
6. 使用 avio_close_dir 关闭目录。
7. AVIODirEntry 结构体表示目录中的一个条目（文件或子目录）。它包含了有关该条目的各种信息，例如名称、类型、大小等。
8. AVIODirContext 结构体表示一个打开的目录上下文，用于迭代目录中的条目。
9. for (;;) { ... } 是一个无限循环，等价于 while (true) { ... }。循环将一直执行，直到遇到 break 语句。
10. PRIo64 是一个宏定义，用于在 C 和 C++ 中格式化 64 位整数为八进制字符串。它是 C99 标准的一部分，定义在 <inttypes.h> 头文件中。这个宏确保了跨平台的一致性，因为不同平台上的 64 位整数类型可能有所不同。C++11 及更高版本要求在字面量和宏之间添加空格以避免解析错误。


### type_string() 类型字符串函数
```c
static const char *type_string(int type){
    switch (type) {
    case AVIO_ENTRY_DIRECTORY:
        return "<DIR>";
    case AVIO_ENTRY_FILE:
        return "<FILE>";
    case AVIO_ENTRY_BLOCK_DEVICE:
        return "<BLOCK DEVICE>";
    case AVIO_ENTRY_CHARACTER_DEVICE:
        return "<CHARACTER DEVICE>";
    case AVIO_ENTRY_NAMED_PIPE:
        return "<PIPE>";
    case AVIO_ENTRY_SYMBOLIC_LINK:
        return "<LINK>";
    case AVIO_ENTRY_SOCKET:
        return "<SOCKET>";
    case AVIO_ENTRY_SERVER:
        return "<SERVER>";
    case AVIO_ENTRY_SHARE:
        return "<SHARE>";
    case AVIO_ENTRY_WORKGROUP:
        return "<WORKGROUP>";
    case AVIO_ENTRY_UNKNOWN:
    default:
        break;
    }
    return "<UNKNOWN>";
}
```
1. 这个函数根据文件类型返回对应的字符串表示。