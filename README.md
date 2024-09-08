## 目录

* [入门](#入门)
    * [安装](#安装)
    * [VSCode](#VSCode)
    * [Cargo](#Cargo)
* [数据类型](#数据类型)
    * [整型](#整型)
    * [字符](#字符)


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
‌‌补码的定义和作用‌:

‌补码‌是‌计算机中表示有符号数的一种方法，包括‌原码、‌反码和补码三种表示方法。在计算机系统中，数值一律用补码来表示和存储。补码可以将符号位和数值域统一处理，同时加法和减法也可以统一处理。

补码的计算方法包括以下几个步骤：

‌正数的补码‌：正数的补码就是其本身，即符号位为0，其余位为该数的二进制表示。
‌负数的补码‌：负数的补码是通过其原码计算得到的。首先，将原码的符号位不变，其余位取反（0变1，1变0），然后加1。例如，-8的原码为10001000，其反码为11110111，补码为11111000。‌

‌补码的优点‌:

补码系统的最大优点是可以在加法或减法处理中，不需因为数字的正负而使用不同的计算方式。只要一种加法电路就可以处理各种有号数加法，而且减法可以用一个数加上另一个数的补码来表示，因此只要有加法电路及补码电路即可完成各种有号数加法及减法，在电路设计上相当方便
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

Rust 会使用 `u8` 类型作为字节值，例如从二进制文件或套接字中读取数据时，会产生一个u8值构成的流。`char` 既不是 ``u8` 也不是 `u32`，尽管它确实有 32 位长。

前缀 0x、0o 和 0b 分别表示十六进制、八进制和二进制字面量。字面量 `b'A'` 与 `65u8` 等价，因为 ASCII 字符 A 的值是 65。

#### 整型溢出

检测算法

回绕算法

饱和算法

溢出算法


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

```shell
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
Unicode 是一种全球通用的字符编码标准，旨在为每种语言中的所有字符分配唯一的编码，从而解决不同编码系统之间的不兼容问题。它为每个字符提供一个唯一的标识符（称为码点），使得文本可以在各种平台、语言和系统之间无缝交换和处理。

全角 Unicode?

全角（Full-width）是指在字符编码中，一个字符占用两个标准字符的宽度（通常指 ASCII 字符的宽度）。在 Unicode 标准中，通常中文、日文、韩文（CJK）字符、一些标点符号等都是全角字符，而 ASCII 字符是半角（Half-width）的。

Unicode 码点?

Unicode 码点（Unicode code point）是指 Unicode 字符集中每个字符对应的唯一标识符。它表示为 U+ 后跟一个十六进制的数字。例如，字符 "A" 的 Unicode 码点是 U+0041。
```


## 相关链接

[标准项目目录结构](https://course.rs/cargo/guide/package-layout.html)
[变更镜像地址](https://course.rs/first-try/slowly-downloading.html)