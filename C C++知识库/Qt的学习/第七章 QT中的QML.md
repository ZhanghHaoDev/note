# 第七章 QT中的QML

QML（Qt Meta-object Language）是一个由Qt开发的用户界面标记语言。它是一个声明式语言，用于设计用户界面相关的应用程序。QML提供了一种易于理解和使用的方式来定义用户界面，这些用户界面可以包含动画，状态和过渡效果。QML是一种基于JavaScript的语言，它允许开发者使用JavaScript代码来处理用户交互和创建复杂的动画效果。

qt原先的QWidget也可以用于开发界面，qml可以用于给qt美化，
qwidget兼容性比较好，适用多个平台和硬件（包括嵌入式），qml则是硬件越好，效果越好
qwidget用于传统的界面开发，适用于传统的行业开发，qml则集中在直播，汽车仪表盘等方面

# 1. qml 简介

qml 是一种用于描述应用程序用户界面的声明式编程语言，使用一些可视组件依据这些组件以及这些组件之间交互来描述用户界面。

# 1.1. Quick

qt 当中的 quick 是 QML 的一个书籍类型和功能的标准库，包含了可视化类型，交互类型，动画，模型和视图，粒子特效和渲染特效

他俩之间的关系类似 HTML，qml 就类似于 html，用于定义用户界面的结构和布局。qml 当中包含了各种 UI 组件的声明和属性设置

quick 类似 html 元素库，提供了一组预定义的 UI 组件（按钮，列表等）

# 1.2. qt ，quick，qml 的关系

我的理解是 qt 是一个 c++的第三方库，主要用于 UI 界面，但是 quick 是 qt 当中另外一个单独的框架，我们可以直接使用 quick 这个，创造出更好看的界面

我们创建一个 cmake 项目，需要有 main.cpp，qml.rc ，mian.qml

首先编写 qml 语言，然后在 qml.rc 当中包含 qml 文件，最后在 main.cpp 当中调用 rc 文件就可以

qrc 文件：qrc 文件主要用于管理资源，包括图片，图标，qml 文件等，可以跨平台，方便统一管理

# 2. 遇到的问题

# 2.1. 运行的时候找不到QtQuick

遇到一个问题，cmake 构建的时候没有错误，make 编译的时候也没有报错，运行的时候报错

```bash
$ ./class-qml/demo-qml
QQmlApplicationEngine failed to load component
qrc:/main.qml:2:1: module "QtQuick.Controls" is not installed
qrc:/main.qml:1:1: module "QtQuick" is not installed
qrc:/main.qml:2:1: module "QtQuick.Controls" is not installed
qrc:/main.qml:1:1: module "QtQuick" is not installed
zh@zh:~/demo-qt/build$
```

解决办法：

更换 qt 的版本，不要使用 qt6 使用 qt5

```bash
sudo apt-get install qtbase5-dev qtdeclarative5-dev qtquickcontrols2-5-dev
```

# 2.2. 运行的时候无法确定版本

运行的时候报错，无法确定版本的错误

```bash
zh@zh:~/demo-qt/build$ ./class-qml/demo-qml
QQmlApplicationEngine failed to load component
qrc:/main.qml: Library import requires a version
qrc:/main.qml: Library import requires a version
```

解决办法

确定 qt 的 qtquick 的版本，在引入 qtquick 的时候确定版本

```bash
import QtQuick 2.15
import QtQuick.Controls 2.15
```