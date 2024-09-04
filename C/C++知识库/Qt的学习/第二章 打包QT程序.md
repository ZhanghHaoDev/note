# 第二章 打包QT程序

# Linux下打包qt程序有两种方法：1. cpacke 2. linuxdeployqt

这里先介绍第二种方法：使用linuxdeployqt

1. linuxdeployqt的简介

在Linux下打包Qt程序，你可以使用linuxdeployqt工具。这个工具可以自动收集你的Qt应用程序需要的

库和插件，并将它们打包到一个单独的目录中。

1. 下载linuxdeployqt
2. 使用wget下载

wget [https://github.com/probonopd/linuxdeployqt/releases/download/continuous/linuxdeployqt-continuous-x86_64.AppImage](https://github.com/probonopd/linuxdeployqt/releases/download/continuous/linuxdeployqt-continuous-x86_64.AppImage)

1. 增加文件权限

chmod a+x linuxdeployqt-continuous-x86_64.AppImage

1. 复制到系统目录下面，让该工具在任何地方都可以运行

可以复制该文件到/usr/local/bin/或/usr/bin/目录

1. linuxdeployqt 支持的glibc版本为2.31，我们这里可以使用ldd --version来查看glibc的版本

但是这里打包软件的适合会遇到一个问题，输出glic版本太高，所以这里建议直接下载重新编译该软件，把main函数当中的一段判断glibc的代码注释掉就可以

git clone [https://github.com/probonopd/linuxdeployqt.git](https://github.com/probonopd/linuxdeployqt.git)

把main函数当中的这段代码注释掉就可以

//if (strverscmp (glcv, "2.32") >= 0) {

//    qInfo() << "ERROR: The host system is too new.";

//    qInfo() << "Please run on a system with a glibc version no newer than what comes with the oldest";

//    qInfo() << "currently supported mainstream distribution (Ubuntu Focal Fossa), which is glibc 2.31.";

//    qInfo() << "This is so that the resulting bundle will work on most still-supported Linux distributions.";

//    qInfo() << "For more information, please see";

//    qInfo() << "[https://github.com/probonopd/linuxdeployqt/issues/340](https://github.com/probonopd/linuxdeployqt/issues/340)";

//    return 1;

//}

---

然后在qmake构建。make编译，make install安装即可

1. 如何创建一个qt程序的包
2. 添加qt的环境变量，需要添加的环境变量包括

export PATH=/home/wah/Qt5.15.0/gcc_64/bin:$PATH

export LD_LIBRARY_PATH=/home/wah/Qt5.15.0/gcc_64/lib:$LD_LIBRARY_PATH

export QT_PLUGIN_PATH=/home/wah/Qt5.15.0/gcc_64/plugins:$QT_PLUGIN_PATH

export QML2_IMPORT_PATH=/home/wah/Qt5.15.0/gcc_64/qml:$QML2_IMPORT_PATH

1. 将可执行的二进制文件复制到一个新的目录下面，确保程序可以双击执行和命令行下执行
2. 执行命令：linuxdeployqt APPNAME -bundle-non-qt-libs -appimage
3. 缺少库的错误：复制开发环境下的库，到lib目录下面就可以
4. 缺少xcb的错误：排查问题，1. 查看lib目录下面有没有xcb*，2. 查看/home/gzb/pack/plugins/platforms/目录下面有没有xcb*，3. ldd查看程序相应的依赖有没有被找到ldd ./myapp 4. 查看/home/gzb/pack/plugins/platforms/目录下的libqxcb.so依赖有没有被找到 ldd libqxcb.so 5. 查看ldd /path/to/your/libs/libxcb-cursor.so.0依赖有没有被找到。我这里遇到的问题是缺少libX11-xcb.so.1，将相应的文件复制到lib目录下面就可以解决问题
5. 缺少字体错误，首先需要下载字体，注意下载ttf格式的字体，ttc格式的字体不一定支持

然后在main函数当中添加设置字体

//字体

int fontId =QFontDatabase::addApplicationFont("./font/AlibabaPuHuiTiRegular.ttf");

if (fontId != -1) {

QFontfont("Noto Sans CJK SC");

app.setFont(font);

qDebug()<< "Font loaded successfully.";

} else {

qDebug()<< "Failed to load font.";

}

---

1. glibc库的版本问题

具体问题是：运行程序，运行不起来，然后会遇到一个glibc版本的问题

验证glibc版本：ldd --version

解决办法：在目标系统上重新编译和打包

原因：linuxdeployqt工具打包的程序，不可能解决所有的Linux发行版版本问题，暂时没有一个好的解决办法，一次编译所有地方运行还不行

1. linuxdeployqt工具的参数都有那些

linuxdeployqt工具有很多参数可以用来定制你的应用程序的打包过程。以下是一些常用的参数：

- appimage：创建一个AppImage文件。AppImage是一种可以在任何Linux发行版上运行的可执

行文件格式。

- bundle-non-qt-libs：包含非Qt的系统库。这可以确保你的应用程序在没有这些库的系统上运

行。

- exclude-libs=<libs>：排除某些库。你可以使用这个参数来排除你不想包含在你的应用程序中

的库。

- extra-plugins=<plugins>：包含额外的Qt插件。你可以使用这个参数来包含你的应用程序需要

的Qt插件。

- no-plugins：不包含任何Qt插件。
- no-strip：不剥离库和可执行文件的符号。这可以使你的应用程序更容易调试，但会增加文件

大小。

- qmake=<path>：指定qmake的路径。如果你的系统上有多个版本的Qt，你可以使用这个参数

来选择你想使用的版本。

- verbose=<level>：设置详细输出级别。你可以使用这个参数来获取更多的信息，以帮助你解决问题。

你可以在终端中运行linuxdeployqt -help命令来获取完整的参数列表和详细的使用说明。

1. 目前只测试过ssh工具：MobaXterm可以显示qt界面
2. 输入中文的问题，程序无法输入中文

暂时没有离线的方案，可以在Windows上输入中文，然后复制过去

# 在Windows上我们使用QT自带的打包工具：windeployqt

该工具位于qt安装目录中的bin目录下面，在命令行模式下使用

这个工具可以自动收集你的Qt应用程序需要的所有依赖项，包括Qt库、插件、QML文件等。

下面是使用该工具的基本步骤：

1. 首先，你需要编译你的Qt应用程序。确保你的应用程序在Release模式下编译，因为Debug模式下的应用程序需要额外的debug库，这些库通常不包含在用户的计算机上。
2. 打开命令提示符，然后导航到你的应用程序的可执行文件所在的目录。
3. 运行windeployqt工具。如果你的Qt安装目录已经添加到你的PATH环境变量，你可以直接运行windeployqt。否则，你需要提供windeployqt.exe的完整路径。你需要将你的应用程序的可执行文件作为windeployqt的参数。

下面是一个基本的实例命令：

C:\Qt\5.15.2\msvc2019_64\bin\windeployqt.exe --release --qmldir C:\path\to\your\qml\files yourapp.exe

---

这个命令会在你的应用程序的可执行文件所在的目录创建一个部署目录，其中包含你的应用程序需要的所有依赖项。

第一个参数是windeployqt位置

第二个参数是只包含release库

第三个参数和第四个参数是qml，如果程序没有则不需要添加

第五个参数是开发的程序

1. 最后，你可以将你的应用程序的可执行文件以及部署目录中的所有文件打包到一个zip文件或者安装程序中，然后分发给你的用户。

遇到的问题

1. windeployqt，如何在任何地方使用

将windeployqt所在的目录添加到环境变量

1. 编译后的程序无法双击启动，报找不到程序入口

这里首先需要确保程序可以在编译目录下面双击启动，然后再打包程序

问题可能是系统环境变量存在多个qt的版本或者编译器，这里删除其他的就可以

1. 记得把可执行文件单独放到一个目录下面
2. 找不到qt插件的位置,Unable to find the platform plugin.
3. 不能识别中文路径的错误，中文显示乱码

这里使用的是mingw编译器，Windows下的gcc，因为gcc只能识别ASCII码，所以中文显示乱码

解决办法：1. 更换编译器，使用msvc编译器，或者clang

1. Unable to find the platform plugin.找不到插件

暂时没有解决办法

我这里打包debug的时候没有错误，打包release的时候报错

windeployqt 是一个用于部署 Qt 应用程序的工具，它有很多参数可以用来定制部署过程。以下是一些常用的参数：

- -release：部署用于发布（Release）版本的库和插件。
- -debug：部署用于调试（Debug）版本的库和插件。
- -qmldir <dir>：指定 QML 文件的目录，windeployqt 会从这个目录复制 QML 文件。
- -no-compiler-runtime：不部署编译器运行时库。默认情况下，windeployqt 会部署这些库。
- -no-translations：不部署翻译文件。默认情况下，windeployqt 会部署这些文件。
- -no-system-d3d-compiler：不部署系统的 D3D 编译器。默认情况下，windeployqt 会部署这个编译器。
- -no-opengl-sw：不部署软件 OpenGL 渲染器。默认情况下，windeployqt 会部署这个渲染器。
- -no-angle：不部署 ANGLE。默认情况下，windeployqt 会部署 ANGLE。
- -no-svg：不部署 SVG 插件。默认情况下，windeployqt 会部署这个插件。
1. 首先需要一个arm版本的qt
2. 这里只能从源码构建了
3. linuxdeployqt目前只支持x86架构的，所以这里可以直接下载linuxdeployqt的源码，然后编译linuxdeployqt，构建出一个arm版本的linuxdeployqt
4. 编译linuxdeployqt的arm版本，使用交叉编译的话，不能使用gcc的qt路径，应该安装arm版本的qt