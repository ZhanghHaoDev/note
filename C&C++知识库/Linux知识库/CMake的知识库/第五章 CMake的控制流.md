### 控制结构

#### if语句条件块
- `if(<condition>)`：条件块，必须以 `endif()` 结束。
- 支持 `elseif()` 和 `else()` 块。
- 条件可以是常数、变量、逻辑运算符（`NOT`, `AND`, `OR`）。

#### 逻辑运算符
- `NOT`, `AND`, `OR`：用于构建复杂的条件表达式。
- 布尔值：`true`（ON, YES, TRUE, Y, 非零数字）和 `false`（OFF, NO, FALSE, N, NOTFOUND, 空字符串, 零）。

#### 循环语句
- `while(<condition>)`：当条件为真时重复执行命令，以 `endwhile()` 结束。
- `foreach(<loop_var> IN <list>)`：遍历列表中的每个元素，以 `endforeach()` 结束。
- `break()`：跳出循环。
- `continue()`：跳至下一个迭代。

### 定义指令

#### macro() 宏
- 类似于查找和替换，不会创建调用堆栈条目。
- 语法：`macro(<name> [<argument>...]) <commands> endmacro()`

#### function() 函数
- 为本地变量创建独立作用域。
- 语法：`function(<name> [<argument>...]) <commands> endfunction()`

### 指令部分

#### include() 指令
- 将CMake代码划分到单独文件中，通过 `include()` 引用。
- 语法：`include(<file|module> [OPTIONAL] [RESULT_VARIABLE <var>])`

#### include_guard() 指令
- 限制文件只包含一次。
- 语法：`include_guard([DIRECTORY|GLOBAL])`

#### file() 指令
- 用于文件的读取、写入和传输。
- 语法：`file(READ|WRITE|APPEND|DOWNLOAD ...)`

#### execute_process() 指令
- 运行系统命令并收集输出。
- 语法：`execute_process(COMMAND <cmd1> [<arguments>...] [OPTIONS])`

### 计算类型

#### 布尔类型
- 由1（真）和0（假）表示。

#### 逻辑运算符
- `$<NOT:arg>`, `$<AND:arg1,arg2>`, `$<BOOL:string_arg>`：逻辑运算。

#### 字符串比较
- `$<STREQUAL:arg1,arg2>`, `$<EQUAL:arg1,arg2>`, `$<IN_LIST:arg,list>`：字符串比较。

#### 查询变量
- `$<TARGET_EXISTS:arg>`, `$<CONFIG:args>`, `$<PLATFORM_ID:args>`, `$<LANG_COMPILER_ID:args>`：查询变量。

#### 字符串求值
- `$<CONFIG>`, `$<PLATFORM_ID>`：配置和平台ID。

#### 查询依赖目标
- `$<TARGET_NAME_IF_EXISTS:target>`, `$<TARGET_FILE:target>`, `$<TARGET_FILE_NAME:target>`：查询目标属性。

