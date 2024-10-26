# c++中使用函数模板报错

使用函数模板的过程中，在类里面定义了一个函数模板，按照普通类的定义方式，将声明放在.h头文件中，将函数体放在.cpp文件中，既模板函数的声明和定义分开，编译的时候出现了”无法解析的外部符号“【C++编译器不支持模板的分离式编译】

当我们声明和定义一个模板的时候，必须要让声明和定义放在一个文件中，否则编译器报错

【解决办法：】

- 将类的声明和定义放在同一个.h文件中
- 在类模板出现的.cpp文件对应的include.cpp文件
- 在主函数所在的main.h中的include.cpp文件
- 模板函数实例化，模板函数实例化全局声明（dll文件也需要实例化全局声明）

template <typename T>

void Swap(T &a, T &b);

/*obj文件*/

template void Swap<int>(int &a, int &b);

/*dll文件*/

template __declspec(dllexport) void Swap<int>(int &a, int &b);

---

【原理】：

首先，一个编译单元是指一个.cpp文件以及它所在#include的所有.h文件，.h文件里的代码将会被扩展到包含她的.cpp文件里，然后编译器编译该.cpp文件为一个obj文件（平台为win32），后者拥有PE（Windows可执行文件）文件格式，并且本身包含的就是二进制码，但是不一定能够执行，因为并不保证其中一定有main函数，当编译器将一个工程里所有的.cpp文件以分离的方式编译完毕后，再由链接器进行链接成为一个.exe文件

//---------------test.h-------------------//

void f();//这里声明一个函数f

//---------------test.cpp--------------//

#include”test.h”

void f()

{

… //dosomething

}

//这里实现出test.h中声明的f函数

//---------------main.cpp--------------//

#include”test.h”

int main()

{

f(); //调用f，f具有外部连接类型

}

- --------------------

---

在这个例子中，test.cpp和main.cpp各自被编译成不同的.obj文件，在main.cpp中，调用了f函数，然而当编译器编译mian.coo时，他所仅仅知道的只是main.cpp中所包含的test.h文件中的一个关于void f()；的声明，所以，编译器将这里的f看作外部链接类型，既认为他的函数实现代码在另外一个obj文件中，本例也就是test.obj，也就是说，main.obj中实际没有关于f函数的哪怕一行二进制代码，而这些代码实际存在于text.cpp所编译成的test.obj中，在main.obj中对f的调用只会生成一行call指令，像这样

call f [C++中这个名字当然是经过mangling[处理]过的]

---

在编译时，这个call指令显然是错误的，因为main.obj中并无一行f的实现代码。那怎么办呢？这就是连接器的任务，连接器负责在其它的.obj中（本例为test.obj）寻找f的实现代码，找到以后将call f这个指令的调用地址换成实际的f的函数进入点地址。需要注意的是：连接器实际上将工程里的.obj文件“连接”成了一个.exe文件，而它最关键的任务就是上面说的，寻找一个外部连接符号在另一个.obj中的地址，然后替换原来的“虚假”地址。

【这就是大概的过程。其中关键就是】

编译main.cpp时，编译器不知道f的实现，所以当碰到对它的调用时只是给出一个指示，指示连接器应该为它寻找f的实现体。这也就是说main.obj中没有关于f的任何一行二进制代码。

编译test.cpp时，编译器找到了f的实现。于是乎f的实现（二进制代码）出现在test.obj里。

连接时，连接器在test.obj中找到f的实现代码（二进制）的地址（通过符号导出表）。然后将main.obj中悬而未决的call XXX地址改成f实际的地址。完成。

然而，对于模板，你知道，模板函数的代码其实并不能直接编译成二进制代码，其中要有一个“实例化”的过程。

//----------main.cpp------//

template<class T>

void f(T t)

{}

int main()

{

…//do something

f(10);  // call f<int> 编译器在这里决定给f一个f<int>的实例

…//doother thing

}

- --------------------

---

也就是说，如果你在main.cpp文件中没有调用过f，f 也就得不到实例化，从而main.obj中也就没有关于f 的任意一行二进制代码！如果你这样调用了：

f(10); // f<int>得以实例化出来

f(10.0); // f<double>得以实例化出来

---

这样main.obj中也就有了f，f两个函数的二进制代码段。以此类推。

然而实例化要求编译器知道模板的定义，不是吗？

看下面的例子（将模板的声明和实现分离）：

//-------------test.h----------------//

template<class T>

class A

{

public:

void f(); // 这里只是个声明

};

//---------------test.cpp-------------//

#include”test.h”

template<class T>

void A<T>::f()  // 模板的实现

{

…//do something

}

//---------------main.cpp---------------//

#include”test.h”

int main()

{

A<int> a;

a.f();    // #1

}

- --------------------

---

编译器在#1处并不知道A::f的定义，因为它不在test.h里面，于是编译器只好寄希望于连接器，希望它能够在其他.obj里面找到A::f的实例，在本例中就是test.obj，然而，后者中真有A::f的二进制代码吗？

NO！！！因为C++标准明确表示，当一个模板不被用到的时侯它就不该被实例化出来，test.cpp中用到了A::f了吗？没有！！所以实际上test.cpp编译出来的test.obj文件中关于A::f一行二进制代码也没有，于是连接器就傻眼了，只好给出一个连接错误。但是，如果在test.cpp中写一个函数，其中调用A::f，则编译器会将其实例化出来，因为在这个点上（test.cpp中），编译器知道模板的定义，所以能够实例化，于是，test.obj的符号导出表中就有了A::f这个符号的地址，于是连接器就能够完成任务。

关键是：

在分离式编译的环境下，编译器编译某一个.cpp文件时并不知道另一个.cpp文件的存在，也不会去查找（当遇到未决符号时它会寄希望于连接器）。这种模式在没有模板的情况下运行良好，但遇到模板时就傻眼了，因为模板仅在需要的时候才会实例化出来，所以，当编译器只看到模板的声明时，它不能实例化该模板，只能创建一个具有外部连接的符号并期待连接器能够将符号的地址决议出来。然而当实现该模板的.cpp文件中没有用到模板的实例时，编译器懒得去实例化，所以，整个工程的.obj中就找不到一行模板实例的二进制代码，于是连接器也黔驴技穷了。