# GDB 调试器使用指南（GDB Debugger Usage Guide）

## GDB 调试器的简介

1. GDB 官网：https://www.sourceware.org/gdb/

### 参考资料

[GDB 官方手册](https://www.gnu.org/software/gdb/documentation/)
[深入理解 GDB](https://www.yuque.com/zhanghao-gnuwf/ah6z1a/bgikpq7bikdwpg0r)

### 添加调试信息

1. 使用gcc 添加调试信息,添加 -g 选项以生成调试信息
    ```shell
    gcc -g -o my_program my_program.c
    ```
2. 使用makefile 添加调试信息,可以在编译选项中添加 -g 选项，以确保生成的可执行文件包含调试信息
    ```makefile
    CC = gcc
    CFLAGS = -g

    all: my_program

    my_program: my_program.o
        $(CC) $(CFLAGS) -o my_program my_program.o

    my_program.o: my_program.c
        $(CC) $(CFLAGS) -c my_program.c

    clean:
        rm -f my_program my_program.o
    ```
3. 使用cmake 添加调试信息,可以设置构建类型为 Debug，以确保生成的可执行文件包含调试信息。
    ```cmake
    cmake_minimum_required(VERSION 3.10)
    project(MyProject)
    set(CMAKE_CXX_STANDARD 11)
    # 设置构建类型为 Debug
    set(CMAKE_BUILD_TYPE Debug)
    # 添加调试信息选项
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g")
    add_executable(my_program my_program.cpp)
    ```

## 2. GDB 的安装

- 在基于 Debian 的 Linux 发行版上，可以使用以下命令安装 GDB：
  ```bash
  sudo apt-get install gdb
  ```

## 3. GDB 常用命令

#### 常用 GDB 命令
| 序号 | 命令 | 解释 | 示例 |
|------|------|------|------|
| 1    | run  | 启动程序 | `run` |
| 2    | break | 设置断点 | `break main.c:10` |
| 3    | delete | 删除断点 | `delete 1` |
| 4    | info | 查看断点信息 | `info breakpoints` |
| 5    | step | 逐行执行 | `step` |
| 6    | next | 逐过程执行（不进入函数内部） | `next` |
| 7    | continue | 继续执行 | `continue` |
| 8    | print | 查看变量 | `print var` |
| 9    | info locals | 查看所有局部变量 | `info locals` |
| 10   | set var = value | 修改变量 | `set var = value` |
| 11   | backtrace | 查看调用堆栈 | `backtrace` |
| 12   | quit | 退出 gdb | `quit` |

### 详细的介绍

1. **设置调试信息**：
   ```sh
   gcc -g main.c -o main
   ```
   `-g` 选项告诉GCC生成调试信息。

2. **开始调试**：
   ```sh
   gdb ./main
   ```
   或者直接使用 `gdb` 命令后跟可执行文件名。

3. **列举源码**：
   ```sh
   list [行号/函数名]
   ```
   显示当前行号或函数名的源代码。

4. **设置断点**：
   ```sh
   break [行号/函数名]
   ```
   在指定的行号或函数名处设置断点。

5. **运行程序**：
   ```sh
   run [参数]
   ```
   运行程序，可以传递参数给程序。

6. **单步执行**：
   ```sh
   next / n
   ```
   执行下一条指令，不进入函数内部。

   ```sh
   step / s
   ```
   执行下一条语句，进入函数内部。

7. **输出变量值**：
   ```sh
   print / p [变量名]
   ```
   输出变量的值。

8. **退出调试**：
   ```sh
   quit / q
   ```
   退出GDB。

9. **处理段错误**：
   当程序崩溃并显示段错误时，GDB会自动停止。使用 `list` 命令查看当前代码位置，`backtrace / bt` 查看调用栈。

10. **查看断点**：
    ```sh
    info breakpoints / info b
    ```
    查看所有设置的断点。

11. **结束当前函数调用**：
    ```sh
    finish
    ```
    执行到当前函数结束。

12. **查看栈帧**：
    ```sh
    backtrace / bt
    ```
    查看当前的调用栈。


### 调试技巧：

- **条件断点**：可以为断点设置条件，只有满足条件时才会停止。
  ```sh
  break [行号/函数名] if [条件表达式]
  ```

- **观察点**：可以监视变量的值，当变量值改变时程序会停止。
  ```sh
  watch [变量名]
  ```
- **反向跟踪**：在程序崩溃后，可以使用反向跟踪（backtrace）查看函数调用栈。

- **信号处理**：可以设置GDB处理或忽略特定信号。

- **多线程调试**：如果程序是多线程的，可以使用 `info threads` 查看所有线程，`thread [线程号]` 切换当前线程。

- **寄存器查看**：可以使用 `info registers` 查看CPU寄存器的状态。

- **内存查看**：可以使用 `x` 命令查看内存内容。

