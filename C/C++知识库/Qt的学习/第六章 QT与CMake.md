# 第六章 QT与CMake

qt在qt6之后推荐使用CMake来构建程序

1. 安装qt和cmake

CMake的安装非常简单：apt-get install cmake

qt的安装则推荐使用qt官网的安装图形界面来安装，这里不多叙述

如果使用源码构建，使用REMADE文件中的构建方式即可

重点是：将qt的安装目录添加到环境变量里面

1. CMake文件如何编写

这里推荐直接在本地创建一个相同名称的项目，然后使用这个CMake文件即可

1. CMake文件详解

这里对CMake当中qt的设置和一些特殊的变量详细讲解

- set(CMAKE_AUTOUIC ON)：这个选项开启了自动 uic，uic 是 Qt 的用户界面编译器。当这个选项开启时，CMake 会自动找到 .ui 文件（这些文件是 Qt Designer 创建的），并将它们转换为 C++ 代码。
- set(CMAKE_AUTOMOC ON)：这个选项开启了自动 moc，moc 是 Qt 的元对象编译器。在 Qt 中，一些特性（如信号和槽）需要通过 moc 来处理。当这个选项开启时，CMake 会自动找到需要 moc 处理的头文件，并生成相应的 moc 文件。
- set(CMAKE_AUTORCC ON)：这个选项开启了自动 rcc，rcc 是 Qt 的资源编译器。在 Qt 中，可以通过资源文件（.qrc 文件）来嵌入一些资源（如图像、音频等）。当这个选项开启时，CMake 会自动找到 .qrc 文件，并将它们转换为 C++ 代码。

总的来说，这些选项让 CMake 能够自动处理 Qt 的一些特性，使得我们在编写 CMakeLists.txt 文件时，不需要手动处理这些步骤。

- 设置qt库的路径

在 CMake 中设置 Qt 库路径，你可以使用 CMAKE_PREFIX_PATH 变量。这个变量用于指定 find_package 命令搜索包的路径。如果你的 Qt 安装在非标准的位置，你可以设置这个变量来指定 Qt 的路径。

你可以在 CMakeLists.txt 文件中设置这个变量，如下所示：

**代码**

---

set(CMAKE_PREFIX_PATH "/path/to/Qt")

---

或者，你也可以在命令行中设置这个变量，如下所示：

**代码**

---

cmake -DCMAKE_PREFIX_PATH=/path/to/Qt ..

---

在这些命令中，你需要将 "/path/to/Qt" 替换为你的 Qt 安装路径。这个路径应该是 Qt 安装目录

中包含 "bin"、"lib"、"include" 等子目录的那个目录。

注意，如果你在多个地方设置了 CMAKE_PREFIX_PATH，它们会合并在一起，而不是覆盖。这意味着，如果你在 CMakeLists.txt 文件和命令行中都设置了这个变量，CMake 会在所有指定的路径中搜索包。

#