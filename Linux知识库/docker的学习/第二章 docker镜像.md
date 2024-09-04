# 第二章 Docker镜像

## 1. Docker镜像相关命令

- **查看镜像**：
  ```bash
  sudo docker images
  ```
  这个命令用于列出本地所有Docker镜像。

- **拉取镜像**：
  ```bash
  sudo docker pull 镜像名称
  ```
  使用这个命令从Docker Hub拉取指定的镜像。

- **查找镜像**：
  ```bash
  sudo docker search 镜像名称
  ```
  通过这个命令在Docker Hub上搜索公共镜像。

- **删除镜像**：
  ```bash
  sudo docker rmi 镜像名称/ID
  ```
  使用该命令删除不再需要的本地Docker镜像。

- **构建自己的镜像**：
  创建一个名为`Dockerfile`的文件来定义镜像内容。
  ```bash
  touch Dockerfile
  ```

## 2. Dockerfile文件
- **Dockerfile**：用于创建Docker镜像的文本文件，包含一系列指令和参数。
- **示例Dockerfile**：
  ```Dockerfile
  # Version:0.1
  FROM ubuntu:14.04
  MAINTAINER James Turnbull "james@example.com"
  RUN apt-get update
  RUN apt-get install -y nginx
  RUN echo 'Hi, I am in your container' > /usr/share/nginx/html/index.html
  EXPOSE 80
  ```
- **注释**：在Dockerfile中，以`#`开头的行是注释。

## 3. 构建指令
- **构建镜像**：
  ```bash
  sudo docker build -t="name" .
  ```
  `-t`参数用于指定新镜像的名称，`.`表示Dockerfile位于当前目录。

## 4. 标签
- **设置标签**：
  ```bash
  sudo docker tag 镜像名称/ID 标签
  ```
  给镜像打标签，方便管理和复用。
