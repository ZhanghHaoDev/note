### gRPC编译与安装笔记

#### 1. 在Windows上的编译与安装
- 下载gRPC及其依赖的插件。
- 以管理员权限打开cmake-gui，使用cmake将gRPC编译成Visual Studio工程。
- 以管理员权限打开Visual Studio，打开build目录下的gRPC工程。
- 先构建`ALL_BUILD`，然后构建`INSTALL`，生成的文件会复制到C盘下。
- 将生成的文件复制到其他目录，注意目录路径中不能包含中文或中文字符。

#### 2. 在Linux上的编译与安装
- 安装编译工具：确保gcc版本不低于7.0，cmake版本不低于3.15。
  ```bash
  sudo apt-get install autoconf automake libtool
  sudo apt-get install cmake
  sudo apt-get install -y software-properties-common
  sudo add-apt-repository ppa:ubuntu-toolchain-r/test
  sudo apt update
  sudo apt install g++-7 -y
  ```
- 解压gRPC文件。
  ```bash
  sudo tar -jxvf XXX.tar.bz2
  ```
- 编译gRPC。
  ```bash
  mkdir -p cmake/build
  cd cmake/build
  cmake ../
  cmake ../.. -DCMAKE_INSTALL_PREFIX=/opt/grpc
  make
  make -j4  # 并行编译
  sudo make install
  ```
- 安装protobuf。
  ```bash
  cd third_party/protobuf/
  ./autogen.sh
  ./configure --prefix=/usr/local
  make
  sudo make install
  sudo ldconfig
  ```
- 如果自定义了安装位置，需要修改环境变量。
  ```bash
  export PATH=/path/to/grpc/bin:$PATH
  export LD_LIBRARY_PATH=/path/to/grpc/lib:$LD_LIBRARY_PATH
  ```
- 重载环境变量。
  ```bash
  source ~/.bashrc
  ```

#### 3. 在Mac上的编译与安装
- 使用Homebrew安装gRPC。
  ```bash
  brew install grpc
  ```
- 或者下载gRPC源码并编译安装。
  ```bash
  git clone -b v1.39.0 https://github.com/grpc/grpc
  cd grpc
  git submodule update --init
  mkdir -p cmake/build
  cd cmake/build
  cmake ../../  # 默认安装
  cmake ../.. -DCMAKE_INSTALL_PREFIX=/opt/grpc  # 安装到指定位置
  make
  sudo make install
  ```

#### 4. gRPC报错处理
- 报错信息：`gRPC failed, call return code:8:Received message larger than max (45129801 vs. 4194304)`
- 原因：gRPC的默认消息长度限制。
- 解决办法：扩容。
  - 服务端设置最大消息大小。
    ```cpp
    builder.SetMaxMessageSize(1024 * 1024 * 1024);
    ```
  - 客户端设置最大接收消息长度。
    ```cpp
    grpc::ChannelArguments channel_args;
    channel_args.SetInt("grpc.max_receive_message_length", 1024 * 1024 * 1024);
    grpc::CreateCustomChannel(tfsAddress, grpc::InsecureChannelCredentials(), channel_args);
    ```
