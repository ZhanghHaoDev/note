# 第八章 Python中的异常

## 1. 了解异常
- **定义**：程序运行时检测到的错误，导致Python解释器无法继续执行，出现错误提示。

## 2. 异常捕获
- **原因**：程序可能存在bug，通过异常捕获可以提前准备处理异常，保证程序稳定运行。
- **基本语法**：
  ```python
  try:
      可能发生错误的代码
  except:
      如果出现异常执行的代码
  ```
- **示例**：
  ```python
  import sys
  try:
      f = open('myfile.txt')
      s = f.readline()
      i = int(s.strip())
  except OSError as err:
      print("OS error: {0}".format(err))
  except ValueError:
      print("Could not convert data to an integer.")
  except:
      print("Unexpected error:", sys.exc_info()[0])
      raise
  ```

## 3. 异常的传递性
- **定义**：异常可以在函数之间传递，直到被捕获处理。

## 4. 模块
- **定义**：Python模块是一个`.py`文件，可以定义函数、类和变量。
- **作用**：模块是功能集合，可以快速实现特定功能。
- **导入方式**：
  - `import 模块名`
  - `from 模块名 import 类/变量/方法`
  - `from 模块名`
- **案例**：导入时间模块
  ```python
  import time
  ```

## 5. 自定义模块
- **定义**：每个Python文件都可以作为一个模块，通过文件名引入使用。

## 6. Python包
- **定义**：包是包含多个模块的文件夹，包含一个`__init__.py`文件。
- **作用**：管理多个模块，方便代码组织。
- **第三方包**：
  - 科学计算：`numpy`
  - 数据分析：`pandas`
- **安装第三方包**：使用`pip`命令
  ```bash
  pip install 包名称
  ```
