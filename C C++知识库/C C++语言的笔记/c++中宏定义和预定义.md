# c++中宏定义和预定义

# 宏定义

宏定义其作用是给程序中的常量，表达式和函数取一个名字，方便在后续程序中直接调用，值得注意的是一般只占一行，如果字段码比较多，跨行用 ‘\’，可以看下面的例子

// 定义符号常量

#define PI 3.1415926

// 定义表达式

#define Max(a,b) (a) > (b) ? a : b

// 定义字码段 宏定义只占一行，其中的'\' 是为了跨行使用

#define P(a){ \

printf("%d \n",a);    \

}

---

在c语言中常使用#define来定义符号常量，但是在c++中最好使用const来定义常量

#define PI 3.1415926

const long double PI = 3.1415926

两者比较，c语言中没有类型的指定容易引起不必要的麻烦，而c++中定义清楚，所以在c++中推荐使用const来定义常量

# #define的缺点

1. 不支持类型检查
2. 不考了作用域
3. 符号名不能限制在一个命名空间中

# 宏定义与常量

众所周知，常量也有给数据取名字之说，例如定义一个常量PI=3.1415926。不同的是宏定义的作用域是全局的，常量的作用域有全局和局部之分。如果在一个函数内部定义了一个常量，那么这个常量只能在这个函数内部使用。但是在一个函数内部定义了一个宏定义，那么这个宏定义在函数外部也是可以调用的。为了书写规范，宏定义一般放在程序开始的位置，方便查看。

# 预定义

# c/c++的编译过程

简单的c++程序

// hello.cpp

#include <isotream>

int main()

{

printf("hello world!\n");

}

---

编译的过程

$ gcc hello.cpp                   # 编译

$ ./a.out                         # 执行

hello world!                      # 输出

---

gcc的命令其实依次执行了四步操作

1. 预处理
2. 编译
3. 汇编
4. 链接

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309300102-96d29ea9-d772-4f0a-863c-65d482dd0ee1.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309300102-96d29ea9-d772-4f0a-863c-65d482dd0ee1.png)

---

# 预定义

预定义是一种特殊的C/C++编译机制，其功能就是使一些变量或函数需要在程序被编译之前就被读取。如上图，在编译（Compilation，对应也称之为编译器）之前会对程序进行预编译（Preprocessing，对应也称之为预编译器或预处理器），它会搜索程序里边带"#" 的代码，然后把它们提前给编译了， 之后再启动编译器进行编译。预定义指令其实是为了配合这种机制而定义出来的旨在我们的程序中对需要与处理的代码段进行标识的一种命令。他的作用包括宏定义，文件包含，和条件编译。

C/C++语言没有内置工具在编译时间包含其他源文件、宏定义，或根据条件包含或排除一些代码行的编译时指令。预处理器提供了这些能力。虽然当前大多数编译器内部集成了预处理器，人们还是认为预处理独立于编译器的过程。预处理器读取源代码，查找预处理指令语句和宏调用，然后翻译源代码，它还去掉程序中的注释和多余的空白。

1. 下面为预定义指令，最终被嵌入到代码中，与其他的代码一起被编译器编译。

#define          宏定义

#undef           未定义宏

#include         文本包含

#ifdef           如果宏被定义就进行编译

#ifndef          如果宏未被定义就进行编译

#endif           结束编译块的控制

#if              表达式非零就对代码进行编译

#else            作为其他预处理的剩余选项进行编译

#elif            这是一种#else和#if的组合选项

#line            改变当前的行数和文件名称

#error           输出一个错误信息

#pragma          为编译程序提供非常规的控制流信息

---

1. 预编译的优点
2. 可以防止头文件被多次引用
3. 可以方便解决代码跨平台编译问题
4. 可以根据自定义变量灵活执行程序
5. 内置宏

__LINE__      ：行号（数字）

__FILE__      :文件路径及名称（字符串）

__DATE__      :日期（字符串）

__TIME__      :时间（字符串）

__FUNCTION__  ：当前执行方法名

---

内置宏和预编译指令, 在代码调试、单元测试、跨平台代码中经常会用到。

具体可以看以下代码实例：

#ifndef __TEST_H

#define __TEST_H

#include<iostream>

using namespace std;

class Test

{

public:

Test(int value){

this -> val = value;

}

void print()

{

cout << "this val is :" << this->val << endl;

cout << "this line is :" << __LINE__ << endl;

cout << "this function is :" << __FUNCTION__ << endl;

cout << "this date is :" << __DATE__ << endl;

}

#ifdef TEST_DEF    // 若定义了 TEST_DEF，则声明变量val为public; 否则为private

public:

#else

private:

#endif

int val;

};

#endif

---

#include"test.h"

using namespace std;

int main()

{

Test t(6);

t.print();

#ifdef TEST_DEF     // 判断编译是否加-DCODE_TEST, 则会执行下面到代码

cout << "this TEST_DEF val : " << t.val << endl;

#endif

return 0;

}

---

执行：

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309300108-2fa7be63-335d-465f-9e6d-c3b010015a06.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309300108-2fa7be63-335d-465f-9e6d-c3b010015a06.png)

---