# 原生类型

Rust 提供了多种原生类型，包括：

## 标量类型

* 有符号整型（signed integers）：`i8`， `i16`， `i32`， `i64` ，`i128`和 `isize`（指针 size）
* 无符号整型（unsigned integers）： `u8`， `u16`， `u64`，`u128` 和 `usize`（指针 size）
* 浮点类型（floating point）： `f32`， `f64`
* `char`（字符）：单独的 Unicode 字符，如 `'a'`，`'α'` 和 `'∞'`（大小是4个字节）
* `bool`（布尔型）：只能是 `true` 或 `false`
* 单元类型(unit type，空元组)： 只有 `()` 这个唯一值

尽管单元类型是元组，但它不被视为符合类型，因为它不包含多个值。

## 复合类型

* 数组：如 `[1, 2, 3]`
* 元组： 如 `(1, true)`



变量都能够显式地给出**类型声明**。数字可以通过**加后缀**或**默认方式**来声明。整型默认为
`i32` 类型，浮点型默认为 `f64` 类型。注意Rust也可以通过上下文推断类型。

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 变量可以声明类型。
    let logical: bool = true;

    let a_float: f64 = 1.0;  // 常规声明
    let an_integer   = 5i32; // 后缀声明

    // 否则自动推断类型。
    let default_float   = 3.0; // `f64`
    let default_integer = 7;   // `i32`

    // 可以从上下文推断类型
    let mut inferred_type = 12; // 从其他行可推断得到该变量是 i64 类型
    inferred_type = 4294967296i64;

    // 变量的值可以被改变
    let mut mutable = 12; // 可变类型 `i32`。
    mutable = 21;

    // 报错！不能改变变量的类型。
    mutable = true;
    
    
    // 变量可以通过遮蔽而重新赋值
    let mutable = true;
}
```

### 参见：

[`std` 库][std]

[std]: http://doc.rust-lang.org/std/
[reference]: http://doc.rust-lang.org/reference.html#number-literals
