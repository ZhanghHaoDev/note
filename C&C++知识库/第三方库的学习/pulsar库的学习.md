# pulsar库的学习

# 1. pulsar简介

pulsar是用来发送消息的，我们使用pulsar的部分都是客户端的部分，用来给服务端发送消息的

# 2. 在Linux上的安装

保证机器可以联网，有sudo权限

1. 安装依赖

```bash
# 更新软件源
sudo apt-get update

# 安装依赖
sudo apt-get install gcc g++ cmake git
sudo apt-get install libssl-dev libcurl4-openssl-dev liblog4cxx-dev
sudo apt-get install libprotobuf-dev protobuf-compiler libboost-all-dev
sudo apt-get install libzstd-dev libsnappy-dev zlib1g-dev
sudo apt-get install
```

1. 安装gtest

```bash
sudo git clone https://github.com/google/googletest.git
cd googletest
mkdir build
cd build
cmake ..
make
sudo make install
```

1. 下载pulsar-cpp-client代码

```bash
git clone https://github.com/apache/pulsar-client-cpp
```

1. 编译安装

别使用make -j 虚拟机可能会崩溃

```bash
cmake ..
make
sudo make install
```

1. 找不到GMOCK_INCLUDE_PATH-NOTFOUND
- lGMOCK_LIBRARY_PATH-NOTFOUND: 没有那个文件或目录

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1719800527945-e669a2ca-28e3-4c3d-bf34-71b76f93f4c4.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1719800527945-e669a2ca-28e3-4c3d-bf34-71b76f93f4c4.png)

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1719801534848-8a31e8ea-3251-4892-bddd-929c84ed2d70.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1719801534848-8a31e8ea-3251-4892-bddd-929c84ed2d70.png)

```bash
sudo git clone https://github.com/google/googletest.git
cd googletest-1.14.0
mkdir build
cd build
cmake ..
make
sudo make install
```

1. c++ 标准错误

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1719802406913-676a3cdd-e9af-4d60-9a45-27fbdb7bdcff.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1719802406913-676a3cdd-e9af-4d60-9a45-27fbdb7bdcff.png)

修改pulsar的cmake，添加下面的语句

```bash
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
```

# 3. pulsar的demo

```cpp
#include <pulsar/Client.h>
#include <iostream>

int main() {
    // 创建客户端
    pulsar::Client client("pulsar://10.1.3.31:31376");

    // 创建生产者
    pulsar::Producer producer;
    pulsar::Result result = client.createProducer("bht.test.camera", producer);
    if (result != pulsar::ResultOk) {
        std::cerr << "Failed to create producer: " << result << std::endl;
        return -1;
    }

    // 发送消息
    pulsar::Message msg = pulsar::MessageBuilder().setContent("Hello, Pulsar!").build();
    result = producer.send(msg);
    if (result != pulsar::ResultOk) {
        std::cerr << "Failed to send message: " << result << std::endl;
        return -1;
    }

    // 关闭客户端
    client.close();

    return 0;
}
```