# GCC 编译器使用指南（GCC Compiler Usage Guide）

## 1. gcc 编译器的简介

1. gcc 官网：https://gcc.gnu.org

### GCC的主要特点

1. **多语言支持**：支持C、C++、Fortran等多种语言。
2. **跨平台**：可在多种操作系统和硬件上运行。
3. **优化**：提供多种优化选项。
4. **开源**：基于GPL发布。
5. **扩展性**：支持插件和扩展。

### GCC的安装

在基于Debian的系统上，使用以下命令安装GCC：

```sh
sudo apt-get install gcc
sudo apt-get install g++
```

## 2. GCC编译过程

1. **预处理（Preprocessing）**
   - 命令：`gcc -E`
   - 任务：处理宏定义、文件包含、条件编译，删除注释和空白。

2. **编译（Compilation）**
   - 命令：`gcc -S`
   - 任务：将预处理后的文件转换成汇编语言文件，并进行语法检查。

3. **汇编（Assembly）**
   - 命令：`gcc -c`
   - 任务：将汇编语言文件转换成机器代码，生成目标文件。

4. **链接（Linking）**
   - 命令：`gcc`
   - 任务：将目标文件与库文件链接，生成可执行文件。

## 3. GCC常用指令选项

- `-ansi`：仅支持ANSI C标准。
- `-c`：仅编译生成目标文件。
- `-DMACRO`：定义宏。
- `-DMACRO=DEFN`：定义宏并赋值。
- `-E`：仅运行预处理器。
- `-g`：生成调试信息。
- `-IDIRECTORY`：添加头文件搜索路径。
- `-LDIRECTORY`：添加库文件搜索路径。
- `-lLIBRARY`：链接指定库。
- `-m486`：针对486处理器优化。
- `-o FILE`：指定输出文件名。
- `-O0`：无优化。
- `-O`/`-O1`：基本优化。
- `-O2`：高级优化。
- `-O3`：最高级别优化。
- `-shared`：生成共享库。
- `-static`：禁止使用共享库。
- `-UMACRO`：取消宏定义。
- `-w`：关闭警告。
- `-Wall`：打开所有警告。
- `-std=standard`：指定C语言标准。
- `-pedantic`：严格按照标准编译。
- `-Wextra`：额外警告。
- `-Werror`：警告视为错误。
- `-fPIC`/`-fpic`：生成位置无关代码。
