## 目录

* [入门](#入门)
    * [安装](#安装)
    * [VSCode](#VSCode)
    * [Cargo](#Cargo)
* [数据类型](#数据类型)
    * [整型](#整型int)
    * [浮点类型](#浮点类型float)
    * [字符](#字符char)
    * [布尔](#布尔bool)
    * [元组](#元组tuple)
    * [指针](#指针)
    * [数组](#数组)
    * [vector](#vector)
    * [切片](#切片)
    * [字符串](#字符串)
* [运算](#运算)
    * [数字运算](#数字运算)
    * [位运算](#位运算)
* [所有权和移动](#所有权和移动)
    * [所有权](#所有权)
    * [移动](#移动)
    * [Copy 类型](#copy-类型)
    * [Rc 和 Arc](#rc-和-arc共享所有权)
* [引用](#引用)
    * [引用](#引用)
* [生命周期](#生命周期)
    * [引用](#生命周期标注)
* [特型和泛型](#特型和泛型)
    * [使用特型](#使用特型)


## 入门

### 安装

`rustup` 是 Rust 的安装程序，也是它的版本管理程序，强烈建议使用 `rustup` 来安装 Rust。 如果你不想用或者不能用 `rustup`，请参见[Rust 其他安装方式](https://forge.rust-lang.org/infra/other-installation-methods.html#other-rust-installation-methods)。

打开终端并输入下面命令（Linux & macOS）:

```bash
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

这个命令将下载一个脚本并开始安装 `rustup` 工具，此工具将安装 Rust 的最新稳定版本。可能会提示你输入管理员密码。

如果安装成功，将出现下面这行:

```bash
Rust is installed now. Great!
```

OK，这样就已经完成 Rust 安装啦。

检查是否正确安装了 Rust，可打开终端并输入下面这行，此时能看到最新发布的稳定版本的版本号、提交哈希值和提交日期:

```bash
$ rustc -V
rustc 1.81.0 (eeb90cda1 2024-09-04)

$ cargo -V
cargo 1.81.0 (2dbb1af80 2024-08-20)
```

### 更新

要更新 Rust，在终端执行以下命令即可更新：

```bash
$ rustup update
```

### 卸载

要卸载 Rust 和 `rustup`，在终端执行以下命令即可卸载：

```bash
$ rustup self uninstall
```

### VSCode

[墙推 VSCode 插件](https://course.rs/first-try/editor.html)

### Cargo

`cargo` 提供了一系列的工具，从项目的建立、构建到测试、运行直至部署，为 Rust 项目的管理提供尽可能完整的手段

包管理工具最重要的意义就是任何用户拿到你的代码，都能运行起来，而不会因为各种包版本依赖焦头烂额。

创建一个新的 Rust 项目:

```bash
$ cargo new hello_cargo
```

上面的命令使用 `cargo new` 创建一个项目，项目名是 `hello_cargo` ，该项目的结构和配置文件都是由 `cargo` 生成，意味着我们的项目被 `cargo` 所管理。

下面来看看创建的项目结构:

```bash
$ tree
.
├── .git
├── .gitignore
├── Cargo.toml
└── src
    └── main.rs
```

#### 运行项目

有两种方式可以运行项目：

* cargo run

* 手动编译和运行项目

首先来看看第一种方式 `cargo run` 命令会编译并运行项目。

```bash
$ cargo run
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.01s
     Running `target/debug/hello_cargo`
Hello, world!
```

手动编译和运行项目。

编译

```
$ cargo build
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
```

运行

```
$ ./target/debug/hello_cargo
Hello, world!
```

上面代码运行在 `debug` 模式，在这种模式下，代码的编译速度会非常快，可是福兮祸所伏，运行速度就慢了. 原因是，在 `debug` 模式下，Rust 编译器不会做任何的优化，只为了尽快的编译完成，让你的开发流程更加顺畅。

如果想要在 `release` 模式下运行，可以使用 `--release` 参数：

```
$ cargo run --release
$ cargo build --release
$ ./target/release/hello_cargo
Hello, world!
```

#### Cargo Check

当项目大了后，`cargo run` 和 `cargo build` 不可避免的会变慢，那么有没有更快的方式来验证代码的正确性呢？大杀器来了，接着！

`cargo check` 是我们在代码开发过程中最常用的命令，它的作用很简单：快速的检查一下代码能否编译通过。因此该命令速度会非常快，能节省大量的编译时间。

```bash
$ cargo check
    Checking world_hello v0.1.0 (/Users/sunfei/development/rust/world_hello)
    Finished dev [unoptimized + debuginfo] target(s) in 0.06s
```

#### Cargo.toml 和 Cargo.lock

`Cargo.toml` 和 `Cargo.lock` 是 `cargo` 的核心文件，它的所有活动均基于此二者。

* `Cargo.toml` 是 `cargo` 特有的项目数据描述文件。它存储了项目的所有元配置信息，如果 Rust 开发者希望 Rust 项目能够按照期望的方式进行构建、测试和运行，那么，必须按照合理的方式构建 `Cargo.toml`。

* `Cargo.lock` 文件是 `cargo` 工具根据同一项目的 toml 文件生成的项目依赖详细清单，因此我们一般不用修改它，只需要对着 `Cargo.toml` 文件撸就行了。

```
什么情况下该把 `Cargo.lock` 上传到 git 仓库里？很简单，当你的项目是一个可运行的程序时，就上传 `Cargo.lock`，如果是一个依赖库项目，那么请把它添加到 `.gitignore` 中。
```

[配置详情](https://course.rs/first-try/cargo.html#package-%E9%85%8D%E7%BD%AE%E6%AE%B5%E8%90%BD)


## 数据类型

### 整型(int)

**整数**是没有小数部分的数字。之前使用过的 `i32` 类型，表示有符号的 32 位整数（ `i` 是英文单词 _integer_ 的首字母，与之相反的是 `u`，代表无符号 `unsigned` 类型）。下表显示了 Rust 中的内置的整数类型：

| 长度       | 有符号类型 | 无符号类型 |
| ---------- | ---------- | ---------- |
| 8 位       | `i8`       | `u8`       |
| 16 位      | `i16`      | `u16`      |
| 32 位      | `i32`      | `u32`      |
| 64 位      | `i64`      | `u64`      |
| 128 位     | `i128`     | `u128`     |
| 视架构而定  | `isize`    | `usize`    |

类型定义的形式统一为：`有无符号 + 类型大小(位数)`。**无符号数**表示数字只能取正数和 0，而**有符号**则表示数字可以取正数、负数还有 0。就像在纸上写数字一样：当要强调符号时，有符号数字以[补码](https://en.wikipedia.org/wiki/Two%27s_complement)形式存储。

```
‌‌补码‌主要是能够让加法器同时处理加法和减法:

‌补码‌是‌计算机中表示有符号数的一种方法，包括‌原码、‌反码和补码三种表示方法。在计算机系统中，数值一律用补码来表示和存储。
补码可以将符号位和数值域统一处理，同时加法和减法也可以统一处理。

‌正数的补码‌：正数的补码就是其本身，即符号位为0，其余位为该数的二进制表示。

‌负数的补码‌：负数的补码是通过其原码计算得到的。首先，将原码的符号位不变，其余位取反（0变1，1变0），然后加 1。
例如，-8的原码为10001000，其反码为11110111，补码为11111000。‌

补码系统的最大优点是可以在加法或减法处理中，不需因为数字的正负而使用不同的计算方式。只要一种加法电路就可以处理各种有号数加法，
而且减法可以用一个数加上另一个数的补码来表示，因此只要有加法电路及补码电路即可完成各种有号数加法及减法，在电路设计上相当方便。

计算 13 - 7:

原码：13 = 00001101，7 = 00000111
补码：13 = 00001101，-7 = 11111001

  00001101   (13)
+ 11111001   (-7)
------------
  00000110   (结果为6)
```

此外，`isize` 和 `usize` 类型取决于程序运行的计算机 CPU 类型： 若 CPU 是 32 位的，则这两个类型是 32 位的，同理，若 CPU 是 64 位，那么它们则是 64 位。

整形字面量可以用下表的形式书写：

| 数字字面量         | 示例          |
| ------------------ | ------------- |
| 十进制             | `98_222`      |
| 十六进制           | `0xff`        |
| 八进制             | `0o77`        |
| 二进制             | `0b1111_0000` |
| 字节 (仅限于 `u8`) | `b'A'`        |

Rust 整型默认使用 `i32`，例如 `let i = 1`，那 `i` 就是 `i32` 类型，因此你可以首选它，同时该类型也往往是性能最好的。`isize` 和 `usize` 的主要应用场景是用作集合的索引。

Rust 会使用 `u8` 类型作为字节值，例如从二进制文件或套接字中读取数据时，会产生一个 u8 值构成的流。`char` 既不是 `u8` 也不是 `u32`，尽管它确实有 32 位长。

前缀 0x、0o 和 0b 分别表示十六进制、八进制和二进制字面量。字面量 `b'A'` 与 `65u8` 等价，因为 ASCII 字符 A 的值是 65。

#### 整型溢出

检测算法

回绕算法

饱和算法

溢出算法

### 浮点类型(float)

**浮点类型数字** 是带有小数点的数字，在 Rust 中浮点类型数字也有两种基本类型： `f32` 和 `f64`，分别为 32 位和 64 位大小。默认浮点类型是 `f64`，在现代的 CPU 中它的速度与 `f32` 几乎相同，但精度更高。Rust 的 f32 和 f64 分别对应 C 和 C++ 以及 Java 中的 float 和 double 类型。

下面是一个演示浮点数的示例：

```rust
fn main() {
    let x = 2.0; // f64
    let y: f32 = 3.0; // f32
}
```

浮点数根据 `IEEE-754` 标准实现。`f32` 类型是单精度浮点型，`f64` 为双精度。

#### 浮点数陷阱

浮点数由于底层格式的特殊性，需要注意下面两点：

* 浮点数往往是你想要数字的近似表达
* 可以使用 `>`，`>=` 等进行比较，不可以测试相等性

浮点数未实现 `std::cmp::Eq` 特征，无法使用浮点数作为 `HashMap` 的 `Key`。

来看个小例子:

```rust
fn main() {
  // 断言0.1 + 0.2与0.3相等
  assert!(0.1 + 0.2 == 0.3);
}
```

你可能以为，这段代码没啥问题吧，实际上它会 _panic_（程序崩溃，抛出异常），因为二进制精度问题，导致了 0.1 + 0.2 并不严格等于 0.3，它们可能在小数点 N 位后存在误差。

那如果非要进行比较呢？可以考虑用这种方式 `(0.1_f64 + 0.2 - 0.3).abs() < 0.00001` ，具体小于多少，取决于你对精度的需求。

```rust
fn main() {
    let abc: (f32, f32, f32) = (0.1, 0.2, 0.3);
    let xyz: (f64, f64, f64) = (0.1, 0.2, 0.3);

    println!("abc (f32)");
    println!("   0.1 + 0.2: {:x}", (abc.0 + abc.1).to_bits());
    println!("         0.3: {:x}", (abc.2).to_bits());
    println!();

    println!("xyz (f64)");
    println!("   0.1 + 0.2: {:x}", (xyz.0 + xyz.1).to_bits());
    println!("         0.3: {:x}", (xyz.2).to_bits());
    println!();

    assert!(abc.0 + abc.1 == abc.2);
    assert!(xyz.0 + xyz.1 == xyz.2);
}
```

运行该程序，输出如下:

```console
abc (f32)
   0.1 + 0.2: 3e99999a
         0.3: 3e99999a

xyz (f64)
   0.1 + 0.2: 3fd3333333333334
         0.3: 3fd3333333333333

thread 'main' panicked at 'assertion failed: xyz.0 + xyz.1 == xyz.2',
➥ch2-add-floats.rs.rs:14:5
note: run with `RUST_BACKTRACE=1` environment variable to display
➥a backtrace
```

### 字符(char)

字符字面量是用单引号括起来的字符，比如 `'8'` 获 `'!'`。 还可以用全角 `Unicode` 字符，比如 `'中'` 或 `'国'`。

下面的代码展示了几个颇具异域风情的字符：

```rust
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let g = '国';
    let heart_eyed_cat = '😻';
}
```

在 Rust 语言中这些都是字符，Rust 的字符不仅仅是 `ASCII`，所有的 `Unicode` 值都可以作为 Rust 字符，包括单个的中文、日文、韩文、emoji 表情符号等等，
都是合法的字符类型。

由于 `Unicode` 都是 4 个字节编码，因此字符类型也是占用 4 个字节：

```rust
fn main() {
    let x = '中';
    println!("字符'中'占用了{}字节的内存大小",std::mem::size_of_val(&x));
    let x = 'a';
    println!("字符'a'占用了{}字节的内存大小",std::mem::size_of_val(&x));
}
```

输出如下:

```
字符'中'占用了4字节的内存大小
字符'a'占用了4字节的内存大小
```

注：Rust 的字符只能用 '' 来表示， "" 是留给字符串的。

Rust 不会在 `char` 和任何其他类型之间进行隐式转换，可以使用 `as` 转换运算符将 `char` 转换为整型，
对于小于 32 位的类型，该字符值的高位会被截断：

```
assert_eq!('*' as i32, 42);
assert_eq!(97 as char, 'a');
assert_eq!('中' as u8, 45);
```

补充：

```
Unicode 是一种全球通用的字符编码标准，旨在为每种语言中的所有字符分配唯一的编码，从而解决不同编码系统之间的不兼容问题。
它为每个字符提供一个唯一的标识符（称为码点），使得文本可以在各种平台、语言和系统之间无缝交换和处理。

全角 Unicode?

全角（Full-width）是指在字符编码中，一个字符占用两个标准字符的宽度（通常指 ASCII 字符的宽度）。
在 Unicode 标准中，通常中文、日文、韩文（CJK）字符、一些标点符号等都是全角字符，而 ASCII 字符是半角（Half-width）的。

Unicode 码点?

Unicode 码点（Unicode code point）是指 Unicode 字符集中每个字符对应的唯一标识符。
它表示为 U+ 后跟一个十六进制的数字。例如，字符 "A" 的 Unicode 码点是 U+0041。
```

### 布尔(bool)

Rust 中的布尔类型有两个可能的值：true 和 false，布尔值占用内存的大小为 1 个字节：

```rust
fn main() {
    let t = true;

    let f: bool = false; // 使用类型标注,显式指定f的类型

    if f {
        println!("这是段毫无意义的代码");
    }
}
```

使用布尔类型的场景主要在于流程控制，例如上述代码的中的 if 就是其中之一。


### 单元类型

单元类型就是 () ，对，你没看错，就是 () ，唯一的值也是 () ，一些读者读到这里可能就不愿意了，你也太敷衍了吧，管这叫类型？

只能说，再不起眼的东西，都有其用途，在目前为止的学习过程中，大家已经看到过很多次 fn main() 函数的使用吧？那么这个函数返回什么呢？

没错， main 函数就返回这个单元类型 ()，你不能说 main 函数无返回值，因为没有返回值的函数在 Rust 中是有单独的定义的：发散函数( diverge function )，顾名思义，无法收敛的函数。

例如常见的 println!() 的返回值也是单元类型 ()。

再比如，你可以用 () 作为 map 的值，表示我们不关注具体的值，只关注 key。 这种用法和 Go 语言的 struct{} 类似，可以作为一个值用来占位，但是完全不占用任何内存。


### 元组tuple

元组是由多种类型组合到一起形成的，因此它是复合类型，元组的长度是固定的，元组中元素的顺序也是固定的.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);

    println!("The value of tup is: {:?}", tup);
}
```

使用模式匹配解构元组

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (_x, y, _z) = tup;

    println!("The value of y is: {}", y);
}
```

访问某个特定元素，索引从 0 开始

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```

元组的成员还可以是一个元组

```rust
fn main() {
    let _t1: (u8, (i16, u32)) = (0, (-1, 1));
}
```

下面两种访问方式是错误的

```
// 错误，不能使用变量来访问元组的元素
fn main() {
    let a = (1, 2, 3); 

    for i in range(0, 3) {
        println!("{}", a.i);
    }

}

// 错误，元祖不支持迭代
fn main() {
    let a = (1, 2, 3); 

    for i in &a {
        println!("{}", i);
    }

}
```

正确方式，元组转换为数组进行迭代（元素数据类型一致）

```rust
fn main() {
    let a = (1, 2, 3); 
    let array = [a.0, a.1, a.2]; 

    for i in &array {
        println!("{}", i);
    }
}
```

包含单个值的元组，称为单元素元组，它的类型是 (T,)，其中 T 是单个元素的类型，逗号是必须的，以区分它和被括号包裹的值。

```rust
fn main() {
    let x = (1,); // 单元素元组
    let y = (2); // 一个整数
}
```

### 指针

#### 引用

`&i32` 是对 `i32` 类型的引用，引用是一个保存着 i32 地址的机器字，这个地址可能位于栈或堆中。

引用有两种形式：

* 不可变引用（immutable references）：`&T`。一个不可变的共享引用，可以同时拥有多个对定值的共享引用。

* 可变引用（mutable references）：`&mut T`。一个可变的，独占的引用，只要改引用还存在，就不能对改值有任何类型的其他引用。


#### Box

`Box<T>` 是一个智能指针，它指向分配在堆上的值。


#### 裸指针

Rust 也有裸指针类型 `*const T` 和 `*mut T`，分别是不可变和可变的裸指针。裸指针是不安全的，因为它们不受 Rust 借用检查器的约束。裸指针可能为空，或者他们可能指向已释放的内存或包含不同类型的值。

只能在 `unsafe` 块中对裸指针解引用（dereference）。


### 数组

数组 `array` 是存储在栈上，元素类型大小固定，且长度也是固定。

数组声明方式:

```
// 方式 1
fn main() {
    let a = [1, 2, 3, 4, 5];
}

// 方式 2
fn main() {
    let a: [i32; 5] = [1, 2, 3, 4, 5];
}
```

可以使用下面的语法初始化一个某个值重复出现 N 次的数组：

```
let a = [3; 5];
// 等价于
let a = [3, 3, 3, 3, 3];
```

**访问数组元素**

因为数组是连续存放元素的，因此可以通过索引的方式来访问存放其中的元素

```rust
fn main() {
    let a = [9, 8, 7, 6, 5];

    let first = a[0];  // 获取第一个元素
    let second = a[1]; // 获取第二个元素
}
```
循环迭代数组元素

```rust
fn main() {
    let a = [9, 8, 7, 6, 5];
    for i in &a {
        println!("{}", i);
    }
}
```

**修改数组元素**

```rust
fn main() {
    let mut a = [3; 5];

    println!("{:?}", a);
    a[2] = 5;
}
```

**数组切片**

```rust
fn main() {
    let mut a = [3; 5];

    println!("{:?}", a);
    a[2] = 5;

    let b = &mut a[1..3];
    println!("{:?}", b);

    b[1] = 10; 
    println!("{:?}", b);
    println!("{:?}", a);
}
```

注：在数组上看到的那些实用方法（遍历元素、搜索、排序、填充、过滤等）都是作为切片而非数组的方式提供的。但是 Rust 在搜索各种方法时会隐式地将对数组的引用转换为切片，因此可以直接在数组上调用任何切片方法。


### Vector

一个 `Vec<T>` 是一个长度可变的类型 T 的数组，它的元素都存储在堆上。

一个 `Vec<T>` 由 3 个值组成：一个指针指向堆上存储元素的缓冲区，这个缓冲区的所有权属于这个 `Vec<T>`；缓冲区可以存储的元素的数量；它现在实际已经拥有的元素的数量（也就是它的长度）。当缓冲区的的元素到达最大容量时，继续添加元素会导致vector重新分配一个更大的缓冲区，再把已有元素都拷贝过去，然后更新 vector的指针和容量，最后释放旧的缓冲区。

**创建**

使用 `vec!` 宏创建一个 `Vec<T>`:

```rust
fn main() {
    let mut v = vec![1, 2, 3, 4, 5];
    println!("v = {:?}", v);  // v = [1, 2, 3, 4, 5]
    v.push(11);
    v.push(13);
    println!("v = {:?}", v);  // v = [1, 2, 3, 4, 5, 11, 13]
}
```

`vec!` 宏等价于调用 `Vec::new` 创建一个新的空 vector:

```rust
fn main() {
    let mut v = Vec::new();
    v.push(1);
    v.push(2);
    v.push(3);
    println!("v = {:?}", v);  // v = [1, 2, 3]
}
```

另一种创建 vector 的方法是通过迭代器创建：

```rust
fn main() {
    let v: Vec<i32> = (0..5).collect();
    println!("v = {:?}", v);  // v = [0, 1, 2, 3, 4]
}
```

可以使用 `Vec::with_capacity` 来创建一个指定的缓冲区的 vector，避免重新分配内存。

```rust
fn main() {
    let mut v = Vec::with_capacity(2);
    println!("{:?}", v.len());      // 0
    println!("{:?}", v.capacity()); // 2
    v.push(1);
    v.push(2);
    println!("{:?}", v.len());      // 2
    println!("{:?}", v.capacity()); // 2
}
```

**插入、移除**

可以在 vector 中任意插入或移除元素，这些操作会移动修改位置前面或者后面的元
素。

```rust
fn main() {
    let mut v = vec![10, 20, 30, 40, 50];
    // 在索引为 3的地方插入 35
    v.insert(3, 35);
    assert_eq!(v, [10, 20, 30, 35, 40, 50]);
    // 移除索引为 1的元素
    v.remove(1);
    assert_eq!(v, [10, 30, 35, 40, 50]);
}
```

你可以使用 pop 方法移除最后一个元素并返回它。更确切地说，从 `Vec<T>` 中弹出只会返回一个 `Option<T>`：如果 vector 已经为空是 None，如果最后一个元素是 v 就是 Some(v)：

```rust
fn main() {
    let mut v = vec!["Snow Puff", "Glass Gem"];
    assert_eq!(v.pop(), Some("Glass Gem"));
    assert_eq!(v.pop(), Some("Snow Puff"));
    assert_eq!(v.pop(), None);
}
```

**循环访问**

```rust
fn main() {
    let a = vec![1, 2, 3, 4, 5];

    // 借用
    for i in &a {
        println!("{}", i);
    }

    for i in a {
        println!("{}", i);
    }

    // 报错，a已经被move了
    println!("{:?}", a);
}
```

### 切片

切片的引用是胖指针：一个包含指向切片中第一个元素的指针和切片中元素数量的双字
值。

假设你正在运行下列代码：

```rust
let v: Vec<f64> = vec![0.0, 0.707, 1.0, 0.707];
let a: [f64; 4] = [0.0, -0.707, -1.0, -0.707];

let sv: &[f64] = &v;
let sa: &[f64] = &a;
```

上面代码运行完后，内存布局如下：

![slice](/images/slice.png)

一个普通的引用是一个指向单个值的无所有权指针，而一个切片的引用是一个指向内存中
连续的范围的指针。这使得如果你想写一个处理数组或 vector的函数，那么切片引用将是一
个很好的选择。例如，这里有一个函数打印出一系列值，每个单独一行：
    
```rust
fn print(n: &[f64]) {
    for elt in n {
        println!("{}", elt);
    } 
}

print(&a); // 可以用于数组
print(&v); // 也可以用于 vector
```

### 字符串

Rust 的字符串类型是 `&str` 和 `String`。

#### 字符串字面量

字符串字面量 &str 被双引号包裹，和 char 字面量一样是通过反斜杠来转义：

```rust
fn main() {
    let speech = "\"Ouch!\" said the well.";
    println!("{}", speech);   // "Ouch!" said the well.
}
```

如果字符串中的一行以反斜杠结尾，那么换行符和下一行的前导空格就会被丢弃掉：

```rust
fn main() {
    let speech = "much ado about \
    nothing";
    println!("{}", speech);   // much ado about nothing
}
```

用小写字母 `r` 来提供了原始字符串，原始字符串中的所有反斜杠和空白字符都被原样包含在字符串里，
不会识别任何转义：

```rust
fn main() {
    let default_win_install_path = r"C:\Program Files\Gorillas";
    println!("{}", default_win_install_path);  
    // C:\Program Files\Gorillas

    println!(r###"
    This raw string started with 'r###"'.
    Therefore it does not end until we reach a quote mark ('"')
    followed immediately by three pound signs ('###'):
    "###);

    // This raw string started with 'r###"'.
    // Therefore it does not end until we reach a quote mark ('"')
    // followed immediately by three pound signs ('###'):
}
```

#### 字节串

以 b 前缀开头的字符串字面量是字节字符串。这种字符串实际上是u8 值的切片——也就是
字节流——而不是 Unicode 文本：

```rust
let method = b"GET";
assert_eq!(method, &[b'G', b'E', b'T']);
```

#### 内存中的字符串

Rust的字符串是 Unicode 字符的序列，但它并不是作为char 的数组存储在内存中。事实上
它使用 UTF-8 编码存储，这是一种可变长度的编码。每一个 ASCII 字符被存储为一个字节，
其他字符可能会占据多个字节。

下图显示下面代码创建的 String 和 &str:

```
let noodles = "noodles".to_string();
let oodles = &noodles[1..];
let poodles = "ನಮಸ್ಕಾರ"
```

![alt text](/images/string.png)

noodles 是一个拥有 8 个字节大小的缓冲区的 String，其中 7 个字节已经被使用。你可以将String 想象为保证内容是有效 UTF-8 编码的 Vec<u8>；事实上，String 就是这么实现的。

一个 &str（读作“stir”或者“字符串切片”）是一个指向其他值拥有的UTF-8 文本的引用：
它“借用”了这段文本。在这个例子中，oodles 是一个指向 noodles 所持有的文本中的最后六
个字节的 &str，因此它表示文本“oodles”。就像其他切片引用一样，&str 是一种胖指针，包
括实际数据的地址和长度。你可以将 &str 看作一个保证内容为合法的 UTF-8 编码的 &[u8]。

字符串字面量是一个指向预先分配好内存的文本的 &str，实际的文本通常和程序的机器码
一起存储到只读的内存区域。在之前的例子中，poodles 是一个字符串字面量，指向程序运
行时就已经被创建好并且持续到程序退出的 7 个字节。

一个 String 或 &str 的 `len()` 方法返回它的长度。但这个长度是以字节为单位，而不是以
字符为单位：

```
assert_eq!("ನಮಸ್ಕಾರ".len(), 21);
```

要在运行时创建新的字符串，要使用 String。

#### String

&str 和 &[T] 很像：都是一个指向某些数据的胖指针。String 类似于 Vec<T>，如表 3-11所示。

<img src="/images/string-vec.png" alt="string-vec" width="650">

类似于 Vec，每个 String 都有它自己的在堆上分配的缓冲区，这个缓冲区不和其他任
何 String 共享。

有几种方式创建 String：

`.to_string()` 方法把 &str 转换为一个 String，这会拷贝字符串：

```rust
let error_message = "too many pets".to_string()
```

`format!()` 宏类似于 `println!()`，区别在于它返回一个新的 String 而不是把它打印到标准输出，而且它不会在最后自动加上换行符：

```rust
assert_eq!(format!("{}°{:02}′{:02}″N", 24, 5, 23),
"24°05′23″N".to_string());
```

字符串的数组、切片、vector 都有两个方法 `.concat()` 和 `.join(sep)`，把多个字符串组合成一个：

```rust
let bits = vec!["veni", "vidi", "vici"];
assert_eq!(bits.concat(), "venividivici");
assert_eq!(bits.join(", "), "veni, vidi, vici");
```

## 运算

### 数字运算

Rust 支持所有数字类型的基本数学运算：加法、减法、乘法、除法和取模运算。下面代码各使用一条 `let` 语句来说明相应运算的用法：

```rust
fn main() {
    // 加法
    let sum = 5 + 10;

    // 减法
    let difference = 95.5 - 4.3;

    // 乘法
    let product = 4 * 30;

    // 除法
    let quotient = 56.7 / 32.2;

    // 求余
    let remainder = 43 % 5;
}
```

[附录 B](https://course.rs/appendix/operators.html#运算符) 中给出了 Rust 提供的所有运算符的列表。

### 位运算

Rust 的位运算基本上和其他语言一样

| 运算符  | 说明                                                   |
| ------- | ------------------------------------------------------ |
| & 位与  | 相同位置均为1时则为1，否则为0                          |
| \| 位或 | 相同位置只要有1时则为1，否则为0                        |
| ^ 异或  | 相同位置不相同则为1，相同则为0                         |
| ! 位非  | 把位中的0和1相互取反，即0置为1，1置为0                 |
| << 左移 | 所有位向左移动指定位数，右位补0                        |
| >> 右移 | 所有位向右移动指定位数，带符号移动（正数补0，负数补1） |

```rust
fn main() {
    // 无符号8位整数，二进制为00000010
    let a: u8 = 2; // 也可以写 let a: u8 = 0b_0000_0010;

    // 二进制为00000011
    let b: u8 = 3;

    // {:08b}：左高右低输出二进制01，不足8位则高位补0
    println!("a value is        {:08b}", a);

    println!("b value is        {:08b}", b);

    println!("(a & b) value is  {:08b}", a & b);

    println!("(a | b) value is  {:08b}", a | b);

    println!("(a ^ b) value is  {:08b}", a ^ b);

    println!("(!b) value is     {:08b}", !b);

    println!("(a << b) value is {:08b}", a << b);

    println!("(a >> b) value is {:08b}", a >> b);

    let mut a = a;
    // 注意这些计算符除了!之外都可以加上=进行赋值 (因为!=要用来判断不等于)
    a <<= b;
    println!("(a << b) value is {:08b}", a);
}
```

## 所有权和移动

计算机语言不断演变过程中，内存管理出现两张方式：

* 垃圾回收机制(GC)，在程序运行时不断寻找不再使用的内存，典型代表：Java、Go

* 手动管理内存的分配和释放, 在程序中，通过函数调用的方式来申请和释放内存，典型代表：C++、C

Rust 选择了第三种方式：所有权，它是一种在编译时检查内存安全的系统，不需要垃圾回收机制，也不需要手动管理内存。

注：所有权规则可以概括为三个核心规则：

* Rust 中的每一个值都与一个变量明确关联，这个变量是这个值的所有者；

* 任一时刻，每个值都只与一个变量有这种关联（禁止共享）；

* 当这个变量离开作用域，与之关联的值就会被回收（释放资源是安全的）。

### 所有权

但在 Rust中，所有权的概念被内建在语言之中，并且通过编译期检查确保强制执行。每个
值都只有一个决定它生命周期的所有者。当所有者被释放，它拥有的值也会同时被释放，
在 Rust中的术语中，释放的行为被称为丢弃（drop）。

```rust
fn print_padovan() {
    let mut padovan = vec![1,1,1]; // 在这里分配
    for i in 3..10 {
        let next = padovan[i-3] + padovan[i-2];
    padovan.push(next);
    }
    println!("P(1..10) = {:?}", padovan);
} // padovan 在这里释放
```

Rust在以下几个方面扩展了所有权的灵活性：

* 你可以将值从一个所有者移动到另一个所有者。这允许你构建、更改、拆除所有权树。

* 很简单的类型例如整数、浮点数和字符被所有权规则排除在外。它们被称为 Copy 类型。

* 标准库提供了引用计数的指针类型 Rc 和 Arc，它们允许值在一定的限制下可以有多个所
有者。

* 你可以“借用一个值的引用”，引用是生命周期受限的非占有的指针。

### 移动

在 Rust里对大多数类型来说，赋值给变量、把值传给函数、或者从函数返回值并不会拷
贝这个值：它们只会移动它。源对象放弃了值的所有权，把所有权转移给了目的对象，同
时源对象变为未初始化的状态；

```rust
let s = vec!["udon".to_string(), "ramen".to_string, "soba".to_string()];
let t = s;
let u = s; // 编译错误
```

赋值语句 `let t = s`; 把 vector 的三个字段从 s 移动到了 t；现在 t 拥有了这个 vector, s 变成了未初始化的状态。如果你尝试使用 s，编译器会报错。

<img src="/images/move.png" alt="move" width="650">

可以对元素进行深拷贝，这样就不会移动所有权：

```rust
let s = vec!["udon".to_string(), "ramen".to_string(), "soba".to_string()];
let t = s.clone();
let u = s.clone();
```

#### 移动更多操作

如果你把值移动进一个已经被初始化的变量，Rust会 drop 变量之前的值。例如：

```rust
let mut s = "Govinda".to_string();
s = "Siddhartha".to_string(); // 值"Govinda"在这里 drop
```

Rust 在几乎所有场景下都使用 move。向函数传参会把所有权移动给函数的参数；从函数返回值会把所有权移动给调用者；创建一个元组会把值移动给元组，等等。

```
struct Person { name: String, birth: i32 }
let mut composers = Vec::new();
composers.push(Person { name: "Palestrina".to_string(),
birth: 1525 });
```

#### 移动与控制流

如果一个变量在if 表达式的条件判断之后还是有值的，那我们在两个分支中都可以使用它：

```rust
let x = vec![10, 20, 30];
if c {
    f(x); // ... 在这里移动 x的值是 ok的
} else {
    g(x); // ... 在这里移动 x的值是 ok的
}
h(x); // 这里 x 不能再使用，因为它已经被移动了
```

出于类似的原因，在循环里移动一个变量的值是禁止的：

```rust
let x = vec![10, 20, 30];
while f() { 
    g(x); // 错误：x会在第一次迭代时被移动
}
``` 

#### 移动与索引

我们已经提到过移动会将源对象设置为未初始化状态，目的对象会获得值的所有权。
但并不是每一种值的所有者都可以设置为未初始化状态。

```rust
let mut v = Vec::new();
for i in 101 .. 106 { 
    v.push(i.to_string());
}

let third = v[2];  // // 错误：不能移动 Vec 的索引
// let third = &v[2];  // 正确：使用引用
println!("The third element is {}", third);

// error[E0507]: cannot move out of index of `Vec<String>`
// |
// 14 | let third = v[2];
// | ^^^^
// | | | move occurs because value has type `String`,
// | which does not implement the `Copy` trait
// | help: consider borrowing here: `&v[2]`
```

有三种方法解决这个问题：

```
// 创建一个 string的 vector："101", "102", ... "105"
let mut v = Vec::new();
    for i in 101 .. 106 { v.push(i.to_string());
}

// 1. 弹出 vector尾部的元素
let fifth = v.pop().expect("vector empty!");
assert_eq!(fifth, "105");

// 2. 移出给定位置的元素，并把最后一个元素移动过来：
let second = v.swap_remove(1);
assert_eq!(second, "102");

// 3. 用另一个值和我们想移出的值交换
let third = std::mem::replace(&mut v[2], "substitute".to_string());
assert_eq!(third, "103");

// 让我们看看 vector中还剩下什么。
assert_eq!(v, vec!["101", "104", "substitute"]);
```

这三种方法都从 vector中移出一个元素，但仍然保证 vector处于没有空隙的状态，可能长
度还会变小。

### Copy 类型

对于简单类型例如整数或字符，移动并不是必须的，这些类型被称为 Copy 类型。

```rust
let string1 = "somnambulance".to_string();
let string2 = string1;

let num1: i32 = 36;
let num2 = num1;

```

Rust 赋予一个 Copy 类型的值会拷贝它，而不是移动它。

<img src="/images/copy.png" alt="copy" width="650">

标准的 Copy 类型包括所有的机器整数和浮点数类型、char 和 bool 类型，以及少数其他类
型。所有元素都是 Copy 类型的元组或数组也是 Copy 类型。


### Rc 和 Arc：共享所有权

Rust提供了引用计数类型 Rc 和 Arc。Rc 和 Arc 类型非常相似，它们唯一的不同之处在于 Arc 可以直接安全地在线程之间共享，名称 Arc 是原子引用计数的缩写，Rc 则使用更快一些的非线程安全代码来更新引用计数。

可以使用引用计数来管理值的生存周期，这样就可以在程序的多个部分之间共享值的所有权。

```rust
use std::rc::Rc;

// Rust可以推断出所有这些类型，写出来是为了更清楚
let s: Rc<String> = Rc::new("shirataki".to_string());
let t: Rc<String> = s.clone();
let u: Rc<String> = s.clone();
```

对于任意类型 T，一个 Rc<T> 值是一个指向在堆上分配的 T 类型值的指针，同时还附有一
个引用计数。克隆一个Rc<T> 类型的值并不意味着拷贝 T，它只是简单的创建另一个指向它的
指针，并且递增引用计数。

<img src="/images/rc.png" alt="rc" width="650">

这三个 Rc<String> 指针都指向内存中的同一块内存，这块内存里存储了一个引用计数和一个 String。通常的所有权规也适用于 Rc 指针，当最后一个 Rc 指针 drop 时，Rust会同时 drop 掉 String。


## 引用 

引入引用就是为了解决所有权禁止共享的问题，引用是一种类型，借用是动作。


## 生命周期

### 生命周期标注

引入生命周期标注，是为了解决编译器需要能够检测代码中是否存在悬垂引用的风险，并在检测到此类风险时拒绝编译。

通过经典的 longest 函数来了解生命周期标注的用处：

```rust
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

这段代码会编译报错的，因为返回的引用的生命周期是不确定的，编译器无法确定返回的引用和 x 还是 y 关联。

```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

增加了生命周期标注后，代码可以正确编译。标注 `’a` 实际上是在告诉编译器一个信息：

* `'a` 指出返回的引用与输入参数x，y之间有关联；

* `'a` 只是关联关系的代号；

```rust
fn largest<T: std::cmp::PartialOrd>(list: &[T]) -> &T {
    let mut largest:&T = &list[0];

    for item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let result = largest(&number_list);
    println!("The largest number is {}", result);

    let char_list = vec!['y', 'm', 'a', 'q'];

    let result = largest(&char_list);
    println!("The largest char is {}", result);
}

// The largest number is 100
// The largest char is y
```

## 特型和泛型

泛型是 `Rust` 中另一种形式的多态。类似于 `C++` 的模板，泛型函数或泛型类型可以和不同类型的值一起使用：

```
fn min<T: Ord>(value1: T, value2: T) -> T {
    if value1 <= value2 {
        value1
    } else {
        value2
    } 
}

fn main() {
    let a = 10;
    let b = 20;
    let c = min(a, b);
    println!("The minimum value is: {}", c);
}
```

此函数中的 `<T: Ord>` 意味着 `min` 函数可以于实现了 `Ord` 特型的任意类型（任意有序类型）`T` 的参数一起使用。
像这样的要求被称为界限（bounds），它对 `T` 可能的类型范围做了限制。编译器会针对你实际使用到的每一个类型 `T` 生成一份单独的机器码。

### 使用特型

特型代表一种能力，即一个类型能做什么。

特型方法有一条需要注意的规则：特型本身必须在作用域内，否则，它的所有方法都是不可见的。

```rust
fn main() {
    let mut buf: Vec<u8> = vec![];
    buf.write_all(b"hello")?; // 错误：没有叫`write_all`的方法
}
```

修复这个问题的方法是在作用域中引入 `std::io::Write` 特型：

```rust
use std::io::Write;

fn main() {
    let mut buf: Vec<u8> = vec![];
    buf.write_all(b"hello")?; // 错误：没有叫`write_all`的方法
}
```

`Clone` 和 `Iterator` 的方法不需要特殊的导入是因为它们默认总是在作用域里：它们是标准库预导入的一部分。

#### 特型对象

在 Rust 中使用特型编写多态代码有两种方法：特型对象和泛型。接下来先介绍特型对象。

```rust
fn main() {
    let mut buf: Vec<u8> = vec![];

    let writer: &mut dyn Write = &mut buf; // ok
}
```

对特型对象（如 writer）的引用叫作特型对象。与其他引用一样，特型对象指向某个值、它有生命周期、它可以是可变的或者是共享的。

在内存中，特型对象是一个胖指针，由指向值的指针和指向该值类型的虚表指针组成。

<img src="/images/trait-mem.png" alt="trait-mem" width="650">

Rust 会在需要时自动将普通引用转换为特型对象，这个过程叫作隐式转换。

```rust
use std::io::Write;
use std::fs::File;

fn say_hello(out: &mut dyn Write) -> std::io::Result<()> {
    out.write_all(b"hello world\n")?;
    out.flush()
}

fn main() {
    let mut local_file = File::create("hello.txt")?;
    say_hello(&mut local_file)?;

    let mut bytes = vec![];
    say_hello(&mut bytes)?;
}
```

`&mut local_file` 的类型是 `&mut File`，而 `say_hello` 的参数类型是 `&mut dyn Write`。
因为 `File` 是一种写入器，因此 Rust 允许将这种普通引用转换为特型对象。

同样的，Rust也乐于把 Box<File> 转换成 Box<dyn Write>，它拥有一个在堆上的写入器：

```rust
let w: Box<dyn Write> = Box::new(local_file);
```

`Box<dyn Write>` 和 `&mut dyn Write` 一样是一个胖指针，它包含写入器自身的地址和虚表的地址。其他指针类型例如 `Rc<dyn Write>` 也一样。

这种转换是唯一创建特型对象的唯一方法。编译器做的工作其实很简单，当转换发生时，
Rust 知道被引用值的真正类型（这个例子中是 File），因此它只是加上了正确的虚表的地址、把普通指针变成了胖指针。

#### 泛型函数和类型参数

把以函数特型对象为参数的函数 `say_hello()` 改写为泛型函数：

```rust
use std::io::Write;
use std::fs::File;

fn say_hello<W: Write>(out: &mut W) -> std::io::Result<()> {
    out.write_all(b"hello world\n")?;
    out.flush()
}

fn main() {
    let mut local_file = File::create("hello.txt")?;
    say_hello(&mut local_file)?;

    let mut bytes = vec![];
    say_hello(&mut bytes)?;
}
```

短语 `<W: Write>` 把函数变成了泛型形式，此短语叫作类型参数。

Rust 会为 `say_hello()` 生成两个版本的机器码，一个是 `File` 版本，另一个是 `Vec<u8>` 版本。
Rust 会从参数的类型推导出类型 W，这个过程被称为单态化。

泛型函数可以有多个类型参数：

```rust
fn run_query<M: Mapper + Serialize, R: Reducer + Serialize>(
        data: &DataSet, map: M, reduce: R) -> Results
{ ... }
```

正如这个例子展示的一样，约束可能太长以至于很难阅读。Rust提供了使用关键字 where 的替代语法：

```rust
fn run_query<M, R>(data: &DataSet, map: M, reduce: R) -> Results
    where M: Mapper + Serialize, 
          R: Reducer + Serialize
{ ... }
```

引用作为函数参数介绍了生命周期的语法。一个泛型函数可以同时有生命周期参数和类型参数。生命周期参数在前：

```rust
fn nearest<'t, 'c, P>(target: &'t P, candidates: &'c [P]) -> &'c P
    where P: MeasureDistance
{
    ... 
}
```

#### 使用哪一个？

泛型函数的劣势在于，Rust 会为每种用到的类型都编译一次，生成一份机器码，这可能会导致二进制文件变大。

但泛型相当于特型对象的优势在于：

* 泛型执行速度更快，在编译期间就能确定类型，不需要运行时的虚方法的调用开销和检查错误的开销；

* 泛型第二个优势在于并不是每个类型都支持特型对象，特型支持的几个特性（例如关联函数）只适用于泛型：
它们完全不支持特型对象。

* 泛型的第三个优势是可以很容易地一次给泛型类型参数添加多个特型约束，例如
我们的 `top_ten` 函数就要求它的参数 `T` 要实现 `Debug + Hash + Eq`。特型对象不能这么做：
Rust 不支持类似 `&mut (dyn Debug + Hash + Eq)` 这样的类型。




#### 定义特征

如果不同的类型具有相同的行为，那么我们就可以定义一个特征，然后为这些类型实现该特征

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

这里使用 `trait` 关键字来声明一个特征，`Summary` 是特征名。在大括号中定义了该特征的所有方法，在这个例子中是： `fn summarize(&self) -> String`。

特征只定义行为看起来是什么样的，而不定义行为具体是怎么样的。因此，我们只定义特征方法的签名，而不进行实现，此时方法签名结尾是 ;，而不是一个 {}。

#### 为类型实现特征

实现特征的语法与为结构体、枚举实现方法很像：`impl Summary for Post`，读作"为 `Post` 类型实现 `Summary` 特征"，
然后在 `impl` 的花括号中实现该特征的具体方法。

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
pub struct Post {
    pub title: String, // 标题
    pub author: String, // 作者
    pub content: String, // 内容
}

impl Summary for Post {
    fn summarize(&self) -> String {
        format!("文章{}, 作者是{}", self.title, self.author)
    }
}

fn main() {
    let post = Post{title: "Rust语言简介".to_string(),
            author: "Sunface".to_string(), content: "Rust棒极了!".to_string()};
    println!("{}",post.summarize());
}
```

**默认实现**

你可以在特征中定义具有默认实现的方法，这样其它类型无需再实现该方法，或者也可以选择重载该方法。

```rust
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}

pub struct Weibo {
    pub username: String,
    pub content: String
}

impl Summary for Weibo {}

fn main() {
    let weibo = Weibo{username: "sunface".to_string(),
        content: "好像微博没Tweet好用".to_string()};
    println!("{}",weibo.summarize());
}
```

**孤儿规则**

关于特征实现与定义的位置，有一条非常重要的原则：如果你想要为类型 A 实现特征 T，那么 A 或者 T 至少有一个是在当前作用域中定义的。

#### 特征作为函数参数

定义一个函数，使用特征作为函数参数:

```rust
pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}
```

`impl Summary`，顾名思义，它的意思是 实现了 `Summary` 特征 的 `item` 参数。

#### 特征约束

虽然 `impl Trait` 这种语法非常好理解，但是实际上它只是一个语法糖：

```rust
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

真正的完整书写形式如上所述，形如 `T: Summary` 被称为特征约束。

```rust
pub fn notify(item1: &impl Summary, item2: &impl Summary) {}

pub fn notify<T: Summary>(item1: &T, item2: &T) {}
```

对于复杂的场景，特征约束可以让我们拥有更大的灵活性和语法表现能力。

**多重约束**

除了单个约束条件，我们还可以指定多个约束条件。

```rust
pub fn notify(item: &(impl Summary + Display)) {}

pub fn notify<T: Summary + Display>(item: &T) {}
```

**Where 约束**

当特征约束变得很多时，函数的签名将变得很复杂：

```rust
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {}
```

严格来说，上面的例子还是不够复杂，但是我们还是能对其做一些形式上的改进，通过 where：

```rust
fn some_function<T, U>(t: &T, u: &U) -> i32
    where T: Display + Clone,
          U: Clone + Debug
{}
```

### 特征对象

可以通过 `&` 引用或者 `Box<T>` 智能指针的方式来创建特征对象。

```rust
trait Draw {
    fn draw(&self) -> String;
}

impl Draw for u8 {
    fn draw(&self) -> String {
        format!("u8: {}", *self)
    }
}

impl Draw for f64 {
    fn draw(&self) -> String {
        format!("f64: {}", *self)
    }
}

fn draw1(x: Box<impl Draw>) -> String {
     x.draw()
}

fn draw2(x: &dyn Draw) -> String {
    x.draw()
}

fn main() {
    let x = 1.1f64;
    let y = 8u8;

    // Box<T> 创建特征对象
    draw1(Box::new(x));
    draw1(Box::new(y));
    
    // & 引用 创建特征对象
    draw2(&x);
    draw2(&y);

    println!("{}", draw2(&x));
    println!("{}", draw2(&y));
}
```

#### 动态分发








## 相关链接

[crates.io](https://crates.io/)
[The Rust Edition Guide](https://doc.rust-lang.org/edition-guide/)
[标准项目目录结构](https://course.rs/cargo/guide/package-layout.html)
[变更镜像地址](https://course.rs/first-try/slowly-downloading.html)
