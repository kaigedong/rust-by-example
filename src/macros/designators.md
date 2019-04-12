# 指示符

宏里面的参数使用一个美元符号 `$` 作为前缀，并使用一个**指示符**（*designator*）来注明类型：

```rust,editalbe
macro_rules! create_function {
    // 此宏接受一个 `ident` 指示符参数，并创建一个名为 `$func_name`
    // 的函数。
    // `ident` 指示符用于变量名或函数名
    ($func_name:ident) => (
        fn $func_name() {
            // `stringify!` 宏把 `ident` 转换成字符串。
            println!("You called {:?}()",
                     stringify!($func_name))
        }
    )
}

// 借助上述宏来创建名为 `foo` 和 `bar` 的函数。
create_function!(foo);
create_function!(bar);

macro_rules! print_result {
    // 此宏接受一个 `expr` 类型的表达式，将它转换成一个字符串，
    // 并伴随着表达式的结果。
    // `expr` 指示符用于表达式。
    ($expression:expr) => (
        // `stringify!` 把表达式转换成一个字符串，正如 stringify
        // （意思为“字符串化”） 所表达的意思那样。
        println!("{:?} = {:?}",
                 stringify!($expression),
                 $expression)
    )
}

fn main() {
    foo();
    bar();

    print_result!(1u32 + 1);

    // 回想一下，代码块也是表达式！
    print_result!({
        let x = 1u32;

        x * x + 2 * x - 1
    });
}
```

这里列出全部指示符：

* `block`
* `expr` 用于表达式
* `ident` 用于变量名或函数名
* `item`
* `pat` (**模式** *pattern*)
* `path`
* `stmt` (**语句** *statement*)
* `tt` (**令牌树** *token tree*)
* `ty` (**类型** *type*)
