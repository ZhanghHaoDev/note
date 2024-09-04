# c++中的结构体

# 1. 结构体的定义

结构体（struct）是由一系列具有相同或不同类型的数据构成的数据集合。

结构体是将不同的数据存放在一块，作为一个整体进行处理。

结构体在函数中的作用不是便捷，最主要的作用是封装，封装的好处就是可以再次利用，使用者不需要关心这个是什么，只需要根据定义使用即可

# 2. 结构体声明

// 声明一个结构体

struct book

{

int stu;

int age;

};

---

1. 使用关键字struct来声明结构体
2. 结构体的结尾是需要添加 ; 分号的，表明这是一条语句
3. 声明并不是创建了一个实际的对象，而是描述了一个组成这类对象的元素
4. book是一个标识，我们可以通过这个标识来创建数据对象

# 2.1 结构体的位置

声明结构体的位置表明了这个结构体的作用域

1. 放到类外边，表明整个类都可以使用
2. 放到类里面表明只能类成员使用
3. 放到函数里面，只能在函数内部使用

# 2.2 定义的三种格式

1. 最标准的格式

#include <stdio.h>

struct student //结构体类型的说明与定义分开。声明

{

int age;  /*年龄*/

float score; /*分数*/

char sex;   /*性别*/

};

int main ()

{

struct student a={ 20,79,'f'}; //定义

printf("年龄：%d 分数：%.2f 性别：%c\n", a.age, a.score, a.sex );

return 0;

}

---

1. 不环保的方式

#include <stdio.h>

struct student /*声明时直接定义*/

{

int age;  /*年龄*/

float score;  /*分数*/

char sex;   /*性别*/

/*这种方式不环保，只能用一次*/

} a={21,80,'n'};

int main ()

{

printf("年龄：%d 分数：%.2f 性别：%c\n", a.age, a.score, a.sex );

}

---

1. 最奈何的方式

#include <stdio.h>

struct   //直接定义结构体变量，没有结构体类型名。这种方式最烂

{

int age;

float score;

char sex;

} t={21,79,'f'};

int main ()

{

printf("年龄：%d 分数：%f 性别：%c\n", t.age, t.score, t.sex);

return 0;

}

---

1. 定义的时候加不加struct关键字

在c语言中定义结构体的时候，必须加上struct关键字，但是在c++中不是强制要求添加关键字struct

struct stu

{

int age;

string name;

int xuehao;

};

// c语言中定义结构体，必须添加struct关键字

struct stu stu1;

// 在c++中不是强制要求添加关键字struct

stu stu1;

---

# 3. c++ 中的结构体

struct和class的区别：

struct默认是private，而class默认是public

struct和class只有上面的区别，没有其他的区别

# 4. 结构体与指针

1. 如何传递结构体指针第i维

存在以下结构体

struct eve_eva_ptr

{

double **eve_data;

double ***eva_data;

};

struct eve_eva_data

{

double *eve_data

double **eva_data;

};

// 函数声明为

void fun(eve_eva_data ev_ptr);

// 在循环中调用fun()函数，这样是可以的，直接将地址赋值

for(int i = 0;i = 10;i++)

{

eve_eva_data ev_ptr;

ev_ptr.eve_data = eve_eva_ptr.eve_data[i];

ev_ptr.eva_data = eve_eva_ptr.eva_data[i];

fun(ev_ptr);

}

// 这样调取比较麻烦，能不能省略掉赋值的部分，直接使用eve_eva_ptr

// 这样写是错误的，能不能有这样的思路

// 这样写是错误的，因为如果是用户自定义数据结构，对于编译器来讲是完全不同的东西

for(int i = 0;i = 10;i++)

{

fun(eve_eva_ptr[i]);

}

---

1. xyz结构体

现有以下结构体，如何传递值

struct xyz_data

{

double x;

double y;

double z;

};

---

新建一个该结构体的指针

xyz_data * temp;

---

如何循环给该值赋值，以及传递该指针的值

该结构体指针就相当于一个三层的表格，第一层存储着x的所有的值，第二层存储着y的所有值，第三层存储着z的所有值，

利用for循环就可以给该结构体赋值和取值

// 给结构体赋值

// 首先申请空间

temp = new xyz_data[100];

for(int i = 0 ; i < 100 ;i++)

{

temp[i].x = 1;

temp[i].y = 1;

temp[i].z = 1;

}

// 取结构体的值

for(int i = 0; i <100;i++)

{

a = temp[i].x;

cout << a << endl;

b = temp[i].y;

cout << b << endl;

c = temp[i].z;

cout << c << endl;

}

---

# 5. 类中的结构体

struct和class的区别是：

struct是访问权限是public，而class的默认访问权限是privect

而且在strcut中只允许定义成员变量，不允许定义成员函数

在c语言中，定义结构体是这样的

struct stu

{

char* name;

int age;

};

main()

{

stu a_stu;

a_sty.name = 's';

a_stu.age = 15;

}

---

在c++语言class中定义struct是这样的

class sutdent

{

private:

struct std // 结构体定义

{

string name;

int age;

};

public:

student();

std my_stu;

student_age();

}

int main()

{

// 允许通过class的public成员访问结构体

student a_stu;

a_stu.my_stu.name = "zzz";

a_stu.my_stu.age = 15;

cout << a_stu.my.name << endl;

// 不允许直接访问class的private成员数据

a_stu::std a;

a.age = 16;

cout << a.age << endl

return 0

}

---