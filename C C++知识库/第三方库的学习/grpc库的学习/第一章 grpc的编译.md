# 第一章 grpc的编译

# 1. 在Windows上的编译与安装

1. 下载全部文件和需要的插件
2. 管理员权限打开cmake-gui，使用cmake将grpc编译成vs工程
3. 管理员权限打开vs，vs打开build目录下的grpc工程
4. 先重新生成ALL_BUILD，然后生成INSTALL，生成的文件会复制到C盘下，最后有输出
5. 将生成的文件全部复制到其他目录，【注意不能有中文或中文字符】

# 2. 在linux上的编译与安装

1. grpc的编译（linux）
2. 安装编译工具：gcc版本不低于7.0，cmake版本不低于3.15

sudoapt-get install autoconf automake libtool

sudoapt-get install cmake

sudoapt-get install -y software-properties-common

sudoadd-apt-repository ppa:ubuntu-toolchain-r/test

sudoapt update

sudoapt install g++-7 -y

# 解压文件

sudotar -jxvf XXX.tar.bz2

---

1. 编译grpc

mkdir-p cmake/build

cdcmake/build

cmake../..

# 安装到指定位置

cmake../.. -DCMAKE_INSTALL_PREFIX=/opt/grpc

make

# 并行编译

make -j4

sudomake install

---

1. 安装protobuf

不能手动安装protobuf，不然版本可能不匹配，必须在grpc执行git submodule update --init命令之后生成的third_party/protobuf里面编译安装对应的protobuf

cdthird_party/protobuf/

./autogen.sh

./configure--prefix=/usr/local

make

sudomake install

sudo ldconfig  # 使得新安装的动态库能被加载

记得添加终端的环境变量，这样就可以在任何地方使用protobuf命令

protoc--version

显示3.19.4

# 编译的时候遇到问题：1. 没有编译cmake模块

2. 编译的时候需要测试，但是测试有问题

# 第一个问题，重新编译protobuf 使用cmake编译

cd cmake

mkdir build

cd build

cmake ..

# 第二个问题，禁用测试

cmake-DCMAKE_INSTALL_PREFIX=/root/protobuf-install -Dprotobuf_BUILD_TESTS=OFF ..

---

1. 如果自定义了安装位置，需要修改环境变量

sudo vim ~/.bashrc

# 增加下面两句，替换为自己的路径

export PATH=/path/to/grpc/bin:$PATH

export LD_LIBRARY_PATH=/path/to/grpc/lib:$LD_LIBRARY_PATH# 重载环境变量

source ~/.bashrc

---

1. grpc在mac上的编译与安装
2. 第一种方法使用brew来安装包

我们可以使用brew来管理包，这里使用brew来安装grpc，不用另外的下载与编译

brew install grpc

如果使用brew来安装包的话，好处有两点：相关的依赖会自动安装，在使用cmake的时候，会自动链接相关的库，不需要另外编写

1. 第二种使用下载grpc包的形式来将包安装到指定位置

首先下载该库：

百度云/学习文件夹/c++文件夹/grpc

使用git来下载该库的源码

git clone-b v1.39.0 [https://github.com/grpc/grpc](https://github.com/grpc/grpc)

---

然后cd进该目录

cd grpc

---

grpc包含一些子模块，你需要更新这些模块，网不好别更新

gitsubmodule update --init

---

开始编译grpc库，首先创建一个目录用于存放编译的结果

mkdir -pcmake/build

cdcmake/build

---

然后使用cmake来配置编译

// 默认安装

cmake ../..// 安装到指定位置cmake-DCMAKE_INSTALL_PREFIX=/opt/grpc ../..

---

然后，开始编译

make

---

编译完成后，将grpc安装到指定的位置，如果没有指定，则安装带/usr/local目录下面，安装会有提示

sudo make install

---

# 3. grpc报错，超出容量限制

报错的输出：gRPC failed, call return code:8:Received message larger than max (45129801 vs. 4194304)

原因：grpc的默认信息长度是int32_max = 410241024

解决办法：扩容

server端

builder.SetMaxMessageSize(1024*1024*1024)

---

client端

grpc::ChannelArguments channel_args;

channel_args.SetInt("grpc.max_receive_message_length",1024*1024*1024);

grpc::CreateCustomChannel(tfsAddress, grpc::InsecureChannelCredentials(),channel_args)

// tfsAddress->地址

---