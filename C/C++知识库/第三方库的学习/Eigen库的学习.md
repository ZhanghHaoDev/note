# Eigen库学习笔记

#### 1. 简介
- **Eigen库** 是一个开源的C++模板库，用于线性代数、矩阵和向量运算、数值分析等。
- **特点**：无需编译，只需包含头文件即可使用。

#### 2. 安装
- **Linux下安装**
  - **使用apt-get安装**
    ```bash
    sudo apt-get install libeigen3-dev
    ```
  - **手动编译安装**
    1. 访问官网 [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) 下载源码。
    2. 解压并编译安装
    ```bash
    tar -xvjf eigen-3.4.0.tar.bz2
    cd eigen
    mkdir build
    cd build
    cmake ..
    sudo make install
    ```
    - **指定安装目录**
    ```bash
    mkdir build
    cd build
    cmake .. -DCMAKE_INSTALL_PREFIX=/path/to/install
    make install
    ```

#### 3. 模块与头文件
| 模块       | 头文件                | 内容描述                   |
|------------|-----------------------|---------------------------|
| Core       | `#include <Eigen/Core>` | 矩阵和数组 (向量) 类 (Matrix, Array)，基于线性代数还有数组操作 |
| Geometry   | `#include <Eigen/Geometry>` | 变换，平移，缩放，2D 旋转和 3D 旋转 (包括四元数和角轴) |
| LU         | `#include <Eigen/LU>` | 使用求解器进行求逆，行列式，LU 分解操作 |
| Cholesky   | `#include <Eigen/Cholesky>` | 使用求解器进行 LLT, LT, Cholesky 分解 |
| Householder | `#include <Eigen/Householder>` | Householder 变换；被用作几个线性代数模块 |
| SVD        | `#include <Eigen/SVD>` | SVD 分解与最小二乘求解器 |
| QR         | `#include <Eigen/QR>` | QR 分解 |
| Eigenvalues | `#include <Eigen/Eigenvalues>` | 特征值，特征向量分解 |
| Sparse     | `#include <Eigen/Sparse>` | 稀疏矩阵存储以及相关的基本线性代数 |
| Dense      | `#include <Eigen/Dense>` | 包括 Core, Geometry, LU, Cholesky, SVD, QR, Eigenvalues 的头文件 |
| Eigen      | `#include <Eigen/Eigen>` | 包括 Dense 和 Sparse 的头文件 |

#### 4. 实例
- **main.cpp**
  ```cpp
  #include <iostream>
  #include <eigen3/Eigen/Dense>

  using Eigen::MatrixXd;

  int main() {
      MatrixXd m(2,2);
      m(0,0) = 3;
      m(1,0) = 2.5;
      m(0,1) = -1;
      m(1,1) = m(1,0) + m(0,1);
      std::cout << m << std::endl;
  }
  ```
- **CMakeLists.txt**
  ```cmake
  cmake_minimum_required(VERSION 3.20)
  project(eigen_demo)
  set(CMAKE_C_STANDARD 11)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_EXTENSIONS OFF)
  set(CMAKE_C_EXTENSIONS OFF)
  set(CMAKE_BUILD_TYPE Debug)
  set(CMAKE_C_FLAGS_DEBUG "-g -Wall")
  set(CMAKE_CXX_FLAGS_DEBUG "-g -Wall")
  set(CMAKE_C_FLAGS_RELEASE "-O3 -Wall")
  set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall")
  set(EIGEN3_INCLUDE_DIR /usr/local/include/eigen3)
  set(EIGEN3_INCLUDE_DIR ${EIGEN3_INCLUDE_DIR} CACHE PATH "Eigen include directory")
  include_directories(${EIGEN3_INCLUDE_DIR}/include)
  set(SRC_DIR ${PROJECT_SOURCE_DIR}/src)
  set(SRC_DIR ${PROJECT_SOURCE_DIR})
  message(STATUS "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")
  message(STATUS "EIGEN3_INCLUDE_DIR: ${EIGEN3_INCLUDE_DIR}")
  if (EIGEN3_INCLUDE_DIR)
      message(STATUS "EIGEN3_INCLUDE_DIR: ${EIGEN3_INCLUDE_DIR}")
  else()
      message(FATAL_ERROR "EIGEN3_INCLUDE_DIR: ${EIGEN3_INCLUDE_DIR}")
  endif()
  add_executable(eigen_demo ${SRC_DIR}/main.cpp)
  ```
- **运行代码**
  ```bash
  mkdir build
  cd build
  cmake ..
  make
  ./eigen_demo
  ```
- **输出结果**
  ```
  3  -1
  2.5 1.5
  ```

#### 5. 进一步学习
- 推荐B站教程：[NoSharp的个人空间 - Eigen库学习心得体会](https://space.bilibili.com/382649355/channel/seriesdetail?sid=3352169&ctype=0)
