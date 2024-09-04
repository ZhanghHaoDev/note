结构体和元组类似，它们都包含多个相关的值。和元组一样，结构体的每一部分可以是不同类型。但不同于元组，结构体需要命名各部分数据以便能清楚的表明其值的意义。由于有了这些名字，结构体比元组更灵活：不需要依赖顺序来指定或访问实例中的值。

# 1. 定义结构体

在rust语言当中，定义一个结构体我们使用struct关键字，比如下面的例子

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}
```

结构体内部的变量，我们称之为字段

创建结构体的实例：

```rust
fn main() {
    let mut user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");
}
```

# 2. imp关键字

在 Rust 中，impl 关键字用于实现类型的方法。你可以把它理解为"实现"的简写。当你看到 impl，你可以理解为我们正在给某个类型（如结构体、枚举或者 trait）添加一些行为或功能。

比如你有一个结构体 Dog，你想让 Dog 有一个 bark 的行为，你可以这样写：

```rust
struct Dog {
    name: String,
}

impl Dog {
    fn bark(&self) {
        println!("{} says: Woof!", self.name);
    }
}
```

在这个例子中，我们使用 impl 关键字给 Dog 结构体添加了一个 bark 方法。这个方法使得 Dog 可以"叫"。

然后你就可以创建一个 Dog 的实例，并调用它的 bark 方法：

```rust
let my_dog = Dog { name: String::from("Spot") };
my_dog.bark();  // 输出 "Spot says: Woof!"
```

所以，简单来说，impl 就是用来给一个类型添加方法的关键字。

# 3. 枚举

枚举：就说罗列出所有可能的字段

rust当中使用enum来创建枚举

```rust
enum IpAddrKind {
    V4,
    V6,
}

let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```

# 3.1. match 控制流结构

Rust 有一个叫做 match 的极为强大的控制流运算符，它允许我们将一个值与一系列的模式相比较，并根据相匹配的模式执行相应代码。模式可由字面值、变量、通配符和许多其他内容构成；match 的力量来源于模式的表现力以及编译器检查，它确保了所有可能的情况都得到处理。

可以把 match 表达式想象成某种硬币分类器：硬币滑入有着不同大小孔洞的轨道，每一个硬币都会掉入符合它大小的孔洞。同样地，值也会通过 match 的每一个模式，并且在遇到第一个 “符合” 的模式时，值会进入相关联的代码块并在执行中被使用。