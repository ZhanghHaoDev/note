# c++优化程序效率

降低函数运行时间，提高函数运行效率

我们在创建函数的时候，尽量使用函数形参的方式获取输出，而不是返回值的形式

因为函数返回值需要重复创建变量，在循环中很浪费空间，而使用形参的方式，我们就可以，提前在函数外边申请好空间，在调用函数的时候，该函数只需要赋值的查找。不需要重复申请空间

// 返回值的形式

// 重复申请空间，造成浪费

double* matrixMultiply(double* a, double b,int size){double * c = new double[size];

for (int i = 0; i < size; i++){c[i] = a[i] * b;}

return c;}

// 函数参数的形式

// 调用函数之前就提前申请空间

void matrixMultiply(double* a, double b, double *c,int size){for (int i = 0; i < size; i++){c[i] = a[i] * b;}

return c;}