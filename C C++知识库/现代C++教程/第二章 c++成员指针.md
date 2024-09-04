# 第二章 c++成员指针

1. 成员指针分为成员函数指针，数据成员指针，注意，数据成员指针或虚函数成员指针并没有真的指向一个内存，它只是表示表示在当前的类，那个字段的位置而已，比如&X::value表示的只是这个数据成员value在X类中的位置。
2. 数据成员指针和虚成员函数指针是一个类似偏移量的东西，成员函数指针则真的存储了一个地址。（我们将在最后为了讲述这个）
3. 成员指针也没办法脱离类的实例对象单独使用，不管是非静态数据成员指针还是非静态成员函数指针(非要强制转换成员函数指针也是可以的)。
4. 静态数据成员和静态成员函数不与类关联，也就不参与这个成员指针的讨论了，切记。实际上我之前打算是直接说成员指针不是指针，毕竟std::is_pointer也没把它包含在内，也不同于一般的指针的行为，但是，标准没规定它是什么，所以我也就严谨一点，只说，成员指针不是常规的指针。

# 1. 成员指针类型

1. 数据成员指针：表示类中某个数据成员的位置。
2. 成员函数指针：表示类中某个成员函数的位置。
3. 虚成员函数指针：表示类中某个虚成员函数的位置。

以下是一个示例，展示了如何使用数据成员指针和成员函数指针：

```cpp
#include <iostream>

class MyClass {
public:
    int value;
    static int staticValue;

    MyClass(int v) : value(v) {}

    void display() {
        std::cout << "Value: " << value << std::endl;
    }

    static void staticDisplay() {
        std::cout << "Static Value: " << staticValue << std::endl;
    }
};

int MyClass::staticValue = 100;

int main() {
    MyClass obj(42);

    // 数据成员指针
    int MyClass::*dataPtr = &MyClass::value;
    std::cout << "Data Member Value: " << obj.*dataPtr << std::endl;

    // 成员函数指针
    void (MyClass::*funcPtr)() = &MyClass::display;
    (obj.*funcPtr)();

    // 静态成员函数调用
    MyClass::staticDisplay();

    return 0;
}
```

解释：

1. 数据成员指针：`int MyClass::*dataPtr = &MyClass::value;` 表示 `value` 在 `MyClass` 类中的位置。使用 `obj.*dataPtr` 访问对象 `obj` 的 `value` 成员。
2. 成员函数指针：`void (MyClass::*funcPtr)() = &MyClass::display;` 表示 `display` 函数在 `MyClass` 类中的位置。使用 `(obj.*funcPtr)()` 调用对象 `obj` 的 `display` 成员函数。
3. 静态成员函数：静态成员函数不与类的实例关联，可以直接通过类名调用，如 `MyClass::staticDisplay();`。

总结：

1. 数据成员指针 和 虚成员函数指针 只是表示类中成员的位置，并不是真正的内存地址。
2. 成员函数指针 存储了一个实际的地址，可以通过对象实例调用。
3. 静态成员 不与类的实例关联，不参与成员指针的讨论。
4. 成员指针不是常规的指针，不能脱离类的实例对象单独使用。