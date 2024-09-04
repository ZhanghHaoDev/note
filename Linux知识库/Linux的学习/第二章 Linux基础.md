# Linux的目录结构

Linux文件系统采用树状目录结构，最顶层是根目录 `/`，以下是一些主要的目录及其用途：

1. **/bin**：存放基本的二进制文件，即系统命令。
2. **/boot**：存放启动Linux时使用的核心文件。
3. **/dev**：存放设备文件。
4. **/etc**：存放系统配置文件。
5. **/home**：用户的主目录。
6. **/lib**：存放库文件，为系统提供共享函数。
7. **/mnt**：临时挂载文件系统的目录。
8. **/opt**：额外安装的应用程序。
9. **/proc**：虚拟文件系统，提供系统和进程信息。
10. **/root**：系统管理员的主目录。
11. **/sbin**：存放系统管理员使用的二进制文件。
12. **/selinux**：存放SELinux相关的文件（Red Hat/CentOS特有）。
13. **/srv**：存放服务启动后需要的数据。
14. **/sys**：与/proc类似，提供系统硬件和内核信息。
15. **/tmp**：存放临时文件。
16. **/usr**：存放用户应用程序和文件。
17. **/var**：存放经常变化的文件，如日志文件。
18. **/run**：存放系统启动以来的临时文件。

## 远程登录Linux

- **安装SSH服务器**：
  ```bash
  sudo apt-get install openssh-server  # Debian/Ubuntu
  sudo yum install openssh-server      # Red Hat/CentOS
  ```

- **SSH服务管理**：
  ```bash
  systemctl status sshd  查看服务状态
  systemctl start sshd   打开服务
  systemctl stop sshd     关闭服务
  systemctl restart sshd  重启服务
  systemctl enable sshd   设置开机启动
  systemctl disable sshd  设置开机不启动
  systemctl reload sshd   重新加载配置文件
  ```

## Linux的基础命令

- **显示日期**：
  ```bash
  date
  ```

- **显示日历**：
  ```bash
  cal
  ```

- **清屏**：
  ```bash
  clear
  ```

## 重要热键

- **Tab键**：命令补全。
- **Ctrl+C**：退出当前指令。

## 路径

- **绝对路径**：从根目录 `/` 开始的完整路径。
- **相对路径**：相对于当前工作目录的路径，如 `./` 表示当前目录，`../` 表示上一层目录。
