# CLAPACK安装与使用笔记

## 1. CLAPACK安装

- **CLAPACK简介**
  CLAPACK是LAPACK的C语言接口，LAPACK是著名的线性代数库，主要用于科学和工程计算。

- **下载地址**
  - LAPACK主页：[http://www.netlib.org/lapack/](http://www.netlib.org/lapack/)
  - CLAPACK主页：[http://www.netlib.org/clapack/](http://www.netlib.org/clapack/)

- **下载特定版本**
  - 适用于Visual Studio的CLAPACK：[http://www.netlib.org/clapack/CLAPACK-3.1.1-VisualStudio.zip](http://www.netlib.org/clapack/CLAPACK-3.1.1-VisualStudio.zip)
  - 适用于VC6.0的CLAPACK：[http://www.netlib.org/clapack/CLAPACK3-Windows.zip](http://www.netlib.org/clapack/CLAPACK3-Windows.zip)

- **目录结构**
  - SRC：CLAPACK源代码
  - BLAS：BLAS源代码
  - F2CLIBS：F2C源代码
  - LIB：编译后的库文件.lib
  - INCLUDE：头文件
  - TESTING：使用范例程序
  - INSTALL：安装文件和方法，包括使用说明

- **编译CLAPACK**
  - 建议自行编译以确保兼容性。
  - 需要编译F2CLIBS、tmglib、BLAS以及CLAPACK本身。
  - 使用Visual Studio打开`clapack.vcproj`文件进行编译。

## 2. 调用CLAPACK

- **头文件和库文件**
  - 将`INCLUDE`目录添加到项目中。
  - 将编译生成的`.lib`文件添加到项目链接器设置中。

- **注意事项**
  - 确保头文件包含顺序正确，先`f2c.h`后`clapack.h`。
  - 如果出现`complex`不明确的问题，需要定义命名空间和extern关键字。

## 3. CLAPACK函数说明

- **命名规则**
  - 函数名由`XYYZZZ`组成，其中`X`表示数据类型，`YY`表示矩阵类型，`ZZZ`表示计算方法。

- **函数参数说明**
  - 可以通过CLAPACK的[在线文档](https://netlib.org/lapack/explore-html/)查找具体函数的参数说明。

## 4. 遇到问题
- 如果在尝试访问CLAPACK的在线文档时遇到网络问题，建议检查网络连接，确保网址正确无误，并尝试重新访问。
