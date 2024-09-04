# 第六章 Shell的函数

## 创建函数
- **使用`function`关键字**：
  ```bash
  function name {
      # ...
  }
  ```
- **使用命名函数**：
  ```bash
  name() {
      # ...
  }
  ```

## 使用函数
- **定义和调用函数**：
  ```bash
  #!/bin/bash

  # 使用function关键字定义函数
  function func1() {
      echo "This is func1"
  }
  func1

  # 使用()定义函数
  func2() {
      echo "This is func2"
  }
  func2
  ```

## 函数的返回值
- **返回状态码**：
  ```bash
  func3() {
      echo "This is func3"
  }
  echo "func3的退出状态码为: $?"
  ```
- **使用`return`指令**：
  ```bash
  func4() {
      echo "This is func4"
      return 1
  }
  func4
  echo "func4的退出状态码为: $?"
  ```

## 函数参数
- **获取函数参数**：
  ```bash
  func5() {
      echo "This is func5"
      echo "第一个参数为: $1"
      echo "第二个参数为: $2"
      echo "第三个参数为: $3"
  }
  func5 1 2 3
  ```
- **获取参数个数**：
  ```bash
  func6() {
      echo "This is func6"
      echo "参数个数为: $#"
  }
  func6 1 2 3
  ```
- **获取所有参数**：
  ```bash
  func7() {
      echo "This is func7"
      echo "所有参数为: $*"
  }
  func7 1 2 3

  func8() {
      echo "This is func8"
      echo "所有参数为: $@"
  }
  func8 1 2 3
  ```