# 第二十章 关于vptr和vtbl

# 关于vptr和vtbl

继承：子类继承父类不仅仅继承了父类的成员数据，同样继承了父类的成员函数，这样子类就可以调用父类的成员函数。

子类也继承了父类函数的调用权限

class A

{

virtual void vfunc1();

virtual void vfunc2();

void func1();

void func2();

};

class B : public A

{

virtual void vfunc1();

void func2();

};

class C : public B

{

virtual void vfunc2();

void func1();

};

---

vptr:是一个指针，指向一个vtbl，vtbl是一个数组，数组中每个元素是一个指针，指向一个函数的地址

vtbl:是一个数组，数组中每个元素是一个指针，指向一个函数的地址

# 关于this

虚函数在使用的时候有两种方式：

1. 一种是多态，继承
2. 第二种是模版

this指针： this指针是一个指针，指向当前对象的地址。

动态绑定的三个条件：

1. 当前对象是指针
2. 他有一个向上（父类）转型的动作
3. 调用了虚函数

# 关于dynamic binding

# 关于new和delete

都是表达式

new：先分配memery，再调用ctor

delete：调用dtor，然后释放memery

# 重载new和delete

注意：重载new和delete是会影响全局的

# 重载成员类的new和delete

class Foo

{

public:

void* operator new(size_t size);

void operator delete(void*,size_t);

...

};

---

我们可以重载class member operator new()，写出多个版本的，前提是每一个版本的声明都必须有独特的参数列，其中第一参数必须是size_t，其余参数以new所指定的placement arguments为初值，出现new(...)小括号内的便是所谓的placement arguments。

Foo* pf= new (300,'c')Foo;

---

我们也可以重载class member operator delete()，写出多个版本，但是他们绝对不会被delete调用。**只有当new所谓的ctor抛出exception时，才会调用这些重载版本的operator delete()。**

他只可能这样被调用，主要用来归还未能完全创建成功的object所占用的memery。