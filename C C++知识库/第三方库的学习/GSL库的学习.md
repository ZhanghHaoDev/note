# GSL库的学习

1. 简介

C++ GSL（GNU Scientific Library）库是一个开源的数值计算库，提供了许多常用的数值计算函数和算法，例如线性代数、微积分、优化、随机数生成等。GSL 库的目标是提供高质量、高性能、可靠的数值计算工具，以便科学家和工程师可以更轻松地进行数值计算和数据分析。

GSL 库的特点包括：

- 高质量的数值计算函数和算法，具有良好的数值稳定性和精度。
- 可以处理各种类型的数值计算问题，例如线性代数、微积分、优化、随机数生成等。
- 提供了丰富的文档和示例代码，以便用户可以快速上手和使用。
- 具有良好的可移植性和兼容性，可以在各种操作系统和编译器上运行。

GSL 库是一个开源的软件，可以在 GNU 通用公共许可证（GPL）下自由使用、修改和分发。GSL 库的源代码

可以从官方网站或 GitHub 上获取。

1. 编译安装

解压： tar -zxvf gsl-2.7.tar

指定安装路径：./configure --prefix=/Users/zhanghao/code/SDK/gsl/

编译：make

安装：make install

1. 例子

#include <iostream>

#include <gsl/gsl_errno.h>

#include <gsl/gsl_odeiv2.h>

/**

- @brief gsl库的demo
- 
- @note 输出结果：

t = 0, y = 0 1

t = 0.1, y = 0.0998334 0.995004

t = 0.2, y = 0.198669 0.980067

t = 0.3, y = 0.29552 0.955336

t = 0.4, y = 0.389418 0.921061

t = 0.5, y = 0.479426 0.877583

t = 0.6, y = 0.564642 0.825336

t = 0.7, y = 0.644218 0.764842

t = 0.8, y = 0.717356 0.696707

t = 0.9, y = 0.783327 0.62161

- /

int func(double t, const double y[], double f[], void *params)

{

// 定义常微分方程

double y1 = y[0];

double y2 = y[1];

double y1dot = y2;

double y2dot = -y1;

// 返回常微分方程的右侧

f[0] = y1dot;

f[1] = y2dot;

return GSL_SUCCESS;

}

int main()

{

// 定义初始条件和时间步长

double t = 0.0;

double y[2] = {0.0, 1.0}; // 初始条件

double h = 0.1;

// 定义ODE求解器

gsl_odeiv2_system sys = {func, NULL, 2, NULL};

gsl_odeiv2_driver *driver = gsl_odeiv2_driver_alloc_y_new(&sys, gsl_odeiv2_step_rk8pd, 1e-6, 1e-6, 0.0);

// 进行数值积分

for (int i = 0; i < 10; ++i)

{

double ti = i * h;

int status = gsl_odeiv2_driver_apply(driver, &t, ti, y);

if (status != GSL_SUCCESS)

{

std::cerr << "Error: gsl_odeiv2_driver_apply failed with status " << status << std::endl;

break;

}

std::cout << "t = " << t << ", y = " << y[0] << " " << y[1] << std::endl;

}

// 释放ODE求解器

gsl_odeiv2_driver_free(driver);

return 0;

}

---

CMakeLists.txt

cmake_minimum_required(VERSION 3.20

# 项目名称

project(gsl_demo)

# 设置语言标准

set(CMAKE_C_STANDARD 11)

set(CMAKE_CXX_STANDARD 17)

# 设置强制检查语法

set(CMAKE_CXX_EXTENSIONS ON)

set(CMAKE_C_EXTENSIONS ON)

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

# 设置GSL库的路径

set(CMAKE_PREFIX_PATH

"/Users/zhanghao/code/SDK/gsl" ${CMAKE_PREFIX_PATH}

)

# 设置GSL库包

find_package(GSL REQUIRED)

# 设置源文件路径

set(SRC_DIR ${PROJECT_SOURCE_DIR}/src)

set(SRC_DIR ${PROJECT_SOURCE_DIR})

# 设置打印信息

# 输出构建类型

message(STATUS "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")

# 判断GSL库是否存在

if (GSL_FOUND)

message(STATUS "GSL_INCLUDE_DIRS: ${GSL_INCLUDE_DIRS}")

message(STATUS "GSL_LIBRARIES: ${GSL_LIBRARIES}")

message(STATUS "GSL_VERSION: ${GSL_VERSION}")

else()

message(FATAL_ERROR "GSL library not found")

endif()

# 设置生成可执行文件

add_executable(gsl_demo ${SRC_DIR}/main.cpp)

# 设置GSL链接库

target_link_libraries(gsl_demo GSL::gsl GSL::gslcblas)

---

a

ss s