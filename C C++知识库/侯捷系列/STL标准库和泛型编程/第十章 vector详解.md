# 第十章 vector详解

# 1. vector的定义

向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）。跟任意其它类型容器一样，它能够存放各种类型的对象。可以简单的认为，向量是一个能够存放任意类型的动态数组。

1. vector赋初值：vector ite{1,2,3,};

# 2. vector的特性

1. 在固定位置插入

// 1. 可以先申请容量

vector<float> temp(ns*2);

for (auto ite : data)

{

// size会增长，但是位置不变

temp.insert(temp.begin() + ns, ite);

}

---

# vector模板

# 多维vector探讨

**定义**：

两个或者两个以上的vector嵌套就是多维vector

**优点**:

多维vector可以看作是多维数组，但是比上多维数组好处在于不需要使用常量提前定义长度

**缺点**:

1. 占用空间较大：vector的空间增长机制是两倍的扩容
2. 运行较慢：数组的内存是连续存放的，vector的数据是连续存放的，

指向行的所有指针是连续存放的。每一行的数据是连续存放的，但是行与行之间是不连续存放的。

# 多维vector（以二维为例子）

1. 初始化

// 声明

vector<vector<int>> num1;

// 初始化

vector<vector<int>> num2

{

vector<int>{1,2,3},

vector<int>{1,2,3}

}

// 固定大小 这里定义了5*5大小的二维数组

vector<vector<int>> num3(5)

---

1. 赋值

vector<vector<float>> temp;

vector<float> tt;// 临时变量

for (int i = 0; i < 25; i++)

{

for (int j = 0; j < 22; j++)

{

tt.push_back(22);

}

// 这里注意push_bakc()是后插入，如果想使用从0开始，可以使用inster

temp.push_back(tt);

}

---

1. 取值

vector<vector<float>> temp;

for (int i = 0; i < temp.size(); i++)

{

for (int j = 0; j < temp[i].size(); j++)

{

cout << "vector的值是" << temp[i][j]<<endl;

}

}

---

# 如何求第一维度的size

vector<vector<float>> temp;

// 求第一维度的size

size_t size = temp.size();

cout << "二维vector的第一维度的size是：" << size << endl;

// 求第二维度的size

size_t size2 = temp[0].size();

cout << "二维vector的第二维度的size是：" << size2 << endl;

---

# vector和vector<pair<double,double>>的区别

1. vector是二维数组，vector<pair<double,double>>是一维数组
2. vector是连续存储的，vector<pair<double,double>>是不连续存储的
3. vector的空间是两倍的扩容，vector<pair<double,double>>的空间是1.5倍的扩容
4. vector的访问速度快，vector<pair<double,double>>的访问速度慢

# vector<pair<double,double>>的使用

1. 初始化

// 初始化

vector<pair<double,double>> temp

{

pair<double,double>(1,2),

pair<double,double>(1,2)

}

// 声明

vector<pair<double,double>> temp;

---

1. 赋值

// 赋值

vector<pair<double,double>> temp;

for (int i = 0; i < 25; i++)

{

temp.push_back(pair<double,double>(1,2));

}

---

1. 取值

vector<pair<double,double>> temp;

for (int i = 0; i < temp.size(); i++)

{

cout << "vector的值是" << temp[i].first << " " << temp[i].second << endl;

}

---

# vector<pair<double,double>>和vector的转换

1. vector<pair<double,double>>转换为vector

vector<pair<double,double>> temp;

vector<vector<double>> temp2;

for (int i = 0; i < temp.size(); i++)

{

vector<double> temp3;

temp3.push_back(temp[i].first);

temp3.push_back(temp[i].second);

temp2.push_back(temp3);

}

---

1. vector转换为vector<pair<double,double>>

vector<vector<double>> temp;

vector<pair<double,double>> temp2;

for (int i = 0; i < temp.size(); i++)

{

temp2.push_back(pair<double,double>(temp[i][0],temp[i][1]));

}

---

# 二维vector的begin()函数

vector<vector<float>> towv;

// 在二维vector中调用begin函数

vector<vector<float>>::iterator ite = towv.begin();

// 在这里的begin函数指向的是里面嵌套的vector<float> 的元素

// 如何确定里面嵌套的vector的begin函数，这个begin指向的是元素本身

vector<vector<float>>::iterator ite = towv[0].begin();

---

# 二维vector的容量提前申请

在一维的vector中我们可以通过传入构造函数常量或者变量来提起申请空间

// 常量

vector one(20);

// 变量

int num = 200;

vector one2(num);

---

在二维vector中也同样可以通过构造函数来申请空间

vector<vector<float>> tow(20,vector<float>(20));

---

### 插入元素

如果提起申请了空间我们可以通过inster来插入元素

同样也可以通过下标来访问位置，插入元素[]

不要在循环中使用resize，除非有特殊需求

### 查找元素的位置，第几个

int findElement2(vector<char> v, char key){

vector<char>::iterator it;    //此迭代器用来判断查找元素在不在容器内

it = find(v.begin(), v.end(), key);

if(it != v.end()){

//distance计算第一个参数到第二个参数之间的距离。

// 如果第二个参数的顺序在第一个参数前面的话,函数是会返回负值的；

// 如果迭代器不在一个容器内,程序会抛出异常。

return distance(v.begin(),it);

}

return -1;

}

---

lower_bound() 函数用于在指定区域内查找不小于目标值的第一个元素。也就是说，使用该函数在指定范围内查找某个目标值时，最终查找到的不一定是和目标值相等的元素，还可能是比目标值大的元素。

# auto关键字

1. for(auto ite : vector)

auto会拷贝一份容器内的vector，在修改ite时不会改变原容器当中的vector值，只会改变拷贝的vector，因为拷贝发生在编译期间，所以并不会对运行速率造成很大影响

#include <iostream>

#include <vector>

using namespace std;

void printVec(vector<int>& vec) {

for (int i = 0; i < vec.size(); i++)

cout << vec[i] << endl;

}

int main() {

vector<int> vec = {4,3,2,1,0 };

cout<<"** for(auto x : vector)**"<<endl;

//这个时候每个取出来的iter只是原来vec元素的副本，不会改变vec中任何元素

//iter可以作为左值进行赋值，但只是在副本范围

for (auto iter : vec) {

iter = iter + 100;

}

printVec(vec);

cout<<"**for(auto& x : vector)**"<<endl;

//这个时候取出来的是 &iter，代表原来vec中元素的引用

//如果对iter进行任何改变都会作用在vec上

for (auto& iter : vec) {    //如果vec返回临时对象，用auto&&

iter = iter + 100;

}

printVec(vec);

}

---

1. for(auto & x : vector)，非常量左值引用

当需要对原数据进行同步修改时，就需要添加&，即vector的引用。会改变x的同时修改vector。

1. for(auto && x : vector )，非常量右值引用

当vector返回临时对象，使用auto&会编译错误，临时对象不能绑定在non-consta-value reference（非常量左值引用），需使用auto&&（非常量右值引用）初始化右值时也可以捕获

1. for(const suto & x : vector)，常量左值引用

使用 const 可以避免无意中修改数据的编程错误；

使用 const 能让函数接收 const 和非 const 类型的实参，否则将只能接收非 const 类型的实参；

使用 const 引用能够让函数正确生成并使用临时变量（当传入实参与形参符合自动转换要求时可以通过临时变量进行自动类型转换）。

const （常类型），不能作为左值

& （引用），不拷贝，不申请新空间，会对原vector修改

当我们不希望拷贝原vector（拷贝需要申请新的空间），同时不愿意随意改变原vector，那么我们可以使用for(const auto& x : vector)，这样我们可以很方便的在不拷贝的情况下读取vector，同时不会修改vector。一般用在只读操作。

1. const auto x : vector，常量左值引用

该操作相对于const auto& x : vector只是少了引用（&），即会申请新的空间（拷贝），不经常使用。

1. 总结一下

想要拷贝元素： for(auto ite : vector)

想要修改元素： for(auto &&x : vector)

想要只读元素： for(const auto &x ：vector)

# push_back和emplace_back