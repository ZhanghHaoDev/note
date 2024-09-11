### 基本概念
- CMake函数通过`function`和`endfunction`命令定义。
- 函数名必须以字母开头，可包含字母、数字和下划线。
- 函数名不能包含空格或其他特殊字符。
- 函数名应该是唯一的，不与其他函数或变量重名。

### CMake函数参数
- 函数可以接受零个或多个参数。
- 参数用于传递数据或配置函数行为。
- 函数参数可以是任何CMake表达式。

### 特殊参数
- `ARGN`：包含所有未命名的参数。
- `ARGV`：包含所有传递给函数的参数。
- `UNPARSED_ARGUMENTS`：包含所有未解析的参数。

### 作用域
- CMake函数引入了变量作用域。
- 函数内部变量的修改不会影响到函数外部。
- 使用`PARENT_SCOPE`可以在函数内部修改外部变量。

### return()指令
- `return()`用于提前结束函数。
- `return()`不返回值，只返回父作用域。

### 指令重载
- CMake不支持函数重载。
- 应使用不同的函数名称或可选参数来实现类似功能。

### CMake函数中的特殊变量
- `ARGV`：包含所有传递给函数的参数。
- `ARGN`：包含所有未命名的参数。
- `CMAKE_CURRENT_LIST_FILE`：包含当前正在处理的CMake文件的完整路径。

### 示例
```cmake
# 定义一个函数，接受一个参数
function(hello name)
  message("Hello, ${name}!")
endfunction(hello)

# 调用函数
hello("John")  # 输出: Hello, John!

# 定义一个函数，使用特殊参数ARGN
function(greet)
  message("All arguments: ${ARGV}")
  message("Unnamed arguments: ${ARGN}")
endfunction(greet)

greet("John" "Doe" "a" "b")  # 输出: All arguments: John Doe a b
                             # 输出: Unnamed arguments: a b

# 使用PARENT_SCOPE在函数内部修改外部变量
function(set_names)
  set(first_name "John" PARENT_SCOPE)
  set(last_name "Doe" PARENT_SCOPE)
endfunction(set_names)

set_names()
message("First name: ${first_name}, Last name: ${last_name}")
# 输出: First name: John, Last name: Doe
```

### 注意事项
- 确保函数名唯一，避免与现有变量或函数重名。
- 函数参数和特殊参数应该在函数定义时明确。
- 使用`PARENT_SCOPE`时，确保外部变量已存在或在函数外部定义。
