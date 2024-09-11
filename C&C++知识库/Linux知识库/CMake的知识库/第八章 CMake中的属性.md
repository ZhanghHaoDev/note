### 属性概述
- 属性附加到特定的实体，如目录、目标、源文件等。
- 属性不同于变量，它们不保存值，而是提供附加信息。

### 通用属性操作
- 使用`set_property()`和`get_property()`来设置和获取属性。

#### 示例
```cmake
# 设置全局属性
set_property(GLOBAL PROPERTY myGlobalProp "hello world")

# 获取全局属性
get_property(myGlobalProp GLOBAL PROPERTY myGlobalProp)
message("myGlobalProp = ${myGlobalProp}")
```

### 通用属性
- `DESCRIPTION`：描述变量的字符串。
- `HIDDEN`：如果设置为TRUE，则变量不会在CMake GUI中显示。
- `ADVANCED`：如果设置为TRUE，则变量被标记为高级选项。
- `CACHEABLE`：如果设置为TRUE，则变量可以被缓存。
- `FORCE`：如果设置为TRUE，则变量会被强制设置为指定的值。
- `INTERNAL`：如果设置为TRUE，则变量不会在CMake GUI中显示，也不会被导出。

### 全局属性
- 全局属性与整体构建相关，例如`CMAKE_BUILD_TYPE`、`CMAKE_INSTALL_PREFIX`。

#### 示例
```cmake
# 获取全局属性
get_cmake_property(buildTypeVar GLOBAL PROPERTY CMAKE_BUILD_TYPE)
message("Build type: ${buildTypeVar}")
```

### 目录属性
- 目录属性位于作用域的全局属性，影响单个目标的属性。
- 目录属性用于设置目标属性的默认值。

#### 示例
```cmake
# 设置目录属性
set_directory_properties(PROPERTIES myDirProp "hello world")

# 获取目录属性
get_directory_property(dirPropVar DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY myDirProp)
message("Directory property: ${dirPropVar}")
```

### 目标属性
- 目标属性直接影响目标如何构建。

#### 示例
```cmake
# 添加可执行文件并设置目标属性
add_executable(hello main.cpp)
set_target_properties(hello PROPERTIES myGlobalProp "hello world")

# 获取目标属性
get_target_property(myGlobalProp hello myGlobalProp)
message("myGlobalProp = ${myGlobalProp}")
```

### 源文件属性
- 源文件属性允许对单个源文件进行细粒度操作。

#### 示例
```cmake
# 设置源文件属性
set_source_files_properties(main.cpp PROPERTIES myGlobalProp "hello world")

# 获取源文件属性
get_source_files_property(myGlobalProp main.cpp myGlobalProp)
message("myGlobalProp = ${myGlobalProp}")
```

### 注意事项
- 属性应该根据需要设置，以确保构建过程的正确性和灵活性。
- 使用`APPEND`选项可以向现有属性值追加值，而不是替换它们。
