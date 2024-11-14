# 第一章 关于UNIX系统开发的学习

## 1. UNIX开发简介

UNIX 系统开发是指在 UNIX 操作系统环境下进行软件开发，利用 UNIX 提供的丰富系统调用和编程接口，实现高效、稳定的程序。UNIX 系统以其稳定性、安全性和多用户多任务特性，被广泛应用于服务器、嵌入式系统和开发环境中。

### 推荐的资料

1. C程序设计语言
2. UNIX环境高级编程
3. UNIX网络编程 卷1：套接字联网API（第3版）
4. TCPIP详解 卷1：协议（原书第2版） 
5. TCPIP高效编程 改善网络程序的44个技巧 
6. Linux高性能服务器编程
7. 深入理解计算机系统（csapp）
8. Linux程序设计
9. Linux-UNIX系统编程手册（上、下册） 
10. CS144 计算机网络课程(https://cs144.github.io)
11. CS162 系统编程课程(https://cs162.org)
12. MIT 6828 操作系统工程课程

### 开发环境

1. 代码仓库：unix_stu
2. 开发环境：macOS，llvm19，CMake，vscode

### note 笔记的结构
```md
# 笔记标题
## 1. 笔记 简介
### 笔记 note
## 2. 笔记 接口
## 3. 笔记 数据结构
```

### POSIX标准

POSIX标准是Portable Operating System Interface of UNIX的缩写，是IEEE制定的一种标准，用于定义操作系统的接口。POSIX标准的目的是为了使UNIX系统的程序能够在其他操作系统上编译和运行。

POSIX标准本质上是一套接口规则，用于定义操作系统的接口，使得应用程序可以在不同的UNIX系统上编译和运行。POSIX标准旨在提高应用程序的可移植性，使得它们可以在不同的操作系统（如Linux的不同发行版、macOS、FreeBSD等）上运行，而无需进行大量的修改。

### man 帮助手册

1. 在unix系统当中，我们可以使用man查看系统手册，man系统手册提供了系统命令，库函数，配置文件等详细信息
2. man 常用的章节
   + 1 用户命令：常用的用户命令。
   + 2 系统调用：内核提供的系统调用。
   + 3 库函数：C 标准库函数。
   + 4 特殊文件：设备文件和特殊文件。
   + 5 文件格式：文件格式和约定。
   + 6 游戏：游戏和演示程序。
   + 7 杂项：杂项信息。
   + 8 系统管理命令：系统管理员使用的命令。
   + 9 内核例程：内核例程。
3. 使用例子
    ```shell
    # 查看系统命令帮助
    man ls
    # 查看库函数手册
    man 3 printf

## 2. note 知识点

1. unix的设计哲学：一切皆文件
2. 注意函数的参数是输入/输出（in输入 ou输出）

### UNIX系统编程练习项目

1. [Workflow](https://github.com/sogou/workflow/tree/master)
2. [TinyWebServer](https://github.com/qinguoyi/TinyWebServer)
3. cs144

### UNIX系统编程知识库的知识体系

```shell
UNIX 环境开发
- 第一章 UNIX 系统编程简介
- 第二章 文件IO（File and IO）
-- 标准输入输出 (Standard IO) 
-- 文件输入输出(File IO)
-- 文件系统操作 (File System Operations)
-- 错误处理 (Error Handling)
- 第三章 进程（Processes）
- 第四章 线程（Threads）
- 第五章 信号（Signals）
- 第六章 网络编程（Network）
- 第七章 其他主题
- 项目笔记
```