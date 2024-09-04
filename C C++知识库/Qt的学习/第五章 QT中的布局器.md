# 第五章 QT中的布局器

1. qt当中布局器的分类

在 Qt 中，布局器是用来管理和组织窗口部件的位置和大小的。Qt 提供了几种不同的布局器，包括：

- QHBoxLayout：在水平方向上排列窗口部件。
- QVBoxLayout：在垂直方向上排列窗口部件。
- QGridLayout：在网格中排列窗口部件。
- QFormLayout：为表单创建两列布局。
1. QHBoxLayout：水平布局器

QHBoxLayout 是 Qt 中的一个布局管理类，它可以在水平方向上排列窗口部件。以下是一些常用的 QHBoxLayout 方法：

- addWidget(QWidget *widget, int stretch = 0, Qt::Alignment alignment = Qt::Alignment())：将一个部件添加到布局中。stretch 参数用于设置部件的拉伸因子，alignment 参数用于设置部件的对齐方式。
- addLayout(QLayout *layout, int stretch = 0)：将另一个布局添加到这个布局中。stretch 参数用于设置布局的拉伸因子。
- addStretch(int stretch = 0)：在布局的末尾添加一个弹性空间。stretch 参数用于设置弹性空间的拉伸因子。
- setSpacing(int spacing)：设置布局中部件之间的间距。
- setMargin(int margin)：设置布局的边距。

以下是一个使用 QHBoxLayout 的例子：

**代码**

---

#include <QApplication>

#include <QWidget>

#include <QPushButton>

#include <QHBoxLayout>

int main(int argc, char *argv[])

{

QApplication app(argc, argv);

QWidget window;

QPushButton *button1 = new QPushButton("Button 1");

QPushButton *button2 = new QPushButton("Button 2");

QHBoxLayout *layout = new QHBoxLayout;

layout->addWidget(button1);

layout->addWidget(button2);

layout->setSpacing(10);  // 设置部件之间的间距为 10 像素

layout->setMargin(5);  // 设置布局的边距为 5 像素

window.setLayout(layout);

window.show();

return app.exec();

}

---

1. QVBoxLayout：垂直布局器

QVBoxLayout 是 Qt 中的一个布局管理类，它可以在垂直方向上排列窗口部件。以下是一些常用的 QVBoxLayout 方法：

- addWidget(QWidget *widget, int stretch = 0, Qt::Alignment alignment = Qt::Alignment())：将一个部件添加到布局中。stretch 参数用于设置部件的拉伸因子，alignment 参数用于设置部件的对齐方式。
- addLayout(QLayout *layout, int stretch = 0)：将另一个布局添加到这个布局中。stretch 参数用于设置布局的拉伸因子。
- addStretch(int stretch = 0)：在布局的末尾添加一个弹性空间。stretch 参数用于设置弹性空间的拉伸因子。
- setSpacing(int spacing)：设置布局中部件之间的间距。
- setMargin(int margin)：设置布局的边距。

以下是一个使用 QVBoxLayout 的例子：

**代码**

---

#include <QApplication>

#include <QWidget>

#include <QPushButton>

#include <QVBoxLayout>

int main(int argc, char *argv[])

{

QApplication app(argc, argv);

QWidget window;

QPushButton *button1 = new QPushButton("Button 1");

QPushButton *button2 = new QPushButton("Button 2");

QVBoxLayout *layout = new QVBoxLayout;

layout->addWidget(button1);

layout->addWidget(button2);

layout->setSpacing(10);  // 设置部件之间的间距为 10 像素

layout->setMargin(5);  // 设置布局的边距为 5 像素

window.setLayout(layout);

window.show();

return app.exec();

}

---

1. QGridLayout：网格布局器

QGridLayout 是 Qt 中的一个布局管理类，它可以在网格中排列窗口部件。以下是一些常用的 QGridLayout 方法：

- addWidget(QWidget *widget, int row, int column, int rowSpan = 1, int columnSpan = 1, Qt::Alignment alignment = Qt::Alignment())：将一个部件添加到布局中的指定位置。row 和 column 参数用于指定部件的位置，rowSpan 和 columnSpan 参数用于指定部件跨越的行数和列数，alignment 参数用于设置部件的对齐方式。
- addLayout(QLayout *layout, int row, int column, int rowSpan = 1, int columnSpan = 1, Qt::Alignment alignment = Qt::Alignment())：将另一个布局添加到这个布局中的指定位置。参数的含义与 addWidget() 方法相同。
- setSpacing(int spacing)：设置布局中部件之间的间距。
- setMargin(int margin)：设置布局的边距。

例子：

**代码**

---

#include <QApplication>

#include <QWidget>

#include <QPushButton>

#include <QGridLayout>

int main(int argc, char *argv[])

{

QApplication app(argc, argv);

QWidget window;

QPushButton *button1 = new QPushButton("Button 1");

QPushButton *button2 = new QPushButton("Button 2");

QGridLayout *layout = new QGridLayout;

layout->addWidget(button1, 0, 0);  // 将 button1 添加到第 0 行第 0 列

layout->addWidget(button2, 0, 1);  // 将 button2 添加到第 0 行第 1 列

layout->setSpacing(10);  // 设置部件之间的间距为 10 像素

layout->setMargin(5);  // 设置布局的边距为 5 像素

window.setLayout(layout);

window.show();

return app.exec();

}

---

1. QFormLayout：表单布局器

QFormLayout 是 Qt 中的一个布局管理类，它为表单创建两列布局，通常用于标签-字段对的布局。以下是一些常用的 QFormLayout 方法：

- addRow(QString &label, QWidget *field)：添加一行到布局中，包含一个标签和一个字段部件。
- addRow(QWidget *label, QWidget *field)：添加一行到布局中，包含一个标签部件和一个字段部件。
- setSpacing(int spacing)：设置布局中部件之间的间距。
- setMargin(int margin)：设置布局的边距。

以下是一个使用 QFormLayout 的例子：

**代码**

---

#include <QApplication>

#include <QWidget>

#include <QLineEdit>

#include <QFormLayout>

int main(int argc, char *argv[])

{

QApplication app(argc, argv);

QWidget window;

QLineEdit *lineEdit1 = new QLineEdit();

QLineEdit *lineEdit2 = new QLineEdit();

QFormLayout *layout = new QFormLayout;

layout->addRow("First Name", lineEdit1);

layout->addRow("Last Name", lineEdit2);

layout->setSpacing(10);  // 设置部件之间的间距为 10 像素

layout->setMargin(5);  // 设置布局的边距为 5 像素

window.setLayout(layout);

window.show();

return app.exec();

}

---

1. QGridLayout（网格）和QFormLayout（表单）区别

QFormLayout 和 QGridLayout 都是 Qt 中的布局管理类，但它们的用途和行为有所不同。

- QFormLayout 是专门为表单设计的布局，它创建了两列布局，通常用于标签-字段对的布局。在 QFormLayout 中，左列通常包含字段的标签，右列包含字段的输入部件。QFormLayout 会自动处理标签和字段之间的对齐和间距，使得表单看起来整齐和一致。
- QGridLayout 则是一个更通用的布局，它可以在网格中排列窗口部件。你可以指定部件的行和列，以及部件跨越的行数和列数。QGridLayout 提供了更大的灵活性，可以用来创建各种复杂的用户界面。

总的来说，如果你需要创建一个表单，QFormLayout 可能是最好的选择。如果你需要创建一个更复杂的用户界面，QGridLayout 可能更适合。