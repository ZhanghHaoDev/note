# c++并发与多线程

# 基本概念

线程：线程是操作系统能够进行运算调度的最小单位，他被包含在进程中，进程包含一个或多个线程。

进程可以理解为完成一件

多线程与仿函数

多线程与Lambdas表达式

在使用c++多线程的时候，需要注意对数据的保护，比如出现了每次执行结果都不一致的情况下，我们可以对数据进行加锁，互斥锁，对数据进行包含，意思的在同一时间节点内，只允许一个线程对数据进行访问

# c++ 多线程

# 第一章 你好，c++的并发世界

在c++11版本当中新增加了对多线程的支持，需要的头文件是\<thread>

#include <iostream>

#include <thread>

using namespace std;

//// 最简单的输出Hello word程序

//int main()

//{

//        cout << "Hello Word" << endl;

//

//        return 0;

//}

void hello()

{

cout << "Hello Threads" << endl;

}

int main()

{

// 调用多线程函数

thread t1(hello);

// 阻塞线程

t1.join();

return 0;

}

---

# 第二章 线程管理

# 线程管理的基础

每个程序都至少会有一个线程：执行main函数的线程，其余的线程有各自的入口函数。

使用c++线程库启动线程，可以归纳为构造std::thread对象

void func();

std::thread my_thread(func);

---

等待线程完成：我们可以使用join()函数来确保子线程执行完成

void func();

std::thread my_thread(func);

my_thread.join();

---

执行join()函数是简单粗暴的讲子线程销毁，但如果想要分离一个线程，我们可以使用detach()函数，

detach()函数可以使得子线程在后台运行，而主线程并不用等待子线程的结束

# 向线程传递参数

之前的例子中，我们都是简单的调用子线程来输出字符，但函数也可以传递参数。

// 多线程传递参数，输出name and age

#include <iostream>

#include <thread>

#include <string>

using namespace std;

void f(string name,int age)

{

cout << name << " is " << age << endl;

}

int main()

{

thread t1(f, "zhangsan", 12);

t1.join();

return 0;

}

---

# 运行的时候确定线程数量

我们可以使用函数thread::hardware_concurrency()，来确定当前系统的cpu核心数量

cout << "CPU 核心数量是：" << thread::hardware_concurrency() << endl;

---

# 标识线程

我们可以通过输出线程的ID来区分不同的线程，使用thread类中的id函数，就可以输出当前线程的ID

cout << "当前线程的ID is " << thread::id() << endl;

---

# 第三章线程间共享数据

# 条件竞争

并发中竞争条件的形成，取决于一个以上的相对执行顺序，每个线程都抢着完成的自己的任务，

大多数的情况下，即使改变执行顺序，也是良性竞争，其结果可以接受。

当结果变量不遭到破坏的时候，我们称之为良性竞争，当结果变量遭到破坏的时候，我们称之为恶行条件竞争

c++标准中也定义了数据竞争这个术语，一种特殊的条件竞争：并发的修改一个独立对象，数据竞争的未定义行为的起因

简单来讲：我们使用多线程去访问同一块内存的时候，线程的执行顺序并不一定，这个时候会造成结果每次执行都不一样

# 使用互斥量保护共享数据

当访问共享数据前，经数据锁住，在访问结束后，再将数据解锁。

任何一个线程在执行时，其他线程试图访问共享数据的时候，就必须等待。除非该线程就在修改共享数据，否则任何线程都不可能会看到被破坏的不变量

【注意】：互斥量自身也有问题，会造成死锁，或对数据保护太多

c++通过实例化std::mutex创建互斥量实例，使用成员函数lock()对互斥量上锁，unlock()函数进行解锁

使用头文件\<mutex>

不过并不推荐直接调用lock()和unlock()函数，因为调用该函数，就意味着必须要在函数的出口调用unlock()函数。

这里推荐使用c++的std::lock_guard()，该成员函数在构造函数中调用lock()上锁，在析构函数中调用unlock()解锁函数

std::list<int> some_list;                // 1

std::mutex some_mutex;                        // 2

void add_to_list(int new_value)

{

std::lock_guard<std::mutex> guard(some_mutex);        // 3

some_list.push_back(new_value);

}

bool list_contains(int valu_to_find)        // 4

{

std::lock_guard<std::mutex> guard(some_mutex);

return std::find(some_list.begin(), some_list.end(), valu_to_find) != some_list.end();

}

---

# 死锁的问题

死锁：线程中有对锁的竞争：一对线程需要对甜蜜所有的互斥量做一些操作，其中每个线程都有一个互斥量，且等待另一个解锁。

这样的话就没有线程工作，因为都在等待对方释放互斥量。这种情况就是死锁，最大的问题就是由两个或两个以上的互斥量来锁定一个操作

如何避免死锁：

让两个互斥量总以相同的顺序上锁：总在互斥量B之前锁住互斥量A，就不会死锁

unique_lock() 灵活的锁

std::unqiue_lock()使用更为自由的不变量，这样std::unqiue_lock实例不会纵欲互斥量的数据类型相关，使用起来要比std::lock_gunard更加灵活

std::unqiue_lock比较std::lock_guard会占用更多的空间，速度上较慢一些

class some_big_object;

void swap(some_big_object& lhs, some_big_object& rhs);

class X

{

private:

some_big_object some_detaill;

std::mutex m;

public:

X(some_big_object const& sd) :som_detaill(sd) {};

friend void swap(X& lhs, X& rhs)

{

if (&lhs == &rhs)

{

return;

}

std::unique_lock<std::mutex> lock_a(lhs.m, std::defer_lock);        // 1

std::unique_lock<std::mutex> lock_b(lhs.m, std::defer_lock);        // 1 留下未上锁的互斥量

std::lock(lock_a, lock_b);

swap(lhs.some_dataill, rhs.some_detaill);

}

};

---

# 第四章 总结

1. 在c++中使用多线程的库是\<thread>

2. 多线程主要的使用方法是通过调用函数来使用，有两种函数

1. 普通的函数

2. lambda函数

这两个的区别：我觉得主要看实际使用，在参数较多的情况下，推荐使用lambda表达式，避免了参数的多次传递

3. 与c语言函数的不同是对函数的返回值没有限制，对函数的参数没有限制

1. c语言的多线程函数的返回值必须是void*，而c++没有限制

2. c语言的多线程函数的参数类型必须是void*，并且只能有一个参数，同样c++没有限制

4. 可以使用指针来创建多个线程

// 指针创建

thread* threads = new thread[10];

for(int i = 0; i < 10; i++>)

{

threads[i](func,age);

}

for(int i = 0; i < 10; i++>)

{

threads[i].join();

}

delete[] threads;

// vector创建，不用释放内存

vector<thread> temp_threas(10);

for(int i = 0; i < temp_threas.size(); i++>)

{

temp_threas[i](func,age);

}

for(int i = 0; i < temp_threas.size(); i++>)

{

temp_threas[i].join();

}

---

5. 线程在使用的时候注意阻塞，在创建线程的时候，就把阻塞线程的语句写好

// 创建线程

thread t1(func,age);

// 阻塞线程

t1.join();

---

6. 锁的问题

如果出现在使用多线程的时候，结果与之前的结果不一致，或者出现每次执行后的结果都不一致，这个时候就需要添加锁

std::metux met;

void func(int age)

{

lock_gunard(met);

....

}

int main()

{

thread threads(func,age);

threads.join();

return 0;

}

---

最好使用```lock_gunard()```

1. c++标准库在11后添加了线程库

头文件

#include <thread>

---

1. 使用多线程计算乘法

在计算数量少的情况下，并不推荐多线程，从结果来看单线程计算比多线程要快，因为线程的创建和销毁都需要时间，这个时间也是计算在程序运行时间内的。

但是在需要计算数量较多的情况下，多线程是可以起到作用的