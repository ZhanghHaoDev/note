# 第一章 docker简介

# 1. docker的简介

docker是一个能够把开发的应用程序自动部署到容器的开源引擎，诞生于2013年，docker可以让开发者打包他们的应用以及依赖包到一个轻量级，可移植的容器中，然后发布到任何流行的Linux机器上，容器是完全使用沙箱机制，互相隔离的。容器性能开销极低，docker分为ce（社区版）和ee（企业版）

# 2. 安装docker

docker可以运行在Windows，Linux，macos上安装步骤: 可以参考官网：[https://docs.docker.com/desktop/install/ubuntu/](https://docs.docker.com/desktop/install/ubuntu/)a. yum包更新：sudo yum updateb. 安装包：sudo yum install -y yum-utils device-mapper-persistent-data lvm2c. 安装docker：sudo yum install -y docker-ced. 查看docker版本，验证安装：docker -ve. 乌班图安装：sudo snap install docker

# 3. docker架构

镜像：docker镜像，就相当于是一个root文件系统。比如官方镜像ubuntu:16.04就包含了完整的一套ubuntu16.4最小系统的root文件系统容器：镜像和容器的关系，就像是面向对象程序设计中的类和对象一样，镜像的静态的定义，容器是镜像运行时的实体。容器可以被创建，启动，停止，删除，暂停等仓库：仓库可以看成是一个代码控制中心，用来保存镜像

# 4. docker服务相关命令

```bash
启动docker服务
systemctl start docker
停止docker服务
systemctl stop docker
重启docker服务
systemctl restsrt docker
查看docker服务状态
systemctl status docker
设置开机启动docker服务
systemctl enable docker
```