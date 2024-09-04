# 第四章 Python循环

#### 1. while 循环的基础语法
- **一般形式**：
  ```python
  while 判断条件(condition):
      执行语句(statements)……
  ```
- **示例代码**：
  ```python
  n = 100
  sum = 0
  counter = 1
  while counter <= n:
      sum = sum + counter
      counter += 1
  print("1 到 %d 之和为: %d" % (n, sum))
  ```

#### 2. while循环注意点
- 条件需要得到布尔类型，True继续循环，False结束循环。
- 需要设置循环终止的条件。
- 空格缩进与if判断一样，都需要设置。
- 嵌套循环需要注意层次关系，主要靠空格缩进确定。
- 避免无限循环，注意条件的控制。
- 循环条件的控制，层次越多越复杂，需要细心+耐心。

#### 3. for循环的基础语法
- **for循环与while循环的区别**：
  - while循环条件自定义，for循环是“轮询”机制，逐个处理数据集。
- **语法**：
  ```python
  for 临时变量 in 待处理数据集：
      循环满足条件时执行的代码
  ```
- **示例代码**：
  ```python
  sites = ["Baidu", "Google", "Runoob", "Taobao"]
  for site in sites:
      print(site)
  ```

#### 4. 注意点
- for循环无法定义循环条件，只能被动取出数据处理。
- 循环内的语句需要有空格缩进。

#### 5. range语句
- **序列类型**：字符串、列表、元组等。
- **语法**：
  - `range(num)`：从0开始，到num结束的数字序列（不含num本身）。
  - `range(num1, num2)`：从num1开始，到num2结束的数字序列（不包含num2本身）。
  - `range(num1, num2, step)`：从num1开始，到num2结束的数字序列，步长为step。

#### 6. 变量作用域
- for循环中的临时变量作用域限定在循环内部。
- 访问外部变量，将变量定义在循环外部。

#### 7. for循环的嵌套循环
- 支持嵌套循环，注意空格缩进。

#### 8. 循环中断
- **continue关键字**：中断本次循环，直接进入下一次循环。
- **break关键字**：直接结束循环。

#### 示例代码
- **使用continue**：
  ```python
  n = 5
  while n > 0:
      n -= 1
      if n == 2:
          continue
      print(n)
  print('循环结束。')
  ```
- **使用break**：
  ```python
  for n in range(2, 10):
      for x in range(2, n):
          if n % x == 0:
              print(n, '等于', x, '*', n//x)
              break
      else:
          print(n, '是质数')
  ```

