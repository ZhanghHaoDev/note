# 第四章 noexcept

`noexcept` 是 C++11 引入的一个关键字，用于指定函数是否会抛出异常。它可以提高代码的性能和安全性，特别是在异常处理和优化方面。以下是对 `noexcept` 关键字的详细讲解：

# 1. 基本用法

`noexcept` 可以用于函数声明和定义，表示该函数不会抛出异常。如果函数确实抛出了异常，程序会调用 `std::terminate` 终止。

```cpp
void func() noexcept {
    // 该函数不会抛出异常
}
```

# 2. 条件noexcept

`noexcept` 还可以接受一个布尔表达式，称为条件 `noexcept`。如果表达式的结果为 `true`，则函数被认为是 `noexcept` 的；否则不是。

```cpp
void func() noexcept(true) {
    // 该函数不会抛出异常
}

void func2() noexcept(false) {
    // 该函数可能会抛出异常
}
```

# 2.1. 与异常规范的关系

在c++11之前，c++使用throw() 来规范表示函数不会抛出异常，但是这种方式已经被弃用

# 3. 运算符noexcept

`noexcept` 也可以作为一个运算符，用于检查表达式是否会抛出异常。它返回一个布尔值。

```cpp
void mayThrow() {
    throw std::runtime_error("error");
}

void noThrow() noexcept {
    // 不会抛出异常
}

int main() {
    std::cout << std::boolalpha;
    std::cout << "mayThrow: " << noexcept(mayThrow()) << std::endl; // 输出 false
    std::cout << "noThrow: " << noexcept(noThrow()) << std::endl;   // 输出 true
    return 0;
}
```

# 4. 使用场景

- 提高性能：编译器可以对 `noexcept` 函数进行更好的优化，因为它们不会抛出异常。
- 增强安全性：明确函数不会抛出异常，可以减少异常处理的复杂性。
- 标准库容器：许多标准库容器在移动操作中使用 `noexcept`，以确保移动操作不会抛出异常，从而提高性能。