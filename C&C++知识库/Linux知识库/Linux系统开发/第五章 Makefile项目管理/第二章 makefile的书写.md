### 书写规则
在 Makefile 中，规则由依赖关系和生成目标的方法组成。

#### 规则语法
```makefile
foo.o : foo.c defs.h	# foo模块
    cc -c -g foo.c
```
- `foo.o` 是目标文件。
- `foo.c` 和 `defs.h` 是依赖的源文件。
- `cc -c -g foo.c` 是生成命令，必须以 Tab 键开头。

#### 依赖关系
- 如果 `foo.c` 或 `defs.h` 的修改时间比 `foo.o` 新，或者 `foo.o` 不存在，则触发依赖关系。

#### 命令换行
- 如果命令太长，可以使用反斜杠 `\` 进行换行。

### 通配符
Makefile 支持多种通配符，用于模式匹配：
- `*`：匹配零个或多个字符。
- `?`：匹配单个字符。
- `[...]`：匹配括号内的任意一个字符。

### 文件搜索
对于大型项目，可以使用 `VPATH` 或 `vpath` 来指定源文件的搜索目录。

#### VPATH
- `VPATH` 变量指定一个或多个目录，用于搜索源文件。

#### vpath
- `vpath` 关键字指定特定类型文件的搜索目录。

### 伪目标
伪目标（Phony Targets）不对应实际文件，而用于执行特定命令，如清理构建文件。

#### 声明伪目标
```makefile
.PHONY: clean
```

### 多目标
Makefile 支持生成多个目标。

#### 示例
```makefile
TARGETS = main1 main2

all: $(TARGETS)

main1: $(OBJS1)
    $(CXX) $(CXXFLAGS) -o $@ $(OBJS1)

main2: $(OBJS2)
    $(CXX) $(CXXFLAGS) -o $@ $(OBJS2)

%.o: %.cpp
    $(CXX) $(CXXFLAGS) -c $< -o $@

.PHONY: clean
clean:
    rm -f $(TARGETS) $(OBJS1) $(OBJS2)
```

### 静态模式规则
静态模式规则用于定义一组文件的生成规则。

#### 示例
```makefile
$(TARGETS): %: %.o
    $(CXX) $(CXXFLAGS) -o $@ $<
```

### 自动生成依赖
依赖文件用于描述目标文件与其依赖文件之间的关系。

#### 生成依赖文件
- 使用编译器选项（如 `-MMD`）生成依赖文件。

### 书写命令
在 Makefile 中，使用 `echo` 关键字打印文本消息。

#### 示例
```makefile
$(TARGET): $(OBJS)
    @echo "Linking $@"
    $(CXX) $(CXXFLAGS) -o $(TARGET) $(OBJS)
```

### MAKEFLAGS
`MAKEFLAGS` 是一个环境变量，用于传递选项给 `make` 命令。

### 定义命令包
在 Makefile 中，可以通过变量定义命令包，以避免重复代码。

#### 示例
```makefile
COMPILE_CMD = $(CXX) $(CXXFLAGS) -MMD -c $< -o $@
LINK_CMD = $(CXX) $(CXXFLAGS) -o $(TARGET) $(OBJS)

$(TARGET): $(OBJS)
    @echo "Linking $@"
    $(LINK_CMD)

%.o: %.cpp
    @echo "Compiling $<"
    $(COMPILE_CMD)
```
