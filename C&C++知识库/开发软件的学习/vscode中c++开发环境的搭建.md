# vscode中c++开发环境的搭建

这里的开发环境的平台是：macOS

工具链包括：vscode（文本编辑器），clang（编译器），lldb（调试器），cmake（构建）

# 环境搭建

vscode安装插件：clangd，记得这里如果安装了clangd，就把微软的c++插件卸载

macos安装：llvm 命令：brew install llvm

环境搭建完成后，开始创建项目，使用cmake构建项目

# 代码提示和跳转

在项目的根目录创建.vscode文件夹，CMakeList.txt文件里面添加这一句，用于生成compile_commands.json文件

set(CMAKE_EXPORT_COMPILE_COMMANDSON)

---

这里生成json文件后可以将该文件放到.vscode目录下面就可以实现代码的跳转和提示功能，记得重启

还可以使用compiledb工具来生成该json文件

安装compiledb，用于生成展开的compile_commands.json

pip install compiledb

使用，cd到build目录下面，保证build目录下面有MakeFile文件的存在

命令：compliedb -n make

# 调试功能

这里是macos平台，所以使用lldb进行调试

点击vscode中的调试功能

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308790332-81542f79-45fb-4458-9717-951aa34f942b.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308790332-81542f79-45fb-4458-9717-951aa34f942b.png)

这里我们选择创建launch.json文件，然后选择调试器

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308790229-6f2a0129-9ac8-4454-8b0b-42df9515383e.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308790229-6f2a0129-9ac8-4454-8b0b-42df9515383e.png)

修改program 这一项为：${fileDirname}/${fileBasenameNoExtension}

第一次调试会有点慢，

安装vscode插件CodeLLDB，后面会自动下载相关文件