# c++ 回调函数

回调函数是一种在 C++ 中常见的编程模式，它允许我们将一个函数作为参数传递给另一个函数，并在适当的时候调用这个函数。这种模式在处理事件、定时器、线程等异步操作时非常有用。

以下是一个简单的回调函数的例子：

```cpp
#include <iostream>
#include <functional>

// 定义一个函数，它接受一个回调函数作为参数
void process_data(std::function<void(int)> callback) {
for (int i = 0; i < 5; ++i) {
// 在适当的时候调用回调函数
callback(i);
}
}

int main() {
// 定义一个回调函数
auto callback = [](int data) {
std::cout << "Processing data: " << data << std::endl;
};

// 将回调函数作为参数传递给 process_data 函数
process_data(callback);

return 0;
}
```

---

在这个例子中，process_data 函数接受一个回调函数作为参数，并在每次处理数据时调用这个回调函数。main 函数定义了一个回调函数，并将它作为参数传递给 process_data 函数。

执行顺序如下：

1. main 函数开始执行。
2. main 函数定义了一个回调函数 callback。
3. main 函数调用 process_data 函数，并将 callback 作为参数传递给它。
4. process_data 函数开始执行。
5. process_data 函数在每次处理数据时调用 callback 函数。
6. 当 process_data 函数处理完所有数据后，它返回到 main 函数。
7. main 函数结束执行。

这就是回调函数的基本概念和执行顺序。在实际的程序中，回调函数可能会更复杂，例如，它们可能会被用于处理图形用户界面的事件、网络请求的响应等。