rust语言当中，所有权的概念是独有的，对语言的其他部分也有深刻的理解

# 1. 什么是所有权

所有程序都必须管理其运行时使用计算机内存的方式。一些语言中具有垃圾回收机制，在程序运行时有规律地寻找不再使用的内存；在另一些语言中，程序员必须亲自分配和释放内存。Rust 则选择了第三种方式：通过所有权系统管理内存，编译器在编译时会根据一系列的规则进行检查。如果违反了任何这些规则，程序都不能编译。在运行时，所有权系统的任何功能都不会减慢程序。

## 1.1. 所有权的规则

1. Rust 中的每一个值都有一个 所有者（owner）。
2. 值在任一时刻有且只有一个所有者。
3. 当所有者（变量）离开作用域，这个值将被丢弃。

# 2. string 类型

我们经常使用的输出语句当中的字符串在rust语言当中属于字符串字面量，这个是不可变的。如果我们需要可以修改的字符串，需要使用到string类型的字符串。

我们使用from函数来创建字符串

```rust
let s = String::from("hello");
```

这两个冒号 :: 是运算符，允许将特定的 from 函数置于 String 类型的命名空间（namespace）下

## 2.1. 修改字符串的值

1. 首先变量的声明，需要添加关键字，mut
2. 如果需要给字符串向后添加字符串，我们可以使用string的函数push_str()

```rust
let mut s = String::from("hello");
s.push_str(", world!"); // push_str() 在字符串后追加字面值
println!("{}", s); // 将打印 `hello, world!`
```

# 3. 变量与数据交互

## 3.1. 变量与数据交互的方式：移动

我们首先来看一个基本类型的例子

```rust
let x = 5;
let y = x;
```

对于上面的例子，将x的值赋值给y，在rust当中基本类型的话是复制（拷贝），x的值并没有消失，但是对于string其他复杂的类型，就不是这个情况

```rust
let s1 = String::from("hello");
let s2 = s1;
```

如果类型修改为string，这个时候我们再次访问s1的话，s1就不可访问

Rust 永远也不会自动创建数据的 “深拷贝”。因此，任何 自动 的复制都可以被认为是对运行时性能影响较小的

## 3.2. 变量与数据的交互方式：克隆

如果我们 确实 需要深度复制 String 中堆上的数据，而不仅仅是栈上的数据，可以使用一个叫做 clone的通用函数。

```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {s1}, s2 = {s2}");
```

# 4. 所有权与函数

将值传递给函数与给变量赋值的原理相似。向函数传递值可能会移动或者复制，就像赋值语句一样

```rust
fn main() {
    let s = String::from("hello");  // s 进入作用域

    takes_ownership(s);             // s 的值移动到函数里 ...
                                    // ... 所以到这里不再有效

    let x = 5;                      // x 进入作用域

    makes_copy(x);                  // x 应该移动函数里，
                                    // 但 i32 是 Copy 的，
                                    // 所以在后面可继续使用 x

} // 这里，x 先移出了作用域，然后是 s。但因为 s 的值已被移走，
  // 没有特殊之处

fn takes_ownership(some_string: String) { // some_string 进入作用域
    println!("{}", some_string);
} // 这里，some_string 移出作用域并调用 `drop` 方法。
  // 占用的内存被释放

fn makes_copy(some_integer: i32) { // some_integer 进入作用域
    println!("{}", some_integer);
} // 这里，some_integer 移出作用域。没有特殊之处
```

## 4.1. 返回值与作用域

返回值也可以转移所有权

```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership 将返回值
                                        // 转移给 s1

    let s2 = String::from("hello");     // s2 进入作用域

    let s3 = takes_and_gives_back(s2);  // s2 被移动到
                                        // takes_and_gives_back 中，
                                        // 它也将返回值移给 s3
} // 这里，s3 移出作用域并被丢弃。s2 也移出作用域，但已被移走，
  // 所以什么也不会发生。s1 离开作用域并被丢弃

fn gives_ownership() -> String {             // gives_ownership 会将
                                             // 返回值移动给
                                             // 调用它的函数

    let some_string = String::from("yours"); // some_string 进入作用域。

    some_string                              // 返回 some_string
                                             // 并移出给调用的函数
                                             //
}

// takes_and_gives_back 将传入字符串并返回该值
fn takes_and_gives_back(a_string: String) -> String { // a_string 进入作用域
                                                      //

    a_string  // 返回 a_string 并移出给调用的函数
}
```

变量的所有权总是遵循相同的模式：将值赋给另一个变量时移动它。当持有堆中数据值的变量离开作用域时，其值将通过 drop 被清理掉，除非数据被移动为另一个变量所有。

# 5. 引用与借用

1. 引用与借用实际上说一个概念的两种说法
2. 引用默认是无法修改变量的值
3. 如果需要修改变量的值需要使用可变引用

引用的概念：我们将一个string类型的变量传递给函数，这个时候我们在主函数当中是无法访问这个变量的，即使这个函数结束，我们也还是无法访问这个变量的。这个时候需要引入一个引用的概念

引用（reference）像一个指针，因为它是一个地址，我们可以由此访问储存于该地址的属于其他变量的数据。

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

&s1 语法让我们创建一个 指向 值 s1 的引用，但是并不拥有它。因为并不拥有这个值，所以当引用停止使用时，它所指向的值也不会被丢弃。

## 5.1. 可变引用

如果我们需要将变量的值修改，这个时候我们就需要使用可变引用

```rust
// 可变引用
let mut s = String::from("hello");
change(&mut s);
println!("{}", s);

fn change(s: &mut String) {
    s.push_str(", world");
}
```