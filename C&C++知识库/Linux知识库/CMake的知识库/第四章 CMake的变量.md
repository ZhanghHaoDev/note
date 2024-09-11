### 命令的基本规则
- 命令不区分大小写。
- 语句不需要加分号结束。

### message指令
- `message(<MODE> "text")`：输出构建过程中的信息。
- `<MODE>` 的可选值：
  - `FATAL_ERROR`：产生CMake错误，停止编译。
  - `WARNING`：CMake警告，不会打断进程。
  - `AUTHOR_WARNING`：作者警告，通常用于告知开发者注意。
  - `STATUS`：常用命令，查看变量的值，类似于debug。
  - `VERBOSE`：详细输出，通常用于更详细的信息。
  - `NOTICE`、`DEBUG`：分别用于输出重要信息和调试信息。

### CMake中的变量
- **普通变量**：使用 `set()` 和 `unset()` 命令设置和取消。
- **环境变量**：通过 `$ENV{varName}` 获取和设置。
- **缓存变量**：存储在 `CMakeCache.txt` 中，生命周期仅限于CMakeLists.txt文件的处理。

### 变量的作用域
- **函数作用域**：用于自定义函数。
- **目录作用域**：用于 `add_subdirectory()` 指令嵌套目录中的CMakeLists.txt文件。

### 列表操作
- `set(my_list a b c)`：设置列表变量。
- `list(APPEND my_list d)`：向列表添加元素。
- `list(GET my_list 2)`：获取列表指定位置的元素。
- `foreach(item IN LISTS my_list)`：遍历列表。

### CMake中的常用变量
- `CMAKE_SOURCE_DIR`：项目的源代码顶级目录。
- `CMAKE_BINARY_DIR`：项目的构建目录。
- `CMAKE_CURRENT_SOURCE_DIR`：当前处理的源代码目录。
- `CMAKE_CURRENT_BINARY_DIR`：当前处理的构建目录。
- `CMAKE_CXX_COMPILER`：C++ 编译器的路径。
- `CMAKE_CXX_FLAGS`：C++ 编译器的标志。
- `CMAKE_CXX_STANDARD`：C++ 标准的版本。
- `CMAKE_BUILD_TYPE`：构建类型。
- `CMAKE_INSTALL_PREFIX`：安装目录的路径。
- `PROJECT_NAME`、`PROJECT_SOURCE_DIR`、`PROJECT_BINARY_DIR`：由 `project()` 命令设置。

### C++编译器的标志
- `-O0`、`-O1`、`-O2`、`-O3`：设置优化级别。
- `-std=c++11`、`-std=c++14` 等：选择C++标准。
- `-Wall`、`-Wextra`、`-Werror`：控制警告。
- `-g`：生成调试信息。

### 对项目进行分区
- **直接使用路径**：不推荐，因为修改源文件需要更新CMakeLists.txt。
- **使用include命令**：引入外部CMake脚本，但可能导致变量污染。
- **使用add_subdirectory()命令**：推荐方法，可以组织项目结构，避免变量污染。

### add_subdirectory()命令
- `add_subdirectory(source_dir [binary_dir])`：添加子目录，执行子目录中的CMakeLists.txt。

### 与平台相关的变量
- `CMAKE_SYSTEM_NAME`：目标系统的名称。
- `CMAKE_CXX_COMPILER_ID` 和 `CMAKE_CXX_COMPILER_VERSION`：编译器ID和版本。
- `WIN32`、`UNIX`、`APPLE`：预定义的布尔变量，用于检测平台。
- `CMAKE_RUNTIME_OUTPUT_DIRECTORY`：运行时文件的输出目录。
- `find_package` 和 `find_library`：查找包和库。
- `target_link_libraries`：链接库。
- `add_definitions` 和 `add_compile_options`：添加编译器定义和选项。
- `CMAKE_CROSSCOMPILING`：表示是否正在进行交叉编译。

这些补充和整理应该能帮助你更好地理解和使用CMake。如果你有任何具体问题或需要进一步的解释，请随时提问。
