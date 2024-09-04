# Visual Studio的使用

# 1. 安装配置

官网： [https://visualstudio.microsoft.com/zh-hans/vs/](https://visualstudio.microsoft.com/zh-hans/vs/)

# 1.1 安装插件

最新版本的vs可以点击扩展来安装插件，其他版本可以通过插件网站来下载安装包安装插件

插件网站： [https://marketplace.visualstudio.com/vs](https://marketplace.visualstudio.com/vs)

常用的插件：

CodeMaid VS2022 :  快速格式化代码

VSColorOutput64： 彩色输出

Viasfora：彩色括号

Productivity Power Tools：多个工具合集

# 2. 开发常见问题

1. 无法解析的外部符号

程序编译的时候经常出现的问题，输出提示有无法解析的外部符号，大部分情况下是因为lib库的链接问题

首先查看链接库的路径问题，在使用相对路径的情况下可能会由于输入错误，导致编译器找不到lib库的路径

然后查看链接的库是否全，或者名称对应的上，通常.h头文件对应的就是lib库的名称

1. 应用程序无法正常启动

这个问题多半是因为dll库的问题，每个lib库都对应dll库

首先检查环境变量的问题，path中是否有正在调用的库的bin目录，如果没有记得添加，重启vs，或重启电脑

或者直接把缺少的dll库直接复制到.exe启动目录下

# 3. 调试技巧

1. 在调试模式下查看变量的值：在监视窗口输入需要查看的变量的名称，vector可以在后面输入索引来查看具体位置的值

value[333]// 在监视窗口输入，查看value在333位置的值

---

1. 调试的时候不显示内存数值

工具-》选项-》调试-》常规-》在变量窗口中显示对象的原始结构

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308828701-82e521d9-b84b-4618-bba9-80ad68d08d16.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308828701-82e521d9-b84b-4618-bba9-80ad68d08d16.png)

---

[vs开发cmake项目](vs开发cmake项目%2034f2e50ba47949ceaf64f1c2e436fab6.md)

[windbg 调试器](windbg%20调试器%207c622296648748beb39af0ea0c2932f8.md)

[Visual Studio的调试技巧](Visual%20Studio的调试技巧%200e192c52a7734a2cbdd2a57fadfe3ca2.md)