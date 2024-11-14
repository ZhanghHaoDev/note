# c++中的debug和release

在c++中，代码在debug和release，不同的模式运行不同的代码

适用于Windows上的vs

1. 首先在项目属性中release，c/c++预处理器中定义一个NDEBUG
2. 但是在debug中去掉NDEBUG 的定义
3. 在代码中输入下面的代码就可以

#ifndef NDEBUGstd::cout << "Hello, World! Debug Mode" << std::endl;#elsestd::cout << "Hello, World! Release Mode" << std::endl;#endif

这样的话，代码就会区分不同的模式，执行不同的代码

在vs中 debug默认将变量赋值为0，而release并不会默认赋值，而是会给随机值，