# HDF5库的学习

#### 1. HDF5在Windows下的安装
- **下载HDF5库**：
  - 访问官方网站：[HDF Group](https://www.hdfgroup.org/)
  - 下载HDF5库：[HDF5 Releases](https://support.hdfgroup.org/ftp/HDF5/releases/)

- **安装步骤**：
  1. 下载.zip文件，里面包含批处理文件，执行即可。
  2. 解压文件，使用管理员权限打开CMD，切换到文件目录，执行对应Visual Studio的批处理文件（.bat）。
  3. 使用Visual Studio打开生成的文件，重新生成ALL_Build，安装文件。

- **常见问题**：
  - **无法解析的外部符号 H5T_NATIVE_FLOAT_g**：
    - 右键项目属性 -> C/C++ -> 预处理器，添加宏定义：
      ```
      _DEBUG
      _CONSOLE
      H5_BUILT_AS_DYNAMIC_LIB
      _CRT_SECURE_NO_WARNINGS
      DLL_IMPLEMENT
      ```

#### 2. HDF5在Linux下的安装
- **下载文件**：
  - 访问官方网站：[HDF Group](https://www.hdfgroup.org/)

- **安装编译工具**：
  ```bash
  sudo apt-get install cmake
  sudo apt-get install gcc
  sudo apt-get install g++
  ```

- **构建HDF5**：
  ```bash
  ./configure --prefix=/usr/local/hdf5
  make
  make check
  make check-install
  export PATH=$PATH:/usr/local/hdf5/bin
  ```

- **安装完成后**：
  - 在`/usr/local`目录下找到hdf5的包。

#### 3. HDF5库交叉编译（arm, aarch64-linux-gnu）
- **下载文件**：
  - 访问官方网站：[HDF5 Releases](https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.9/src/)

- **安装交叉编译工具**：
  ```bash
  sudo apt-get install cmake
  sudo apt-get install gcc-aarch64-linux-gnu
  sudo apt-get install g++-aarch64-linux-gnu
  ```

- **修改CMakeLists.txt**：
  ```bash
  set(CMAKE_C_COMPILER /usr/bin/aarch64-linux-gnu-gcc)
  set(CMAKE_CXX_COMPILER /usr/bin/aarch64-linux-gnu-g++)
  ```

- **构建步骤**：
  ```bash
  mkdir arm-bin
  cd arm-bin
  cmake ..
  make
  ```

- **验证编译生成的文件**：
  ```bash
  find -name "H5detect"
  find -name "H5make_libsettings"
  ```

- **导出文件到开发板**：
  ```bash
  sudo scp ./libhdf5.settings root@$DeviceIP:/libhdf5.settings
  sudo scp ./arm-bin/H5detect root@$DeviceIP:/tmp
  sudo scp ./arm-bin/H5make_libsettings root@$DeviceIP:/tmp
  ```

- **在开发板上执行**：
  ```bash
  ./tmp/H5make_libsettings > ./tmp/H5lib_settings.c
  ./tmp/H5detect > ./tmp/H5T_init.c
  ```

- **将生成的文件导入到虚拟机中**：
  ```bash
  ./tmp/H5make_libsettings > ./tmp/H5lib_settings.c
  ./tmp/H5detect > ./tmp/H5T_init.c
  ```

- **再次运行make命令**：
  ```bash
  cd ..
  make
  ```
