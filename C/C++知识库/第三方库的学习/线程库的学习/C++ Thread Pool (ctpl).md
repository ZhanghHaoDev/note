# C++ Thread Pool (ctpl)

1. 如何安装

这个线程池库只有一个头文件，在GitHub页面下载下来，项目包含进去就可以

GitHub：https://github.com/vit-vit/CTPL

1. ctpl可以创建固定数量的线程使用，也可以创建不固定数量的线程

这里使用cpu的核心数来确定线程的数量，如果有空闲的线程，线程池会自动进行调度，将任务分配给空闲的线程，如果所有的线程都在忙，那就等待

1. 例子：

**代码**

---

#include "ctpl_stl.h"

#include <iostream>

void foo(int id) {

std::cout << "Task " << id << " is running on thread " << std::this_thread::get_id() << std::endl;

}

// 固定数量的线程

int main() {

ctpl::thread_pool pool(4); // 创建一个有4个线程的线程池

for (int i = 0; i < 10; ++i) {

pool.push(foo, i); // 提交任务

}

pool.stop(true); // 等待所有任务完成

return 0;

}

// cpu核心数量的线程

int main() {

int num_threads = std::thread::hardware_concurrency();

ctpl::thread_pool pool(num_threads); // 创建一个线程池，线程数量等于CPU的核心数

for (int i = 0; i < 10; ++i) {

pool.push(foo, i); // 提交任务

}

pool.stop(true); // 等待所有任务完成

return 0;

}

---