# 变量命名规则
- 可以包含字母、数字、下划线。
- 不能包含逗号、井号、等号或空格。
- 大小写敏感。

### 变量赋值
- 使用 `=` 进行赋值，如 `CC = g++`。
- 变量在 Makefile 中执行时会自动展开。

### 追加变量值
- 使用 `+=` 进行追加，如 `CFLAGS += -g`。

### 修改变量值
- 使用 `=` 覆盖原来的值。
- `override` 关键字用于覆盖变量的值，即使该变量已经在命令行或环境变量中被定义。

### 环境变量
- 可以在命令行中设置环境变量，如 `CC=gcc make`。
- 环境变量可以在 Makefile 中被引用和使用。
- 变量优先级：命令行变量 > `override` 变量 > 环境变量 > Makefile 中定义的变量。

### 目标变量
- 仅在特定目标或模式规则中有效。
- 语法：`target: variable = value` 或 `target-pattern: variable = value`。

### 模式变量
- 用于为匹配特定模式的目标指定变量。
- 语法：`target-pattern: variable = value`。

### 示例 Makefile
```makefile
# 指定编译器
CC = g++

# 编译选项
CFLAGS = -Wall

# 追加调试选项
CFLAGS += -g

# 目标文件
TARGET = main

# 源文件
SRCS = main.c

# 目标文件
OBJS = $(SRCS:.c=.o)

# 默认目标
all: $(TARGET)

# 链接目标文件生成可执行文件
$(TARGET): $(OBJS)
    $(CC) $(CFLAGS) -o $(TARGET) $(OBJS)

# 编译源文件生成目标文件
%.o: %.c
    $(CC) $(CFLAGS) -c $< -o $@

# 清理生成的文件
clean:
    rm -f $(OBJS) $(TARGET)

# 伪目标
.PHONY: all clean
```

### 目标变量和模式变量的应用
- 目标变量允许为不同的目标指定不同的编译选项。
- 模式变量允许为匹配特定模式的文件指定不同的编译选项。
