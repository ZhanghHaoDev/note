# vector

## 1. vector note

1. vector是一个类模板，它的成员函数和操作符的功能和用法与数组类似，但是vector的容量能够动态增长或减少，能够根据需要自动分配或释放内存。
2. vector：可变大小数组，支持快速随机访问，在尾部之外的位置插入或删除元素可能很慢 
3. vector 的内存增长是指数增长的，当vector的容量不足的时候，会分配当前容量大两倍的内存
4. vector是一个类模版，使用了模版参数来实现泛型编程，使得vector可以存储任意类型的元素
5. vector 维护的是一个连续线性空间，所以对于vector来说，访问任何位置的元素都很方便
6. vector的数据结构

## 2. vector 成员函数

### 构造函数

1. 默认构造函数，创建一个空的 vector，但是没有初始化这个容器
```cpp
#include <vector>

std::vector<int> v;
```

2. 指定大小的构造函数，创建一个指定大小的 vector，元素值为默认值
```cpp
#include <vector>

std::vector<int> v(10); // 创建一个包含10个元素的 vector，元素值为默认值
```

3. 指定大小和初始值的构造函数，创建一个指定大小的 vector，所有元素初始化为指定值
```cpp
#include <vector>

std::vector<int> v(10, 5); // 创建一个包含10个元素的 vector，所有元素值为5
```

4. 通过迭代器范围构造函数，创建一个包含指定范围内元素的 vector，这个也可以用于初始化元素而不指定大小
```cpp
#include <vector>

std::vector<int> source = {1, 2, 3, 4, 5};
std::vector<int> v(source.begin(), source.end()); // 创建一个包含 source 所有元素的 vector
```

5. 拷贝构造函数，创建一个包含另一个 vector 所有元素的 vector
```cpp
#include <vector>

std::vector<int> source = {1, 2, 3, 4, 5};
std::vector<int> v(source); // 创建一个包含 source 所有元素的 vector
```

6. 移动构造函数，创建一个通过移动另一个 vector 的所有元素的 vector
```cpp
#include <vector>

std::vector<int> source = {1, 2, 3, 4, 5};
std::vector<int> v(std::move(source)); // 创建一个包含 source 所有元素的 vector，source 变为空
```

### 赋值操作

1. 拷贝赋值操作符
```cpp
#include <vector>

std::vector<int> source = {1, 2, 3, 4, 5};
std::vector<int> v;
v = source; // v 变为 {1, 2, 3, 4, 5}
```

2. 移动赋值操作符
```cpp
#include <vector>

std::vector<int> source = {1, 2, 3, 4, 5};
std::vector<int> v;
v = std::move(source); // v 变为 {1, 2, 3, 4, 5}，source 变为空
```

3. `assign` 函数，赋值指定大小和初始值
```cpp
#include <vector>

std::vector<int> v;
v.assign(10, 5); // v 变为包含10个元素，所有元素值为5
```

4. `assign` 函数，赋值迭代器范围内的元素
```cpp
#include <vector>

std::vector<int> source = {1, 2, 3, 4, 5};
std::vector<int> v;
v.assign(source.begin(), source.end()); // v 变为 {1, 2, 3, 4, 5}
```

### 其他成员函数

1. `get_allocator` 函数，返回用于分配内存的 allocator 对象
```cpp
#include <vector>

std::vector<int> v;
auto allocator = v.get_allocator();
```

### 元素访问

1. `at` 函数，返回指定位置的元素，并进行边界检查
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
int value = v.at(2); // value = 3
```

2. `operator[]`，返回指定位置的元素，不进行边界检查
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
int value = v[2]; // value = 3
```

3. `front` 函数，返回第一个元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
int value = v.front(); // value = 1
```

4. `back` 函数，返回最后一个元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
int value = v.back(); // value = 5
```

5. `data` 函数，返回指向底层数组的指针
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
int* ptr = v.data(); // ptr 指向数组的第一个元素
vector<int> b = v.date(); // 这个操作是错误的
```

### 迭代器

意思是如果调用迭代器，返回的返回值也一定是迭代器类型

1. `begin` 函数，返回指向第一个元素的迭代器
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
auto it = v.begin(); // it 指向第一个元素
```

2. `end` 函数，返回指向最后一个元素之后的迭代器
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
auto it = v.end(); // it 指向最后一个元素之后的位置
```

3. `rbegin` 函数，返回指向最后一个元素的逆向迭代器
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
auto it = v.rbegin(); // it 指向最后一个元素
```

4. `rend` 函数，返回指向第一个元素之前的逆向迭代器
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
auto it = v.rend(); // it 指向第一个元素之前的位置
```

### 容量

1. `size` 函数，返回元素的个数
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
size_t size = v.size(); // size = 5
```
+ 需要注意的是：vector的容量的类型是size，而不是int，所以我们在循环访问容器当中的元素的时候，不能使用int类型

2. `max_size` 函数，返回可以容纳的最大元素个数
```cpp
#include <vector>

std::vector<int> v;
size_t max_size = v.max_size();
```

3. `resize` 函数，改变容器的大小
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.resize(3); // v 变为 {1, 2, 3}
```

4. `capacity` 函数，返回当前分配的存储空间能够容纳的元素个数
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
size_t capacity = v.capacity();
```

5. `empty` 函数，检查容器是否为空
```cpp
#include <vector>

std::vector<int> v;
bool isEmpty = v.empty(); // isEmpty = true
```
+ 检查容器是否为空最好使用这个函数

6. `reserve` 函数，预留存储空间
```cpp
#include <vector>

std::vector<int> v;
v.reserve(10); // 预留存储空间，可以容纳至少10个元素
```

7. `shrink_to_fit` 函数，减少内存使用
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.shrink_to_fit();
```

### 修改器

1. `clear` 函数，清空所有元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.clear(); // v 变为空
```

2. `insert` 函数，在指定位置插入元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.insert(v.begin() + 2, 10); // v 变为 {1, 2, 10, 3, 4, 5}
```

3. `erase` 函数，删除指定位置的元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.erase(v.begin() + 2); // v 变为 {1, 2, 4, 5}
```

4. `push_back` 函数，在尾部添加元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.push_back(6); // v 变为 {1, 2, 3, 4, 5, 6}
```
+ push_back 函数会在 vector 的尾部插入一个元素。它需要一个已经构造好的对象作为参数，然后将该对象复制或移动到 vector 中。

5. `pop_back` 函数，删除尾部元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.pop_back(); // v 变为 {1, 2, 3, 4}
```

6. `swap` 函数，交换两个 vector 的内容
```cpp
#include <vector>

std::vector<int> v1 = {1, 2, 3};
std::vector<int> v2 = {4, 5, 6};
v1.swap(v2); // v1 变为 {4, 5, 6}, v2 变为 {1, 2, 3}
```

7. `emplace` 函数，在指定位置构造元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.emplace(v.begin() + 2, 10); // v 变为 {1, 2, 10, 3, 4, 5}
```

8. `emplace_back` 函数，在尾部构造元素
```cpp
#include <vector>

std::vector<int> v = {1, 2, 3, 4, 5};
v.emplace_back(6); // v 变为 {1, 2, 3, 4, 5, 6}
```
+ 我们在使用vector这个容器的时候，如果是往容器的尾部插入元素，最好使用emplace_back这个成员函数
  + 因为emplace_back 的效率比 push_back 高，由于 emplace_back 直接在 vector 的内存空间中构造对象，因此它的效率通常比 push_back 高。
  + 使用 emplace_back 可以避免不必要的复制或移动操作，因为对象是直接在 vector 的内存空间中构造的。
  + emplace_back 函数会在 vector 的尾部直接构造一个元素。它接受构造函数的参数，并在 vector 的内存空间中直接构造对象。



## 3. 其他操作

1. 遍历元素
在c++98的版本当中，我们需要使用迭代器来访问容器当中的元素，但是c++11后更新了auto这个关键字，所以如果使用c++11后的版本我们直接使用范围for来遍历是最合适的方法
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    // 使用显式迭代器类型进行遍历 c++ 98
    for (std::vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用范围 for 循环进行遍历 c++ 11
    for (auto& elem : v) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

2. 拷贝容器
+ 涉及到拷贝到问题，要注意深拷贝和浅拷贝，但是vector本身并不支持浅拷贝，因为它总是进行深拷贝
+ 如果仅仅只是拷贝元素的话，可以直接使用=，使用for循环一个一个赋值是多余的操作，因为vector的深拷贝更加的搞笑
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> a(2, 1); // a = {1, 1}
    std::vector<int> b = a; // 深拷贝，b = {1, 1}
    auto c = a; // 也可以使用auto关键字

    // 修改 b 的元素，不影响 a
    b[0] = 2;

    std::cout << "a: ";
    for (int i : a) std::cout << i << " "; // 输出 a: 1 1
    std::cout << "\nb: ";
    for (int i : b) std::cout << i << " "; // 输出 b: 2 1

    return 0;
}
```