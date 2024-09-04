# 第一章 Shell简介

## 1.1 Shell简介
- **Shell**：指的是Shell脚本程序，与单个在终端执行的命令不同，Shell脚本是将多个命令以文件形式存储。

## 1.2 查看Shell帮助
- **man命令**：用于查看命令的帮助文档。
  ```bash
  man echo
  ```

## 1.3 Hello Shell
- **创建Shell文件**：
  ```bash
  touch main.sh
  ```
- **指定使用的Shell**：
  ```bash
  #!/bin/bash
  ```
- **输出内容**：
  ```bash
  echo "Hello shell"
  ```
- **执行文件**：
  ```bash
  bash main.sh
  ```

## 1.4 注释
- **单行注释**：
  ```bash
  # 这是单行注释
  ```
- **多行注释**：
  ```bash
  :<<EOF
  这是多行注释
  这是多行注释
  这是多行注释
  EOF
  ```

## 1.5 echo命令
- **用途**：用于在屏幕上输出文本。
  ```bash
  echo "要显示的内容"
  ```

## Shell脚本特性
- **无需编译**：Shell脚本不需要编译，可以直接执行。
- **无结束符号**：与某些编程语言不同，Shell脚本中没有语句结束符号。

