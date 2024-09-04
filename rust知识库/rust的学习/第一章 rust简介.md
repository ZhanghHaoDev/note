# 1. rust语言简介

Rust是一种系统编程语言，专注于速度、内存安全和并行性。它被设计为能够提供高级的抽象，同时保持低级别的硬件控制。

## 1.1. 学习rust

可以去官网参考官方文档

[https://www.rust-lang.org/zh-CN/learn](https://www.rust-lang.org/zh-CN/learn)

# 2. rust语言特性

1. 零成本抽象：Rust的抽象机制设计得既安全又高效，几乎不会引入运行时开销。
2. 内存安全：Rust通过一种称为所有权（ownership）的系统来管理内存，这可以在编译时防止数据竞争和空指针等问题，而无需垃圾收集。
3. 并发无恐惧：Rust的所有权和生命周期系统使得在没有数据竞争的情况下编写并发代码成为可能。
4. C兼容：Rust提供了C兼容的接口，可以无缝地与C库和旧的C代码库一起工作。
5. 包管理：Rust有一个内置的包管理器cargo，它可以帮助你构建你的项目和管理依赖

# 3. 安装rust

rust官网：[Rust Programming Language](https://www.rust-lang.org/)

1. Windows
打开rust官网，下载[rustup-init.exe](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe) 安装就可以
1. Linux

```python
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --help
```

1. macOS

macos 推荐使用rustup
Rust和rustup是两个不同的概念，但它们都是Rust编程语言的重要组成部分。
1. Rust：这是一种系统编程语言，注重安全、速度和并发性。它的设计目标是提供内存安全而不需要垃圾收集。Rust语言包括一组核心库和一个名为`rustc`的编译器。

2. rustup：这是Rust的版本管理和工具链安装工具。你可以使用rustup来安装Rust编译器、标准库和其他相关工具，如Rust的包管理器Cargo、Rust的语言服务器RLS等。rustup还允许你轻松切换Rust的版本，这对于测试你的代码在不同版本的Rust上的兼容性非常有用。

总的来说，Rust是编程语言本身，而rustup是一个帮助你管理和使用Rust的工具。

```python
brew install rustup
```

## 3.1. vscode
rust推荐使用vscode来编写代码，vscode的插件推荐：rust，rust-analyzer
vscode 设置 rust的LSP
安装好rustup和vscode的插件以后，vs会自动运行rust的LSP
# 4. rust包管理器cargo

Cargo是Rust的官方包管理器。它负责处理Rust项目的许多任务，包括构建代码、下载和编译依赖项，以及构建和发布包。

cargo的安装在安装rust的时候已经安装了，我们可以使用命令来查看cargo的版本

```python
cargo --version
```

## 4.1. cargo的常用命令
1.cargo new <name>：创建一个新的Rust项目。这将创建一个新的目录，其中包含一个基本的Rust项目结构和一个Cargo.toml文件。
2. cargo build：构建你的项目。这将编译你的代码，并在target/debug目录下生成一个可执行文件。
3. cargo run：构建并运行你的项目。这相当于先运行cargo build，然后运行生成的可执行文件。
4. cargo test：运行你的项目的测试。这将构建你的项目和它的测试，然后运行测试。
5. cargo check：检查你的代码是否可以编译，但不生成可执行文件。这比cargo build更快，因为它不需要生成可执行文件。
6. cargo doc：为你的项目生成文档。这将在target/doc目录下生成HTML文档。
7. cargo update：更新你的依赖项。这将检查你的Cargo.toml文件中列出的所有依赖项，看看是否有新的版本可用，如果有，它将更新Cargo.lock文件以使用新的版本。
8. cargo publish：发布你的库到cargo.io，Rust的包注册中心。

# 5. hello-word项目

## 5.1. 创建项目

我们使用new命令来创建一个新rust项目
```
cargo new hello-word
```

使用cargo创建的项目，目录结构如下，rust项目的源码在src目录下面，我们打开src/main.rc

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717837147745-03515c6c-81af-4004-8159-d04807543b90.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717837147745-03515c6c-81af-4004-8159-d04807543b90.png)

# 5.2. 编译项目

Rust项目需要编译。Rust是一种编译型语言，这意味着你的源代码在运行之前需要被转换成机器代码。这个过程由Rust的编译器rustc完成。

在你提供的代码中，你可以使用Rust的包管理器Cargo来编译你的项目。在你的项目目录中打开终端，然后运行cargo build命令。这将编译你的项目，并在target/debug目录下生成一个可执行文件。

```python
cargo build
```

# 5.3. 运行项目

如果你想编译并立即运行你的项目，你可以使用cargo run命令。这将编译你的项目，然后运行生成的可执行文件。

```python
cargo run
```

# 6. 注释

rust语言当中，也支持注释，分为两种

1. 单行注释，\\
2. 多行注释，\****\
3. 文档注释 \\\