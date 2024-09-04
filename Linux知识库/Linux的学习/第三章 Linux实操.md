# 第三章 Linux实操

## 1. vi和vim的使用
- **vi和vim**：vim是vi的增强版本，是Linux系统中常用的文本编辑器。
- **模式**：
  - **正常模式**：默认模式，可以移动光标，使用快捷键。
  - **插入模式**：按`i`进入，可以编辑文本。
  - **命令行模式**：按`Esc`进入，输入命令操作文件。

### 实例
- 打开文件：
  ```bash
  vim hello.cpp
  ```
- 编辑文件，输入代码后按`Esc`退出编辑模式。
- 保存并退出：
  ```bash
  :wq
  ```

### 1.4 快捷键
- 快捷键的具体列表可以通过网络搜索或查看vim的帮助文档获取。

## 2. 开机，关机，重启
- **shutdown**：用于系统关机和重启。
  ```bash
  shutdown -h now        # 立即关机
  shutdown -h 1          # 1分钟后关机
  shutdown -r now        # 立即重启
  ```
- **halt**：直接关机。
- **reboot**：重启系统。
- **sync**：将内存数据同步到硬盘。

### 2.1 用户的登陆和注销
- **su**：切换用户。
  ```bash
  su 用户名称
  ```
- **logout**：注销用户。

## 3. 用户的管理
- **添加用户**：`useradd`命令。
  ```bash
  useradd 选项 用户名
  ```
- **设置密码**：`passwd`命令。
  ```bash
  passwd 用户名
  ```
- **删除用户**：`userdel`命令。
  ```bash
  userdel -r 用户名
  ```
- **修改用户**：`usermod`命令。
  ```bash
  usermod 选项 用户名
  ```
- **查询用户**：`id`命令。
  ```bash
  id 用户名
  ```
- **查看当前用户**：`whoami`命令。
  ```bash
  whoami
  ```

### 3.3 Linux系统用户组的管理
- **增加用户组**：`groupadd`命令。
  ```bash
  groupadd 选项 用户组
  ```
- **删除用户组**：`groupdel`命令。
  ```bash
  groupdel 用户组
  ```
- **修改用户组**：`groupmod`命令。
  ```bash
  groupmod 选项 用户组
  ```

### 3.4 与用户账号有关的系统文件
- **/etc/passwd**：存储用户信息。

## 4. 运行级别和找回密码
- **运行级别**：Linux有7个运行级别，从0到6。
- **init**：切换运行级别。
  ```bash
  init 级别
  ```
- **找回密码**：通过单用户模式修改密码。