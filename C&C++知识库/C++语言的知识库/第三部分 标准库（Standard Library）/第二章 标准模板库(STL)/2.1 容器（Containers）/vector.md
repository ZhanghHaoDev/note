# vector

## 1. vector note

1. vector是一个封装了动态大小数组的顺序容器（Sequence Container），是STL中的一个重要组件，也是C++中的一个重要特性。
2. vector是一个类模板，它的成员函数和操作符的功能和用法与数组类似，但是vector的容量能够动态增长或减少，能够根据需要自动分配或释放内存。
3. 使用的时候需要包含头文件`#include <vector>`
4. vector：可变大小数组，支持快速随机访问，在尾部之外的位置插入或删除元素可能很慢 
5. vector 的内存增长是指数增长的，当vector的容量不足的时候，会分配当前容量大两倍的内存
6. vector是一个类模版，使用了模版参数来实现泛型编程，使得vector可以存储任意类型的元素

## 2. vector 成员类型

## 3. vector 成员函数

### 构造函数

1. 构造函数，默认构造函数
```cpp
#include <vector>

vector<int>();
```

2. 构造函数，指定大小，括号里面指定vector的大小
```cpp
#include <vector>

std::vector<int> v(10);
```

3. 构造函数，指定大小和初始值，括号里面第一个元素为大小，第二个元素为初始值
```cpp
#include <vector>

std::vector<int> v(10, 5);
```

= 操作
== 操作
assign 函数
assign_range 函数
get_allocator 函数


### 元素访问

### 迭代器

### 容量

### 修改器
插入，删除 等操作