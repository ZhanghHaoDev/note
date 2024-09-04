# cblas_zaxpy()函数

# 1. 函数作用

计算复数的乘法

# 2. 头文件

#include "cblas.h"

---

# 3. 参数详解

1. 函数原型

void cblas_zaxpy(const int N, const void *alpha, const void *X,

const int incX, void *Y, const int incY);

---

1. 参数详解
- 参数1：N，size，表示数组的长度
- 参数2：alpha，表示一个复数，乘法的系数
- 参数3：X，表示一个复数数组，表示被乘数
- 参数4：incX，表示被乘数数组的步长
- 参数5：Y，白色一个复数数组，表示乘积
- 参数6：incY，表示乘积数组的步长

# 4. 实例

# 5. 其他

cblas_zaxpy()的参数为双精度浮点数（double）,要使用单精度浮点数（float）就使用参数修改为float类型，函数接口修改为

cblas_caxpy()

---