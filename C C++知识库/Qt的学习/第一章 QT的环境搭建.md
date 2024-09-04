# 第一章 QT的环境搭建

1. macOS上环境的搭建

这里也可以使用brew来下载qt

brew install qt

1. 下载qt包：https://download.qt.io/archive/qt/
2. 编译安装：
3. 解压：tar -xJvf file.tar.xz
4. 安装到指定位置：./configure -prefix $PWD/qtbase
5. 编译：cmake --build .
6. 安装：make install
7. 下载qt-creator：macos 上使用brew来安装qt-creator

brew install qt-creator

1. 使用qt-creator来创建项目

打开安装的qt-creator，点击创建项目：

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978926-e22174d1-4571-4800-8e1c-7283902a95be.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978926-e22174d1-4571-4800-8e1c-7283902a95be.png)

选择名称和项目路径：

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318979013-d3149c77-f434-4e87-a834-560796b47707.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318979013-d3149c77-f434-4e87-a834-560796b47707.png)

选择构建系统，分为cmake和qmake

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978976-12a524fb-2b94-468b-b3c5-cd7551240035.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978976-12a524fb-2b94-468b-b3c5-cd7551240035.png)

选择要创建的项目类型

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978922-d2d4d2fd-2316-45ad-bc3d-932e2cc1997a.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978922-d2d4d2fd-2316-45ad-bc3d-932e2cc1997a.png)

选择构建套件

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978926-0dbc4f9d-e392-4246-8359-8ba56642d211.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318978926-0dbc4f9d-e392-4246-8359-8ba56642d211.png)

这里如果为灰色，无法选择的话，需要点击管理，选择qt的版本

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318979806-ab4d531b-a299-4dc2-90c9-a44e86aec773.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318979806-ab4d531b-a299-4dc2-90c9-a44e86aec773.png)

设置好以后，就可以创建完成一个qt项目

1. Linux上的qt环境的安装

这里推荐使用直接下载qt的安装器，来安装qt

[https://download.qt.io/official_releases/online_installers/](https://download.qt.io/official_releases/online_installers/)

添加参数来使用国内的源，加速下载安装：

# linux

installer --mirror [https://mirrors.tuna.tsinghua.edu.cn/qt](https://mirrors.tuna.tsinghua.edu.cn/qt)

# windows

installer.exe --mirror [https://mirrors.tuna.tsinghua.edu.cn/qt](https://mirrors.tuna.tsinghua.edu.cn/qt)

下载安装成功后，就可以使用qt的IDE来创建项目

如果遇到xcb的错误，表示系统缺失xcb的组件，使用下面的命令解决

sudo apt-get install libxcb-xinerama0

sudo apt-get install '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev

1. 在arm上安装qt
2. 首先搭建arm开发环境，确定设备可以联网，下载xcb

必须安装xcb，否则程序有可能会启动不起来，qt不安装xcb插件

sudo apt-get install libxcb1-dev libxcb-xinerama0-dev libxcb-keysyms1-dev libxcb-icccm4-dev libxcb-image0-dev libxcb-render-util0-dev libxcb-xfixes0-dev libxcb-randr0-dev libxkbcommon-dev libxkbcommon-x11-dev

1. 下载qt的源码：https://download.qt.io/archive/qt/6.5/6.5.3/submodules/
2. 解压：tar -xvf qt
3. 这里根据qt的remade文件，来构建程序

./configure -prefix $PWD/qtbase

qt程序安装在qtbase目录下面

这里可以将配置文件的输出写入到一个文件里面，确定xcb安装

./configure -prefix $PWD/qtbase > configure_output.txt

在txt文件里面查找确定：XCB Xlib ............................. yes

这样的话，qt会安装xcb，qt6之后就不使参数来指定安装了

1. 开始构建：cmake --build .

加速构建：cmake --build . --j4

在构建的时候，可以关注输出，确保XCB可以使用，执行cmake ..的时候会输出下面

确保这几个都是yes

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318993406-c45917bd-1366-4ca4-be5c-5a78b313ce3e.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318993406-c45917bd-1366-4ca4-be5c-5a78b313ce3e.png)

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318993416-d3b673b2-1536-4488-9059-838a055def70.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717318993416-d3b673b2-1536-4488-9059-838a055def70.png)

还有OpenGL 也得安装