# vcpkg的安装与使用

# 1. vcpkg的简介

vcpkg是Microsoft的跨平台开源软件包管理器，极大地简化了 Windows、Linux 和 macOS 上第三方库的购置与安装。如果项目要使用第三方库，建议通过 vcpkg 来安装它们。vcpkg 同时支持开源和专有库。

# 2. 安装

git clone [https://github.com/microsoft/vcpkg](https://github.com/microsoft/vcpkg)

---

# 2.1 编译

# 在Windows下cd到vcpkg的安装目录，执行该命令

bootstrap-vcpkg.bat

---

# 2.2 集成到Windows环境变量

| **环境变量** | **值** | **描述** |
| --- | --- | --- |
| path | 安装目录 | 命令行直接启动vcpkg |
| VCPKG_DEFAULT_TRIPLET | x64-windows | vcpkg默认构建的三元组，通常在Windows 64位平台下可以直接设置为x64-windows |

### 2.3 文件夹层次结构

| **文件夹名称** | **描述** |
| --- | --- |
| buildtrees | 包含从中生成每个库的源的子文件夹。 |
| docs | 文档和示例。 |
| downloads | 所有已下载的工具或源的缓存副本。 运行安装命令时，vcpkg 会首先搜索此处。 |
| installed | 包含每个已安装库的标头和二进制文件。 与 Visual Studio 集成时，实质上是相当于告知它将此文件夹添加到其搜索路径。 |
| packages | 在不同的安装之间用于暂存的内部文件夹。 |
| ports | 用于描述每个库的目录、版本和下载位置的文件。 如有需要，可添加自己的端口。 |
| scripts | 由 vcpkg 使用的脚本（CMake、PowerShell）。 |
| toolsrc | vcpkg 和相关组件的 C++ 源代码。 |
| triplets | 包含每个受支持目标平台（如 x86-windows 或 x64-uwp）的设置。 |

# 3. 使用

在vcpkg中默认安装的库是X86的库，需要安装64位的库，则需要指定

#安装64位

> vcpkg install package_name:x64-windows

> vcpkg install package_name:x64 --triplet=x64-windows

#安装32位

> vcpkg install package_name

> vcpkg install package_name:x86-windows

> vcpkg install package_name:x64 --triplet=x86-windows

---

**要是遇到vs不能找到安装的库，很有可能就是因为安装的版本（x86，x64）不一致**

1. 查看 vcpkg支持的库

vcpkg serch

---

1. 查看vcpkg安装的库

vcpkg list

---

1. 安装开源库

vcpkg install 库名称

---

1. 集成到VS中

vcpkg integrate install

vcpkg integrate remove #如果希望去掉vcpkg的全局集成可以使用以下命令：

---

Applied user-wide integration for this vcpkg root 表示集成成功，这时候就可以在VS中使用vcpkg了

1. 移除vcpkg

vcpkg integrate remove

---

1. 移除安装的库

vcpkg remove NAME

---

# 3.2 VS中设置vcpkg

1. 生成配置

vcpkg integrate project

---

执行命令成功后会在“\scripts\buildsystems”目录下，生成nuget配置文件

1. 配置Nuget

点击菜单“工具”， 选择"NuGet 包管理器->程序包管理器设置".

添加新的源, 选择vcpkg目录下的“scripts\buildsystems”目录，然后点击右侧的“更新”按钮。点击“确定”按钮，关闭对话框。

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890803-a71bb5f4-9d38-4691-a886-55659d2b19a5.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890803-a71bb5f4-9d38-4691-a886-55659d2b19a5.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890488-10328ce8-b346-42db-b2ce-600142020fd0.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890488-10328ce8-b346-42db-b2ce-600142020fd0.png)

---

1. 工程配置

右键点击需要设置的工程弹出菜单，选择“管理 NuGet 程序包”。在右上角的“程序包源”中选择刚刚设置的“vcpkg”。这样在“浏览”选项卡中就可以看到“vcpkg.D.vcpkg”。点击最右侧的“安装”。此时就集成到某个工程了。

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308891252-c70d1c9f-c8d5-4e5d-8eb7-b4af61e6dde8.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308891252-c70d1c9f-c8d5-4e5d-8eb7-b4af61e6dde8.png)

---

1. vcpkg在clion中的使用

clion在最新的版本中已经集成了vcpkg，我们点击搜索，输入vcpkg

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890156-01e8c7da-33b2-4a5a-86fd-1c3d1ace7c35.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890156-01e8c7da-33b2-4a5a-86fd-1c3d1ace7c35.png)

在打开的窗口中输入vcpkg的安装目录

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890145-f57ac20f-57f5-4249-8136-a95564a9ba31.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890145-f57ac20f-57f5-4249-8136-a95564a9ba31.png)

我们在使用的时候可以使用Windows命令行来安装第三方包，或者在Clion中输入想要安装的包

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890687-aae840b3-03e9-4dd1-9aca-da8b199d3998.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717308890687-aae840b3-03e9-4dd1-9aca-da8b199d3998.png)