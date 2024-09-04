# 第二章 protobuf语法

# protobuf语法的简介

1. protobuf是谷歌开源的一种数据格式，适合高性能，对响应速度有要求的数据传输场景。因为protobuf是二进制数据格式，需要编码和解码。数据本身不具有可读性。因此只能反序列化之后得到真正可读的数据。
2. 优势：
- 序列化后体积相比json和xml很小，适合网络传输
- 支持跨平台多语言
- 消息格式升级和兼容性还不错
- 序列化反序列化速度很快
1. 如何使用protobuf
- 定义一种源文件，扩展名称未.proto，使用这种源文件，可以定义存储类的内容（消息类型）
- protobuf有自己的编译器protoc，可以将.proto编译成对应语言的文件，就可以进行使用
- 使用 Protobuf 编译器（protoc）生成 C++ 文件的步骤如下：
1. 首先，你需要一个 .proto 文件，这个文件定义了你的数据结构。例如，你可能有一个名为 demo.proto 的文件。
2. 打开终端，导航到 .proto 文件所在的目录。
3. 在终端中，运行以下命令：

protoc --cpp_out=. demo.proto

在这个命令中，--cpp_out 参数指定了生成的 C++ 文件的输出目录，. 表示当前目录。demo.proto 是你的 .proto 文件的名称。

1. 运行这个命令后，protoc 会生成两个文件：demo.pb.h 和 demo.pb.cc。这两个文件包含了你在 .proto 文件中定义的数据结构的 C++ 实现。

注意：如果你的 .proto 文件中定义了 gRPC 服务，你还需要使用 --grpc_out 和 --plugin 参数来生成 gRPC 的代码：

protoc --cpp_out=. --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` demo.proto

在这个命令中，--grpc_out 参数指定了生成的 gRPC 代码的输出目录，--plugin 参数指定了 gRPC 插件的路径。

# 

# 基础语法

1. 指定的当前proto语法的版本

// 版本3

syntax= "proto3";

// 版本2

syntax= "proto2";

---

1. 注释
2. 单行注释：//
3. 多行注释：/* */

// 这是单行注释

/*

这是多行注释

这是多行注释

这是多行注释

- /

---

1. pachage

在 Protobuf 中，package 关键字用于防止不同的消息类型之间发生命名冲突。它的作用类似于 C++ 中的命名空间或者 Java 中的包。

例如，你可以这样定义一个 package：

syntax = "proto3";

package tutorial;

message SearchRequest {

string query = 1;

}

在这个例子中，SearchRequest 消息的完全限定名是 tutorial.SearchRequest。如果你在另一个 .proto 文件中定义了一个同名的 SearchRequest 消息，但使用了不同的 package，那么这两个消息就不会发生冲突。

在生成的代码中，package 也会影响生成的类的名称和位置。例如，在 Java 中，package 会变成类的包名；在 C++ 中，package 会变成类的命名空间。

1. message

message:protobuf中定义一个消息类型是通过关键字message字段指定的

消息就是需要传输的数据格式的定义

message关键字类似与c++中的class，java中的class，go中的struct

messageuser

{

string username = 1;

int32 age = 2;

}

---

在消息中承载的数据分别对应于每一个字段

其中每个字段都有一个名字和一种类型

1. 字段类型

| **.proto Type** | **notes** | **c++** | **python** | **go** |
| --- | --- | --- | --- | --- |
| double |  | double | float | float64 |
| float |  | float | float | float32 |
| int32 | 使用变长解码，对于负值的效率很低，如果有负值，使用sint64 | int32 | int | int32 |
| uint32 | 使用变长解码 | uint32 | int/long | uint32 |
| uint64 | 使用变长解码 | uint64 | int/long | uint64 |
| sint32 | 使用变长解码，这些编码在负值时比int32高效的多 | int32 | int | int32 |
| sint64 | 使用变长解码，有符号的整型值。编码时比通常的int64高效 | int64 | int/long | int64 |
| bool |  | bool | bool | bool |
| string | 一个字符串必须是UTF-8编码或者7-bit ASSCII 编码的文本 | string | str/unicode | string |
| bytes | 可能包含任意顺序的字节数据 | string | str | []bye |

# 

# 默认值

| **类型** | **默认值** |
| --- | --- |
| bool | false |
| 整型 | 0 |
| string | 空字符串 |
| 枚举 enum | 第一个枚举元素的值，因为protobuf3强制要求第一个枚举元素的值必须是0，所以默认就是0 |
| message | 不是null，而是DEFAULT_INSTANCE |

# 

# 标识号

标识号：在消息体的定义中，每个字段都必须要有一个唯一的标识号，标识号是0，2^29-1范围内的一个整数

messageuser

{

string username = 1;

int32 age = 2;

}

---

以user为例，name = 1，age = 2，其中1，2就是标识号

# 

# 定义多个消息类型

一个proto文件中可以定义多个消息类型

messageUserRequest{

string username = 1;

int32 age = 2;

optional string passsword = 3;

repeated string address = 4;

}

messageUserResponse{

string username = 1;

int32 age = 2;

optional string passsword = 3;

repeated string address = 4;

}

---

# 嵌套消息

可以在其他消息类型中定义，使用消息类型，在下面的例子中，Person消息就定义在Personinfo消息内，比如：

messagePersonInfo {

message Person{

string name = 1;

int32 height = 2;

repeated int32 weight = 3;

}

repeated Person info = 1;

}

---

如果你想在他的父消息类型的外部重用这个消息类型，你需要以Personinfo.Person的形式使用他，如：

messagePersonMessage{

PersonInfo.Person info = 1;

}

---

当然也可以将消息嵌套任意多层

# 定义服务

如果想要将消息类型应用在RPC系统中，可以在.proto文件中定义一个RPC服务接口，protocol buffer编译器将会根据所选择的不同语言生成服务接口代码及存根

serviceSearchService {

// rpc 服务的函数名 （传入参数）返回（返回参数）

rpc Search (SearchRequest)returns(SearchREsponse);

}

---

上述代表表示，定义一个RPC服务，该方法接收SearchRequest返回SeaechResponse

# 

# 枚举

protobuf也支持枚举值，但要注意枚举值的标识号是从0开始的

ennumflag{

NOT_ERROR = 0;

ERROR = 1;

}

---

# 数组

protobuf也支持数组类型

// 结果

messageimage_acoustic_reply {

int32 flag = 1;                            // 结果标志位

repeated float result =2;                // 结果

repeated bytes result_txt= 3;            // 结果txt

}

---

其中repeated关键字是数组类型，在使用的时候，用add函数添加内容

# protobuf中的string和bytes

我们知道bytes用于存储二进制数据，但在c++中string可以存储ascii文本字符串，也能存储任意数量的二进制序列

string类型（protobuf中的string，与c++区分）不能存储非法的UTF-9字符，如果遇到该字符，序列化会报错

[libprotobuf ERROR google/protobuf/wire_format.cc:1091] String field ‘str’

【解决办法】：将string类型修改为bytes类型

# 总结一下

在使用protobuf的时候，一般分为下面几步

1. 定义好接口文件，包括字段类型，字段名称，返回值
2. 确定服务，指的是输入和输出
3. 编写好.proto文件，利用命令行生成文件框架
4. 在代码中导入框架文件，开始使用

# 对比分析xml，json，protobuf之间的优缺点

XML、JSON 和 Protobuf 是三种常见的数据交换格式，各有优缺点：

1. XML：
- 优点：格式清晰，可读性好，支持复杂的嵌套结构，支持元数据，被广泛支持和使用。
- 缺点：格式冗长，文件大小较大，解析速度较慢。
- 效率：由于其冗长的格式和复杂的解析过程，XML 的效率相对较低。
1. JSON：
- 优点：格式简洁，可读性好，支持基本的数据类型和嵌套结构，被广泛支持和使用，尤其在 Web 开发中。
- 缺点：不支持二进制数据，不支持注释，对数据类型的支持不如 XML 和 Protobuf。
- 效率：由于其简洁的格式和简单的解析过程，JSON 的效率相对较高。
1. Protobuf：
- 优点：格式紧凑，支持复杂的嵌套结构，支持版本控制，支持多种语言。
- 缺点：可读性差，需要 .proto 文件定义数据结构，不如 XML 和 JSON 那么通用。
- 效率：由于其紧凑的格式和高效的序列化/反序列化过程，Protobuf 的效率非常高。

总的来说，如果你需要高效的数据交换，并且不需要人类可读的格式，那么 Protobuf 是一个很好的选择。如果你需要人类可读的格式，并且数据不是很大，那么 JSON 是一个很好的选择。如果你需要复杂的数据结构和元数据支持，那么 XML 可能是一个好的选择。