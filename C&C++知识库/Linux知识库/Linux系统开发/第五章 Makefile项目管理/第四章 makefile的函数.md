### 条件判断
Makefile 支持以下条件表达式：
- `ifeq` 和 `ifneq`：用于比较两个字符串是否相等或不等。
- `ifdef` 和 `ifndef`：用于检查变量是否被定义。

#### 示例 Makefile
```makefile
# 检查是否定义了 DEBUG 变量
ifdef DEBUG
    CFLAGS = -g -DDEBUG
else
    CFLAGS = -O2
endif

# 检查是否定义了特定的编译器
ifeq ($(CC), gcc)
    CFLAGS += -Wall
else
    CFLAGS += -Wextra
endif
```

### 函数
Makefile 提供了多种内置函数，用于处理字符串、文件名等。

#### 字符串处理函数
- `subst`：替换字符串中的子串。
- `patsubst`：模式替换。
- `strip`：去除字符串中的前导和尾随空白。
- `findstring`：查找子串。
- `filter` 和 `filter-out`：过滤字符串列表。
- `sort`：排序并去重。
- `word`、`wordlist`、`words`：操作字符串中的单词。
- `firstword` 和 `lastword`：获取第一个或最后一个单词。

#### 文件名处理函数
- `dir`、`notdir`：获取文件的目录或非目录部分。
- `suffix`、`basename`：获取文件的后缀或基本名称。
- `addsuffix`、`addprefix`：添加后缀或前缀。
- `wildcard`：返回符合模式的文件列表。
- `realpath` 和 `abspath`：获取绝对路径。

#### 示例 Makefile 使用函数
```makefile
SOURCES := src/main.c src/utils.c src/helper.c
OBJECTS := $(patsubst %.c,%.o,$(SOURCES))

all: $(TARGET)

$(TARGET): $(OBJECTS)
    $(CC) $(CFLAGS) -o $@ $^

%.o: %.c
    $(CC) $(CFLAGS) -c $< -o $@

clean:
    rm -f $(OBJECTS) $(TARGET)

info:
    @echo "Sources: $(SOURCES)"
    @echo "Objects: $(OBJECTS)"
    @echo "Directories: $(dir $(SOURCES))"
    @echo "File Names: $(notdir $(SOURCES))"
    @echo "Base Names: $(basename $(SOURCES))"
    @echo "Suffixes: $(suffix $(SOURCES))"
    @echo "Absolute Paths: $(abspath $(SOURCES))"
```

### 复杂函数
- `foreach`：对列表中的每个元素执行操作。
- `if`：条件判断。
- `call`：调用用户自定义函数。
- `origin`：确定变量的定义来源。
- `shell`：执行 shell 命令并获取输出。

#### 示例 Makefile 使用复杂函数
```makefile
# 获取当前日期
CURRENT_DATE := $(shell date)

# 定义变量
TARGET := myprogram

all: $(TARGET)

$(TARGET): $(OBJECTS)
    $(CC) $(CFLAGS) -o $@ $^

%.o: %.c
    $(CC) $(CFLAGS) -c $< -o $@

clean:
    rm -f $(OBJECTS) $(TARGET)

info:
    @echo "Current Date: $(CURRENT_DATE)"
```
