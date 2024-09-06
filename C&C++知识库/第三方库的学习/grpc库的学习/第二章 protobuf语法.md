### Protobuf语法学习笔记

#### 1. Protobuf简介
- **定义**：Protobuf是Google开源的数据格式，适用于高性能、对响应速度有要求的数据传输场景。
- **特点**：
  - 二进制格式，高效传输。
  - 支持跨平台多语言。
  - 良好的向后兼容性。
  - 序列化和反序列化速度快。

#### 2. 如何使用Protobuf
- **定义数据结构**：使用`.proto`文件定义数据结构。
- **编译**：使用Protobuf编译器`protoc`将`.proto`文件编译成对应语言的代码。
- **生成代码**：
  ```bash
  protoc --cpp_out=. demo.proto
  ```
- **gRPC服务**：
  ```bash
  protoc --cpp_out=. --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` demo.proto
  ```

#### 3. 基础语法
- **指定语法版本**：
  ```proto
  syntax = "proto3";
  ```
- **注释**：
  - 单行注释：`//`
  - 多行注释：`/* ... */`
- **Package**：用于命名空间，防止命名冲突。
  ```proto
  package tutorial;
  ```
- **Message**：定义数据结构。
  ```proto
  message User {
    string username = 1;
    int32 age = 2;
  }
  ```
- **字段类型**：
  - 基本类型：`double`, `float`, `int32`, `uint32`, `uint64`, `sint32`, `sint64`, `bool`, `string`, `bytes`
- **默认值**：
  - `bool`：`false`
  - 整型：`0`
  - `string`：空字符串
  - `enum`：第一个枚举值
  - `message`：`DEFAULT_INSTANCE`

#### 4. 标识号
- 每个字段必须有一个唯一的标识号，范围是`0`到`2^29-1`。

#### 5. 定义多个消息类型
- 一个`.proto`文件中可以定义多个消息类型。

#### 6. 嵌套消息
- 可以在其他消息类型中定义嵌套消息。

#### 7. 定义服务
- 在`.proto`文件中定义RPC服务接口。
  ```proto
  service SearchService {
    rpc Search (SearchRequest) returns (SearchResponse);
  }
  ```

#### 8. 枚举
- Protobuf支持枚举值，枚举值的标识号从`0`开始。

#### 9. 数组
- 使用`repeated`关键字定义数组类型。

#### 10. Protobuf中的`string`和`bytes`
- `string`用于存储UTF-8或ASCII文本。
- `bytes`用于存储二进制数据。

#### 11. 总结
- 定义好`.proto`文件，使用`protoc`生成代码框架，然后在代码中使用。

#### 12. XML、JSON、Protobuf对比
- **XML**：格式清晰，支持复杂结构，但文件大，解析慢。
- **JSON**：格式简洁，支持基本数据类型，解析速度快，但不支持二进制数据。
- **Protobuf**：格式紧凑，支持复杂结构，解析速度快，但可读性差。
