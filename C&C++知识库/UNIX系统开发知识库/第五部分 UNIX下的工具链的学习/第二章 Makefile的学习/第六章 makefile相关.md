# 1. 简单的Makefile

```makefile
CROSS_COMPILE=/opt/4.5.1/bin/arm-linux-
CC=$(CROSS_COMPILE)gcc
AS=$(CROSS_COMPILE)as
LD=$(CROSS_COMPILE)ld

CFLAGS=-g -Wall
LIBS=-lpthread

all: main

main: main.o gsm_gprs.o socket.o telosb.o wifi.o
    $(CC) $(CFLAGS) $(LIBS) $^ -o $@

main.o: main.c gsm_gprs.h option.h telosb.h
    $(CC) $(CFLAGS) -c $<

gsm_gprs.o: gsm_gprs.c gsm_gprs.h socket.h
    $(CC) $(CFLAGS) -c $<

socket.o: socket.c socket.h option.h
    $(CC) $(CFLAGS) -c $<

telosb.o: telosb.c telosb.h option.h
    $(CC) $(CFLAGS) -c $<

wifi.o: wifi.c wifi.h option.h
    $(CC) $(CFLAGS) -c $<

clean:
    -rm -f main *.o *~ *~
.PHONY: clean
```

# 2. Makefile赋值

- `=`：基本的赋值，赋值在Makefile的最后进行。
- `:=`：覆盖之前的值，赋值会立即进行。
- `?=`：如果没有赋值过就赋值。
- `+=`：在已有值的基础上添加值。

# 3. 伪目标

- `.PHONY`：用于定义伪目标，即使存在同名文件也不会被当作文件目标。

# 4. Makefile内建函数

- `$(subst from,to,text)`：替换文本中的字符串。
- `$(patsubst pattern,replacement,text)`：根据模式替换文本。
- `$(strip string)`：去掉字符串两端的空格。
- `$(findstring find,in)`：在字符串中查找子字符串。
- `$(filter pattern…,text)`：过滤文本，只保留匹配模式的部分。
- `$(filter-out pattern…,text)`：过滤文本，删除匹配模式的部分。
- `$(sort list)`：对文本列表进行排序。
- `$(word n,text)`：取字符串列表的第n个元素。
- `$(wordlist s,e,text)`：取字符串列表的指定范围。
- `$(words text)`：返回文本中的单词数量。
- `$(firstword names…)`：取第一个单词。
- `$(lastword names…)`：取最后一个单词。

# 5. 文件名处理函数

- `$(dir names…)`：取文件的目录部分。
- `$(notdir names…)`：取文件名，不包括目录部分。
- `$(suffix names…)`：取文件的后缀。
- `$(basename names…)`：取文件的基本名，不包括目录和后缀。

# 6. 添加后缀和前缀

- `$(addprefix prefix,names…)`：给列表中的每个元素添加前缀。
- `$(addsuffix suffix,names…)`：给列表中的每个元素添加后缀。

# 7. 连接函数

- `$(join list1,list2)`：将两个列表连接起来。

# 8. 通配符函数

- `$(wildcard pattern)`：根据模式匹配文件名。

# 9. 真实路径

- `$(realpath names…)`：获取文件的真实路径。
- `$(abspath names…)`：获取文件的绝对路径。

# 10. foreach函数

- `$(foreach var,list,text)`：对列表中的每个元素执行文本替换。

# 11. if函数

- `ifeq (arg1, arg2)`：如果两个参数相等则为真。
- `ifneq (arg1, arg2)`：如果两个参数不等则为真。
- `ifdef variable-name`：如果变量已定义则为真。
- `ifndef variable-name`：如果变量未定义则为真。

# 12. call函数

- `$(call VARIABLE,PARAM,PARAM,...)`：调用变量作为函数。

# 13. value函数

- `$(value variable)`：获取变量的值，不进行扩展。

# 14. realpath函数

- `$(realpath ../../)`：获取相对路径的绝对路径。

# 15. wildcard函数

- `$(wildcard *.c)`：获取所有`.c`文件。

# 16. origin函数

- `$(origin variable)`：获取变量的来源。

# 17. shell函数

- `$(shell command)`：执行shell命令并返回输出。

# 18. make LOG以及控制函数

- `$(info text)`：打印信息。
- `$(warning text)`：打印警告信息。
- `$(error text)`：打印错误信息并退出。

# 补充知识

- **自动变量**：`$@`（目标文件）、`$<`（第一个依赖文件）、`$^`（所有依赖文件）。
- **模式规则**：使用`%`符号定义规则，可以匹配多个文件。
- **静态模式规则**：使用`%`符号定义规则，但生成目标文件时使用`$@`。
- **伪目标**：`.PHONY`用于声明伪目标，防止与同名文件冲突。
- **VPATH**：设置文件搜索路径。
- **FIND**：查找文件系统目录中的文件。
- **MAKEFLAGS**：传递给递归make调用的标志。

通过这些Makefile的特性和函数，你可以编写出功能强大、灵活的Makefile，以自动化构建过程。
