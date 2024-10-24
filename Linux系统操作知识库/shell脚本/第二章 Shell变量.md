# 第二章 Shell变量

## 2.1 环境变量
- **定义**：系统预定义的变量，可以在Shell脚本中访问。
- **查看变量**：
  ```bash
  echo $HOME
  ```

## 2.2 用户变量
- **定义**：在Shell脚本中自定义的变量。
- **命名规则**：由字母、数字、下划线组成，区分大小写，不超过20个字符。
- **创建变量**：
  ```bash
  var1=20
  echo $var1
  ```
- **注意事项**：赋值时等号`=`两边不能有空格。

## 2.3 输入输出重定向
- **输出重定向**：将命令的输出保存到文件。
  ```bash
  ls -l > test1
  ```
- **输入重定向**：从文件读取输入到命令。
  ```bash
  wc < test1
  ```
## 2.4 数学运算
- **expr指令**：用于执行数学运算。
  ```bash
  var3=20
  var4=30
  var5=$(expr $var3 + $var4)
  echo $var5
  ```
- **方括号**：简化的算术运算。
  ```bash
  var6=20
  var7=30
  var8=$[$var6 + $var7]
  echo $var8
  ```
- **bc指令**：用于更复杂的数学运算。
  ```bash
  var9=20
  var10=30
  var11=$(echo "scale=4; $var9 / $var10" | bc)
  echo $var11
  ```

## 2.5 退出Shell
- **exit指令**：退出Shell脚本，并返回状态码。
  ```bash
  exit 0
  ```

## Shell字符串
- **单引号**：原样输出字符串，不支持变量扩展。
  ```bash
  var15='hello world'
  echo $var15
  ```
- **双引号**：支持变量扩展和转义字符。
  ```bash
  var16="hello world"
  echo $var16
  echo ${#var16}  # 输出字符串长度
  echo ${var16:1:4}  # 子串
  echo $(expr index "$var16" word)  # 查找子串
  ```

## Shell数组
- **定义**：支持一维数组，数组从0开始。
  ```bash
  array1=(1 2 3 4 5)
  echo ${array1[@]}  # 输出所有元素
  echo ${#array1[@]}  # 数组长度
  echo ${array1[0]}  # 第一个元素
  ```
