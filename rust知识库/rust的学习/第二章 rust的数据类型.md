# 1. 变量与不可变性

1. 在rust语言当中，我们使用let来声明变量
2. rust语言当中，变量的值是不可以修改的，
3. 对于需要修改值的变量，我们需要添加关键字mut
4. 在rust语言当中，rust语言支持类型推导，当然也可以显式的指定变量的类型
5. rust语言当中，对于变量的命名我们使用蛇形变量命名方法，单词全部是小写，使用下划线链接
6. 强制类型转换使用as
7. 打印变量使用 {} {:?}

```bash
// 在rust语言当中，我们使用let来声明变量
// rust语言当中，变量是不可修改的

fn main() {
    // 3.1 变量与不可变性
    let x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");

}
```

# 2. const和static

## 2.1. const

1. 常量的值必须是在编译时已知的常量表达式必须指定类型与值，意思是声明的时候必须指定类型
2. 与c语言的宏定义（宏替换）不同，rust的const常量的值被直接嵌入到生成的底层机器代码中，而不是进行简单的字符替换
3. 常量与静态变量的命名必须全部是大写字母，单词之间使用下划线分割
4. 常量的作用域是块级作用域，他们只在声明他们的作用域内可见
5. 常量不能使用mut关键字

## 2.2. static

1. 与const不同，static变量是在运行时分配内存的
2. 并不是不可变的，可以使用unsafe修改
3. 静态变量的生命周期为整个程序的生命周期

# 3. rust当中常用的数据类型

rust语言是静态类型的语言，也就是表示在编译的时候，叫必须知道变量的类型

## 3.1. 基础数据类型

1. 有符号整形，默认为i32类型

i8,i16,i32,i64

1. 无符号整形

u8,u16,u32,u64

1. 整数类型，由平台决定

usize，isize

usize 和 isize 主要用于处理与内存大小和对象数量相关的场景，它们的大小可以动态地适应不同的机器架构。

1. 浮点类型

f32，f64

1. bool类型

true，false

1. char类型，字符类型

rust支持unicode字符，表示char使用单引号

# 3.2. 数值运算

rust语言支持基本的数学运算，包括：加法，减法，乘法，除法，取余运算

# 4. 元组和数组

相同点

1. 元组和数组都是复合类型，而vec和map都是集合类型
2. 元组和数组的长度的固定的

复合类型：多个相同的类型的值组合在一块

集合类型：多个不同类型的值集合在一块

元组和数组的值是可以修改的，需要添加mut关键字，但是需要注意的是，只能修改值，不能修改类型

## 4.1. 数组

数组是固定长度的同构集合

创建方式

[a,b,c]，[value;size]

1. 获取数组元素，arr[index]
2. 获取数组长度，arr.len()

## 4.2. 元组

元组是固定长度的异构的集合，意思是元组允许不同类型的变量存在一个集合当中，类似结构体

# 5. 所有权

基础数据类型与数组，元组他们和string数据类型的不同

基础的数据类型，rust默认是copy操作，但是对于string和struct，以及一些复杂的数据类型，默认是move操作

# 6. code

```rust
fn main() {
    // 3.1 变量与不可变性
    let x = 5;
    println!("The value of x is: {x}");
    // x = 6;
    // println!("The value of x is: {x}");

    // mut 关键字
    let mut y = 5;
    println!("The value of y is: {y}");
    y = 6;
    println!("The value of y is: {y}");

    // 常量
    const MAX_POINTS: u32 = 100_000;
    println!("The value of MAX_POINTS is: {MAX_POINTS}");

    // 3.2 数据类型
    // 整型
    let a = 5;
    let b: u32 = 5;
    let c: i32 = -5;
    println!("The value of a is: {a}");
    println!("The value of b is: {b}");
    println!("The value of c is: {c}");

    // 浮点型
    let d = 2.0;
    let e: f32 = 3.0;
    println!("The value of d is: {d}");
    println!("The value of e is: {e}");

    // 布尔型
    let f = true;
    let g: bool = false;
    println!("The value of f is: {f}");
    println!("The value of g is: {g}");

    // 字符型
    let h = 'h';
    let i: char = 'i';
    println!("The value of h is: {h}");
    println!("The value of i is: {i}");

    // 数值运算
    let sum = 5 + 10;
    let difference = 95.5 - 4.3;
    let product = 4 * 30;
    let quotient = 56.7 / 32.2;
    let remainder = 43 % 5;
    println!("The value of sum is: {sum}");
    println!("The value of difference is: {difference}");
    println!("The value of product is: {product}");
    println!("The value of quotient is: {quotient}");
    println!("The value of remainder is: {remainder}");
}

```