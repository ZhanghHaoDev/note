# c++标准库线程-std::thread

std::thread是C++11标准库中的一个类，它用于表示一个可以并行执行的线程。std::thread提供了创建和管理线程的基本功能。

以下是std::thread的一些主要方法：

1. 构造函数：std::thread的构造函数接受一个函数和一些参数，它会创建一个新的线程并开始执行该函数。例如，std::thread t(func, arg1, arg2);会创建一个新的线程并开始执行函数func(arg1, arg2)。
2. join：join()方法会阻塞当前线程，直到std::thread对象表示的线程执行完毕。如果不调用join()，并且std::thread对象被销毁，程序会终止。
3. detach：detach()方法会将std::thread对象表示的线程变为后台线程。这意味着，当std::thread对象被销毁时，线程会继续执行，程序不会终止。
4. joinable：joinable()方法返回一个布尔值，表示是否可以对std::thread对象调用join()或detach()。
5. get_id：get_id()方法返回一个std::thread::id对象，表示std::thread对象的线程ID。
6. hardware_concurrency：hardware_concurrency()是一个静态方法，它返回一个表示系统中可并发执行的线程数量的值。

以下是一个std::thread的简单示例：

**代码**

---

#include <iostream>

#include <thread>

void hello() {

std::cout << "Hello, World!" << std::endl;

}

int main() {

std::thread t(hello);

t.join();

return 0;

}

---

这个程序创建了一个新的线程，并在该线程上执行hello函数。然后，主线程等待新线程执行完毕。