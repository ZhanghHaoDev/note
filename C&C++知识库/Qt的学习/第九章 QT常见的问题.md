# 第九章 QT常见的问题

1. 读取中文路径报错

原因有可能是：Windows（中文版）的系统编码是GBK的，但是c++std::string 只能识别ASCII和UTF8的编码，所以这个问题只出现在Windows上Linux上没有问题

1. 解决的办法是：先将输入转换为wstring（宽字符），显示正常以后，再将wstring转换为

string，就可以正常了

1. 可以使用QString类型，转换为string类型就可以

**代码**

---

#include <QTextStream>

#include <QApplication>

#include <QString>

#include <windows.h>

int main(int argc, char *argv[]) {

QApplication app(argc, argv);

SetConsoleOutputCP(CP_UTF8);

QTextStream out(stdout);

out << QString("中文路径") << Qt::endl;

return app.exec();

}

---

**代码**

---

#include <iostream>

#include <string>

#include <windows.h>

#include <qstring>

#include <qdebug>

int main() {

SetConsoleOutputCP(CP_UTF8);

std::u8string str = u8"中文路径";

std::cout << reinterpret_cast<const char*>(str.c_str()) << std::endl;

QString file_name = "中文路径";

std::cout << file_name.toStdString() << std::endl;

std::string file_name_str = file_name.toStdString();

std::cout << file_name_str << std::endl;

return 0;

}

---