# LAPACKE_zheevd()函数

# 1. 函数作用

该函数是计算矩阵特征值和特征向量使用，要求输入的矩阵必须为Hermite矩阵

Hermite矩阵：自共轭矩阵，对称共轭

# 2. 头文件

在Windows中调用LAPACKE_zheevd()函数需要包含下面的头文件

在较新的Visual Studio版本中，Microsoft改变了处理复杂类型的方式。即使使用 OpenBLAS 的预编译版本，也可能需要定义以便为 MSVC 正确定义复杂类型。例如，以下某些变体可能会有所帮助

#if defined(_MSC_VER)

#include <complex.h>

#define LAPACK_COMPLEX_CUSTOM

#define lapack_complex_float _Fcomplex

#define lapack_complex_double _Dcomplex

#endif

#include "lapacke.h"

---

# 3. 函数参数详解

函数原型

lapack_int LAPACKE_zheevd( int matrix_layout, char jobz, char uplo, lapack_int n,

lapack_complex_double* a, lapack_int lda,

double* w );

---

1. 参数1：

# 4. 实例

/*

LAPACKE_zheevd Example.

=======================

Program computes all eigenvalues and eigenvectors of a complex Hermitian

matrix A using divide and conquer algorithm, where A is:

(  3.40,  0.00) ( -2.36, -1.93) ( -4.68,  9.55) (  5.37, -1.23)

( -2.36,  1.93) (  6.94,  0.00) (  8.13, -1.47) (  2.07, -5.78)

( -4.68, -9.55) (  8.13,  1.47) ( -2.14,  0.00) (  4.68,  7.44)

(  5.37,  1.23) (  2.07,  5.78) (  4.68, -7.44) ( -7.42,  0.00)

Description.

============

The routine computes all eigenvalues and, optionally, eigenvectors of an

n-by-n complex Hermitian matrix A. The eigenvector v(j) of A satisfies

A*v(j) = lambda(j)*v(j)

where lambda(j) is its eigenvalue. The computed eigenvectors are

orthonormal.

If the eigenvectors are requested, then this routine uses a divide and

conquer algorithm to compute eigenvalues and eigenvectors.

Example Program Results.

========================

LAPACKE_zheevd (column-major, high-level) Example Program Results

Eigenvalues

- 21.97 0.05 6.46 16.34

Eigenvectors (stored columnwise)

(  0.41,  0.00) ( -0.34,  0.00) ( -0.69,  0.00) (  0.49,  0.00)

(  0.02, -0.30) (  0.32, -0.21) ( -0.57, -0.22) ( -0.59, -0.21)

(  0.18,  0.57) ( -0.42, -0.32) (  0.06,  0.16) ( -0.35, -0.47)

( -0.62, -0.09) ( -0.58,  0.35) ( -0.15, -0.31) ( -0.10, -0.12)

- /

#include <stdlib.h>

#include <stdio.h>

#include "lapacke.h"

/* Auxiliary routines prototypes */

extern void print_matrix( char* desc, MKL_INT m, MKL_INT n, MKL_Complex16* a, MKL_INT lda );

extern void print_rmatrix( char* desc, MKL_INT m, MKL_INT n, double* a, MKL_INT lda );

/* Parameters */

#define N 4

#define LDA N

/* Main program */

int main() {

/* Locals */

MKL_INT n = N, lda = LDA, info;

/* Local arrays */

double w[N];

MKL_Complex16 a[LDA*N] = {

{ 3.40,  0.00}, {-2.36,  1.93}, {-4.68, -9.55}, { 5.37,  1.23},

{ 0.00,  0.00}, { 6.94,  0.00}, { 8.13,  1.47}, { 2.07,  5.78},

{ 0.00,  0.00}, { 0.00,  0.00}, {-2.14,  0.00}, { 4.68, -7.44},

{ 0.00,  0.00}, { 0.00,  0.00}, { 0.00,  0.00}, {-7.42,  0.00}

};

/* Executable statements */

printf( "LAPACKE_zheevd (column-major, high-level) Example Program Results\n" );

/* Solve eigenproblem */

info = LAPACKE_zheevd( LAPACK_COL_MAJOR, 'V', 'L', n, a, lda, w );

/* Check for convergence */

if( info > 0 ) {

printf( "The algorithm failed to compute eigenvalues.\n" );

exit( 1 );

}

/* Print eigenvalues */

print_rmatrix( "Eigenvalues", 1, n, w, 1 );

/* Print eigenvectors */

print_matrix( "Eigenvectors (stored columnwise)", n, n, a, lda );

exit( 0 );

} /* End of LAPACKE_zheevd Example */

/* Auxiliary routine: printing a matrix */

void print_matrix( char* desc, MKL_INT m, MKL_INT n, MKL_Complex16* a, MKL_INT lda ) {

MKL_INT i, j;

printf( "\n %s\n", desc );

for( i = 0; i < m; i++ ) {

for( j = 0; j < n; j++ )

printf( " (%6.2f,%6.2f)", a[i+j*lda].real, a[i+j*lda].imag );

printf( "\n" );

}

}

/* Auxiliary routine: printing a real matrix */

void print_rmatrix( char* desc, MKL_INT m, MKL_INT n, double* a, MKL_INT lda ) {

MKL_INT i, j;

printf( "\n %s\n", desc );

for( i = 0; i < m; i++ ) {

for( j = 0; j < n; j++ ) printf( " %6.2f", a[i+j*lda] );

printf( "\n" );

}

}

---

# 5. 其他

该函数的参数为双精度浮点数（double）,如果使用单精度浮点数(float)，除了将函数参数修改为float外，函数名称也得修改为：

lapack_int LAPACKE_cheevd( int matrix_layout, char jobz, char uplo, lapack_int n,

lapack_complex_float* a, lapack_int lda, float* w );

---