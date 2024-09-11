### 生成器表达式的定义
- 生成器表达式用于在构建时动态计算值。
- 语法：`$<...expression...>`

### 常见的生成器表达式
- `$<TARGET_PROPERTY:target,prop>`：获取目标属性的值。
- `$<TARGET_FILE:target>`：获取目标文件的路径。
- `$<TARGET_OBJECTS:target>`：获取目标对象文件的路径。
- `$<TARGET_LINKER_FILE:target>`：获取目标链接器文件的路径。
- `$<TARGET_LINK_LIBRARIES:target>`：获取目标链接的库的名称。
- `$<CONFIG>`：获取当前构建配置的名称。
- `$<PLATFORM_ID>`：获取当前平台的标识符。
- `$<C_COMPILER_ID>`：获取当前C编译器的标识符。
- `$<CXX_COMPILER_ID>`：获取当前C++编译器的标识符。

### 示例：使用生成器表达式
```cmake
add_executable(myTarget main.cpp)
target_link_libraries(myTarget $<TARGET_LINK_LIBRARIES:myLib>)
```
在这个示例中，`$<TARGET_LINK_LIBRARIES:myLib>` 表达式用于获取 `myLib` 目标链接的库的名称。

### 基本信息表达式
- 基本信息表达式用于在构建时动态计算基本信息。

### 示例：基本信息表达式
```cmake
add_executable(myTarget main.cpp)
target_compile_options(myTarget PRIVATE $<$<CONFIG:Debug>:-g>)
```
在这个示例中，`$<CONFIG>` 表达式用于获取当前构建配置的名称，并在Debug配置中添加 `-g` 编译选项。

### 实用信息表达式
- 实用信息表达式用于在构建时动态计算实用信息。

### 示例：实用信息表达式
```cmake
add_executable(myTarget main.cpp)
target_link_libraries(myTarget $<TARGET_LINK_LIBRARIES:myLib>)
```
在这个示例中，`$<TARGET_LINK_LIBRARIES:myLib>` 表达式用于获取 `myLib` 目标链接的库的名称。

### 注意事项
- 生成器表达式只能在某些上下文中使用，如目标属性、源文件属性和编译选项。
- 生成器表达式不能在CMake脚本中的所有命令中使用，如 `set()` 或 `if()` 命令。
- 生成器表达式通常与 `target_compile_options()`、`target_include_directories()`、`target_link_libraries()` 等命令一起使用。