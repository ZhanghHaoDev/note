# 第二章 Git常用命令

## 2.1 设置用户签名
- **设置用户名和邮箱**：
  ```bash
  git config --global user.name 用户名
  git config --global user.email 邮箱
  ```
- **验证设置**：
  - macOS：`vim ~/.gitconfig`
  - Windows：`open .gitconfig`
  - 注意：设置的用户名和邮箱与GitHub账户无关。

## 2.2 初始化本地库
- **基本语法**：
  ```bash
  git init
  ```
- **目的**：初始化Git管理目录，增加Git管理权限，追踪目录历史版本。

## 2.3 查看本地库状态
- **基本语法**：
  ```bash
  git status
  ```
- **输出说明**：
  - 显示当前分支、未暂存变更、未跟踪文件。

## 2.4 添加到暂存区
- **基本语法**：
  ```bash
  git add 需要提交的文件
  ```
- **全部提交**：
  ```bash
  git add --all
  ```
- **删除暂存区文件**：
  ```bash
  git rm --cached 文件名称
  ```

## 2.5 提交本地库
- **基本命令**：
  ```bash
  git commit -m "提交日志" 文件名称
  ```
- **查看版本信息**：
  - `git reflog`：查看提交版本记录。
  - `git log`：查看详细记录。

## 2.6 版本穿梭
- **基本语法**：
  ```bash
  git reflog  # 获取版本号
  git reset --hard 版本号  # 穿梭到指定版本
  ```

## 2.7 查看修改信息
- **基本命令**：
  ```bash
  git diff
  ```

## 2.8 处理Git乱码
- **设置命令**：
  ```bash
  git config --global core.quotepath false
  git config --global i18n.commitencoding utf-8
  ```

## 2.9 Git中英文切换
- **macOS设置**：
  - 切换为英文：
    ```bash
    alias git='LANG=en_US git'
    ```
  - 切换为中文：
    ```bash
    alias git='LANG=zh_CN git'
    ```
- **注意**：修改`~/.zshrc`文件。
