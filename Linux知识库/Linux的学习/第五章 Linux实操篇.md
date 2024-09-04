# 第五章 Linux实操篇

## 组管理和权限管理

- **文件权限**：Linux文件系统通过权限来控制对文件的访问，包括所有者、所在组和其他用户的读（r）、写（w）和执行（x）权限。

- **查看文件所有者**：
  ```bash
  ls -ahl
  ```

- **修改文件所有者**：
  ```bash
  chown 用户名 文件名称
  ```

- **文件权限**：使用`ls -l`查看文件权限，权限由10位字符表示，包括文件类型、所有者权限、组权限和其他用户权限。

- **修改文件权限**：
  ```bash
  chmod 权限 文件/目录
  ```
  例如，赋予所有用户读写执行权限：
  ```bash
  chmod +rwx file
  ```

## Linux进程

- **查看当前进程**：
  ```bash
  ps -l
  ```

- **动态查看进程变化**：
  ```bash
  top
  ```

## Linux磁盘分区

- **查看磁盘剩余空间**：
  ```bash
  df -h
  ```

## 包管理器

- **RPM**：Red Hat Package Manager，用于管理RPM包。
  - 查询已安装的RPM包：
    ```bash
    rpm -qa | grep 包名
    ```

- **YUM**：Yellow dog Updater, Modified，用于自动下载和安装RPM包，处理依赖关系。
  - 安装包：
    ```bash
    sudo yum install 包名称
    ```
  - 更新软件：
    ```bash
    sudo yum update
    ```
  - 删除包：
    ```bash
    sudo yum remove 包名称
    ```

## 文件权限和属性

- **修改文件所属组**：
  ```bash
  chgrp 用户组 文件/目录
  ```

- **修改文件所有者**：
  ```bash
  chown 用户名 文件/目录
  ```

- **修改文件权限**：
  ```bash
  chmod 权限 文件/目录
  ```

## 文件种类和扩展名

- Linux文件没有扩展名的概念，但通常使用扩展名来表示文件类型，如`.sh`（脚本文件）、`.zip`、`.tar`（压缩文件）等。
