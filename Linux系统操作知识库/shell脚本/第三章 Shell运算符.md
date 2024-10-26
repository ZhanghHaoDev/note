# 第三章 Shell运算符

## 算数运算符
- **加法**：`expr $a + $b`
- **减法**：`expr $a - $b`
- **乘法**：`expr $a \* $b`
- **除法**：`expr $b / $a`
- **取余**：`expr $b % $a`
- **赋值**：`a=$b`
- **相等**：`[ $a == $b ]`
- **不相等**：`[ $a != $b ]`

## 关系运算符
- **等于**：`[ $a -eq $b ]`
- **不等于**：`[ $a -ne $b ]`
- **大于**：`[ $a -gt $b ]`
- **小于**：`[ $a -lt $b ]`
- **大于等于**：`[ $a -ge $b ]`
- **小于等于**：`[ $a -le $b ]`

## 布尔运算符
- **非**：`!`
- **或**：`-o`
- **与**：`-a`

## 逻辑运算符
- **AND**：`&&`
- **OR**：`||`

## 字符串运算符
- **等于**：`[ $a = $b ]`
- **不等于**：`[ $a != $b ]`
- **长度为0**：`[ -z $a ]`
- **长度非0**：`[ -n "$a" ]`
- **非空**：`[ $a ]`

## 文件测试运算符
- **块设备**：`[ -b $file ]`
- **字符设备**：`[ -c $file ]`
- **目录**：`[ -d $file ]`
- **普通文件**：`[ -f $file ]`
- **可读**：`[ -r $file ]`
- **可写**：`[ -w $file ]`
- **可执行**：`[ -x $file ]`
- **非空**：`[ -s $file ]`
- **存在**：`[ -e $file ]`
