# c++中的复数

1. 复数的乘法

// 这个算法的效率不高，时间较慢

void matrixMultiply(complex<double>* a, complex<double>* b, complex<double>*& c, int size)

{

for (int i = 0; i < size; i++)

{

c[i] = a[i] * b[i];

}

}

// 下面的复数的乘法效率很高，时间快一倍左右

void matrixMultiply(complex<double>* a, complex<double>* b, complex<double>*& c, int size)

{

for (int i = 0; i < size; i++)

{

c[i].real(a[i].real() * b[i].real() - a[i].imag() * b[i].imag());

c[i].imag(a[i].real() * b[i].imag() + a[i].imag() * b[i].real());

}

}

---

复数：有实部和虚部组成的一个节点

形如：z=a+bi(a,b均为实数)的数称为复数，其中，a称为实部，b称为虚部，i称为虚数单位

1. 在c++中需要包含的头文件：
2. 创建一个简单的复数

// 声明一个复数

complex<double> num;

// 给复数赋值

num = complex<double>(0,0);

// 也可以简单点写

num = (0,0);

---

1. 获取复数变量的实部和虚部

complex<double> num(1,0);

cout << "复数num的实部为：" << num.real() << endl;

cout << "复数num的虚部为：" << num.image() << endl;

---

1. 求共轭复数

共轭复数就是将复数的实部和虚部的正负号取反

complex<double> num(-1,0);

cout << "复数num的实部为：" << num.real() << endl;

cout << "复数num的虚部为：" << num.image() << endl;

conj(num);

cout << "复数num的实部为：" << num.real() << endl;

cout << "复数num的虚部为：" << num.image() << endl;

---

---

cout << "复数num的虚部为：" << num.image() << endl;

cout << "复数num的实部为：" << num.real() << endl;

conj(num);

cout << "复数num的虚部为：" << num.image() << endl;

cout << "复数num的实部为：" << num.real() << endl;

complex<double> num(-1,0);

共轭复数就是将复数的实部和虚部的正负号取反

1. 求共轭复数

---

cout << "复数num的虚部为：" << num.image() << endl;

cout << "复数num的实部为：" << num.real() << endl;

complex<double> num(1,0);

1. 获取复数变量的实部和虚部

---

num = (0,0);

// 也可以简单点写

num = complex<double>(0,0);

// 给复数赋值

complex<double> num;

// 声明一个复数

1. 创建一个简单的复数
2. 在c++中需要包含的头文件：

形如：z=a+bi(a,b均为实数)的数称为复数，其中，a称为实部，b称为虚部，i称为虚数单位

复数：有实部和虚部组成的一个节点

---

}

}

c[i].imag(a[i].real() * b[i].imag() + a[i].imag() * b[i].real());

c[i].real(a[i].real() * b[i].real() - a[i].imag() * b[i].imag());

{

for (int i = 0; i < size; i++)

{

void matrixMultiply(complex<double>* a, complex<double>* b, complex<double>*& c, int size)

// 下面的复数的乘法效率很高，时间快一倍左右

}

}

c[i] = a[i] * b[i];

{

for (int i = 0; i < size; i++)

{

void matrixMultiply(complex<double>* a, complex<double>* b, complex<double>*& c, int size)

// 这个算法的效率不高，时间较慢

1. 复数的乘法