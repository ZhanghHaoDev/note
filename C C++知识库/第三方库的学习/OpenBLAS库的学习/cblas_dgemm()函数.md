# cblas_dgemm()函数

# 1. 函数作用

计算矩阵乘法

# 2. 头文件

需要包含的头文件为：

#include "cblas.h"

---

# 3. 函数参数详解

1. 函数原型：

void cblas_dgemm(CBLAS_LAYOUT layout, CBLAS_TRANSPOSE TransA,

CBLAS_TRANSPOSE TransB, const int M, const int N,

const int K, const double alpha, const double *A,

const int lda, const double *B, const int ldb,

const double beta, double *C, const int ldc);

---

1. 参数详解：
- layout：指定行优先或列优先（行：CblasRowMajor，列：CblasColMajor ）
- TransA：指定是否转置矩阵A（不转置：CblasNoTrans ，转置：CblasTrans ）
- TransB：指定是否转置矩阵B（不转置：CblasNoTrans ，转置：CblasTrans ）
- M：矩阵A和C的行数，（A(2*3)B(23) = C(2*3)）
- N：矩阵B和C的列数,（A(2*3)B(23) = C(2*3)）
- K：矩阵A的列，B的行
- alpha：矩阵A和B乘积的比例因子
- A：A矩阵
- lda：矩阵A的第一维的大小
- B：B矩阵
- ldb：矩阵B的第一维的大小
- beta：矩阵C的比例因子
- C：矩阵C的地址（输入/输出）
- ldc：矩阵C的第一维的大小
1. 矩阵的比例因子

alpha = 1.0; beta = 0.0;

---

# 4. 实例

#include <cblas.h>

#include <stdio.h>

void main()

{

int i=0;

double A[6] = {1.0,2.0,1.0,-3.0,4.0,-1.0};

double B[6] = {1.0,2.0,1.0,-3.0,4.0,-1.0};

double C[9] = {.5,.5,.5,.5,.5,.5,.5,.5,.5};

cblas_dgemm(CblasColMajor, CblasNoTrans, CblasTrans,3,3,2,1,A, 3, B, 3,2,C,3);

for(i=0; i<9; i++)

printf("%lf ", C[i]);

printf("\n");

}

---

# 5. 其他