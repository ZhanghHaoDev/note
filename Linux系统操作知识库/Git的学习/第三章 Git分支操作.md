# 第三章 Git分支操作

## 3.1 分支简介
- **分支的作用**：允许同时推进多个任务，每个任务使用单独的分支。
- **分支的好处**：
  - 并行推进多个功能开发，提高效率。
  - 某一个分支失败，不影响其他分支。

## 3.2 分支的操作

- **查看分支**：
  ```bash
  git branch -v
  ```

- **创建分支**：
  ```bash
  git branch 分支名称
  ```

- **切换分支**：
  ```bash
  git checkout 分支名称
  ```

- **合并分支**：将其他分支合并到当前分支。
  ```bash
  git merge 分支名称
  ```

- **修改当前项目分支为main**：
  ```bash
  git branch -M main
  ```

- **修改默认分支为main**：
  ```bash
  git config --global init.defaultBranch main
  ```

## 3.3 合并冲突
- **产生冲突的原因**：合并分支时，两个分支在同一文件的同一位置有冲突的修改。
- **解决冲突**：
  1. 手动合并代码。
  2. 提交代码时，不再带文件名称。
  3. 注意修改后，只能提交合并后的分支，不影响其他分支。

## 3.4 默认分支

- **查看本地的Git默认分支**：
  ```bash
  git config --global --get init.defaultBranch
  ```

- **修改本地的Git默认分支**：
  ```bash
  git config --global init.defaultBranch main
  ```