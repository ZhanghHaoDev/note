# fftw的学习

官网： [http://www.fftw.org/](http://www.fftw.org/)

# 1. linux下的安装

1. 下载源码

// 1. 创建文件夹存放库文件

mkdir fftw_install

// 2. 解压文件

tar -xzvf fftw-3.3.8.tar.gz

// 3. 进入解压的文件夹

cd fftw..

// 4. 安装配置

./configure --prefix=/home/fftw_install

// 5. 编译

make

// 6. 安装

make insatall

---