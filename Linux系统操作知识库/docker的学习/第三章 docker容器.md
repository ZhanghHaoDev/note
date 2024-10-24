# 第三章 Docker容器

## 1. Docker容器相关命令

- **创建容器**：
  ```bash
  docker run -it --name=c1 centos:7 /bin/bash
  ```
  - `-i`：保持容器的标准输入（STDIN）打开，即使不附加到容器终端。
  - `-t`：分配一个伪终端。
  - `--name=c1`：为容器指定一个名称。
  - `centos:7`：指定要使用的镜像。
  - `/bin/bash`：启动容器后执行的命令。

- **退出容器**：使用`exit`命令退出容器。

### 1.1 查看正在运行的容器
- **查看当前运行的容器**：
  ```bash
  docker ps
  ```
- **查看所有容器**：
  ```bash
  docker ps -a
  ```

### 1.2 进入和启动容器
- **进入指定容器**：使用`docker exec`命令。
- **启动容器**：
  ```bash
  docker start 名称/ID
  ```
- **重新进入容器**：
  1. 启动容器：
     ```bash
     sudo docker start 容器名称/ID
     ```
  2. 附着到容器：
     ```bash
     sudo docker attach 容器名称/ID
     ```

### 1.3 查看容器日志
- **查看容器日志**：
  ```bash
  sudo docker logs 容器名称/ID
  ```

### 1.4 查看容器内部进程
- **查看容器内部进程**：
  ```bash
  sudo docker top 容器名称/ID
  ```

### 1.5 查看容器信息
- **查看容器详细信息**：
  ```bash
  sudo docker inspect 容器名称/ID
  ```

### 1.6 删除容器
- **删除容器**：
  ```bash
  sudo docker rm 容器名称/ID
  ```
  注意：正在运行的容器无法直接删除。
