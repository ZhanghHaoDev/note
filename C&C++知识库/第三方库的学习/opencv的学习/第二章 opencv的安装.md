# 第二章 opencv的安装

## OpenCV安装笔记

## 1. OpenCV在Windows上的安装
- **官网**：[https://opencv.org/](https://opencv.org/)
- **GitHub**：[https://github.com/opencv/opencv](https://github.com/opencv/opencv)
- **安装步骤**：
  1. 访问官网下载适用于Windows的预编译OpenCV exe安装程序。
  2. 双击下载的exe文件进行安装。
  3. 将OpenCV的`bin`目录添加到系统环境变量中。

## 2. OpenCV在Linux上的安装
- **更新系统**：
  ```bash
  sudo apt-get update
  sudo apt-get upgrade
  ```
- **安装依赖**：
  ```bash
  sudo apt-get install build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
  ```
- **下载OpenCV**：
  ```bash
  git clone https://github.com/opencv/opencv.git
  ```
- **构建安装OpenCV**：
  ```bash
  cd opencv
  mkdir build
  cd build
  cmake ..
  make
  sudo make install
  ```

## 3. OpenCV在macOS上的安装
- **使用Homebrew安装**：
  ```bash
  brew install opencv
  ```
- **从源码构建**：
  1. 克隆OpenCV仓库。
  2. 创建构建目录并运行CMake。
  3. 编译和安装。

## 4. 在Python中使用OpenCV
- **创建虚拟环境**：
  ```bash
  python -m venv myenv
  ```
- **激活虚拟环境**：
  ```bash
  myenv\Scripts\activate  # Windows
  source myenv/bin/activate  # Linux/macOS
  ```
- **安装OpenCV**：
  ```bash
  pip install opencv-python
  pip install opencv-python-headless
  ```
- **退出虚拟环境**：
  ```bash
  deactivate
  ```

## 5. OpenCV与CMake
- **CMake项目中使用OpenCV**：
  ```cmake
  cmake_minimum_required(VERSION 3.0)
  project(MyProject)

  # 查找 OpenCV
  find_package(OpenCV REQUIRED)

  # 添加你的源文件
  add_executable(MyProject main.cpp)

  # 链接 OpenCV 库
  target_link_libraries(MyProject ${OpenCV_LIBS})
  ```

## 6. 其他注意事项
- **验证安装**：在Python中运行`import cv2`来验证OpenCV是否正确安装。
- **库版本**：确保安装的OpenCV版本与项目需求一致。
- **依赖管理**：在复杂的项目中，使用CMake可以更好地管理依赖和构建过程。
