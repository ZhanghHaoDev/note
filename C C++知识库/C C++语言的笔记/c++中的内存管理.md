# c++中的内存管理

# memset()函数

函数作用：memset函数常用于将一块内存设置为一个值

函数原型：void* memset(void* ptr, int value, size_t num);

函数参数：

其中，ptr为要设置的内存区域的指针，value为要设置的值，num为要设置的内存区域的大小（以字节为单位）。

函数示例：

char myArray [50];          // define an array of characters

memset (myArray, 'x', 50);  // set the first 50 elements of myArray to 'x'

该函数也可以用于清零等作用

【注意】：在申请二维指针的时候，不能使用该函数，

可以用于一维指针的，但在二维指针的使用的时候，需要将二维里面的一维先初始化，不能直接初始化二维

# 关于c++函数中神内存的问题

原则是：谁申请，谁管理

在c++中，申请内存尽量不在函数内部申请，而在函数调用的地方申请，以便内存的释放

如果必须在被调用函数中申请内存，则记得申请和释放

要保持一个良好的内存管理习惯

范例：

// 好习惯

void func(int* ptr)

{

...

}

int main()

{

int* ptr = new int[10];

func(ptr);

delete[] ptr;

return 0;

}

// 坏习惯

void func(int* ptr)

{

ptr = new[10];

delete[] ptr;

}

int main()

{

int* ptr = nullptr;

func(ptr);

return 0;

}

---

在上面的代码中，我们在调用函数的时候并不一定知道该函数中是否会去申请内存，

所以我们在编写自定义函数的时候，一定要在调用函数的位置去管理内存

# 关于c++中的变量初始化

在定义普通变量和指针的时候，一定要初始化

变量的三要素：类型，名称，初始值

# string与auto

我们在定义string数组的时候，也可以使用auto关键字来输出数组内容

int main()

{

string temp_str[5] = {"aa","bb","cc","dd","ee"};

for(auto ite : temp_str)

{

cout << ite << endl;

}

return 0;

}

---