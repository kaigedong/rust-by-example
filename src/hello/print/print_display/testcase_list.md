# 测试实例：List

对一个结构体来说，须对各个元素逐个实现 `fmt::Display` 可能会很麻烦。问题在于每个 `write!`
都要生成一个 `fmt::Result`。彻底地实现需要处理**所有**的结果。出于这方面考虑，Rust 提供了`？`操作符。

在 `write!` 上使用 `?`类似这样：

```rust,ignore
// 尝试`write!`，观察是否出错。若发生错误，返回相应的错误。
// 否则（没有出错）继续执行后面的语句。
write!(f, "{}", value)?;
```

另外，也可以使用 `try!`宏，其与`?`的工作方式相同，只是有点冗长(现在不被推荐)。在老Rust代码中，
你可能会看到这样的用法：

```rust,ignore
try!(write!(f, "{}", value));
```

使用`?`的情况下，对一个 `Vec` 实现 `fmt::Display` 是相当直接的：

```rust,editable
use std::fmt; // 导入 `fmt` 模块。

// 定义一个包含 `Vec` 的结构体，名为 `List`。
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // 通过索引获得tuple的值
        let vec = &self.0;

        write!(f, "[")?;

        // 对 `vec` 进行迭代，`v` 为每次迭代的值，`count` 为计数。
        for (count, v) in vec.iter().enumerate() {
            // 在调用 `write!` 前对每个元素（第一个元素除外）加上逗号。
            // 使用 `?` ，在出错的情况返回。
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // 加上配对中括号，并返回一个 `fmt::Result` 值
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

### 动手试一试：
更改程序使 vector 里面元素的索引也能够打印出来。新的结果如下：
``` rust
[0: 1, 1: 2, 2: 3]
```

### 参见：

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`try!`][try], [`vec!`][vec]

[for]: ./flow_control/for.html
[result]: ./std/result.html
[ref]: ./scope/borrow/ref.html
[struct]: ./custom_types/structs.html
[try]: ./std/result/try.html
[vec]: ./std/vec.html
