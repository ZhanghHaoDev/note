# `LAPACKE_zheevd()`函数学习笔记

#### 1. 函数作用
- 用于计算复数Hermite（自共轭）矩阵的特征值和特征向量。

#### 2. 头文件
- 在Windows中调用`LAPACKE_zheevd()`函数需要包含以下头文件：
  ```c
  #ifdef _MSC_VER
  #include <complex.h>
  #define LAPACK_COMPLEX_CUSTOM
  #define lapack_complex_float _Fcomplex
  #define lapack_complex_double _Dcomplex
  #endif
  #include "lapacke.h"
  ```

#### 3. 函数参数详解
- **函数原型**：
  ```c
  lapack_int LAPACKE_zheevd( int matrix_layout, char jobz, char uplo, lapack_int n,
  lapack_complex_double* a, lapack_int lda, double* w );
  ```
- **参数详解**：
  - `matrix_layout`：矩阵布局，行主序或列主序。
  - `jobz`：计算所有特征值和特征向量（'V'）或仅特征值（'N'）。
  - `uplo`：矩阵的上三角（'U'）或下三角（'L'）被使用。
  - `n`：矩阵的大小。
  - `a`：输入矩阵的指针。
  - `lda`：矩阵`a`的领先维度。
  - `w`：输出特征值的数组。

#### 4. 实例
- **示例代码**：
  ```c
  #include <stdlib.h>
  #include <stdio.h>
  #include "lapacke.h"

  // Auxiliary routines prototypes
  extern void print_matrix( char* desc, MKL_INT m, MKL_INT n, MKL_Complex16* a, MKL_INT lda );
  extern void print_rmatrix( char* desc, MKL_INT m, MKL_INT n, double* a, MKL_INT lda );

  #define N 4
  #define LDA N

  int main() {
      MKL_INT n = N, lda = LDA, info;
      double w[N];
      MKL_Complex16 a[LDA*N] = {
          { 3.40,  0.00}, {-2.36,  1.93}, {-4.68, -9.55}, { 5.37,  1.23},
          { 0.00,  0.00}, { 6.94,  0.00}, { 8.13,  1.47}, { 2.07,  5.78},
          { 0.00,  0.00}, { 0.00,  0.00}, {-2.14,  0.00}, { 4.68, -7.44},
          { 0.00,  0.00}, { 0.00,  0.00}, { 0.00,  0.00}, {-7.42,  0.00}
      };

      printf( "LAPACKE_zheevd (column-major, high-level) Example Program Results\n" );
      info = LAPACKE_zheevd( LAPACK_COL_MAJOR, 'V', 'L', n, a, lda, w );
      if( info > 0 ) {
          printf( "The algorithm failed to compute eigenvalues.\n" );
          exit( 1 );
      }
      print_rmatrix( "Eigenvalues", 1, n, w, 1 );
      print_matrix( "Eigenvectors (stored columnwise)", n, n, a, lda );
      exit( 0 );
  }

  void print_matrix( char* desc, MKL_INT m, MKL_INT n, MKL_Complex16* a, MKL_INT lda ) {
      MKL_INT i, j;
      printf( "\n %s\n", desc );
      for( i = 0; i < m; i++ ) {
          for( j = 0; j < n; j++ )
              printf( " (%6.2f,%6.2f)", a[i+j*lda].real, a[i+j*lda].imag );
          printf( "\n" );
      }
  }

  void print_rmatrix( char* desc, MKL_INT m, MKL_INT n, double* a, MKL_INT lda ) {
      MKL_INT i, j;
      printf( "\n %s\n", desc );
      for( i = 0; i < m; i++ ) {
          for( j = 0; j < n; j++ ) printf( " %6.2f", a[i+j*lda] );
          printf( "\n" );
      }
  }
  ```
- **输出**：
  ```
  LAPACKE_zheevd (column-major, high-level) Example Program Results
  Eigenvalues
  -21.97 0.05 6.46 16.34
  Eigenvectors (stored columnwise)
  ( 0.41, 0.00) ( -0.34, 0.00) ( -0.69, 0.00) ( 0.49, 0.00)
  ( 0.02, -0.30) ( 0.32, -0.21) ( -0.57, -0.22) ( -0.59, -0.21)
  ( 0.18, 0.57) ( -0.42, -0.32) ( 0.06, 0.16) ( -0.35, -0.47)
  ( -0.62, -0.09) ( -0.58, 0.35) ( -0.15, -0.31) ( -0.10, -0.12)
  ```

#### 5. 注意事项
- 确保矩阵`a`是Hermite矩阵，即自共轭矩阵。
- 确保`lda`参数正确，它应该至少等于矩阵的行数。
- `jobz`参数控制是否计算特征向量，'V'表示计算，'N'表示不计算。
- `uplo`参数控制使用矩阵的上三角还是下三角。

#### 6. 其他
- 对于单精度复数运算，可以使用`LAPACKE_cheevd()`函数，其参数类型为`float`。