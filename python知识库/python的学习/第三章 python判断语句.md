# 第三章 python判断语句

## 1. 布尔类型和比较运算符

### 布尔类型

- **布尔类型（bool）**：True表示真，False表示假。True本质上是一个数字，True等于1，False等于0。
- **布尔类型的定义**：布尔类型的字面量
  - True 表示真（是，肯定）
  - False表示假（否，否定）
  - 定义变量存储布尔类型数据：变量名称 = 布尔类型字面量

### 比较运算符

以下假设变量a为10，变量b为20：

| 运算符 | 描述 | 实例 |
| --- | --- | --- |
| == | 等于 - 比较对象是否相等 | (a == b) 返回 False。 |
| != | 不等于 - 比较两个对象是否不相等 | (a != b) 返回 True。 |
| > | 大于 - 返回x是否大于y | (a > b) 返回 False。 |
| < | 小于 - 返回x是否小于y | (a < b) 返回 True。 |
| >= | 大于等于 - 返回x是否大于等于y | (a >= b) 返回 False。 |
| <= | 小于等于 - 返回x是否小于等于y | (a <= b) 返回 True。 |

### 示例代码

```python
a = 21
b = 10

if a == b:
    print("1 - a 等于 b")
else:
    print("1 - a 不等于 b")

if a != b:
    print("2 - a 不等于 b")
else:
    print("2 - a 等于 b")

if a < b:
    print("3 - a 小于 b")
else:
    print("3 - a 大于等于 b")

if a > b:
    print("4 - a 大于 b")
else:
    print("4 - a 小于等于 b")

# 修改变量 a 和 b 的值
a = 5
b = 20

if a <= b:
    print("5 - a 小于等于 b")
else:
    print("5 - a 大于 b")

if b >= a:
    print("6 - b 大于等于 a")
else:
    print("6 - b 小于 a")

```

## 2. if语句的基本格式
Python是通过缩进来判断代码块所属的。

程序中的判断
```python
if 要判断的条件:
    条件成立时，要做的事情
```

示例代码
```python
# 定义变量
age = 30

# 进行判断
if age >= 18:
    print("成年人")
```

注意点
- 在判断的行尾需要添加冒号（:）。
- 在if语句的判断范围内要使用缩进。
- 判断的条件的结果一定要是布尔类型。
- 不要忘记判断条件后的冒号。
- 归属于if语句的代码块，需要在前方填充4个空格缩进。

## 3. if else语句
基本格式
```python
if 要判断的条件:
    条件成立时，要做的事情
else:
    条件不成立时，要做的事情
```

注意点
- else不需要判断条件，当if的条件不满足时，else执行。
- else的代码块，同样需要4个空格作为缩进。

## 4. if elif else语句
示例代码
```python
age = int(input("请输入你家狗狗的年龄: "))

if age <= 0:
    print("你是在逗我吧!")
elif age == 1:
    print("相当于 14 岁的人。")
elif age == 2:
    print("相当于 22 岁的人。")
elif age > 2:
    human = 22 + (age - 2) * 5
    print("对应人类年龄: ", human)

# 退出提示
input("点击 enter 键退出")
```
说明
- if elif else 语句的作用是：可以完成多个条件的判断。
- 使用if elif else 的注意点是：
    - elif可以写多个。
    - 判断是互斥且有序的，上一个满足后面的就不会判断了。
    - 可以在条件判断中，直接写input语句，节省代码量。