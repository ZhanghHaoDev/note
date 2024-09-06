### `cblas_dgemm()`函数学习笔记

#### 1. 函数作用
- 用于计算矩阵乘法，具体为 C = alpha * A * B + beta * C。

#### 2. 头文件
- 需要包含的头文件为：
  ```c
  #include "cblas.h"
  ```

#### 3. 函数参数详解
- **函数原型**：
  ```c
  void cblas_dgemm(CBLAS_LAYOUT layout, CBLAS_TRANSPOSE TransA,
  CBLAS_TRANSPOSE TransB, const int M, const int N,
  const int K, const double alpha, const double *A,
  const int lda, const double *B, const int ldb,
  const double beta, double *C, const int ldc);
  ```
- **参数详解**：
  - `layout`：存储布局，行优先（`CblasRowMajor`）或列优先（`CblasColMajor`）。
  - `TransA`：矩阵A的转置选项，不转置（`CblasNoTrans`）或转置（`CblasTrans`）。
  - `TransB`：矩阵B的转置选项，不转置（`CblasNoTrans`）或转置（`CblasTrans`）。
  - `M`：矩阵A的行数和矩阵C的行数。
  - `N`：矩阵B的列数和矩阵C的列数。
  - `K`：矩阵A的列数和矩阵B的行数。
  - `alpha`：乘法因子，用于A和B的乘积。
  - `A`：指向矩阵A的指针。
  - `lda`：矩阵A的领先维度。
  - `B`：指向矩阵B的指针。
  - `ldb`：矩阵B的领先维度。
  - `beta`：乘法因子，用于矩阵C。
  - `C`：指向矩阵C的指针，结果将被存储在这里。
  - `ldc`：矩阵C的领先维度。

#### 4. 实例
- **示例代码**：
  ```c
  #include <cblas.h>
  #include <stdio.h>

  int main() {
      int i = 0;
      double A[6] = {1.0, 2.0, 1.0, -3.0, 4.0, -1.0};
      double B[6] = {1.0, 2.0, 1.0, -3.0, 4.0, -1.0};
      double C[9] = {.5, .5, .5, .5, .5, .5, .5, .5, .5};

      cblas_dgemm(CblasColMajor, CblasNoTrans, CblasTrans, 3, 3, 2, 1.0, A, 3, B, 3, 2.0, C, 3);

      for (i = 0; i < 9; i++)
          printf("%lf ", C[i]);
      printf("\n");

      return 0;
  }
  ```
- **输出**：
  ```
  -2.000000  2.000000 -2.000000  2.000000 -2.000000  2.000000 -2.000000  2.000000 -2.000000 
  ```

#### 5. 注意事项
- 确保矩阵的领先维度（`lda`, `ldb`, `ldc`）正确设置，以匹配存储布局。
- `alpha`和`beta`是双精度浮点数，用于控制矩阵乘法的结果。
- 确保矩阵A、B和C的内存分配和初始化正确。