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
* [运算](#运算)
    * [数字运算](#数字运算)
    * [位运算](#位运算)


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

#### cargo check

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

正确方式，元组转换为数组并进行迭代

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

## 相关链接

[标准项目目录结构](https://course.rs/cargo/guide/package-layout.html)
[变更镜像地址](https://course.rs/first-try/slowly-downloading.html)
