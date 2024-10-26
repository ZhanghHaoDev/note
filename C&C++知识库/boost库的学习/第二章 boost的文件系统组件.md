# boost的文件系统组件

## 1. boost的文件系统组件的简介

1. 代码路径：boost_stu/boost_stu
2. 测试路径：boost_stu/test/boost_stu_test
3. 包含的头文件：#include <boost/filesystem.hpp>

### 主要特点
+ 跨平台支持：Boost.Filesystem库支持多种操作系统，包括Windows、Linux和macOS，提供一致的API接口。
+ 丰富的功能：提供了路径操作、文件和目录操作、文件状态查询、目录遍历和符号链接等功能。
+ 易用性：设计简洁，易于使用，适合各种规模的项目。
+ 高效性：通过优化的实现，提供高效的文件系统操作。

### 安装和配置Boost.Filesystem
1. [Boost.Filesystem库的官方文档和教程](https://www.boost.org/doc/libs/1_86_0/libs/filesystem/doc/index.htm#quick_start)
2. 如何在CMake项目中配置Boost.Filesystem库。
    ```cmake
    find_package(Boost REQUIRED COMPONENTS system filesystem)
    target_link_libraries(test Boost::system Boost::filesystem)
    ```
   
## 2. 路径操作

### 2.1 创建路径对象
1. 创建路径对象：使用Boost.Filesystem库中的boost::filesystem::path类来表示文件或目录的路径对象
   使用构造函数将可以窗口路径对象 `boost::filesystem::path p{}`
2. 解析路径：是指从路径对象中提取路径的各个组成部分。
   1. 获取获取文件名: p.filename()
   2. 获取扩展名 p.extension()
   3. 获取父路径 p.parent_path()

## 3. 文件和目录操作
1. 创建目录
    函数原型：
    ```cpp
    bool create_directory(const boost::filesystem::path& p);
    ```
    函数参数：const boost::filesystem::path& p：要创建的目录的路径。

    函数返回值：true创建成功，false失

    boost::filesystem 没有创建单个文件的函数，create_directory 只能用于创建目录

2. 删除目录和文件
    函数原型：bool remove(const boost::filesystem::path& p);
    ```cpp
    bool remove(const boost::filesystem::path& p);
    ```
    函数参数：onst boost::filesystem::path& p：要删除的文件或目录的路径。
    
    函数返回值：true-删除成功，false-删除失败

3. 复制文件
    函数原型：
    ```cpp
    void copy_file(const boost::filesystem::path& from, const boost::filesystem::path& to, boost::filesystem::copy_option option = boost::filesystem::copy_option::fail_if_exists);
    ```
    函数参数：
    ```cpp
    const boost::filesystem::path& from：源文件或目录的路径。
    const boost::filesystem::path& to：目标文件或目录的路径。
    boost::filesystem::copy_option option：复制选项，默认为boost::filesystem::copy_option::fail_if_exists，表示如果目标文件已存在则复制失败。
    ```
    函数返回值：无

4. 复制目录/文件夹
    函数原型：
    ```cpp
    void copy(const boost::filesystem::path& from, const boost::filesystem::path& to, boost::filesystem::copy_option option = boost::filesystem::copy_option::fail_if_exists);
    ```
    函数参数：
    ```cpp
    const boost::filesystem::path& from：源文件或目录的路径。
    const boost::filesystem::path& to：目标文件或目录的路径。
    boost::filesystem::copy_option option：复制选项，默认为boost::filesystem::copy_option::fail_if_exists，表示如果目标文件已存在则复制失败。
    ```
    函数返回值：无

5. 移动文件/目录
   函数原型：
   ```cpp
   void rename(const boost::filesystem::path& from, const boost::filesystem::path& to);
   ```
   函数参数：
   ```cpp
    const boost::filesystem::path& from：源文件或目录的路径。
    const boost::filesystem::path& to：目标文件或目录的路径。
   ```
   函数返回值：无

## 4. 文件状态查询

1. 查询文件或目录是否存在
    函数原型：
    ```cpp
    bool exists(const boost::filesystem::path& p);
    ```
    函数参数：boost::filesystem::path 文件对象

    函数返回值：true-存在，false-不存在

2. 检测是不是目录
    函数原型：
    ```cpp
    bool is_directory(const boost::filesystem::path& p);
    ```
    函数参数：boost::filesystem::path 文件对象

    函数返回值：true-是，false-不是

3. 检测是不是普通文件
   函数原型：
   ```cpp
   bool is_regular_file(const boost::filesystem::path& p);
   ```
   函数参数：boost::filesystem::path 文件对象

   函数返回值：true-是，false-不是

4. 获取文件大小
    函数原型：
    ```cpp
    boost::uintmax_t file_size(const boost::filesystem::path& p);
    ```
    函数参数：boost::filesystem::path 文件对象

    函数返回值：boost::uintmax_t 类型的值，表示文件的大小，单位通常是字节。如果文件不存在或者无法获取文件大小，函数会抛出一个异常，通常是 boost::filesystem::filesystem_error 类型的异常。

## 5. 目录遍历

1. 遍历目录中的文件和子目录 boost::filesystem::directory_iterator
    这个是boost当中的一个类class，如果传入的参数是boost::filesystem::path 文件对象，迭代器将默认返回该目录中的所有文件和子目录。
    ```cpp
    #include <boost/filesystem.hpp>
    #include <iostream>

    namespace fs = boost::filesystem;

    int main() {
        fs::path dir{"example_directory"};

        if (fs::exists(dir) && fs::is_directory(dir)) {
            std::cout << dir << " is a directory containing:\n";
            for (const auto& entry : fs::directory_iterator(dir)) {
                std::cout << entry.path() << '\n';
            }
        } else {
            std::cout << dir << " is not a directory or does not exist.\n";
        }

        return 0;
    }
    ```

2. 递归遍历目录结构 boost::filesystem::recursive_directory_iterator
    这个是boost当中的一个类class，类用于递归遍历目录结构，包括所有子目录中的文件和子目录。
    ```cpp
    #include <boost/filesystem.hpp>
    #include <iostream>

    namespace fs = boost::filesystem;

    int main() {
        fs::path dir{"example_directory"};

        if (fs::exists(dir) && fs::is_directory(dir)) {
            std::cout << dir << " is a directory containing:\n";
            for (const auto& entry : fs::recursive_directory_iterator(dir)) {
                std::cout << entry.path() << '\n';
            }
        } else {
            std::cout << dir << " is not a directory or does not exist.\n";
        }

        return 0;
    }
    ```
3. boost::filesystem::directory_iterator 和 boost::filesystem::recursive_directory_iterator 的区别
    directory_iterator 只遍历当前目录，recursive_directory_iterator 会便利整个目录树，包括子目录

## 6. 符号链接

Boost.Filesystem库提供了用于创建和解析符号链接的功能。符号链接（Symbolic Link）是一种特殊的文件，它包含指向另一个文件或目录的路径。

1. 创建符号链接
    函数原型：
    ```cpp
    void create_symlink(const boost::filesystem::path& to, const boost::filesystem::path& from);
    ```
    函数参数：
    ```cpp
    const boost::filesystem::path& to：符号链接指向的目标路径。
    const boost::filesystem::path& from：符号链接的路径。
    ```

2. 解析符号链接
    函数原型：
    ```cpp
    boost::filesystem::path read_symlink(const boost::filesystem::path& p);
    ```
    函数参数：
    ```cpp
    const boost::filesystem::path& p：符号链接的路径。
    ```
    函数返回值：返回符号链接指向的目标路径。

3. 判断符号链接的目标
    函数原型：
    ```cpp
    bool is_symlink(const boost::filesystem::path& p);
    ```
    函数参数：
    ```cpp
    const boost::filesystem::path& p：要判断的路径。
    ```
    函数返回值：返回 true 表示路径是符号链接。返回 false 表示路径不是符号链接。

## 7. 错误处理

1. 用异常机制处理错误
Boost.Filesystem库中的大多数函数在发生错误时会抛出boost::filesystem::filesystem_error异常。你可以使用标准的C++异常处理机制（try-catch块）来捕获和处理这些异常。

2. 使用boost::system::error_code进行错误处理

Boost.Filesystem库中的许多函数还提供了接受boost::system::error_code参数的重载版本。这些函数在发生错误时不会抛出异常，而是将错误信息存储在error_code对象中。你可以检查error_code对象来确定是否发生了错误。