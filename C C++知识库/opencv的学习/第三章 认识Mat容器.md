# 第三章 认识Mat容器

# 1. 什么是Mat类

1. Mat是opencv中的主要数据结构，本质是一个矩阵

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320289995-b45cf3d7-c93a-4ece-accb-e271c7c62528.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320289995-b45cf3d7-c93a-4ece-accb-e271c7c62528.png)

---

1. Mat分为矩阵头和数据两部分

矩阵头中存储矩阵的尺寸，行数，列数，数据类型，通道数，引用次数

1. Mat能存储的数据类型包括：整数类型，浮点类型，char类型
2. opencv中规定的类型

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320290041-09d49320-4bfe-4fd7-836d-1cfc3f22695e.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320290041-09d49320-4bfe-4fd7-836d-1cfc3f22695e.png)

---

# 2. Mat类的创建

1. 利用矩阵宽，高和类型参数创建Mat类

Mat()

cv::Mat::Mat(int rows,int cols,int type);

---

- rows：构造矩阵的行数
- cols： 矩阵的列数
- type： 矩阵中存储的数据类型。此处除了CV_8UC1，CV_64FC4等1到4通道以外，最大可以到512
1. 利用矩阵Size()结构和数据类型参数创建Mat类

Mat()

cv::Mat::Mat(Size size,int type);

---

- size: 2D数组变量尺寸，通过Size(cols,rows)进行赋值
- type：与前面一致
1. 利用已有的Mat类创建新的Mat类

Mat()

cv::Mat::Mat(const Mat& m,const Range& rowRange,const Range& colRange = range::all);

---

- m：已经构建完成的Mat类矩阵数据
- rowRange：在已有矩阵中需要截取的行数范围，是一个Range变量，例如从第二行到第五行表示为Range（2，5）
- colRange： 在已有矩阵中需要截取的列数范围，是一个Range变量，同上

# 2.2 Mat类方法赋值

- eye：单位矩阵
- diag：对角矩阵
- ones：元素全为1的矩阵
- zeros：元素全为0的矩阵

# 2.3 枚举方法赋值

cv::Mat a = (cv::Mat_<int>(3,3)<<1,2,3,4,5,6,7,8,9);

---

# 3. Mat类数据的读取

# 3.1 Mat数据在内存中存放形式

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320289989-03e889a4-2a0e-4efd-bba9-562a717d20c8.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320289989-03e889a4-2a0e-4efd-bba9-562a717d20c8.png)

---

# 3.2 Mat类矩阵的常用属性

| **属性** | **作用** |
| --- | --- |
| cols | 矩阵的列数 |
| rows | 矩阵的行数 |
| step | 矩阵的有效宽度（字节单位） |
| elemSize | 每个元素的字节数 |
| channels | 矩阵中的通道数 |
| total | 矩阵中元素的个数 |

# 3.3 Mat元素的读取

at方法读取矩阵的元素at(int row,int col)

也可以使用for循环遍历输出mat单个元素

# 4. Ma类支持的运算

# 4.1 四则运算

1. opencv中的Mat类支持数学中的加减乘除运算，但需要保证两个Mat类的大小行列数一致

Mat a(3, 3, CV_8UC1);

Mat b(3, 3, CV_8UC1);

Mat c = a*b;

---

1. 矩阵乘积*：行列大小一致
2. 向量内积.dot
3. 对应位元素乘积.mul()

# 4.2 运算函数

1. 常用的函数

| 函数名称 | 作用 |

| --- | --- |

| absdiff() | 两个矩阵对应元素差的绝对值 |

| add() | 两个矩阵求和 |

| add Weighted() | 两个矩阵线性求和 |

| divide() | 矩阵除法 |

| invert() | 矩阵求逆 |

| log() | 矩阵求对数 |

| max() / min() | 两个矩阵计算最大值/最小值 |

// Mat矩阵的四则运算

Mat num1(3, 3, CV_8UC1, Scalar(1));

Mat num2(3, 3, CV_8UC1, Scalar(2));

cout << "num1 = " << endl << num1 << endl << endl;

cout << "num2 = " << endl << num2 << endl << endl;

// 加法

Mat add = num1 + num2;

cout << "add = " << endl << add << endl << endl;

// 减法

Mat sub = num1 - num2;

cout << "sub = " << endl << sub << endl << endl;

// 乘法

Mat mul = num1.mul(num2);

cout << "mul = " << endl << mul << endl << endl;

// 除法

Mat div = num1 / num2;

cout << "div = " << endl << div << endl << endl;

---

# 5. 图像的通道

我们知道彩色图像是由像素组成的，像素由一系列代码表示的原色组合而成的，在这种情况下，通道是与彩色图像大小相同的灰度图像，仅有这些原色构成

简单来说：图像由最基本的几种颜色构成，该图像就是几通道

# 灰度图像：

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320290305-14dd3df2-c54e-493d-9283-cb5e1dad7a88.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320290305-14dd3df2-c54e-493d-9283-cb5e1dad7a88.png)

---

灰度图像是单通道图像，其中每个像素只携带有关光强度的信息。

# RGB图像

与灰度图像不同的是，RGB图像是三通道，每个像素是由三个通道组成的，每个通道代表一种颜色

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320290702-2bb1a530-1853-43ad-8678-397bdda87a73.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717320290702-2bb1a530-1853-43ad-8678-397bdda87a73.png)

---