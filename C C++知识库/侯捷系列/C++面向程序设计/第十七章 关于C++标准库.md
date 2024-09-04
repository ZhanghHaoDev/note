# 第十七章 关于C++标准库

# 关于C++标准库

C++ 本身只提供一些基本的数据类型

而STL会提供给我们一些更高级的数据类型，比如vector、map、set、unordered_map、unordered_set等等

还有一些用到的算法，比如排序，查找等

**算法+数据结构=程序**

我们可以通过下面的代码来测试编译器和程序的兼容性

#include <iostream>

using namespace std;

int main()

{

cout << "__cplusplus"<<endl;

return 0;

}

// 程序会输出C++的版本号

---