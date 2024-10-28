# c++中的转换函数

# 1. 字符串转换函数

# 1. 字符串转整数（int）

atoi()函数是用来将字符串转换为整数（int），其原型为

int atoi(const char * str);

---

【函数说明】：atoi()函数会扫描参数str字符串，跳过前面的空白字符串（空格，tab缩进等）。直到遇到数字或正负号才开始做转换，再遇到非数字或字符串结束（\0）并将结果返回。

【包含头文件】：#include <stdlib.h>

【参数说明】：str：需要转换的字符串

【返回值】：转换成功，返回转换后的字符串，转换失败，返回0

【实例】

#include <stdio.h>

#include <stdlib.h>

#include <string.h>

int main()

{

int val;

char str[20];

strcpy(str, "98993489");

val = atoi(str);

printf("字符串值 = %s, 整型值 = %d\n", str, val);

strcpy(str, "runoob.com");

val = atoi(str);

printf("字符串值 = %s, 整型值 = %d\n", str, val);

return(0);

}

// 结果：

字符串值 = 98993489, 整型值 = 98993489

字符串值 = runoob.com, 整型值 = 0

---

# 2. 字符串转浮点数（double）

c库函数strtod() 是用来将字符串转换为浮点数（double），其原型为：

double strtod(const char *str, char **endptr);

---

【函数说明】：C 库函数 double strtod(const char *str, char **endptr) 把参数 str 所指向的字符串转换为一个浮点数（类型为 double 型）。如果 endptr 不为空，则指向转换中最后一个字符后的字符的指针会存储在 endptr 引用的位置。

【包含头文件】：#include <stdlib.h>

【参数说明】：

- str -- 要转换为双精度浮点数的字符串。
- endptr -- 对类型为 char* 的对象的引用，其值由函数设置为 str 中数值后的下一个字符。

【返回值】：转换成功，返回转换后的数值（double），转换失败，返回0

【实例】：

#include <stdio.h>

#include <stdlib.h>

int main()

{

char str[30] = "20.30300 This is test";

char *ptr;

double ret;

ret = strtod(str, &ptr);

printf("数字（double）是 %lf\n", ret);

printf("字符串部分是 |%s|", ptr);

return(0);

}

// 结果：

数字（double）是 20.303000

字符串部分是 | This is test|

---

1. 类型转换运算符

在c++当中有四种类型转换运算符，使用的时候需要确保转换是安全的，否则会出现未定以的行为

1. static_cast：这是最常用的类型转换。它可以在任何不包含底层 const 的类型之间进行转换，但是转换的

类型需要是相关的。例如，你可以将一个 int 转换为 float，或者将一个基类指针转换为派生类指针。

int i = 10;

float f = static_cast<float>(i);  // 将 int 转换为 float

1. dynamic_cast：这种类型转换主要用于类层次结构中基类和派生类之间的转换。它包含了类型检查，只有

确定转换是安全的时候才会进行。

Base* b = new Derived();

Derived* d = dynamic_cast<Derived*>(b);  // 将 Base* 转换为 Derived*

1. const_cast：这种类型转换用于修改类型的 const 或 volatile 属性。例如，你可以使用 const_cast 来获取一个 const 对象的非 const 引用，然后修改这个对象。

const int ci = 10;

int& ri = const_cast<int&>(ci);  // 获取 ci 的非 const 引用

ri = 20;  // 修改 ci

1. reinterpret_cast：这种类型转换会产生一个新的值。它可以在任何指针或整数类型之间进行转换，但是结果是依赖于机器的。

int i = 10;

int* p = reinterpret_cast<int*>(i);  // 将 int 转换为 int*