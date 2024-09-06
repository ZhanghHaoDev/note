# c++中的数组与指针

c++ 是支持数组数据结构的，可以存储应该固定大小的相同类型元素的顺序集合

数组与vector相比，数组的大小是固定的，如果不清楚元素的个数，应该使用vector

# 声明数组

1. c++中声明一个数组需要指定数组元素的。
2. 使用指针数组之前必须先申请空间，必须初始化，否则会出现写入权限不够或数据错误的事情
3. 二维指针申请空间

double **ptr = new double*[10];

for(int i = 0 ;i < 10;i++)

{

ptr[i] = new double[10];

}

---

上面是二维指针如何申请空间，但注意下面这些申请空间的方法是错误的

double ** ptr = new double[10][10]; // 错误，编译器过不去

double ** ptr = new double[10*10]; // 申请了100个double类型的指针

---

1. 单个指针赋值

double *num1 = 10;

double * num2;

num2 = num1;

---

1. 指针数组赋值

double *num1 = new double[10];

double *num2;

for(int i =0;i<10;i++)

{

num1[i] = i;

}

// 直接这样赋值是错误的

num2 = num1;

// 应该这样赋值

// 首先申请空间

num2 = new double[10];

// 然后再赋值

for(int i = 0;i< 10;i++)

{

num2[i]=num1[i];

}

---

# 指针数组的初始化

使用指针之前必须先初始化，可以将指针先定义为NULL或者nullptr，

NULL和nullptr的区别

1. NULL说c语言里面定义的一个宏，被定义为空，NULL替换的说数字整型的0
2. nullptr是c++的关键字，nullptr代表的是空指针。

---

# 数组作为函数参数（形参）

### 1. 数组有两个特殊的性质

1. 不允许数组的拷贝和赋值：不能将数组的内容拷贝给其他数组作为其初始值，也不能用数组为其他数组赋值

int a[] = {0,1,2}; // 含有三个整数的数组

int a2[] = a;         // 【错误】不允许使用一个数组初始化另一个数组

a2 = a;               // 【错误】不允许把另一个数的值，直接赋给另一个数

---

1. 使用数组的时候，通常转换为指针

通过以上的两个性质来看，数组无法拷贝，因此数组无法以值传递的方式使用数组参数，因为数组会被转换成指针，所以当我们为函数传递一个数组时，实际上传递的是指向数组首元素的指针

### 2. 函数数组形参的传递

不能因值传递的方式传递数组，但是可以写成形参类似的数组的形式

// 形式不同，但是这三个print()函数是等价的

// 每个函数都有一个const int*类型的形参

void print(const int*);

void print(const int[]); // 可以看出，函数的意图是作用与一个数组

void print(const int[10]); // 这里的维度表示我们期望数组含有多少个元素，实际不一定

---

尽管表现形式不同，但上面三个参数是等价的，每个函数唯一的类型的形参都是是const int*类型的，函数在运行的时候，只检查传入的参数是否为const int*

【注意】：和其他使用数组的代码由于，以数组作为形参的函数也必须保证使用数组时不会越界

因为数组，是以指针的形式传递给函数的，所以数组一开始并不知道数组的确切尺寸。通常有三种方法对数组进行管理。

1. 使用标记制定数组长度

void print(const char *cp)

{

if(cp)        // 若cp不是一个空指针

while(*cp)    // 指针所指的字符不是空字符串

cout << *cp++;    // 输出当前字符并将指针向前移动一个位置

}

---

该种方法只适用于那些有明显标记不会与普通数据混淆的情况，但是对于像int这种所用取值都合法的数据就不好处理

1. 使用标记指定数组长度

void print(const int *beg,const int *end)

{

// 输出beg到end之间（不含end）的所有元素

while(beg != end)

cout << *beg++ <<endl;

}

---

1. 显示传递一个表示数组大小的形参

// const int ia[] 等价于const int* ia

// size 表示数组的大小，将他显示地传递给函数用于控制对ia元素的访问

void print(const int ia[],size_t size)

{

for(size_t i = 0;i != size;i++)

cout << ia[i] <<endl;

}

---

### 3. 函数数组的引用传值

c++语言允许将变量定义成数组引用，基于同样的道理，形参也可以的数组的引用。此时，引用形参绑定到对应的实参上，也就是绑定到数组上。

// 【正确】：形参是数组的引用，维度是类型的一部分

void print(int (&arr)[10])

{

for(auto elem : arr)

cout <<elem <<endl;

}

---

上述写法，数组的大小构成数组的一部分，只要不超过维度，就可以在函数体内，放心使用数组。但是，这一用法无形中，限制了print()函数的可用性，我们只能将函数作用于大小为10的数组

int i = 0,j[2] = {0,1};

int k[10] = {0,1,2,3,4,5,6,7,8,9};

print(&i);    // 【错误】：实参不是含有10个整数的数组

print(j);    // 【错误】：实参不是含有10个整数的数组

print(k);    // 【正确】：实参含有10个整数的数组

---

### 4. char* 字符串

在传递字符串的时候，字符串作为函数参数，并且不需要改变参数的值的时候，我们使用const char*

并且函数的形参参数类型只能定义为const cahr*，不能定义为char*，具体原因：

void fun(const char* str); // 编译器不报错

void fun1(char* str2);// 编译不报错，调用的时候报错

char* str = "ssss";

fun1(str);    // 报错，应该修改为const char*

---

1. 保证了实参不能被修改，增加了安全性
2. 扩大了该函数的参数接收范围，使得函数更具有通用性

### 5. 形参为指针，输入参数为普通类型参数

有下面的函数，参数形参为指针，函数 作用是交换两个变量的值

void fun(int *a,int *b)

{

int temp = a;

a = b;

b = temp;

}

// 我们还可以传递普通非指针变量的地址进去

int a = 9,b = 4;

fun(&a,&b);

---

这样写也是可以的，如果函数形参为二维指针，我们也可以传递进去一维指针的地址进去，来实现函数的作用，这样可以可以起到改变函数值的作用

# 指针数组作为函数形参

指针作为函数行参传递参数的时候有两种形式，值传递和引用传递。

值传递不会改变原来的值本身，而引用传递则会改变值本身

引用传递需要使用到引用符号 &

// 值传递 ：交换两个变量的值,函数外不改变值

void fun1(int *a,int *b)

{

cout << "a的值是："<< a << "b的值是："<< b << endl;

// 交换两个值

int *temp = 0;

temp = a;

a = b;

b = temp;

cout << "在函数内部这两个值会引起改变"<< endl;

cout << "a的值是：" << a << "b的值是："<< b <<endl;

}

// 引用传递：交换两个变量的值，函数外也改变值

void fun2(int *&a,int *&b)

{

// 在这个函数中我们使用&取地址符，可以将函数外的值改变

cout << "a的值是：" << a << "b的值是：" << b <<endl;

// 交换两个值

int *temp = 0;

temp = a;

a = b;

b = temp;

cout << "在函数内部这两个值会引起改变" << endl;

cout << "a的值是：" << a << "b的值是："<< b <<endl;

}

int main()

{

// 值传递

int *a = 1，*b = 2;

fun1(a,b);

// 这里将连个参数传递进去函数，值在函数里面会发生改变，

// 但是当函数执行完毕，这里并不会引起函数的改变

cout << "a的值是："<< a << "b的值是：" << b << endl;

// 结果： a = 1，b = 2

// 引用传递

fun2(a,b);

// 引用传递改变两个值本身，在函数外也可以

cout << "a的值是：" << a << "b的值是："<< b <<endl;

// 结果：a = 2， b = 1

}

---

文章： [https://blog.csdn.net/m0_51701233/article/details/122416306](https://blog.csdn.net/m0_51701233/article/details/122416306)

# 数组与指针的size

1. 普通的数组在定义的时候就必须给大小

int array[10] = {0};

---

1. 没有给定大小的数组也要赋初值

int array[] = {1,2,3,4,5,6,7,8};

// sizeof求大小

int size = sizeof(array) / sizeof(array[]);

int size = sizeof(array) / sizeof(array[0]);

---

1. 指针数组的在使用之前是需要new来申请大小的

int *array = new int[10];

---

这个时候指针元素的个数就是你new的大小

1. 如果对new出来的指针求大小，那么指针的大小为4

# 如何获取一维数组的个数

#include <iostream>

#include <algorithm>

int main()

{

int arr[] = { 5, 3, 7, 6, 8, 2 };

int target = 7;

int n = sizeof(arr) / sizeof(*arr);

bool exists = std::find(arr, arr + n, target) != arr + n;

if (exists) {

std::cout << "Element found";

}

else {

std::cout << "Element not found";

}

return 0;

}

---

但是指针不能这样使用，sizeof()指针的话，指针的size永远都是4，

int* temp_array = nullptr;

temp_array = new int[10];

for (int i = 0; i < 10; i++)

{

temp_array[i] = i;

}

int size = sizeof(temp_array) / sizeof(*temp_array);

---

# 内存的申请与释放

在c++中要注意内存的神与释放，当你new一块内存之后，一定要在内存的生命周期结束之后，对内存进行释放，防止内存的泄漏；

// 一维指针的内存申请与释放

// 申请内存

double *data = new double[100];

for (int i = 0;i<100;i++)

{

data[i] = i;

}

// 释放内存

delete data;

// 二维指针的内存申请与释放

// 申请内存

double **date_2d = new double[10];

for (int i = 0;i < 10; i++)

{

data_2d[i] = new double[10];

}

// 释放内存

for (int i = 0;i < 10; i++)

{

delete []data_2d[i];

}

---

在c++中 delete是释放new分配的单个对象的指针所指向的内存

delete[]则是释放new分配的对象数组指针所指向的内存

# 获取固定位置的数据

1. 一维指针

int *sum = new int[10];

for (int i = 0;i<10;i++)

{

sun[i] = i;

}

int num = sum + 5;

cout << num << endl;

// 输出sum的第五个数值

---

1. 二维指针

int **sum = new int*[10];

for (int i = 0;i<10;i++)

{

sum[i] = new int[10];

for(int j=0;j<10;j++)

{

sun[i][j] = i;

}

}

int *num = sum + 5;

cout << num << endl;

// [注意]：二维数组得首先获取固定行的地址，然后再获取固定位置的元素

---

# char*与char[]

1. char*是一个字符指针，而cahr[]是一个字符数组
2. char*是通过new来申请内存的，通过delete来释放内存。

char[]是通过[]方括号内的数字来申请内存的，或者通过直接赋值来确定内存的，不需要释放内存

1. char*是动态申请内存，可以使用变量来申请，但char[]只能通过常量来申请内存，是固定的
2. 但如果char*和char[]作为函数参数是没有区别的，两者起到同样的作用

在c++中指针是先申请空间还是先初始化

1. 如果需要初始化为0，则先申请空间，利用循环把每个值赋值为0，或者使用memset()函数

2. 如果需要初始化为null，则先初始化，再申请空间