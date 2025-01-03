# 第二章 python基础语法

## 1. 字面量

字面量：在代码中，被写下来的固定的值，被称之为字面量。

- 字符串（string）：由任意数量的字符组成，如中文、英文、符号、数字等。用双引号`""`包围起来。
  - 示例：`"hello world"`

### 使用print语句输出字面量

```python
print(10)
print(13.14)
print("hello world")
```

## 2. 注释
注释：对程序代码进行解释说明的文字，不能被执行。

注释的分类
1. 单行注释：以#开头，#右边的所有文字当作说明。
    示例：# 我是单行注释
2. 多行注释：以一对三个双引号"""引起来。
    示例：
```python
"""
我是多行注释
我是多行注释
我是多行注释
"""
```

## 3. 变量
变量：在程序运行时，能存储计算结果或表示值的抽象概念。

变量的定义格式
```python
变量名 = 值
```
示例
```python
a = 10
b = 20
c = a + b
print(c)
```

## 4. 数据类型
主要使用三种数据类型：



| 类型   | 描述           | 说明                             |
| ------ | -------------- | -------------------------------- |
| string | 字符串类型     | 用引号引起来的数据都是字符串     |
| int    | 整形（有符号） | 存放整数，如-1，10，0            |
| float  | 浮点类型（有符号） | 存放小数，如：3.14，-3.14，0.0 |

查看数据类型
使用type()函数查看数据类型
```python
print(type(333))
print(type(7.089))
print(type("sss"))
```

## 5. 数据转换类型
常用的转换语句

| 语句（函数） | 说明               |
| ------------ | ------------------ |
| int(x)       | 将x转换为一个整数  |
| float(x)     | 将x转换为一个浮点数 |
| str(x)       | 将对象x转换为字符串 |

示例
```python
num_str = str(111)
print(type(num_str))
```

## 6. 运算符
标识符：用于给变量、类、方法等命名的名字。

标识符命名规则
- 只能使用字母、数字、下划线
- 不能使用数字为开头首字符
- 大小写敏感
- 不能使用关键字作为标识符

示例
```python
Ithime = 30
ithime = 40
print(Ithime)
print(ithime)
```

## 7. 运算符
### 算术运算符

| 运算符 | 描述     | 示例 |
| ------ | -------- | ---- |
| +      | 加       | 10+20 |
| -      | 减       | 10-20 |
| *      | 乘       | 10*20 |
| /      | 除       | 10/20 |
| %      | 取余数   | 10%20 |
| **     | 幂       | 10**20 |
| //     | 取整除   | 10//20 |

实例
```python
a = 21
b = 10
c = a + b
print("1 - c 的值为：", c)
c = a - b
print("2 - c 的值为：", c)
c = a * b
print("3 - c 的值为：", c)
c = a / b
print("4 - c 的值为：", c)
c = a % b
print("5 - c 的值为：", c)
a = 2
b = 3
c = a ** b
print("6 - c 的值为：", c)
a = 10
b = 5
c = a // b
print("7 - c 的值为：", c)
```

### 赋值运算符

| 运算符 | 描述     | 示例 |
| ------ | -------- | ---- |
| =      | 简单赋值 | c = a + b |

### 复合赋值运算符

| 运算符 | 描述     | 示例 |
| ------ | -------- | ---- |
| +=     | 加法赋值 | c += a 等效于 c = c + a |
| -=     | 减法赋值 | c -= a 等效于 c = c - a |
| *=     | 乘法赋值 | c *= a 等效于 c = c * a |
| /=     | 除法赋值 | c /= a 等效于 c = c / a |
| %=     | 取余赋值 | c %= a 等效于 c = c % a |
| **=    | 幂赋值   | c **= a 等效于 c = c ** a |
| //=    | 取整除赋值 | c //= a 等效于 c = c // a |

示例
```python
a = 21
b = 10
c = 0
c = a + b
print("1 - c 的值为：", c)
c += a
print("2 - c 的值为：", c)
c *= a
print("3 - c 的值为：", c)
c /= a
print("4 - c 的值为：", c)
c = 2
c %= a
print("5 - c 的值为：", c)
c **= a
print("6 - c 的值为：", c)
c //= a
print("7 - c 的值为：", c)
```

## 8. 字符串
字符串定义形式
单引号定义法：name = 'hello world'
双引号定义法：name = "hello world"
三引号定义法：name = """hello world"""

### 转义字符
| 转义字符 | 描述          | 示例 |
| -------- | ------------- | ---- |
| \n       | 换行          |      |
| \t       | 水平制表符    |      |
| \r       | 回车          |      |
| \b       | 退格          |      |

示例
```python
print("hello\nworld")
print("hello\tworld")
print("hello\rworld")
print("hello\bworld")
```

### 字符串运算符
1. +：字符串连接
2. *：重复输出字符串
3. []：通过索引获取字符串中字符
4. [:]：截取字符串中的一部分
5. in：成员运算符 - 如果字符串中包含给定的字符返回True
6. not in：成员运算符 - 如果字符串中不包含给定的字符返回True

示例
```python
a = "hello"
b = "world"
print(a + b)
print(a * 2)
print(a[1])
print(a[1:4])
print("h" in a)
print("h" not in a)
```

### 字符串格式化
- %s：格式化字符串
- %d：格式化整数
- %f：格式化浮点数
- %c：格式化字符
- %x：格式化十六进制整数

示例
```python
name = "ithime"
age = 18
print("name: %s, age: %d" % (name, age))
```

## 9. 输入输出
### 输入
input()函数：接收用户输入的内容

示例
```python
name = input("请输入姓名：")

print("姓名：", name)
```

### 输出
print()函数：输出内容

示例
```python
print("hello world")
```