# vector的笔记

## 1. vector的简介

vector是一个封装了动态大小数组的顺序容器（Sequence Container），是STL中的一个重要组件，也是C++中的一个重要特性。vector是一个类模板，它的成员函数和操作符的功能和用法与数组类似，但是vector的容量能够动态增长或减少，能够根据需要自动分配或释放内存。

使用的时候需要包含头文件`#include <vector>`

## 2. vector包括的函数

### 构造函数和析构函数
vector()：默认构造函数。
vector(size_type count, const T& value = T())：构造一个包含 count 个元素的 vector，每个元素的值为 value。
vector(const vector& other)：拷贝构造函数。
vector(vector&& other) noexcept：移动构造函数。
~vector()：析构函数。

### 迭代器
begin()：返回指向第一个元素的迭代器。
end()：返回指向最后一个元素之后的迭代器。
rbegin()：返回指向最后一个元素的逆向迭代器。
rend()：返回指向第一个元素之前的逆向迭代器。

### 容量
size()：返回当前元素数量。
max_size()：返回 vector 能容纳的最大元素数量。
resize(size_type count)：调整 vector 的大小。
capacity()：返回当前分配的存储容量。
empty()：检查 vector 是否为空。
reserve(size_type new_cap)：请求分配至少能容纳 new_cap 个元素的存储空间。
shrink_to_fit()：减少 vector 的容量以适应其大小。

### 元素访问
operator[]：访问指定位置的元素。
at(size_type pos)：访问指定位置的元素并进行边界检查。
front()：访问第一个元素。
back()：访问最后一个元素。
data()：返回指向数据数组的指针。

### 修改器
assign(size_type count, const T& value)：用新值替换内容。

**参数详解**
- count：新元素的数量。 
- value：新元素的值。


push_back(const T& value)：在末尾添加元素。
pop_back()：移除末尾的元素。
insert(const_iterator pos, const T& value)：在指定位置插入元素。
erase(const_iterator pos)：移除指定位置的元素。
clear()：清除所有元素。
swap(vector& other)：交换内容。

### 比较操作符
operator==：比较两个 vector 是否相等。
operator!=：比较两个 vector 是否不相等。
operator<：比较两个 vector 的大小。
operator<=：比较两个 vector 的大小。
operator>：比较两个 vector 的大小。
operator>=：比较两个 vector 的大小。