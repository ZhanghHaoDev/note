### OpenBLAS库的学习

#### 简介
- **OpenBLAS**：一个优化的Basic Linear Algebra Subprograms (BLAS) 库，基于 GotoBLAS2 1.13 BSD 版本。

#### Windows下的安装
- **下载源文件**：
  - 官方网站：[http://www.openblas.net/](http://www.openblas.net/)
  - 官方推荐版本：[How-to-use-OpenBLAS-in-Microsoft-Visual-Studio](https://github.com/xianyi/OpenBLAS/wiki/How-to-use-OpenBLAS-in-Microsoft-Visual-Studio)

- **使用CMake编译**：
  1. 打开CMake GUI，添加OpenBLAS源代码路径，新建build目录。
  2. 选择Visual Studio版本，点击“Generate”。
  3. 在build目录下打开.sln文件，使用Visual Studio生成lib库。

- **添加OpenBLAS到Visual Studio**：
  1. 将生成的include和lib目录添加到项目中。
  2. 添加必要的定义，例如`LAPACK_COMPLEX_CUSTOM`。

- **示例代码**：
  ```cpp
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
  ```

#### 遇到的问题
1. **缺少DLL**：
   - **解决办法**：将OpenBLAS的bin目录添加到Windows的PATH环境变量中。

2. **无法识别的外部符号**：
   - **解决办法**：在Visual Studio中，右键项目属性 -> C/C++ -> 代码生成 -> 运行时库，将多线程(/MT)改为多线程调试(/MTd)。

#### Linux下的安装
- **安装编译工具**：
  ```bash
  sudo apt-get install cmake
  sudo apt-get install gcc
  ```

- **下载OpenBLAS**：
  ```bash
  git clone https://github.com/xianyi/OpenBLAS.git
  ```

- **编译安装**：
  ```bash
  cd OpenBLAS
  make -j8
  sudo make PREFIX=/usr/local/OpenBLAS install
  ```

#### macOS下的安装
- **下载**：
  ```bash
  git clone https://github.com/xianyi/OpenBLAS.git
  ```

- **编译安装**：
  ```bash
  make install PREFIX=your_installation_directory
  ```

#### 相关函数
- **cblas_zaxpy()**：[Documentation](https://www.openblas.net/)
- **cblas_dgemm()**：[Documentation](https://www.openblas.net/)
- **LAPACKE_zheevd()**：[Documentation](https://www.openblas.net/)
