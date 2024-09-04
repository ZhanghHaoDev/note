# 第三章 认识Mat容器

## 认识Mat容器

## 1. 什么是Mat类
- **Mat类**：是OpenCV中用于存储图像和矩阵的主要数据结构。
- **组成**：由矩阵头和数据两部分组成。矩阵头包含了图像的尺寸、类型、通道数等信息，而数据部分则存储实际的像素值。

## 2. Mat类的创建
- **基本创建**：
  ```cpp
  cv::Mat matrix(rows, cols, type);
  ```
- **使用Size结构**：
  ```cpp
  cv::Mat matrix(Size(cols, rows), type);
  ```
- **从现有Mat创建**：
  ```cpp
  cv::Mat subMatrix(m, rowRange, colRange);
  ```

## 3. Mat类方法赋值
- **单位矩阵**：`cv::Mat::eye()`
- **对角矩阵**：`cv::Mat::diag()`
- **全1矩阵**：`cv::Mat::ones()`
- **全0矩阵**：`cv::Mat::zeros()`
- **枚举方法**：
  ```cpp
  cv::Mat matrix = (cv::Mat_<int>(3, 3) << 1, 2, 3, 4, 5, 6, 7, 8, 9);
  ```

## 4. Mat类数据的读取
- **内存存储形式**：图像数据在内存中通常以行优先的方式连续存储。
- **常用属性**：
  - `cols`：列数
  - `rows`：行数
  - `step`：每行的字节大小
  - `elemSize`：每个元素的字节大小
  - `channels`：通道数
  - `total`：元素总数
- **元素读取**：使用`at<>()`方法或通过下标操作符`()`。

## 5. Mat类支持的运算
- **四则运算**：支持基本的加减乘除运算。
- **矩阵乘积**：`operator*`
- **元素乘积**：`cv::multiply()`
- **运算函数**：
  - `absdiff()`：绝对差值
  - `add()`：求和
  - `addWeighted()`：线性求和
  - `divide()`：除法
  - `invert()`：求逆
  - `log()`：对数
  - `max()` / `min()`：最大值/最小值

## 6. 图像的通道
- **灰度图像**：单通道，只包含亮度信息。
- **RGB图像**：三通道，分别代表红、绿、蓝颜色信息。
