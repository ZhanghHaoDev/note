# OpenBLAS库的学习

# Windows下的安装

1. 下载源文件： [http://www.openblas.net/](http://www.openblas.net/)

官方推荐版本： [https://github.com/xianyi/OpenBLAS/wiki/How-to-use-OpenBLAS-in-Microsoft-Visual-Studio](https://github.com/xianyi/OpenBLAS/wiki/How-to-use-OpenBLAS-in-Microsoft-Visual-Studio)

1. cmake编译vs过程

打开cmake-gui，添加openbals过程，新建build目录

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457644-10330ac7-ab82-4516-9069-b6b7f395dfbf.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457644-10330ac7-ab82-4516-9069-b6b7f395dfbf.png)

---

选择vs版本，点击生成

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457635-f7057e54-4bac-4d1b-a0d5-1224f7f60b16.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457635-f7057e54-4bac-4d1b-a0d5-1224f7f60b16.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457634-5dc72175-461d-4dee-bb84-86fff819444f.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457634-5dc72175-461d-4dee-bb84-86fff819444f.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457650-751903bc-b34d-4592-88d5-08a7d6f0b7de.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457650-751903bc-b34d-4592-88d5-08a7d6f0b7de.png)

---

1. vs生成lib库

在新建的build目录下打开.sln vs工程，vs选择版本右键重新生成

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457647-0263de63-2f20-45c3-9d1d-5e456c270a8b.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319457647-0263de63-2f20-45c3-9d1d-5e456c270a8b.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319458180-950d01a8-9c61-4a53-85bd-1e072752b6da.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319458180-950d01a8-9c61-4a53-85bd-1e072752b6da.png)

---

在 D:\OpenBLAS\lapack-netlib\CBLAS\include目录下找到include目录

在D:\OpenBLAS\build\lib目录下找到lib目录

1. vs添加openblas

vs选择生成的include和lib库

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319458240-7be186db-340b-4abe-8412-55e2a1d55154.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319458240-7be186db-340b-4abe-8412-55e2a1d55154.png)

---

输入下面的代码，点击生成

在较新的Visual Studio版本中，Microsoft改变了处理复杂类型的方式。即使使用 OpenBLAS 的预编译版本，也可能需要定义以便为 MSVC 正确定义复杂类型。例如，以下某些变体可能会有所帮助：LAPACK_COMPLEX_CUSTOM

所以需要添加，把下面的定义添加到文件的最开始，如果遇到“clog”,不明确的符号，则是因为<complex.h>和定义冲突，把下面的定义放到文件开始即可。

#if defined(_MSC_VER)

#include <complex.h>

#define LAPACK_COMPLEX_CUSTOM

#define lapack_complex_float _Fcomplex

#define lapack_complex_double _Dcomplex

#endif

---

#include "cblas.h"

#include <stdio.h>

#include <stdlib.h>

void main() {

int i = 0;

double A[6] = { 1.0, 2.0, 1.0, -3.0, 4.0, -1.0 };

double B[6] = { 1.0, 2.0, 1.0, -3.0, 4.0, -1.0 };

double C[9] = { .5, .5, .5, .5, .5, .5, .5, .5, .5 };

int M = 3; // row of A and C

int N = 3; // col of B and C

int K = 2; // col of A and row of B

double alpha = 1.0;

double beta = 0.0;

cblas_dgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans, M, N, K, alpha, A, K, B, N, beta, C, N);

for (i = 0; i < 9; i++) {

printf("%lf ", C[i]);

}

printf("\n");

system("pause");

}

---

工程生成没有报错，结果为下面的，就表示成功

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319458313-87c31a57-cc40-4d4c-acaa-ae950e831e28.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319458313-87c31a57-cc40-4d4c-acaa-ae950e831e28.png)

---

# 遇到的问题

1. 官方推荐的编译方式： [https://github.com/xianyi/OpenBLAS/wiki/How-to-use-OpenBLAS-in-Microsoft-Visual-Studio](https://github.com/xianyi/OpenBLAS/wiki/How-to-use-OpenBLAS-in-Microsoft-Visual-Studio)

【问题】：缺少dll：

【解决办法】：按照官方推荐的编译方式会在运行的时候，报缺少dll，找到该dll的位置将该bin目录添加到Windows的path环境变量中，然后重启vs即可，其他缺少dll的方式也可以使用该方式

【问题】：无法识别的外部符号 LNK2001: 无法解析的外部符号 __imp__calloc_dbg

【解决办法】：右键属性-》c/c++-》代码生成-运行时库  将多线程（/MT）改为多线程调试（/MTd）

# linux 下的安装

1. 安装编译需要的工具

sudo apt-get install cmake

sudo apt-get install gcc

---

1. 下载openblas

// git 下载

git clone [https://github.com/xianyi/OpenBLAS.git](https://github.com/xianyi/OpenBLAS.git)

// 如果是zip文件，则使用

unzip 文件名称

// tar文件，则使用

tar -xzvf 文件名称

---

1. 编译openblas

cd openblas

make -j8

sudo make PREFIX=/usr/local/OpenBLAS install

---

macOS下的安装

下载：git clone [https://github.com/xianyi/OpenBLAS.git](https://github.com/xianyi/OpenBLAS.git)

编译安装：make install PREFIX=your_installation_directory

[cblas_zaxpy()函数](cblas_zaxpy()函数%202e532f19103c419cb8f4f11a8b323c97.md)

[cblas_dgemm()函数](cblas_dgemm()函数%2067f05855c4fb43e39b1aeba7eea4f221.md)

[LAPACKE_zheevd()函数](LAPACKE_zheevd()函数%20f83c80d80ab74e5e81becb7ad85eb27a.md)