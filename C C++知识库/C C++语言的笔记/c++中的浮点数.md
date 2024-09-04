# c++中的浮点数

1. 在c++中使用浮点数来表示小数，float-单精度，double-双精度

在计算机中表示一个小数，比如3.14，它在计算机中是使用3.13999999这样的形式来表示的，这样表示并不影响打印输出，以及计算

1. 在c++中输出打印一般是小数点后六位小数，但如果需要打印更多的位数需要使用函数setprecision()

#include <fstream> // 需要包含的头文件

double num = 9.33333566;

cout << setprecision(3) << num<< endl;

---

# 将数组的值写入文件，提高数据精度

#include <iomanip> // 包含头文件

// 将ft写入到文件中，精确到小数点后10位

ofstream outfile;

outfile.open("D:\\fft.txt", ios::app);

for (int j = 0; j < ft.size(); j++)

{

for (int k = 0; k < ft[0].size(); k++)

{

outfile << setprecision(9) <<"("<< ft[j][k].real() << "+" << setprecision(9) << ft[j][k].imag()<<"j)" << endl;;

}

outfile << endl;

}

outfile.close();

---