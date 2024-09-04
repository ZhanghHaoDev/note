# HDF5库的学习

# 1. HDF5在Windows下的安装

1. 下载文件： [https://www.hdfgroup.org/](https://www.hdfgroup.org/) 下载.zip文件，里面有批处理文件，执行即可

[https://support.hdfgroup.org/ftp/HDF5/releases/](https://support.hdfgroup.org/ftp/HDF5/releases/)下载HDF5库

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383940-2f9b0592-397e-4e2d-8f0a-1528279685b5.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383940-2f9b0592-397e-4e2d-8f0a-1528279685b5.png)

---

1. 解压文件，在cmd（管理员）下cd到该文件的位置，执行对应vs的批处理文件（.bat）
2. 使用vs打开生成的文件，重新生成ALL_Build，安装文件

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383710-ba71d7f7-3f29-463d-8a8e-be4c41364989.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383710-ba71d7f7-3f29-463d-8a8e-be4c41364989.png)

---

【问题】：无法解析的外部符号 H5T_NATIVE_FLOAT_g

右键属性-》c/c++->预处理器

_DEBUG

_CONSOLE

H5_BUILT_AS_DYNAMIC_LIB

_CRT_SECURE_NO_WARNINGS

DLL_IMPLEMENT

---

【问题】：使用double类型

在使用HDF5库读取HDF5文件的时候，必须使用float类型，使用double类型会产生很大的误差

// 获取HDF5文件的value

void get_value(const char* filename, const char* key, std::vector<double>& value)

{

hid_t file_id = H5Fopen(filename, H5F_ACC_RDONLY, H5P_DEFAULT);

hid_t group_id = H5Gopen(file_id, "/", H5P_DEFAULT);

hid_t dataset_id = H5Dopen(group_id, key, H5P_DEFAULT);

hid_t dataspace_id = H5Dget_space(dataset_id);

hsize_t dims_out[2];

int rank = H5Sget_simple_extent_ndims(dataspace_id);

H5Sget_simple_extent_dims(dataspace_id, dims_out, NULL);

hsize_t size = dims_out[0] * dims_out[1];

float* data_mem = new float[size];// 这里必须使用float，使用double会有很大的误差

H5Dread(dataset_id, H5T_NATIVE_FLOAT, H5S_ALL, H5S_ALL, H5P_DEFAULT, data_mem);

for (int i = 0; i < size; i++)

{

value.push_back(data_mem[i]);

}

delete[] data_mem;

H5Sclose(dataspace_id);

H5Dclose(dataset_id);

H5Gclose(group_id);

H5Fclose(file_id);

}

---

# 2. HDF5在Linux下的安装

1. 下载文件
2. 安装编译工具和构建工具，gcc，cmake

sudo apt-get install cmake

sudo apt-get install gcc

sudo apt-get install g++

---

1. 开始构建

// 指定安装路径

./configure --prefix=/usr/local/hdf5

make

make check

make check-install

export PATH=$PATH:/usr/local/mpi/hdf5

---

1. 安装完成后会在/usr/local下面找到hdf5的包

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319384392-c1b2dc23-f0ab-42a5-a2df-11a071e228ed.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319384392-c1b2dc23-f0ab-42a5-a2df-11a071e228ed.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383882-487f83b6-d017-46d8-af14-d0a40455eab0.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383882-487f83b6-d017-46d8-af14-d0a40455eab0.png)

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383748-1309c73c-2fd6-4e66-8226-e0843a634f12.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319383748-1309c73c-2fd6-4e66-8226-e0843a634f12.png)

---

【问题】：make的时候找不到HDF5

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319386112-220d31d4-dad7-403f-85bc-fa56334897ab.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319386112-220d31d4-dad7-403f-85bc-fa56334897ab.png)

---

【解决办法】：检查HDF5的安装，重新定位到HDF5的安装位置

make check

make check-install

---

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319384861-e53d83ad-d36a-425e-b3a2-b80632b7c27c.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319384861-e53d83ad-d36a-425e-b3a2-b80632b7c27c.png)

---

# 3. HDF5库交叉编译（arm,aarch64-linux-gnu）

【注意】：这里最好让开发板有一个操作系统，而不是Linux源码，有操作系统的话就可以像Linux上面一样直接编译安装，不用进行下面的操作

1. 下载文件： [https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.9/src/](https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.9/src/)
2. Linux下安装cmake，安装交叉编译工具，确保没有安装X86的gcc编译器

sudo apt-get install cmake

sudo apt-get install gcc-aarch64-linux-gnu

sudo apt-get install g++-aarch64-linux-gnu

// 检查是否安装成功

cmake -v

aarch64-linux-gnu-gcc -v

aarch64-linux-gnu-g++ -v

---

1. 修改CMakeList.txt文件，添加交叉编译的编译器，在文件的开头

set(CMAKE_C_COMPILER /usr/bin/aarch64-linux-gnu-gcc)

set(CMAKE_CXX_COMPILER /usr/bin/aarch64-linux-gnu-g++)

---

1. 新建arm-bin目录，cmake

mkdir arm-bin

cd arm-bin

cmake ..

---

【问题】：cmake找不到c和c++编译器[[🎨image.png]](https://cdn.nlark.com/yuque/0/2023/png/33648751/1677223306220-1f6f075a-1df9-4e9c-baf3-90fb29082699.png#averageHue=%23fbfbfa&clientId=u4cffd74b-94a7-4&from=paste&height=437&id=ufcaace23&originHeight=655&originWidth=1698&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=257012&status=done&style=none&taskId=uef885b33-39b9-43cd-9ea9-03379333e29&title=&width=1132)

在终端下执行：

sudo apt-get update

sudo apt-get install -y build-essential

---

1. 执行完cmake，会需要很长时间，我大概编译了2天，然后回到主目录make

cd ..

make

make

---

1. 验证编译生成的文件，查找H5detect，H5detect，H5make_libsettings

find -name "H5detect"

find -name "H5detect"

find -name "H5make_libsettings"

---

1. 在虚拟机中执行查找到的文件，如果无法执行，则表示生成成功
2. 将生成的三个文件，导出到板子上，执行这三个文件

// 将文件导出到板子上

sudo scp ./libhdf5.settings root@$DeviceIP:/libhdf5.settings

sudo scp ./arm-bin/H5detect root@$DeviceIP:/tmp

sudo scp ./arm-bin/H5make_libsettings root@$DeviceIP:/tmp

// 在板子上执行该文件

./tmp/H5make_libsettings > ./tmp/H5lib_settings.c

./tmp/H5detect> ./tmp/H5T_init.c

---

1. 将上面的两个文件导入到虚拟机中，复制到HDFpath目录中，运行下面的两个命令

./tmp/H5make_libsettings > ./tmp/H5lib_settings.c

./tmp/H5detect> ./tmp/H5T_init.c

---

1. 在虚拟机中，再次运行make命令，直到完成
2. 生成的文件在arm-bin目录下，可以复制到任何地方