# 关于cmake中引入第三方库

这个也是下一步cmake学习的目标：
在编写c/c++代码的时候，尽量使用cmake，不管是Linux还是Windows，或者mac

从单个源文件，到多个源文件（包括头文件），再到调用库文件，算是学习cmake的一个阶段
cmake包括很多的内容，还包括项目的测试，文档等内容，在熟练的掌握cmake以及可以在工作中使用cmake，后再去进阶的使用cmake

构建出完整的工具链，c/c++源码，cmake构建项目，gcc/g++编译项目，gdb/winDbg调试项目

我们在cmake中是可以调用第三方库的，一般有两种方法

1. 在cmake构建的时候，使用网络下载第三方库
2. 下载第三库到本地，编译好库以后在源码中引入

# 第一种方法（需要网络）

第一种方法是最简单的，我们可以使用库的GitHub仓库来进行构建我们的项目，具体的方法还未知。

我们还可以使用包管理器，微软推出的vcpkg c++包管理器，是全平台通用的，在Windows，Linux以及Macos上都支持vcpkg。
使用方法：在Windows上我们可以使用命令行来查找，安装，升级包。vcpkg安装的包是可以编译好的，包括32位和64位都可以自定义安装，他还支持vs系列和clion系列的IDE，

我们这里讲cmake对vcpkg的支持，在使用cmake的时候，可以通过编写cmakelists.txt的方法来调用构建第三方库，具体代码或实例，可以搜集整理。

还有clion种结合cmake和vcpkg来调用库，这种最为简单。开发的时候，使用vcpkg来下载安装，编译第三方库，然后在源码当中调用该库文件，最后使用cmake添加该库（头文件，库文件，包）。同时Clion是IDE，我们还可以对代码进行调试和修改。

# 第二种方法（推荐使用）

推荐使用第二种方法，万一遇到没网的情况，还可以使用库源码构建

在使用第三方库的时候，注意记录

在使用cmake构建的时候，第三方库需要添加头文件和库文件，但是在cmake中还需要添加该库的包
注意搜集记录

我记得还有一种方法是库文件一般带有以.cmake为后缀结尾的文件，这个文件引入cmakelists也可以进行构建

在对源码进行构建的时候，如果源码对平台都支持，我们可以自定义该库的位置等信息