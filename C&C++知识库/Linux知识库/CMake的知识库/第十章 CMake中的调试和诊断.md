### 日志信息

#### message() 指令
- `message([<mode>] "message to display" ...)`：用于输出日志信息。
- `<mode>` 是可选的，可以指定消息的类型。

#### 日志等级
- `STATUS`：输出状态消息，通常用于指示当前的配置或处理状态。
- `WARNING`：输出警告消息，指出可能的问题，但不会停止构建过程。
- `AUTHOR_WARNING`：输出作者警告消息，通常用于指示可能需要开发者注意的问题。
- `SEND_ERROR`：输出错误消息，用于指出错误，但构建过程会继续。
- `FATAL_ERROR`：输出致命错误消息，这将停止构建过程。

#### 示例
```cmake
message(STATUS "Configuring my project...")
message(WARNING "This is a warning message.")
message(FATAL_ERROR "This is a fatal error message.")
```

### CMake性能分析

#### 启用性能分析
- 使用 `--trace` 选项来启用性能分析，输出构建过程中的所有命令和操作的详细信息。

#### 示例
```shell
cmake --trace .
```

#### 展开生成器表达式和变量引用
- 使用 `--trace-expand` 选项来展开所有的生成器表达式和变量引用。

#### 示例
```shell
cmake --trace-expand .
```

### 注意事项
- 使用 `message()` 指令时，如果没有指定 `<mode>`，默认输出的是信息消息。
- `--trace` 和 `--trace-expand` 选项主要用于调试CMake脚本，它们可以提供关于CMake处理过程的深入信息。
- `--trace-expand` 选项特别有用，因为它可以显示变量和生成器表达式展开后的值，帮助开发者理解CMake是如何计算这些值的。
