# Eigen库的学习

1. 简介

Eigen库是一个开源的模板库，支持线性代数的运算，包括矩阵运算，向量运算，数值分析等，Eigen库不需要编译，使用的时候只需要包含头文件即可

1. 安装

Linux下的安装

**代码**

---

// 我们可以使用apt-get来安装

sudo apt-get install libeigen3-dev

---

手动编译安装

**代码**

---

// 但是使用apt-get来安装的话，apt包更新比较慢

// 这里推荐使用下载文件来手动安装

官网：http://eigen.tuxfamily.org/index.php?title=Main_Page

// 下载好文件后，解压

tar -xvjf eigen-3.4.0.tar.bz2

cd eigen

mkdir build

cd build

cmake ..

sudo make install

---

这里的手动安装会将库安装到/usr/local目录下面，如果想要指定安装目录则

**代码**

---

mkdir build

cd build

# 指定位置

cmake .. -DCMAKE_INSTALL_PREFIX=/path/to/install

make install

---

1. 模块与头文件

| **模块** | **头文件** | **内容** |
| --- | --- | --- |
| Core | #include <Eigen/Core> | 矩阵和数组 (向量) 类 (Matrix, Array)，基于线性代数还有数组操作 |
| Geometry | #include <Eigen/Geometry> | 变换，平移，缩放，2D 旋转和 3D 旋转 (包括四元数和角轴) |
| LU | #include <Eigen/LU> | 使用求解器进行求逆，行列式，LU 分解操作 |
| Cholesky | #include <Eigen/Cholesky> | 使用求解器进行 LLT, LT, Cholesky 分解 |
| Householder | #include <Eigen/Householder> | Householder 变换；被用作几个线性代数模块 |
| SVD | #include <Eigen/SVD> | SVD 分解与最小二乘求解器 |
| QR | #include <Eigen/QR> | QR 分解 |
| Eigenvalues | #include <EIgen/Eigenvalues> | 特征值，特征向量分解 |
| Sparse | #include <Eigen/Sparse> | 稀疏矩阵存储以及相关的基本线性代数 |
| Dense | #include <Eigen/Dense> | 包括 Core, Geometry, LU, Cholesky, SVD, QR, Eigenvalues 的头文件 |
| Eigen | #include <Eigen/Eigen> | 包括 Dense 和 S |
1. 实例

mian.cpp

**代码**

---

#include <iostream>

#include <eigen3/Eigen/Dense>

using Eigen::MatrixXd;

int main()

{

MatrixXd m(2,2);

m(0,0) = 3;

m(1,0) = 2.5;

m(0,1) = -1;

m(1,1) = m(1,0) + m(0,1);

std::cout << m << std::endl;

}

---

CMakeLists.txt

**代码**

---

# CMake最小版本

cmake_minimum_required(VERSION 3.20)

# 项目名称

project(eigen_demo)

# 设置语言标准

set(CMAKE_C_STANDARD 11)

set(CMAKE_CXX_STANDARD 17)

# 设置强制检查语法

set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_C_EXTENSIONS OFF)

# 设置构建类型

set(CMAKE_BUILD_TYPE Debug)

# set(CMAKE_BUILD_TYPE Release)

# 设置编译选项

if (CMAKE_BUILD_TYPE STREQUAL "Debug")

set(CMAKE_C_FLAGS_DEBUG "-g -Wall")

set(CMAKE_CXX_FLAGS_DEBUG "-g -Wall")

elseif(CMAKE_BUILD_TYPE STREQUAL "Release")

set(CMAKE_C_FLAGS_RELEASE "-O3 -Wall")

set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall")

endif()

# 设置Eigen库路径变量

set(EIGEN3_INCLUDE_DIR /usr/local/include/eigen3)

# 设置Eigne库头文件

set(EIGEN3_INCLUDE_DIR ${EIGEN3_INCLUDE_DIR} CACHE PATH "Eigen include directory")

# 设置Eigne库库文件

set(EIGEN3_LIBRARY_DIR ${EIGEN3_LIBRARY_DIR} CACHE PATH "Eigen library directory")

# 设置头文件路径

include_directories(${EIGEN3_INCLUDE_DIR}/include)

# 设置源文件路径

set(SRC_DIR ${PROJECT_SOURCE_DIR}/src)

set(SRC_DIR ${PROJECT_SOURCE_DIR})

# 设置打印信息

# 输出构建类型

message(STATUS "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")

# 输出Eigen库路径

message(STATUS "EIGEN3_INCLUDE_DIR: ${EIGEN3_INCLUDE_DIR}")

# 判断Eigen库是否加载成功

if (EIGEN3_INCLUDE_DIR)

message(STATUS "EIGEN3_INCLUDE_DIR: ${EIGEN3_INCLUDE_DIR}")

else()

message(FATAL_ERROR "EIGEN3_INCLUDE_DIR: ${EIGEN3_INCLUDE_DIR}")

endif()

# 设置生成可执行文件

add_executable(eigen_demo ${SRC_DIR}/main.cpp)

---

运行代码

**代码**

---

mkdir build

cd build

cmake ..

make

./eigen_demo

---

输出结果

**代码**

---

3  -1

2.5 1.5

---

1. 进一步学习

如果想要进一步的学习和使用Eigen库，这里推荐B站的教程

[https://space.bilibili.com/382649355/channel/seriesdetail?sid=3352169&ctype=0](https://space.bilibili.com/382649355/channel/seriesdetail?sid=3352169&ctype=0)