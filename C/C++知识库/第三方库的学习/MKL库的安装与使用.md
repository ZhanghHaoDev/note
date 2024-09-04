# MKL库的安装与使用

#### MKL库简介
- **MKL**：Intel Math Kernel Library，是Intel公司提供的数学库，优化了多种数学运算，广泛应用于科学计算领域。

#### 安装MKL库
- **注意事项**：安装32位MKL前，需要先安装64位版本。
- **下载与安装**：
  - 访问Intel官网：[Intel MKL Download](https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html)
  - 选择操作系统，下载并安装。

#### C++配置MKL库
- **Visual Studio配置**：
  1. 打开Visual Studio 2019，选择“工具” -> “选项” -> “项目和解决方案” -> “VC++目录”。
  2. 设置包含目录和库目录：
     - 包含目录：`C:\Program Files (x86)\Intel\oneAPI\mkl\latest\include`
     - 库目录：`C:\Program Files (x86)\Intel\oneAPI\mkl\latest\lib\intel64`
  3. 设置附加依赖项：
     ```
     mkl_intel_lp64.lib; mkl_sequential.lib; mkl_core.lib; libiomp5md.lib
     ```

#### 包含的头文件
```cpp
#include <mkl.h>
#include <mkl_lapacke.h>
```

#### MKL库函数介绍
- **命名规则**：
  - 第一个字母表示数据类型：
    - `S`：REAL，单精度实数
    - `D`：DOUBLE PRECISION，双精度实数
    - `C`：COMPLEX，单精度复数
    - `Z`：COMPLEX*16 或 DOUBLE COMPLEX
  - 第二个字母表示使用精度。

#### LAPACK函数命名规则
- LAPACK函数名通常以`XYYZZZ`的形式命名，其中：
  - `X`：表示数据类型和精度。
  - `YY`：表示操作类型。
  - `ZZZ`：表示操作的具体细节。

#### 使用示例
- **初始化NE10库**：
  ```cpp
  if (ne10_init() != NE10_OK) {
      fprintf(stderr, "Failed to initialise Ne10.\n");
      return 1;
  }
  ```
