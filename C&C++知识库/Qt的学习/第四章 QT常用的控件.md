# 第四章 QT常用的控件

# QWidget

1. 窗口的基类：qwidget

qt当中有三个窗口的基类：qwidget,qmainwindows,qdialog

我们在创建qt过程的时候，会让我们选择项目继承那个窗口类

qmainwindow, qdialog其实都是基于qwidget类

1. 所有的空间的基类

qt中的控件类（按钮，输入框，单选框等）也属于窗口类，他们的基类也是qwidegt

可以内嵌到其他的窗口的内部，此时需要给其指定父窗口

可以作为独立的窗口显示，此时不能给其指定父窗口

1. 常用的属性和方法

窗口位置

// 1、设置窗体的几何信息

// 获取相对于当前窗口父窗口的几何信息：宽高、坐标点信息

const QRect &geometry() const;

void setGeometry(int x, int y, int w, int h);

void setGeometry(const QRect &);

// 2、移动窗口。

// 重新设置窗口的位置

void move(int x, int y);

void move(const QPoint &);

---

窗口大小

// 1、设置窗口尺寸

QSize size() const

void resize(int w, int h);

void resize(const QSize &);

// 2、设置最大尺寸

QSize maximumSize() const;

void setMaximumSize(const QSize &);

void setMaximumSize(int maxw, int maxh);

// 3、设置最小尺寸

QSize minimumSize() const;

void setMinimumSize(const QSize &);

void setMinimumSize(int minw, int minh);

// 4、设置固定尺寸

void QWidget::setFixedSize(const QSize &s);

void QWidget::setFixedSize(int w, int h);

// 5、单独设置窗口的高度

int height() const;

int minimumHeight() const;

int maximumHeight() const;

void setFixedHeight(int h);

void setMaximumHeight(int maxh);

void setMinimumHeight(int minh);

// 6、单独设置窗口的宽度

int width() const;

int minimumWidth() const;

int maximumWidth() const;

void setFixedWidth(int w);

void setMaximumWidth(int maxw);

void setMinimumWidth(int minw);

---

窗口标题，图标

// 获取和设置窗口的标题

QString windowTitle() const;

void setWindowTitle(const QString &);

// 获取和设置窗口的图标

QIcon windowIcon() const;

void setWindowIcon(const QIcon &icon);

// 构造 QIcon 图标对象

// 有 6 个重载的构造方法，通常我们使用最后一个

// 参数为图标文件的路径

QIcon::QIcon(const QString &fileName);

---

# QPushButton

qt当中常用的按钮控件

1. 设置显示的文本

**代码**

---

#include <QPushButton>

// 创建一个 QPushButton 对象

QPushButton *button = new QPushButton();

// 使用 setText() 方法设置按钮的文本

button->setText("Click me");

---

1. 设置显示的图标

**代码**

---

#include <QPushButton>

#include <QIcon>

// 创建一个 QPushButton 对象

QPushButton *button = new QPushButton();

// 创建一个 QIcon 对象

QIcon icon("path/to/your/icon.png");

// 使用 setIcon() 方法设置按钮的图标

button->setIcon(icon);

---

1. 设置样式表

样式表可以设置包括文本颜色、背景色、边框、字体等很多样式

**代码**

---

// 获取和设置样式表

// 这是继承自QWidget类的属性和方法

// 只要继承自QWidget类的控件，都有该属性

QString styleSheet() const

void setStyleSheet(const QString &styleSheet)

---

1. 设置信号

设置按钮在按下按钮的时候，发送信号

**代码**

---

// 当按钮被点击（按下并抬起）时，发送该信号，其中带有一个默认参数

// 对于QPushButton 通常不需要传递这个默认参数

// 对于可选中/取消选中的按钮，比如复选框QCheckBox、单选框QRadioButton 可以通过该参数，获取其是否选中

void clicked(bool checked = false);

// 当按钮被按下时，发送该信号

void pressed();

// 当按钮被抬起时，发送该信号

void released();

---

QLabel

QLabel是qt当中的标签类，用于显示提示的文本，也可以用于显示图像

1. 设置文本和获取文本

**代码**

---

#include <QLabel>

// 创建一个 QLabel 对象

QLabel *label = new QLabel();

// 使用 setText() 方法设置标签的文本

label->setText("Hello, World!");

// 使用 text() 方法获取标签的文本

QString labelText = label->text();

---

1. 设置对齐的方式

用于设置标签中的内容在水平和垂直两个方向上的对齐方式，比如左对齐，右对齐，居中等

**代码**

---

// 获取和设置文本的对齐方式

Qt::Alignment alignment() const;

void setAlignment(Qt::Alignment);

---

- Qt::AlignLeft（0x0001） 水平方向-左对齐
- Qt::AlignRight（0x0002） 水平方向-右对齐
- Qt::AlignHCenter（0x0004） 水平方向-居中对齐
- Qt::AlignTop（0x0020）垂直方向-上对齐
- Qt::AlignBottom（0x0040）垂直方向-下对齐
- Qt::AlignVCenter（0x0080）垂直方向-居中对齐
- Qt::AlignCenter（AlignVCenter | AlignHCenter） 垂直方向和水平方向-居中对齐
1. 设置换行

**代码**

---

// 获取和设置文本是否允许换行

// 换行时：在 word-breaks处，不会将一个完整的单词显示在两行

bool wordWrap() const; // 判断是否允许换行

void setWordWrap(bool on); // 设置是否允许换行

---

1. 设置想要显示的图像

**代码**

---

// 获取和设置显示的图像

const QPixmap *pixmap() const;

void setPixmap(const QPixmap &pixmap);

---

# QLineEdit

QlineEdit是qt当中的文本框，单行的文本框，接收用户输入

1. 设置占位符

设置占位符就是当文本框中输入内容为空的时候，需要显示的字符，用于提示用户文本框中应该输入什么内容

**代码**

---

// 获取和设置占位字符串

QString placeholderText() const

void setPlaceholderText(const QString &)

---

1. 设置对齐方式

设置左对齐，右对齐，居中等

**代码**

---

// 获取和设置文本的对齐方式

Qt::Alignment alignment() const

void setAlignment(Qt::Alignment flag)

---

- Qt::AlignLeft（0x0001） 水平方向-左对齐
- Qt::AlignRight（0x0002） 水平方向-右对齐
- Qt::AlignHCenter（0x0004） 水平方向-居中对齐
- Qt::AlignTop（0x0020）垂直方向-上对齐
- Qt::AlignBottom（0x0040）垂直方向-下对齐
- Qt::AlignVCenter（0x0080）垂直方向-居中对齐
- Qt::AlignCenter（AlignVCenter | AlignHCenter） 垂直方向和水平方向-居中对齐
1. 设置回显模式

所谓的回显模式，就是输入的内容如何的显示

**代码**

---

// 获取和设置回显模式

QLineEdit::EchoMode echoMode() const

void setEchoMode(QLineEdit::EchoMode)

---

有四个取值

- QLineEdit::Normal

正常模式。输入什么就显示什么，默认就是这种方式

- QLineEdit::Password

密码模式。不显示实际输入的字符，而是以小圆圈代替，这样别人就无法看到输入的字符。

Do not display anything. This may be appropriate for passwords where even the length of the password should be kept secret.

- QLineEdit::NoEcho

无回显模式。无论输入什么内容，在文本框中都不会显示，这样别人既无法看到输入的内容，也无法知道输入字符的长度

这对于输入密码非常有用，在linux下输入密码时，就是这种模式

- QLineEdit::PasswordEchoOnEdit

正在输入时显示正常模式显示，当失去焦点时以密码模式显示，也就是显示小圆圈

1. 设置读写控制

设置文本框是否可编辑

**代码**

---

// 获取和设置文本框的只读属性

bool isReadOnly() const

void setReadOnly(bool)

// 获取和设置文本框的是否使能

bool isEnabled() const

void setEnabled(bool)

---

1. 格式控制

用于指定文本框输入特定格式的内容，比如电话号码等

**代码**

---

// 设置和获取格式控制

QString inputMask() const

void setInputMask(const QString &inputMask)

---

QRadioButton

qt当中的单选按钮

1. 设置文本

**代码**

---

// 获取和设置显示的文本

QString text() const

void setText(const QString &text)

---

1. 设置选中状态

**代码**

---

// 获取和设置单选按钮的选中状态

bool isChecked() const

void setChecked(bool)

---

1. 自动排他

单选的按钮是多选一，设置属性为true则是单选

**代码**

---

// 获取和设置自动排他

bool autoExclusive() const

void setAutoExclusive(bool)

---

1. 信号槽

**代码**

---

// 单选按钮 QRadioButton 被点击时，会发出该信号

void clicked();

// 当单选按钮的选中状态发生改变时，会发射该信号

// 所谓状态改变，是指选中变为非选中，和非选中变为选中

void toggled(bool checked)

---

# QRadioButton

qt当中的复选按钮

1. 设置文本

**代码**

---

// 获取和设置显示的文本

QString text() const

void setText(const QString &text)

---

1. 设置三态

选中，非选中，半选中

**代码**

---

// 用于获取和设置是否支持三态

bool isTristate() const

void setTristate(bool y = true)

// 获取和设置复选按钮是否选中：checked/unchecked

bool isChecked() const

void setChecked(bool)

// 设置和获取复选按钮的状态

Qt::CheckState checkState() const

void setCheckState(Qt::CheckState state)

---

1. 自动排他

**代码**

---

// 获取和设置自动排他

bool autoExclusive() const

void setAutoExclusive(bool)

---