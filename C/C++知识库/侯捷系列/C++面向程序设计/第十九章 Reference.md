# 第十九章 Reference

# Reference

在内存中分为三个区域：

value: 值区，存储数据

reference: 引用区

指针：指向value区的某个地址

int x=0;

int* p = x;

int& r = x; // r代表X，现在r,x 都是0

int x2 =5;

r = x2; // r不能代表其他变量，现在r,x都是5

int& r2 = r;    // 现在r2是5

---

reference的常见用途：

很少用来声明一个变量，经常用来声明一个函数的参数以及返回值

void func1(Cls* pobj) {pobj->XXX();}

void func2(Cls obj) {obj.XXX();}

void func3(Cls& robj) {robj.XXX();}

...

Cls obj;

func1(&obj); // 参数是指针

func2(obj); // 参数是对象

func3(obj); // 参数是引用

---

如果两个函数重载，函数名称相同，参数列表相同，单其中一个的参数加了&引用，

那这个函数就不能算作是重载

# 继承关系下的构造和析构

复习：

class Base

{};

class Derived public: Base

{};

---

**构造由内而外调用**

Derived的构造函数首先调用Base的构造函数，然后调用Derived的构造函数

**析构由外而内调用**

Derived的析构函数首先调用Derived的析构函数，然后调用Base的析构函数

# 复合关系下的构造和析构

构造由内而外调用

析构由外而内调用