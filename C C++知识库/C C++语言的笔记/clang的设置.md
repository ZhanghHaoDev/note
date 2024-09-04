# clang的设置

开发环境设置为vacose+clang的设置

1. macOS上的设置

macOS的开发环境为vscode+cmake+clang

安装cmake：brew install cmake

安装vscode：官网

安装vscode插件：clangd

这里主要设置vscode中clangd的插件：设置clangd的位置

查找clangd的位置：whereis clangd

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309584459-49f0f4ce-4d87-4e1f-ba58-552ed694995b.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309584459-49f0f4ce-4d87-4e1f-ba58-552ed694995b.png)

2023/10/27

设置vscode 中的clangd path

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309584471-8b6f7ad5-9d96-41a0-be8f-9f50ddc59543.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717309584471-8b6f7ad5-9d96-41a0-be8f-9f50ddc59543.png)

在项目中创建文件夹【.vscode】，然后在该目录下面创建【settings.json】文件，输入下面的代码，然后重启vscode就可以使用clang的代码提示，解决报错问题

记得保存该设置后一定要重启vscode，然后才可以起作用

{

"clangd.fallbackFlags":[

# 头文件位置

"-I../include",

# eigen库位置

"-I/Users/zhanghao/code/SDK/eigen/include/eigen3",

"-I/Users/zhanghao/code/SDK/gsl/include",

# c语言标准

"--std=c17",

# c++语言标准

"--std=c++17"

]

}

---

1. 如果想要在Windows上使用clang则需要下载clang，然后设置vscode