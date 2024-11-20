# 第一章 C++的简介

## 1. 简介

1. 条款-01：视c++为一个语言联邦
2. C++是一种通用的编程语言，由Bjarne Stroustrup在20世纪80年代初开发。它是C语言的扩展，增加了面向对象编程、泛型编程和低级内存操作等特性。C++被广泛应用于系统编程、游戏开发、嵌入式系统、金融工程等领域。
3. C++的语言特性包括多种编程范式，如面向对象编程、泛型编程等。这些编程范式的存在是为了提供灵活的工具和方法，以解决不同的**程序设计问题**

### 代码部分

1. 代码仓库：[std_stu](https://github.com/ZhanghHaoDev/std_stu)
2. 开发环境：C++20，macos，cmake，vscode，llvm

### C++ 参考资料

+ 网站：
  - [cppreference](https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5)
  - [cplusplus](https://legacy.cplusplus.com/)
  - [C++ 核心指导方针](https://github.com/lynnboy/CppCoreGuidelines-zh-CN?tab=readme-ov-file)
  - [小彭老师领衔编写，现代C++的中文百科全书](https://github.com/parallel101/cppguidebook)
+ 书籍：
  - C++ Primer（以这个为主导）
  - C++标准库：第二版
  - C++ 20 红宝书
  - C++程序设计语言
  - STL 内核剖析
  - Effective STL中文版：50条有效使用STL的经验
+ 工具：
  - cppman

## 2. C++的知识体系

### 语法部分
1. 基本语法
+ 变量和基本数据类型
+ 运算符和表达式
+ 控制流语句

2. 函数
+ 函数的定义和声明
+ 函数参数和返回值
+ 函数重载和默认参数
+ 内联函数和递归函数

3. 类和对象
+ 类的定义和声明
+ 类的成员变量和成员函数
+ 构造函数和析构函数
+ 访问控制和封装
+ 继承和派生

4. 模板
+ 函数模板和类模板
+ 模板特化和模板偏特化
+ 可变参数模板

### 标准库部分

1. 标准模板库 STL （Standard Template Library）
C++的标准模板库（STL）是C++标准库的核心，基于泛型编程，包含容器、迭代器、算法和函数对象等组件，需要重点关注每个组件的原理和内部实现：
+ 容器（Containers）：vector、list、deque、set、map、unordered_set、unordered_map
+ 算法（Algorithms）：sort、find、copy、transform、accumulate、count
+ 迭代器（Iterators）：input_iterator、output_iterator、forward_iterator、bidirectional_iterator、random_access_iterator
+ 仿函数（Functors）：plus、minus、multiplies、divides、modulus、negate
+ 适配器（Adapters）：stack、queue、priority_queue
+ 配接器（Binders）：bind、mem_fn、function、lambda

1. 输入输出流（I/O Streams）
C++标准库提供了一组类和函数，用于处理输入和输出操作。主要包括：
+ 标准输入输出流 ：std::cin、std::cout、std::cerr、std::clog
+ 文件流： ifstream、ofstream、fstream
+ 字符串流： istringstream、ostringstream、stringstream
+ 基础流类：std::ios、std::istream、std::ostream、std::iostream
+ 字符串流类：std::istringstream、std::ostringstream、std::stringstream

1. 字符串和正则表达式（Strings and Regular Expressions）
C++标准库提供了强大的字符串处理功能和正则表达式支持。
+ 字符串类：如std::string、std::wstring。
+ 字符串操作（String Operations）：如std::find、std::replace、std::substr。
+ 正则表达式：如std::regex、std::smatch、std::regex_search、std::regex_replace。

1. 多线程和并发（Multithreading and Concurrency）
C++标准库提供了多线程和并发编程的支持。
+ 线程类：如std::thread。
+ 互斥量：如std::mutex、std::recursive_mutex。
+ 条件变量：如std::condition_variable。
+ 原子操作：如std::atomic。

1. 时间和日期（Time and Date）
C++标准库提供了处理时间和日期的功能。
+ 时间点：如std::chrono::time_point。
+ 时钟：如std::chrono::system_clock、std::chrono::steady_clock。
+ 时间间隔：如std::chrono::duration。

1. 数学库（Math Library）
C++标准库提供了常用的数学函数和常量。
+ 数学函数：如std::abs、std::sqrt、std::pow、std::sin、std::cos、std::tan。
+ 随机数生成：如std::random_device、std::mt19937、std::uniform_int_distribution

1. 类型支持库（Type Support Library）
类型支持库提供了类型特征和类型转换的功能。
+ 类型特征：如std::is_same、std::is_integral、std::is_floating_point。
+ 类型转换：如std::static_pointer_cast、std::dynamic_pointer_cast。

1. 内存管理库（Memory Management Library）
内存管理库提供了内存分配和管理的功能。
+ 智能指针：如std::unique_ptr、std::shared_ptr、std::weak_ptr。
+ 内存分配：如std::allocator、std::allocate_shared。

1. 错误处理库（Error Handling Library）
错误处理库提供了异常处理和错误报告的功能。
+ 异常类：如std::exception、std::runtime_error、std::logic_error。
+ 错误代码：如std::error_code、std::error_condition。

### 面向对象部分

面向对象编程是C++语言的一个重要特性，它通过类和对象的方式组织代码，提高了代码的可维护性和可重用性。以下是面向对象部分的知识体系：
1. 基本概念
+ 类（Class）：
    类的定义和声明。
    成员变量和成员函数。
    访问控制（public、protected、private）。

+ 对象（Object）：
    对象的创建和使用。
    对象的生命周期。

2. 构造函数和析构函数
+ 构造函数（Constructor）：
    默认构造函数。
    带参数的构造函数。
    拷贝构造函数。
    移动构造函数（C++11）。

+ 析构函数（Destructor）：
    析构函数的定义和使用。
    析构函数的自动调用。
3. 继承（Inheritance）
+ 单继承：
    基类和派生类。
    继承的访问控制（public、protected、private继承）。
+ 多继承：
    多继承的定义和使用。
    菱形继承问题和虚继承。

4. 多态（Polymorphism）
+ 虚函数（Virtual Function）：
    虚函数的定义和使用。
    虚函数表（vtable）。

+ 纯虚函数和抽象类：
    纯虚函数的定义。
    抽象类的定义和使用。

+ 运行时类型识别（RTTI）：
    typeid操作符。
    dynamic_cast操作符。

5. 封装和数据隐藏（Encapsulation and Data Hiding）
+ 封装：
    使用类和对象实现封装。
    通过访问控制隐藏实现细节。

+ 友元（Friend）：
    友元函数。
    友元类。

6. 运算符重载（Operator Overloading）
+ 运算符重载的基本概念：
    运算符重载的定义和使用。
    成员函数和非成员函数的运算符重载。

+ 常见运算符的重载：
    算术运算符（+、-、*、/）。
    关系运算符（==、!=、<、>）。
    赋值运算符（=）。
    输入输出运算符（<<、>>）。

7. 模板类（Template Classes）
+ 类模板的定义和使用：
    类模板的基本语法。
    类模板的实例化。

+ 模板特化：
    完全特化和部分特化。

8. 智能指针（Smart Pointers）
+ 智能指针的基本概念：
    智能指针的定义和使用。
    智能指针的类型（std::unique_ptr、std::shared_ptr、std::weak_ptr）。

+ 智能指针的实现原理：
    引用计数。
    自动内存管

### 泛型编程部分

泛型编程是C++语言中的一个重要编程范式，它允许编写与类型无关的代码，使得代码可以处理多种数据类型。C++中的泛型编程主要通过模板（Templates）来实现。以下是泛型编程部分的知识体系：

1. 模板基础

函数模板（Function Templates）：
+ 定义和使用函数模板。
+ 模板参数推导。
+ 显式模板参数。

类模板（Class Templates）：
+ 定义和使用类模板。
+ 模板成员函数。
+ 模板特化（Template Specialization）。

2. 高级模板技术

模板特化（Template Specialization）：
+ 完全特化（Full Specialization）。
+ 部分特化（Partial Specialization）。

模板元编程（Template Metaprogramming）：
+ 编译时计算。
+ 递归模板。
+ SFINAE（Substitution Failure Is Not An Error）。

可变参数模板（Variadic Templates）：
+ 定义和使用可变参数模板。
+ 展开参数包。
