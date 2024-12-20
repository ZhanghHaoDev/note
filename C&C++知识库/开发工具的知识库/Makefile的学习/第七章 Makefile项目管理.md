﻿
Makefile 是一个非常强大的工具，用于自动化编译和构建项目。以下是Makefile的一些基本概念和用法的整理：

# 1. 用途
- **项目代码编译管理**：Makefile 可以自动化编译和管理项目代码。
- **节省编译项目时间**：通过只重新编译改动过的文件，Makefile 可以显著减少编译时间。
- **一次编写终身受益**：编写一次Makefile，可以在项目的整个生命周期中重复使用。

# 2. 掌握以下几点

## 一个规则
- 一个规则由三部分组成：目标（target）、依赖（dependencies）、命令（commands）。
- 规则格式：
  ```makefile
  target: dependencies
  [tab]command
  ```
- 目标：规则要生成的文件或伪目标。
- 依赖：目标文件依赖的文件列表。
- 命令：生成目标时需要执行的命令，必须以一个Tab字符开头。

## 两个函数
- `$(wildcard pattern)`：找到匹配模式的所有文件。
  ```makefile
  src = $(wildcard *.c)
  ```
- `$(patsubst pattern,replacement,text)`：替换文本中的模式。
  ```makefile
  obj = $(patsubst %.c,%.o,$(src))
  ```

## 三个自动变量
- `$@`：表示规则中的目标文件。
- `$<`：表示规则中的第一个依赖文件。
- `$^`：表示规则中的所有依赖文件，如果有重复则只保留一个。

## 模式规则
- 模式规则使用`%`作为模式匹配。
  ```makefile
  %.o: %.c
    gcc -c $< -o $@
  ```

## 伪目标
- 伪目标不是实际的文件，而是用来表示一系列操作的标签。
  ```makefile
  .PHONY: clean ALL
  ```

# 3. 一个最简单的Makefile
```makefile
hello: hello.c
    gcc hello.c -o hello
```
编写完成后，直接执行`make`命令，会在目录下生成可执行文件`hello`。

# 4. 推荐的书籍
- 推荐阅读GNU make的官方文档，它提供了Makefile的详细指南和高级技巧。
- 国内推荐《和我一起写Makefile》[https://github.com/seisman/how-to-write-makefile]

### 注意事项
- 确保Makefile中的命令行以Tab字符开头。
- Makefile的文件名通常为`Makefile`或`makefile`。
- 使用`.PHONY`伪目标可以定义伪目标，以便`make`命令可以识别并执行相关的命令。

# 推荐资源
- 你提供了一个链接，但由于网络原因，我无法解析该网页的内容。请检查链接的合法性或稍后重试。如果链接有效，它可能会提供更多关于Makefile的有用信息。

通过掌握Makefile，你可以更有效地管理项目构建过程，节省时间，并减少错误。
