# MKL库的安装与使用

# MKL库

安装mkl库的时候注意：如果安装64位直接下载安装即可，

但如果想要安装32位的时候就需要先安装64位的，然后再安装32位的

# numpy.linalg.eigh

返回复厄米特矩阵（共轭对称）或实对称矩阵的特征值和特征向量。

特征值/特征向量使用LAPACK例程计算 _syevd， _heevd

# c++ 配置LAPACK库

1. 下载安装MKL库，官网： [https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html](https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html)
2. 选择操作系统，下载安装

# vs配置MKL库

1. 打开vs2019，选择工具->选项->项目和解决方案->VC++目录
2. 在新版MKL库中，安装的时候，会默认安装vs的插件，需要包含MKL库的时候不需要另外设置

按照下面的设置即可：

右键项目属性

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319417345-23730554-b601-43bd-a59e-d6191eebd93d.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319417345-23730554-b601-43bd-a59e-d6191eebd93d.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319417370-6a84fb40-8122-49cc-bc12-935555b9eead.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319417370-6a84fb40-8122-49cc-bc12-935555b9eead.png)

---

设置这些即可使用MKL库

1. 包含目录：C:\Program Files (x86)\Intel\oneAPI\mkl\latest\include

2. 库目录：C:\Program Files (x86)\Intel\oneAPI\mkl\latest\lib\intel64

---

1. 选择工具->选项->链接器->输入

1. 附加依赖项：mkl_intel_lp64.lib;mkl_sequential.lib;mkl_core.lib;libiomp5md.lib

---

1. 需要包含的头文件

#include <mkl.h>

#include <mkl_lapacke.h>

---

# MKL库函数介绍

1. 命名规则

LAPACK里的每个函数名已经说明了该函数的使用规则。所有函数都是以XYYZZZ的形式命名，对于某些函数，没有第六个字符，只是XYYZZ的形式。

# 第一个字母X代表以下的数据类型：

S REAL，单精度实数

D DOUBL

E PRECISION，双精度实数

C COMPLEX，单精度复数

Z COMPLEX*16 或DOUBLE COMPLEX

# 头2个字母表示使用的精度：( [https://netlib.org/lapack/lug/node24.html](https://netlib.org/lapack/lug/node24.html))