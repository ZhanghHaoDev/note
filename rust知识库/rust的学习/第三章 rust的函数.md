# 1. 函数

在rust语言当中，我们与其他语言一样使用main函数作为函数的入口

rust语言当中，使用fn关键字来作为函数的声明

```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```

1. rust中的使用fn关键字来声明函数
2. 函数的命名使用小写单词和下划线链接
3. 我们在 Rust 中通过输入 fn 后面跟着函数名和一对圆括号来定义函数。大括号告诉编译器哪里是函数体的开始和结尾。

# 2. 参数

1. 在rust语言当中，函数头的圆括号内，我们可以添加参数
2. 参数的形式为：名字：类型

```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {x}");
}
```

# 3. 函数的返回值

1. 在rust语言当中，默认是将函数的最后一个值作为函数的返回值
2. 当然也可以使用return关键字，提前返回函数的返回值
3. 我们并不对函数的返回值做声明，但是需要指定函数返回值的类型，使用->指定类型

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```