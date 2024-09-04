# 第二章 opencv的安装

1. opencv在Windows上的安装

官网：https://opencv.org/

GitHub：https://github.com/opencv/opencv

在Windows上安装比较简单，直接下载exe应用程序，双击安装即可，最后把bin目录添加到环境变量即可

1. opencv在Linux上的安装
2. 更新系统

**代码**

---

sudo apt-get update

sudo apt-get upgrade

---

1. 安装依赖

**代码**

---

sudo apt-get install build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

---

1. 下载opencv

**代码**

---

git clone [https://github.com/opencv/opencv.git](https://github.com/opencv/opencv.git)

---

1. 构建安装opencv

**代码**

---

cd opencv

mkdir build

cd build

cmake ..

make

sudo make install

---

1. opencv在macos上的安装
2. 在macos上我们可以使用brew来安装opencv

**代码**

---

brew install opencv

---

1. 从源码构建
2. 在Windows上直接使用opencv安装包既可安装
3. 在Linux上使用源码构建

**代码**

---

cd opencv

mkdir build

cd build

cmake ..

make

sudo make install

---

1. 在python中使用opencv

这里使用python的虚拟环境来使用opencv

1. 创建虚拟环境

**代码**

---

# 创建一个名为 myenv 的虚拟环境

python -m venv myenv

---

1. 激活虚拟环境

**代码**

---

# 激活虚拟环境

myenv\Scripts\activate

---

1. 安装opencv

**代码**

---

# 安装opencv的主要模块

pip install opencv-python

# 安装opencv的所有功能

pip install opencv-python-headless

---

1. 退出虚拟环境

**代码**

---

# 退出虚拟环境

deactivate

---

1. opencv与cmake

使用cmake构建项目，项目依赖opencv的话，下面是使用cmake管理opencv依赖的例子

**代码**

---

cmake_minimum_required(VERSION 3.0)

project(MyProject)

# 查找 OpenCV

find_package(OpenCV REQUIRED)

# 添加你的源文件

add_executable(MyProject main.cpp)

# 链接 OpenCV 库

target_link_libraries(MyProject ${OpenCV_LIBS})

---