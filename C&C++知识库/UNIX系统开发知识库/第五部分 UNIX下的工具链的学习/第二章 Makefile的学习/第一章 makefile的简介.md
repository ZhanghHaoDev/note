# 环境搭建
在 Linux 系统上，通常需要安装以下工具来构建 C/C++ 项目：
- **gcc**：GNU 编译器集合，用于编译 C 语言程序。
- **g++**：GNU 编译器集合，用于编译 C++ 程序。
- **make**：自动化构建工具，用于编译和链接程序。

安装命令：
```bash
sudo apt-get install gcc
sudo apt-get install g++
sudo apt-get install make
```

安装完成后，可以通过以下命令检查版本信息：
```bash
gcc -v
g++ -v
make -v
```

### Makefile 规则
Makefile 定义了如何构建程序，包括目标文件、依赖关系和构建命令。一个基本的 Makefile 规则如下：
```makefile
target : prerequisites
    command
```
- **target**：目标文件，可以是对象文件或可执行文件。
- **prerequisites**：生成目标文件所需的文件或目标。
- **command**：生成目标时需要执行的命令。

### Makefile 的文件名
- 默认情况下，`make` 会查找 `GNUmakefile`、`makefile` 或 `Makefile`。通常使用 `Makefile` 作为文件名。

### Make 的工作方式
1. 读入所有的 Makefile。
2. 读入被 `include` 的其他 Makefile。
3. 初始化文件中的变量。
4. 推导隐晦规则，分析所有的规则。
5. 为所有的目标文件创建依赖关系链。
6. 根据依赖关系，决定哪些目标需要重新生成。
7. 执行生成命令。

### Makefile 包含的内容
- **显示规则**：明确指定如何生成目标文件。
- **隐晦规则**：由 `make` 自动推导的规则。
- **变量定义**：在 Makefile 中定义变量，类似于 C 语言中的宏。
- **文件指示**：包括 `include` 指令和其他文件指示。
- **注释**：使用 `#` 字符进行注释。

### 引用其他 Makefile
在 Makefile 中使用 `include` 关键字来包含其他 Makefile 文件：
```makefile
include math.mk
```

### Makefile 示例
```makefile
# 源文件
SRCS = main.c

# 目标文件
OBJS = $(SRCS:.c=.o)

# 库文件
LIBRARY = math/libmath.a

# 默认目标
all: $(TARGET)

# 链接目标文件生成可执行文件
$(TARGET): $(OBJS) $(LIBRARY)
    $(CC) $(CFLAGS) -o $(TARGET) $(OBJS) -Lmath -lmath

# 编译源文件生成目标文件
%.o: %.c
    $(CC) $(CFLAGS) -c $< -o $@

# 清理生成的文件
clean:
	rm -f $(TARGET)
```

### 注意事项
- 在 Makefile 中，空格和制表符的使用有严格规定：
  - 变量赋值和规则定义可以使用空格。
  - 命令行前的缩进必须使用制表符（Tab），不能使用空格。
