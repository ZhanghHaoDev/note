# 第二章 STL体系结构基础介绍

# 第二章 STL体系结构基础介绍

# 1. STL六大部件

1. 容器
2. 分配器
3. 算法
4. 迭代器
5. 适配器
6. 仿函数

容器可以看作是一块内存，迭代器可以看作是一个泛化的指针，适配器可以看作是一个类型转换器。

#include <iostream>

#include <vector>

#include <algorithm>

#include <functional>

using namespace std;

int main()

{

int ia[6]={12,45,67,102,34,2};

vector<int,allocator<int>> iv(ia,ia+6);

cout << count_if(iv.begin(),iv.end(),bind2nd(less<int>(),100)) << endl;

}

---

# 2. 复杂度

目前常用的是大On复杂度：

1. 时间复杂度：O(n)，称为常数复杂度
2. O(n)的时间复杂度，称为线性复杂度
3. O(log2n): 称为次线性复杂度的平方
4. O(n^):称为平方复杂度
5. O(n3):称为立方复杂度
6. O(2n):称为指数复杂度
7. O(nlog2n):介于线性及次线性之间的复杂度

# 3. 前闭后开区间

**在STL中:c.begin()一定指向的是第一个元素，但是c.end()指的是最后一个元素的下一个元素**

所有的容器都遵循这个规则

容器不一定是连续的空间

vector<int> iv;

// 旧版的写法

vector<int>::iterator iv=v.begin();

for(;it!=v.end();++it)

{

cout << *ite<<endl;

}

// C++11的新语法

for(auto ite : iv)

{

cout << *ite << endl;

}

---

# 4. 结构

高级编程语言的结构分为三种：

1. 选择结构
2. 循环结构
3. 迭代结构

选择结构：

if(条件)

代码

else

代码

---

循环结构：

while(条件)

代码

---

迭代结构

for(初始化;条件;渐进)

代码

---