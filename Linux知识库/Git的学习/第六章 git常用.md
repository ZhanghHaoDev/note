# 第六章 Git常用

## Git使用说明

- **添加文件到暂存区**：
  ```
  git add .
  ```

- **删除文件**：
  ```
  git rm .
  ```

- **提交改动到本地**：
  ```
  git commit -m "first commit"
  ```

- **上传改动到服务器**：
  ```
  git push
  ```

- **列出当前分支**：
  ```
  git branch
  ```

- **列出所有分支，包括远程分支**：
  ```
  git branch -a
  ```

- **从已有的分支创建新的分支（例如从master分支创建dev分支）**：
  ```
  git checkout -b dev
  ```

- **从服务器拉取分支到本地分支**：
  ```
  git pull origin gh-pages:gh-pages
  ```
  注意：如果本地已有gh-pages分支，操作可能会被拒绝。

- **上传本地分支到远程分支**：
  ```
  git branch --set-upstream-to=gh-pages
  git push origin gh-pages
  ```

## Gerrit操作

- **如何修改一个commit**：
  1. 在一个干净的仓库中拉取特定commit：
     ```
     git fetch ssh://xxx@xxxx/xxx/xxx refs/changes/20/190820/6 && git cherry-pick FETCH_HEAD
     ```
     具体指令需参考Gerrit网页右上角的指示。

  2. 修改代码后，提交到本地：
     ```
     git add
     git commit --amend
     ```

  3. push到Gerrit：
     ```
     git push origin HEAD:refs/changes/<change id>
     ```
     需要指定push到哪个change id。

## 附录

- **Git cheatsheet**：
  - 官方提供的Git cheatsheet可以在Gitlab找到。
  - 由于网络原因，提供的链接可能无法直接访问。请检查链接的合法性或稍后重试。
