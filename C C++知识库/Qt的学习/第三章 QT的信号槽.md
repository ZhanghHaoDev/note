# 第三章 QT的信号槽

1. 什么是信号槽

信号

首先我们了解什么是事件和信号

我们这里使用QPushButton的单击事件为例子：

我们按下按钮的时候，会触发mousePressEvent事件，然后QPushButton会发射prssed()信号；

松下按钮，会触发mouseReleaseEvent事件，然后QPushButton会发射released()信号和clicked()信号

常用的事件有很多，比如鼠标的单击和双击事件，鼠标的移动事件，键盘的输入事件

当某个实例化的对象上产生这些事件的时候，该实例化对象就会发出特定的信号

信号的本质就是函数，并且只需要声明，无需实现该函数

QT中常用的信号

//当按钮被点击（按下并抬起）之后，发送该信号，其中带有一个默认参数

//对于QPushButton 通常不需要传递这个默认参数

//对于可选中/取消选中的按钮，比如复选框QCheckBox、单选框QRadioButton 可以通过该参数，获取其是否选中

voidclicked(bool checked = false);

//当按钮被按下时，发送该信号

voidpressed();

//当按钮被抬起时，发送该信号

voidreleased();

//当按钮状态改变时，发送该信号，其中带有一个参数checked

//checked 用于标识复选框QCheckBox、单选框QRadioButton是否被选中

voidtoggled(bool checked);

---

槽

QT中的槽就是槽函数

当我们点击了QPushButton按钮的之后，通常需要执行对应的操作，比如让QMainWindow窗口最大/最小/正常/关闭窗口。

QT中常用的槽函数

//最大化显示

voidshowMaximized();

//最小化显示

voidshowMinimized();

//正常显示

voidshowNormal();

//关闭窗口

boolclose();

---

connect函数详解

connect函数的作用，这里主要用于将信号和槽函数进行连接，比如将QPushButton按钮和QMainWindow窗口的close函数进行连接，当我们点击QPushButton按钮后，QT框架会自动调用QMainWindow窗口的close槽函数，从而实现窗口的关闭。

connect()函数的一般形式如下：

connect(sender, signal, receiver, slot);

其中：

sender：发出信号的对象，比如QPushButton按钮

signal：发出的信号，比如clicked()

receiver：接收信号的对象，比如QMainWindow窗口

slot：接收到信号之后，所调用的函数

一句话总结：信号槽是对象之间的信息通讯的方式

1. 自定义信号槽

自定义的信号和槽需要满足的条件

1. 自定义的类，需要继承QObject
2. 自定义的类，其中要声明一个宏Q_OBJECT

只有满足这两个条件才可以正常使用信号槽机制（当然，槽函数是全局函数，Lambda表达式等无需接收者的时候除外）

1. 信号槽总结
2. 使用信号和槽点条件

如果想要使用信号和槽，需要满足下面的条件

- 自定义的类，要继承QObject
- 自定义的类，其中要声明一个宏Q_OBJECT

只有满足这两个条件的时候，我们才可以正常使用信号槽机制

1. 信号
- 无需实现，信号的本质是函数，并且只需要声明，不需要实现；
- 可以重载，信号的本质的函数，因此可以重载
- 信号声明在类头文件的signals作用域下
- 信号返回值类型为void，参数的类型和个数不限
- 信号可以使用emit关键字，也可以不使用
1. 槽
- 需要实现，槽的本质是函数，需要实现
- 可以重载，槽本质的函数，因此可以重载
- 槽函数用slots关键字修饰
- 返回值，槽函数的返回值，要和信号一直，由于信号的返回值为void，因此槽函数的返回值也是void
- 参数，槽函数的参数个数要《=信号的参数个数
1. 信号槽-多种链接方式

信号和槽要建立链接，本质上说通过connect函数来实现的。但是具体操作上有很多的方式

1. signal/SLQT（qt4）
2. 函数地址（qt5）
3. UI设计师界面-转到槽
4. UI设计师界面-信号槽编辑器
5. lambda表达式

这里只做第一种和第二种方式

connect函数，具体的函数原型如下：

connect(sender, SIGNAL(signal()), receiver, SLOT(slot()));

---

- sender：信号发送者
- Signal(Signal()); 发送的信号，Signal宏将信号转换成字符串
- receiver：信号接收者
- SLOT(slot())：槽函数。SLOT红将槽函数转换为字符串

这种方式，编译器不会做错误检查，即使函数名或者参数写错了，也可以编译通过，这样我们就把问题留在了运行阶段。因此这种方式不被推荐

这里一个小案例：将窗口最大化

MainWindow::MainWindow(QWidget *parent)

: QMainWindow(parent)

, ui(new Ui::MainWindow)

{

ui->setupUi(this);

// 1.使用 SIGNAL/SLOT 的方式连接信号和槽

connect(ui->btnMax, SIGNAL(clicked()), this, SLOT(showMaximized()));

}

---

第二种方式：函数地址

这种方式中，信号和槽使用函数地址

connect(sender, &Sender::signal, receiver, &Receiver::slot);

---

- sender：信号发送者
- &Sender::Signal ：发送的信号
- receiver：信号的接收者
- &Receiver::slot：槽函数

我们使用这种方式，编译就会对函数类型，参数个数进行检查

案例：实现点击按钮，实现窗口的正常化

MainWindow::MainWindow(QWidget *parent)

: QMainWindow(parent)

, ui(new Ui::MainWindow)

{

ui->setupUi(this);

// 1.使用 SIGNAL/SLOT 的方式连接信号和槽

connect(ui->btnMax, SIGNAL(clicked()), this, SLOT(showMaximized()));

// 2.使用函数地址的方式连接信号和槽

connect(ui->btnNormal, &QPushButton::clicked, this, &QMainWindow::showNormal);

}

---

1. 如何连接重载的信号和槽

在信号和槽存在重载的时候，qt4和qt5的写法是有区别的

qt4：可以在SIGNAL / SLOT中指定函数参数类型，因此写法比较简单

qt5：指定信号和槽时，只能指定函数名，无法向qt4那样指定函数参数类型，需要单独定义函数指针，写法上比较麻烦。

//1、Qt4信号槽的连接：SIGNAL/SLOT

#if 0

Commander commander;

Soldier soldier;

connect(&commander, SIGNAL(go()),&soldier, SLOT(fight()));

connect(&commander,SIGNAL(go(QString)), &soldier, SLOT(fight(QString)));

emit commander.go();

emit commander.go("freedom");

#endif

// 2、Qt5信号槽的连接：函数地址

#if 0

Commander commander;

Soldier soldier;

// 没有同名的信号和槽时，可以直接这样写。因为不存在二义性

// connect(&commander,&Commander::go, &soldier, &Soldier::fight);

// 有同名的信号和槽时，需要向下面这样定义函数指针。因为存在二义性

// 编译器自动推断：将无参的信号go和无参的槽，赋值给函数指针（ctrl+鼠标点击可以智能跳转过去）

void (Commander::*pGo)() =&Commander::go;

void (Soldier::*pFight)() =&Soldier::fight;

connect(&commander, pGo,&soldier, pFight);

// 编译器自动推断：将有参的信号go和有参的槽，赋值给函数指针（ctrl+鼠标点击可以智能跳转过去）

void(Commander::*pGoForFreedom)(QString) = &Commander::go;

void(Soldier::*pFightForFreedom)(QString) = &Soldier::fight;

connect(&commander, pGoForFreedom,&soldier, pFightForFreedom);

emit commander.go();

emit commander.go("freedom");

#endif

---

# 

1. 一个信号连接多个槽

一个信号可以连接多个槽，如下所示：

connect(sender, SIGNAL(signal), receiver1, SLOT(fun1()));

connect(sender, SIGNAL(signal), receiver2, SLOT(fun2()));

---

这里需要注意的是：当信号发送的时候，连接的两个槽函数都会被执行，并且：

qt4：信号发送时，与之相连的槽函数的执行顺序是随机的

qt5：信号发送时，这些槽函数的执行顺序与建立连接的顺序相同

1. 多个信号连接一个槽函数

我们可以将多个信号连接到同一个槽韩素，比如：

connect(sender, SIGNAL(signal1), receiver, SLOT(fun()));

connect(sender, SIGNAL(signal2), receiver, SLOT(fun()));

---

当我们执行signal1和aignal2的时候，都会执行fun函数

1. 信号连接信号

信号不仅仅可以连接槽函数，也可以连接信号，具体写法：

connect(obj1, SIGNAL(signal1), obj2, SIGNAL(signal2));

---

当obj1发送信号signal1的时候，就会触发obj2发送signal2的信号

# 案例1：

这里创建一个项目，放置四个按钮，每个按钮的作用是：1. 当前窗口最大化，2. 当前床最小化，3. 当前窗口正常显示，4. 当前窗口关闭

步骤1：创建qt项目

步骤2：打开ui文件，放置四个按钮，注意这里的按钮名称和按钮name是不一样的

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044914-de567c8a-9490-4644-8da5-391394c91e0e.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044914-de567c8a-9490-4644-8da5-391394c91e0e.png)

步骤3：打开mainwindow.cpp文件，输入下面的代码

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319045172-de7dbb88-9426-41ad-bf26-db1eb3c51ab3.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319045172-de7dbb88-9426-41ad-bf26-db1eb3c51ab3.png)

具体代码：

//连接信号和槽

connect(ui->btnMax,SIGNAL(clicked()), this, SLOT(showMaximized()));

connect(ui->btnNormal,SIGNAL(clicked()), this, SLOT(showNormal()));

connect(ui->btnMin,SIGNAL(clicked()), this, SLOT(showMinimized()));

connect(ui->btnClose,SIGNAL(clicked()), this, SLOT(close()));

---

# 案例2：

创建一个自定义的槽函数和信号

步骤1:创建新的qt项目

步骤2:创建新的Commander类

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044884-d05e4efc-477d-4300-8e10-df0a5482cef7.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044884-d05e4efc-477d-4300-8e10-df0a5482cef7.png)

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044901-57588d80-8a3e-4b31-8b8b-a3f32cfc547c.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044901-57588d80-8a3e-4b31-8b8b-a3f32cfc547c.png)

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044916-4d443c52-02f6-4a07-b918-fca05da8ca57.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319044916-4d443c52-02f6-4a07-b918-fca05da8ca57.png)

步骤3:添加自定义信号

classCommander : public QObject

{

Q_OBJECT

public:

explicit Commander(QObject *parent =nullptr);

signals:

// 1.信号只需声明，无需实现

// 2.信号返回值为 void

void go();

};

---

步骤4:添加Soldier类，在该类当中实现fight函数

classSoldier : public QObject

{

Q_OBJECT

public:

explicit Soldier(QObject *parent =nullptr);

signals:

// 1.通常将槽函数添加到 slots 后面

// 这个 slots 也可以不写。不过建议写上，以指明这是一个槽函数

// pulic，表示槽函数既可以在当前类及其子类的成员函数中调用，也可以在类外部的其它函数（比如 main() 函数）中调用

public slots:

// 2.槽函数的返回值和参数，要和信号保持一致

// 由于信号无返回值，因此槽函数也无返回值

// 由于信号无参数，因此槽函数也无参数

void fight();

};

---

步骤5:实现该函数

void Soldier::fight()

{

qDebug() << "fight";

}

---

步骤6:链接信号和槽函数

在 mainwindow.cpp 中，定义 Commander 和 Soldier 类的实例，并建立信号和槽的连接，如下：

MainWindow::MainWindow(QWidget*parent)

: QMainWindow(parent)

, ui(new Ui::MainWindow)

{

ui->setupUi(this);

// 1. 创建两个类的实例

Commander commander;

Soldier soldier;

// 2. 建立信号和槽的连接

connect(&commander, SIGNAL(go()),&soldier, SLOT(fight()));

// 3. 发送信号

// emit 可省略

/*emit*/commander.go();

}

---

这样就可以构建，编译该项目，显示输出：

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319056004-b8302ace-dd34-43fb-9339-94af289c8be4.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717319056004-b8302ace-dd34-43fb-9339-94af289c8be4.png)