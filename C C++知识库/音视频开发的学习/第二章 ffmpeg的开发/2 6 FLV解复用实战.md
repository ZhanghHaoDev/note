# 2.6 FLV解复用实战

# 1. 总体流程

# 1.1. main函数

读取文件，调用Process进行处理

```cpp
int main(int argc, char *argv[]){
    cout << "Hi, this is FLV parser test program!\n";
    if (argc != 3){
        cout << "FlvParser.exe [input flv] [output flv]" << endl;
        return 0;
    }
    fstream fin;
    fin.open(argv[1], ios_base::in | ios_base::binary);
    if (!fin)
        return 0;
    Process(fin, argv[2]);
    fin.close();

    return 1;
}
```

# 1.2. 处理函数Process

读取文件，开始解析，打印解析信息，把解析之后的数据输出到另外一个文件

# 1.3. 解析函数

解析FLV 头部，解析FLV的tag

# 2. FLV相关的数据结构

# 2.1. CFlvParsar表示FLV解析器

# 2.2. FLV Header表示的头部

# 2.3. 标签

### 2.3.1. 标签头部

### 2.3.2. 标签数据

### 2.3.2.1. script类型的标签

### 2.3.2.2. 音频标签

### 2.3.2.3. 视频标签

# 2.4. 解析FLV头部

# 2.5. 入口函数

# 2.6. FLV头部解析函数

# 3. 解析视频标签

# 3.1. 标签的解析过程

# 3.2. 解析标签头部的函数

# 4. 解析视频标签

# 4.1. 入口函数CreateTag

# 4.2. 创建视频标签

# 4.3. 解析视频配置信息

# 4.4. 解析视频数据

# 4.5. 自定义的视频处理

# 5. 解析音频标签

# 5.1. 入口函数CreateTag

# 5.2. 创建音频标签

# 5.3. 解析音频标签

# 5.4. 处理音频配置

# 5.5. 处理原始音频数据

# 6. 解析其他标签

# 6.1. 入口函数CreateTag

# 6.2. 解析普通标签