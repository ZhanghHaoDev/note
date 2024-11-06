# UNIX系统编程的简介

## 1. UNIX系统编程的简介

1. 代码仓库：unix_stu
2. 测试仓库：unix_stu/test
3. Linux操作系统note：Linux系统操作知识库/Linux的学习
4. 开发环境：操作系统：macOS，编辑器：VSCode，构建工具：CMake，编译器：llvm

### note 知识点
1. unix的设计哲学：一切皆文件
2. 注意函数的参数是输入/输出（in输入 ou输出）

### 参考资料

1. C程序设计语言
2. UNIX环境高级编程
3. UNIX网络编程 卷1：套接字联网API（第3版）
4. TCPIP详解 卷1：协议（原书第2版） 
5. TCPIP高效编程 改善网络程序的44个技巧 
6. Linux高性能服务器编程
7. 深入理解计算机系统（csapp）

### UNIX系统编程练习项目

1. [使用 C 语言构建终端文本编辑器](https://confucianzuoyuan.github.io/build-your-own-text-editor/)
2. 简易的网络聊天室
3. 简易的文件传输工具
4. [Workflow](https://github.com/sogou/workflow/tree/master)
5. [TinyWebServer](https://github.com/qinguoyi/TinyWebServer)

### man 帮助手册

1. 在unix系统当中，我们可以使用man查看系统手册，man系统手册提供了系统命令，库函数，配置文件等详细信息
2. man 常用的章节
   + 用户命令：常用的用户命令。
   + 系统调用：内核提供的系统调用。
   + 库函数：C 标准库函数。
   + 特殊文件：设备文件和特殊文件。
   + 文件格式：文件格式和约定。
   + 游戏：游戏和演示程序。
   + 杂项：杂项信息。
   + 系统管理命令：系统管理员使用的命令。
   + 内核例程：内核例程。
3. 使用例子
    ```shell
    # 查看系统命令帮助
    man ls
    # 查看库函数手册
    man 3 printf
    ```

## 2. UNIX系统编程知识库的知识体系

```shell
UNIX 环境开发
- 第一章 UNIX 系统编程简介
- 第二章 UNIX 系统编程的基础知识
- 第三章 文件IO（File and IO）
-- 标准输入输出 (Standard IO) 
-- 文件输入输出(File IO)
-- 文件系统操作 (File System Operations)
-- 错误处理 (Error Handling)
- 第四章 进程（Processes）
- 第五章 线程（Threads）
- 第六章 信号（Signals）
- 第七章 网络编程（Network）
- 第八章 其他主题
- 项目笔记
```