# 第一章 关于boost库的简介

## 1. boost库的简介

1. Boost库的官方网站：[http://www.boost.org/](http://www.boost.org/)
2. 学习boost的仓库：【boost_stu】
3. Boost库是一个广泛使用的C++库集合，提供了许多强大且灵活的功能，扩展了C++标准库的能力。Boost库由一组独立的库组成，每个库都可以单独使用，也可以与其他库结合使用。Boost库的许多组件已经被纳入C++标准库（如C++11、C++14、C++17和C++20）。
4. Boost库的历史
Boost库最早由Beman Dawes在1998年发起，旨在为C++标准库提供高质量的库组件。Boost库由全球的C++专家和开发者共同维护和开发，经过多年的发展，已经成为C++开发者的重要工具之一。
5. Boost库的主要特点：
    + 提供了许多高质量的库组件，覆盖了各种领域，如智能指针、容器、算法、多线程、网络编程、正则表达式等。
    + 采用了现代C++技术，提供了许多C++标准库中没有的功能。
    + 通过广泛的社区支持和活跃的开发，保持了库的更新和发展。
    + 可以与C++标准库和第三方库无缝集成，提高了代码的可移植性和可扩展性。

## 2. boost库的安装

1. linux 系统下安装boost库
```shell
sudo apt-get install libboost-all-dev
```

2. macos 系统下安装boost库
```shell
brew install boost
```

3. Windows 系统下的安装
    + 下载boost库的源代码：[http://www.boost.org/](http://www.boost.org/)
    + 解压源代码文件，进入boost目录
    + 执行bootstrap.bat脚本，生成b2编译工具
    + 执行b2命令，编译boost库
    + 设置环境变量BOOST_ROOT为boost库的安装路径

## 3. boost库的主要组件

1. Boost.Asio：一个跨平台的网络和低级I/O库，提供了同步和异步操作，支持TCP、UDP、SSL等协议。
2. Boost.Filesystem：一个文件系统库，提供了对文件和目录的操作。
3. Boost.Regex：一个正则表达式库，提供了对正则表达式的支持。
4. Boost.Thread：一个多线程库，提供了线程、互斥量、条件变量等多线程操作。
5. Boost.SmartPtr：一个智能指针库，提供了shared_ptr、weak_ptr、scoped_ptr等智能指针。
6. Boost.Bind：一个函数对象库，提供了对函数对象的绑定和适配。
7. Boost.Lambda：提供轻量级的匿名函数（lambda）支持。
8. Boost.Python：提供C++与Python的互操作支持。
9. Boost.Serialization：提供对象序列化支持。
10. Boost.Test：提供单元测试框架。
11. Boost.Log: boost的日志库

## 4. boost与CMake

1. 我们在大多数的发行版Linux和macOS上都可以使用包管理器来安装预编译好的boost库
2. Boost库默认使用的是Boost.Build（也称为b2或bjam）构建系统。Boost.Build是一个强大的构建系统，专门用于构建和安装Boost库及其组件。
3. Boost库对CMake的支持是积极的。虽然Boost库默认使用Boost.Build（b2或bjam）作为其构建系统，但Boost库也提供了良好的CMake支持，使得开发者可以方便地在CMake项目中查找和链接Boost库。
4. CMake 3.17 及以上版本中，FindBoost 模块已被移除，因此需要设置策略 CMP0167 来使用新的 Boost 配置方式。
    解决办法：cmake_policy(SET CMP0167 NEW)  # 设置策略以消除警告
            find_package(Boost REQUIRED COMPONENTS system filesystem) # 查找特定的组件
            target_link_libraries(boost_stu Boost::system Boost::filesystem)