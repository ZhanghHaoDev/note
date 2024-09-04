# 第七章 Shell的实例

## 1. Shell脚本库

- **shtool库**：一个提供多种实用函数的第三方Shell脚本库。

### 下载和安装
- **下载**：
  ```bash
  wget http://ftp.gnu.org/gnu/shtool/shtool-2.0.8.tar.gz
  ```
- **解压**：
  ```bash
  tar -zxvf shtool-2.0.8.tar.gz
  ```
- **安装**：
  ```bash
  cd shtool-2.0.8/
  ./configure
  make
  sudo make install
  ```

## 2. shtool库简介
- **函数描述**：
  - `Arx`：创建归档文件。
  - `Echo`：显示字符串。
  - `fixperm`：改变文件权限。
  - `install`：安装脚本或文件。
  - `mdate`：显示文件或目录的修改时间。
  - `mkdir`：创建目录。
  - `Mkln`：创建链接。
  - `move`：移动文件。
  - `Path`：处理程序路径。
  - `Prop`：显示进度条。
  - `rotate`：转置日志文件。
  - `version`：创建版本信息文件。

## 3. 例子
- **使用shtool库函数**：
  ```bash
  #!/bin/bash
  # 使用shtool库中的函数输出平台信息
  shtool platform
  ```

## 4. 执行结果
- 执行上述脚本，输出系统信息：
  ```bash
  $ bash shtool_example.sh
  Ubuntu 23.04 (AMD64)
  ```
