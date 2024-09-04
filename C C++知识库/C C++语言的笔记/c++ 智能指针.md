# c++ 智能指针

# new和delete

这里我们创建的指针也可以叫做：裸指针

我们在c++中可以使用new来申请动态的内存

int num= 10;

int *num_ptr = new int[num]

释放内存使用delete，delete使用的时候，不需要传递数量

delete[] num_ptr;

# shared_ptr 共享指针

使用共享指针的时候，需要包含头文件

#include <memory>

shared_ptr 共享指针语法

shared_ptr<类型> p;

p = make_sharead<类型>(数量)；

我们这里使用make_shared来给指针分配内存，当然也可以使用new来分配内存

shared_ptr<int> p { new int(100)};

这两种方法都可以给共享指针分配内存，但更推荐使用make_shared，因为效率更高和安全。

shared_ptr是使用到了引用，不可避免的会产生性能

【共享指针不需要释放内存，使用智能指针的时候不需要使用delete】

# unique_ptr 独享指针

unique_ptr是独享指针，没有额外的性能开销

头文件：#include <memory>

语法：

unique_ptr<类型> p {new <类型>(数量)}

unique_ptr<类型> p {make_unique <类型>(数量)}

# c++当中的智能指针

c++当中的智能指针分别有三种：

unique_ptr，shared_ptr，wed_ptr

需要的头文件 <memory>

1. unique_ptr：是一种独占所有权的指针，他确保在拥有的对象超出范围时自动删除他
2. shared_Ptr：是一种多个指针可以同时参与所有权管理的指针。当没有指针指向对象时，他会被自动删除
3. weak_ptr是用于避免shared_ptr循环引用问题的一种指针。他可以访问shared_ptr所管理的对象，但包含影响所有权

# 基础使用方法

1. unique_ptr是一种独占所有权的指针，它确保在拥有的对象超出范围时自动删除它。这种指针是C++11标准引入的，并且只有一个指针可以拥有对象所有权，不能转移所有权，因此是类型安全和高效的。

可以使用make_unique来实例化一个unique_ptr对象，例如：

std::unique_ptr<int> p = std::make_unique<int>(100);

1. shared_ptr是一种多个指针可以同时参与所有权管理的指针。当没有指针指向对象时，它会被自动删除。与unique_ptr不同，shared_ptr可以拥有多个指针，它们都可以使用同一个资源。每个shared_ptr附带一个计数器，当计数器为零时，资源被释放。

可以使用make_shared来实例化一个shared_ptr对象，例如：

std::shared_ptr<int> p = std::make_shared<int>(100);

1. weak_ptr是用于避免shared_ptr循环引用问题的一种指针。它可以访问由shared_ptr所管理的对象，但不会影响所有权。

可以使用weak_ptr与shared_ptr结合使用，例如：

std::weak_ptr<int> wp;

{

std::shared_ptr<int> sp = std::make_shared<int>(100);

wp = sp;

// 此时sp与wp共享指向100的对象

}

// sp已经超出范围，但是由于wp存在，资源仍然处于有效状态

# 智能指针常用函数

1. get()：返回指向对象的指针。
2. reset()：释放共享对象的所有权并将指针重置为null。
3. use_count()：返回与共享指针相关联的指针数，不包括弱引用计数。
4. unique()：返回true如果unique_ptr对象是唯一的所有者，否则返回false。
5. operator bool()：如果指针非零，则返回true，否则返回false。
6. operator*()和operator->()：用于前提条件检查的=default或=delete或标准实现的smart pointer类自定义操作符。
7. swap()：交换两个智能指针的内容。

# 使用智能指针需要注意的地方

1. 传递到函数的智能指针可能会被函数修改（包括重置、增加、减少共享引用计数等）导致它的值在函数返回后已经失效。为了防止这种情况发生，建议使用const智能指针、传入指针或者引用智能指针。
2. 在使用shared_ptr时，避免形成循环引用会导致内存泄漏。一旦出现循环引用就需要使用weak_ptr来打破循环引用。
3. 对于已经使用shared_ptr管理的动态分配的对象，避免使用常规指针来操作它。如果使用常规指针可能会导致所有权问题以及悬空指针。
4. 当使用智能指针时，需要注意内存使用以避免大量内存开销。
5. 当使用unique_ptr时，需要注意不能拷贝unique_ptr对象。如果需要多个所有权，应使用shared_ptr。

# 智能指针的不同点

在C++中常用的智能指针有三种：unique_ptr、shared_ptr和weak_ptr。

unique_ptr是一种独占所有权的指针，shared_ptr是一种多个指针可以同时参与所有权管理的指针，而weak_ptr是用于避免shared_ptr循环引用问题的一种指针。

性能开销方面，unique_ptr通常是最快的，因为它只有一个指针可以拥有对象所有权，这使得它非常轻量级和高效。shared_ptr通常比unique_ptr慢一些，因为它需要一个计数器来管理所有权。而weak_ptr通常是最慢的，因为它需要一个额外的计数器来管理弱引用计数。

总体而言，unique_ptr在性能和内存使用方面都是最优的选择，但是在多个所有权的情况下，shared_ptr是必需的。weak_ptr则是用于解决shared_ptr循环引用问题。