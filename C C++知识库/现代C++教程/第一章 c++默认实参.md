# 第一章 c++默认实参

# 1. 什么是默认实参

在C++中，默认实参（默认参数）是函数参数的一个默认值，当调用函数时没有为该参数提供实参时，编译器会使用这个默认值。默认实参允许函数调用者在调用函数时省略某些参数，从而简化函数调用。

# 2. 规则

- 默认参数必须从右向左依次指定。
- 类当中的特殊函数，构造，析构等不能添加默认实参
- 
- 默认参数只能出现在函数声明或定义中的一个地方，通常是在函数声明中。
- 如果在函数声明中指定了默认参数，则在函数定义中不能再次指定。

## 2.1. 规则一

**我理解的大概意思是：函数如果第二个行参有默认的实参，后面也必须有**

在函数声明中，所有在拥有默认实参的形参之后的形参必须拥有在这个或同一作用域中先前的声明中所提供的默认实参。你可能觉得很绕，其实说白了就是说，你可以给任何形参默认实参，但是，你需要在当前作用域提前给你已经声明了默认实参的形参后面的形参默认实参。

**上面规则的解释：示例代码**

```cpp
#include <iostream>

// 函数声明
int add(int a, int b = 10, int c = 20);

int main() {
    std::cout << add(5) << std::endl; // 输出 35，因为 b 使用默认值 10，c 使用默认值 20
    std::cout << add(5, 15) << std::endl; // 输出 40，因为 b 被显式设置为 15，c 使用默认值 20
    std::cout << add(5, 15, 25) << std::endl; // 输出 45，因为 b 被显式设置为 15，c 被显式设置为 25
    return 0;
}

// 函数定义
int add(int a, int b, int c) {
    return a + b + c;
}
```

在这个示例中，函数`add`的参数`b`和`c`都有默认值。根据规则，所有在拥有默认实参的形参之后的形参必须拥有默认实参。因此，参数`c`也必须有默认值。

**违反规则的实例：**

如果我们尝试在拥有默认实参的形参之后声明一个没有默认实参的形参，编译器会报错：

```cpp
#include <iostream>

// 错误的函数声明
int add(int a, int b = 10, int c);

int main() {
    std::cout << add(5) << std::endl; // 这将导致编译错误
    return 0;
}

// 函数定义
int add(int a, int b, int c) {
    return a + b + c;
}
```

在这个示例中，参数`c`没有默认值，而参数`b`有默认值，这违反了规则，因此编译器会报错。

总结

在函数声明中，所有在拥有默认实参的形参之后的形参必须拥有默认实参。这意味着你可以给任何形参默认实参，但你需要在当前作用域提前给已经声明了默认实参的形参后面的形参默认实参。

## 2.2. 规则二

**我理解是：构造函数、析构函数、复制构造函数、移动构造函数和赋值运算符，这些特殊的类成员函数，不能添加默认的实参**

对于非模板类的成员函数，类外的定义中允许出现默认实参，并与类体内的声明所提供的默认实参组合。如果类外的默认实参会使成员函数变成默认构造函数或复制/移动(C++11 起)构造函数/赋值运算符，那么程序非良构。对于类模板的成员函数，所有默认实参必须在成员函数的初始声明处提供

**正确是代码示例**

```cpp
#include <iostream>

class MyClass {
public:
    // 类内声明
    void display(int a, int b = 20);
};

// 类外定义
void MyClass::display(int a, int b = 20) {
    std::cout << "a: " << a << ", b: " << b << std::endl;
}

int main() {
    MyClass obj;
    obj.display(10); // 输出 a: 10, b: 20
    obj.display(10, 30); // 输出 a: 10, b: 30
    return 0;
}
```

在这个示例中，`display`函数在类内声明时提供了默认参数`b = 20`，在类外定义时也提供了默认参数`b = 20`。这两者会组合在一起使用。

**错误的代码示例**

如果类外的默认实参会使成员函数变成默认构造函数或复制/移动构造函数/赋值运算符，那么程序将是非良构的：

```cpp
#include <iostream>

class MyClass {
public:
    // 类内声明
    MyClass(int a = 10);
};

// 类外定义
MyClass::MyClass(int a = 10) {
    std::cout << "a: " << a << std::endl;
}

int main() {
    MyClass obj; // 这将导致编译错误，因为它会变成默认构造函数
    return 0;
}
```

## 2.3. 规则三

类模板的成员函数

对于类模板的成员函数，所有默认实参必须在成员函数的初始声明处提供：

```cpp
#include <iostream>

template <typename T>
class MyClass {
public:
    void display(T a, T b = 20); // 必须在初始声明处提供默认实参
};

template <typename T>
void MyClass<T>::display(T a, T b) {
    std::cout << "a: " << a << ", b: " << b << std::endl;
}

int main() {
    MyClass<int> obj;
    obj.display(10); // 输出 a: 10, b: 20
    obj.display(10, 30); // 输出 a: 10, b: 30
    return 0;
}
```

在这个示例中，`display`函数的默认参数在类模板的初始声明处提供。

## 2.4. 规则四

虚函数的覆盖函数不会从基类定义获得默认实参，而在进行虚函数调用时，默认实参根据对象的静态类型确定

在C++中，虚函数的覆盖函数不会从基类定义中继承默认实参，而是在进行虚函数调用时，默认实参根据对象的静态类型确定。

```cpp
#include <iostream>

class Base {
public:
    virtual void display(int a = 10) {
        std::cout << "Base: " << a << std::endl;
    }
};

class Derived : public Base {
public:
    void display(int a = 20) override {
        std::cout << "Derived: " << a << std::endl;
    }
};

int main() {
    Base* basePtr;
    Derived derivedObj;
    basePtr = &derivedObj;

    basePtr->display(); // 输出 "Base: 10"，因为默认参数根据静态类型 Base 确定
    derivedObj.display(); // 输出 "Derived: 20"，因为调用的是 Derived 类的 display 函数

    return 0;
}
```

代码的解释：

- `Base`类中定义了一个虚函数`display`，它有一个默认参数`a = 10`。
- `Derived`类中覆盖了`display`函数，并提供了一个不同的默认参数`a = 20`。
- 在`main`函数中，通过基类指针`basePtr`调用`display`函数时，默认参数根据对象的静态类型`Base`确定，因此使用默认值`10`。
- 直接通过`Derived`对象`derivedObj`调用`display`函数时，使用的是`Derived`类中的默认参数`20`。

## 2.5. 规则五

我的理解是：默认的实参类型不能使用动态的类型

默认实参中可以使用不求值语境的表达式，例如`sizeof`，但不能使用局部变量或非静态的类成员，除非用于构成成员指针或在成员访问表达式中使用。

**正确的示例：**

```cpp
#include <iostream>

class MyClass {
public:
    static int staticVar;

    void display(int a = sizeof(staticVar)) { // 正确：可以在默认实参中使用静态成员
        std::cout << "a: " << a << std::endl;
    }
};

int MyClass::staticVar = 0;

int main() {
    MyClass obj;
    obj.display(); // 输出 a: 4 或 8，取决于系统中 int 的大小

    return 0;
}
```

在这个示例中，使用静态成员`staticVar`在默认实参中是允许的，因为`sizeof`是一个不求值的表达式。

**错误的示例：**

```cpp
#include <iostream>

class MyClass {
public:
    int memberVar;

    void display(int a = sizeof(memberVar)) { // 错误：不能在默认实参中使用非静态成员
        std::cout << "a: " << a << std::endl;
    }
};

int main() {
    MyClass obj;
    obj.display(); // 这将导致编译错误

    return 0;
}
```

在这个示例中，尝试在默认实参中使用非静态成员`memberVar`会导致编译错误。

**总结**

- 默认实参中可以使用不求值语境的表达式，例如`sizeof`。
- 默认实参中不能使用局部变量。
- 默认实参中不能使用非静态的类成员，除非用于构成成员指针或在成员访问表达式中使用。

## 2.6. 静态类型和动态类型

静态类型：对程序进行编译时分析所得到的表达式的类型被称为表达式的静态类型。程序执行时静态类型不会更改。

动态类型：如果某个[泛左值表达式](https://link.zhihu.com/?target=https%3A//zh.cppreference.com/w/cpp/language/value_category)指代某个[多态对象](https://link.zhihu.com/?target=https%3A//zh.cppreference.com/w/cpp/language/object)，那么它的最终派生对象的类型被称为它的动态类型。