# 第四章 Shell流程控制

## 控制语句

### if-then语句
- **基本格式**：
  ```bash
  if command
  then
      # commands
  fi
  ```
- **说明**：如果`command`执行成功（退出状态为0），则执行`then`部分的命令。

#### 示例
```bash
#!/bin/bash
if pwd
then
    echo "It worked"
fi
```

### if-then-else语句
- **格式**：
  ```bash
  if command
  then
      # commands
  else
      # commands
  fi
  ```
- **说明**：如果`command`执行成功，执行`then`部分；否则，执行`else`部分。

### 嵌套if
- **示例**：
  ```bash
  testuser=NoSuchUser
  if grep $testuser /etc/passwd
  then
      echo "The user $testuser exists on this system."
  elif ls -d /home/$testuser/
  then
      echo "The user $testuser does not exist on this system."
      echo "However, $testuser has a directory."
  else
      echo "The user $testuser does not exist on this system."
      echo "And, $testuser does not have a directory."
  fi
  ```

## test指令
- **用途**：提供在`if-then`语句中测试不同条件的方式。
- **数值测试**：
  ```bash
  value1=10
  value2=11
  if [ $value1 -gt 5 ]
  then
      echo "The test value $value1 is greater than 5"
  fi
  if [ $value1 -eq $value2 ]
  then
      echo "The values are equal"
  else
      echo "The values are different"
  fi
  ```
- **字符串测试**：
  ```bash
  user=baduser
  if grep $user /etc/passwd
  then
      echo "The user $user exists on this system."
  elif ls -d /home/$user/
  then
      echo "The user $user does not exist on this system."
      echo "However, $user has a directory."
  else
      echo "The user $user does not exist on this system."
      echo "And, $user does not have a directory."
  fi
  ```
- **文件测试**：
  ```bash
  if [ -e $HOME ]
  then
      echo "OK on the directory. Now checking the file."
      if [ -e $HOME/testing ]
      then
          echo "The file exists. Getting ready to remove the file."
          rm $HOME/testing
      else
          echo "File does not exist. Nothing to do."
      fi
  else
      echo "Sorry, you do not have a HOME directory."
  fi
  ```

## 循环语句

### for语句
- **基本格式**：
  ```bash
  for var in list
  do
      # commands
  done
  ```
- **示例**：
  ```bash
  for test in Alabama Alaska Arizona Arkansas California Colorado
  do
      echo The next state is $test
  done
  ```

### while命令
- **格式**：
  ```bash
  while test command
  do
      # other commands
  done
  ```
- **示例**：
  ```bash
  var1=10
  while [ $var1 -gt 0 ]
  do
      echo $var1
      var1=$[ $var1 - 1 ]
  done
  ```

### until命令
- **格式**：
  ```bash
  until test command
  do
      # other commands
  done
  ```
- **示例**：
  ```bash
  var1=100
  until [ $var1 -eq 0 ]
  do
      echo $var1
      var1=$[ $var1 - 25 ]
  done
  ```

### 循环控制
- **break命令**：退出循环。
  - **示例**：
    ```bash
    for var1 in 1 2 3 4 5 6 7 8 9 10
    do
        if [ $var1 -eq 5 ]
        then
            break
        fi
        echo "Iteration number: $var1"
    done
    echo "The for loop is completed"
    ```
- **continue命令**：跳过当前循环的剩余部分，继续执行下一次循环。
  - **示例**：
    ```bash
    for ((var1 = 1; var1 < 15; var1++))
    do
        if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
        then
            continue
        fi
        echo "Iteration number: $var1"
    done
    ```
