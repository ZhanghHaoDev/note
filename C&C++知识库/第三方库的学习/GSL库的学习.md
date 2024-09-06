# GSL库的学习

#### 简介
- **GSL**：GNU Scientific Library，是一个开源的C++数值计算库。
- **特点**：
  - 提供高质量的数值计算函数和算法。
  - 支持线性代数、微积分、优化、随机数生成等。
  - 丰富的文档和示例代码。
  - 良好的可移植性和兼容性。
- **开源协议**：GNU通用公共许可证（GPL）。

#### 编译安装
- **下载GSL库**：
  - 访问官方网站：[GNU Scientific Library](https://www.gnu.org/software/gsl/)
  - 或者GitHub：[GSL GitHub](https://github.com/ampl/gsl)

- **编译安装步骤**：
  ```bash
  tar -zxvf gsl-2.7.tar
  cd gsl-2.7
  ./configure --prefix=/Users/zhanghao/code/SDK/gsl/
  make
  sudo make install
  ```

#### 示例代码
- **示例**：使用GSL库进行常微分方程求解。
  ```cpp
  #include <iostream>
  #include <gsl/gsl_errno.h>
  #include <gsl/gsl_odeiv2.h>

  int func(double t, const double y[], double f[], void *params) {
      double y1 = y[0];
      double y2 = y[1];
      double y1dot = y2;
      double y2dot = -y1;
      f[0] = y1dot;
      f[1] = y2dot;
      return GSL_SUCCESS;
  }

  int main() {
      double t = 0.0;
      double y[2] = {0.0, 1.0};
      double h = 0.1;
      gsl_odeiv2_system sys = {func, NULL, 2, NULL};
      gsl_odeiv2_driver *driver = gsl_odeiv2_driver_alloc_y_new(&sys, gsl_odeiv2_step_rk8pd, 1e-6, 1e-6, 0.0);
      for (int i = 0; i < 10; ++i) {
          double ti = i * h;
          int status = gsl_odeiv2_driver_apply(driver, &t, ti, y);
          if (status != GSL_SUCCESS) {
              std::cerr << "Error: gsl_odeiv2_driver_apply failed with status " << status << std::endl;
              break;
          }
          std::cout << "t = " << t << ", y = " << y[0] << " " << y[1] << std::endl;
      }
      gsl_odeiv2_driver_free(driver);
      return 0;
  }
  ```

#### CMakeLists.txt
- **配置CMakeLists.txt**：
  ```cmake
  cmake_minimum_required(VERSION 3.20)
  project(gsl_demo)
  set(CMAKE_C_STANDARD 11)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_EXTENSIONS ON)
  set(CMAKE_C_EXTENSIONS ON)
  set(CMAKE_BUILD_TYPE Debug)
  set(CMAKE_PREFIX_PATH "/Users/zhanghao/code/SDK/gsl" ${CMAKE_PREFIX_PATH})
  find_package(GSL REQUIRED)
  add_executable(gsl_demo ${PROJECT_SOURCE_DIR}/main.cpp)
  target_link_libraries(gsl_demo GSL::gsl GSL::gslcblas)
  ```