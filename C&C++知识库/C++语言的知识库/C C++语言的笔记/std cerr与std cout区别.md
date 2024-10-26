# std::cerr与std::cout区别

cerr是一个ostream对象，关联到标准错误，通常写入到与标准输出相同的设备。默认情况下，写道cerr的数据是不缓冲的，cerr通常用于错误信息与其他不属于正常逻辑的输出内容

简单来讲：cerr用于输出错误提示信息，输出的内容不缓冲

# 为什么要使用cerr

用于输出错误信息

有了cerr，在最紧急的情况下，也可以输出信息

实例

#include <iostream>

int main()

{

std::cout << "Hello World!\n";

std::cerr << "错误" << std::endl;

return 0;

}

---