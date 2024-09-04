# CLAPACK的安装与使用

# 1. CLAPACK安装

CLAPACK是LAPACK的C语言接口。LAPACK的全称是Linear Algebra PACKage，是非常著名的线性代数库。原版的LAPACK是用Fortran写的，为了方便C/C++程序的使用，就有了LAPACK的C接口CLAPACK。

LAPACK的主页是： [http://www.netlib.org/lapack/](http://www.netlib.org/lapack/)

CLAPACK则在 ：    [http://www.netlib.org/clapack/](http://www.netlib.org/clapack/)。

# 1.1 下载CLAPACK

所谓的安装其实就是把源代码编译成我们可以调用的库.lib文件。

首先从主页上下载CLAPACK包。 [http://www.netlib.org/clapack/](http://www.netlib.org/clapack/) 上有很多版本。我们选择

[http://www.netlib.org/clapack/CLAPACK-3.1.1-VisualStudio.zip](http://www.netlib.org/clapack/CLAPACK-3.1.1-VisualStudio.zip)

大小: 42MB

版本: 3.1.1

是专门提供给VS用户的。

（注意:VS的版本不能太低。VC6.0是无法使用的。VS2005及以上都应该没问题。本人用的是VS2022。测试的时候发现工程文件版本太老，还需要转换一下呢。当然转换后运行也很正常。如果你坚持要使用VC++6.0那请下载 [http://www.netlib.org/clapack/CLAPACK3-Windows.zip](http://www.netlib.org/clapack/CLAPACK3-Windows.zip) 这是CLAPACK3.0版，比我介绍的版本3.1.1版要旧一些）

# 1.2 CLAPACK目录结构

下载解压后，我们可以看到如下目录结构:

| **文件夹名称** | **作用** |
| --- | --- |
| SRC | CLAPACK的源代码 |
| BLAS | BLAS的源代码 |
| F2CLIBS | F2C的源代码 |
| LIB | 编译后的库文件.lib |
| INCLUDE | 头文件 |
| TESTING | 一些使用范例程序 |
| INSTALL | 里面有UNIX和其他平台下安装的文件和方法。lawn81.pdf文件是CLAPACK的使用说明 |

# 1.3 编译CLAPACK

**这里我要提醒大家。虽然软件包里已经有编译好的.lib文件，就在\LIB中。但是我建议大家不要直接使用他们，还是自己编译一下再用才保险。很多人就是因为直接使用他们而出错的。这点非常重要！如果你就是直接调用他们失败的，那不妨先自己编译一下再试试。**

另外，CLAPACK需要F2CLIBS库，并且使用了blas和tmglib这两个外部的库。这几个库都已经包含在了CLAPACK的安装包中。所以，大家无需另外下载。当然，使用前我们还是要重新编译一下的，原因上面已经说过了。

接下来，我详细地讲讲如何编译他们。

首先双击 clapack.vcproj打开工程项目文件。工程中已经包含了所有的子项目。

我们根据个人需要，编译成debug模式，或者release模式。为了能在自己的程序调用中方便的进行debug，我这里就以debug模式为例说明。我的系统是win32。如果你是64位系统也是支持的，操作方法类似。

1. **首先编译F2CLIBS**，用于将fortran转换为c语言。

选择libf2c子项目。直接生成之。编译过程中可能会有一些warning，不要理会他们。编译成功后，输出文件是libf2cd.lib。这里的d就 是debug模式，如果是release模式就是libf2cd.lib。输出文件默认路径是\LIB文件夹。注意，\LIB\Win32下已经有一些 lib了。大家最好把他们都先删除了，以免新旧文件混淆。

1. **接着编译tmglib**。这是一个矩阵库。

这个库在TESTING\MATGEN里面。选择他生成就好了。

输出文件还是在\LIB里面。文件名是tmglibd.lib。

1. **然后是编译blas**，选择项目blas, 编译之。输出文件BLASd.lib。
2. **最后是编译CLAPACK**，生成clapackd.lib.

# 1.4 调用CLAPACK

前面，我们已经生成了CLAPACK的库文件了。那么如何在自己的程序中使用他们呢？

其实很简单。你所需要的只有两部分:

1. 头文件

头文件就是.h文件。存放在\INCLUDE中。在自己的工程里加入这个目录就行了。里面的文件最好不要作任何修改。程序中主要调用的头文件是clapack.h和f2c.h。

1. 库文件

库文件就是我们前面编译生成的那些lib文件了。

首先，VC中项目的设置方式是:

项目的属性里。C/C++选项卡中，附加包含目录里添加\INCLUDE目录。

**在这里一定需要注意的是添加头文件的顺序，一定要保证先f2c.h后clapack.h的顺序，不然就会出错**

连接器选项卡中。附加库目录里添加\LIB\Win32目录。然后附加依赖项添加libf2cd.lib BLASd.lib clapackd.lib tmglibd.lib。(根据不同的编译模式和个人需要以及系统需要选择库文件)

另外，如果想在调试时能对库函数进行源码级调试。那么需要在VS的 工具--选项--项目和解决方案--VC++目录 中添加\SRC的目录。

1. 如果程序中调用clapack库，出现complex不明确，解决办法
2. 因为clapack是c语言的库，所以这里需要使用extern关键字，并且这里的头文件需要定义在自定义头文件前面。

extern "C"

{

#include "f2c.h"

#include "blaswrap.h"

#include "clapack.h"

}

---

1. 需要将前面的文件中的complex添加作用域，std::complex，但是不要删除#include
2. 需要把该文件中所引用的头文件中所有的std命名空间都删除，在使用到std命名空间的地方添加std::关键字

# 2. CLAPCK函数说明

# 2.1 命名规则

CLAPACK的函数都采用XYYZZZ的命名格式，X表示函数期望接收的数据类型。下表是X可以采用的类型及其意义的映射关系。

| **X的取值** | **说明** |
| --- | --- |
| S | 实数，对应C中的float |
| D | 双精度，对应C中的double |
| C | 复数，对应c++中的complex |
| Z | 双精度复数，对应c++中的complex |

**字母YY表示矩阵类型**

| **字母YY的取值** | **矩阵类型** |
| --- | --- |
| BD | 双对角矩阵 |
| DI | 对角矩阵 |
| GB | 一般带状矩阵 |
| GE | 一般情形（非对称） |
| GG | 一般矩阵，广义问题（一对一版矩阵） |
| GT | 一般三对角矩阵 |
| HB | 复数厄密特带状矩阵 |
| HE | 复数厄密特矩阵 |
| HG | 上海森伯格矩阵，广义问题（即一个海森伯矩阵和一共三角矩阵） |
| HP | （复数）压缩存储的厄密特矩阵 |
| HS | 上海森伯格矩阵 |
| OP | （实数）压缩存储的正交阵 |
| OR | （实数）正交阵 |
| PB | 对称或厄密特正定带状矩阵 |
| PO | 对称或厄密特正定矩阵 |
| PP | 压缩存储的对称或厄密特正定矩阵 |
| PT | 对称或厄密特正定三对角阵 |
| SB | （实数）对称带状阵 |
| SP | 压缩存储的对称阵 |
| ST | （实数）对称三对角阵 |
| SY | 对称阵 |
| TB | 三角形带状矩阵 |
| TG | 三角形矩阵，广义问题（即一对三角形阵） |
| TP | 压缩存储的三角形阵 |
| TR | 三角形阵（类三角形阵） |
| TZ | 梯形阵 |
| UN | （复数）酉矩阵 |
| UP | （复数）压缩后的酉矩阵 |

最后三个字母表示ZZZ表示计算方法

# 2.2 函数参数说明

[https://netlib.org/lapack/explorehtml/df/d9a/group__complex16_h_eeigen_ga9b3e110476166e66f2f62fa1fba6344a.html#ga9b3e110476166e66f2f62fa1fba6344a](https://netlib.org/lapack/explore-html/df/d9a/group__complex16_h_eeigen_ga9b3e110476166e66f2f62fa1fba6344a.html#ga9b3e110476166e66f2f62fa1fba6344a)

还可以直接搜索函数名称的文件就可以找到参数说明，英文的