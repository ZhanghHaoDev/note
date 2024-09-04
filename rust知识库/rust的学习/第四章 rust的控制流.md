# **1. if控制语句**
1. if 表达式允许根据条件执行不同的代码分支
2. 所有的 if 表达式都以 if 关键字开头，其后跟一个条件
3. 条件的结果必须是bool类型的值
```rust
let if_num = 5;
    if if_num > 10{
        println!("输入的数字大于10");
    }
```
`
# **2. if-else 控制语句语句**
1. 可以包含一个可选的 else 表达式来提供一个在条件为 false 时应当执行的代码块，这里我们就这么做了。如果不提供 else 表达式并且条件为 false 时，程序会直接忽略 if 代码块并继续执行下面的代码。
2. 在rust当中，也支持if-else的多层嵌套
```rust
fn main() {
    let number = 3;
    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```
``
# **3. loop循环**
1. loop 关键字告诉 Rust 一遍又一遍地执行一段代码直到你明确要求停止。
2. 我们可以使用关键字break，来停止循环
3. 也可以使用关键字continue来暂停这一次的循环，但是下一次循环继续
```rust
// 下面的代码会一直循环
fn main() {
    loop {
        println!("again!");
    }
}

// 使用关键break
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

``
# **4. while循环**
1. while循环结构消除了很多使用 loop、if、else 和 break 时所必须的嵌套，这样更加清晰。当条件为 true 就执行，否则退出循环
```rust 
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```
``
# **5. for循环**
1. 当我们循环数组元素的时候，我们可以获取数组元素的个数，这个时候推荐使用for循环
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```