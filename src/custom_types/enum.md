# 枚举

`enum` 关键字可以创建类型为一组变量之一的类型。在 `struct` 中任何合法的变量在 `enum` 同样是合法的。

```rust,editable
// 隐藏未使用代码警告的属性。
#![allow(dead_code)]

// 创建一个 `enum` (枚举)类型来区分web 事件。注意，使用了名称和类型一起指定变量：
// `PageLoad != PageUnload` and `KeyPress(char) != Paste(String)`.
// 每者都不相同且相互独立。

enum WebEvent {
    // `enum` 类型可以是`unit-like`,
    PageLoad,
    PageUnload,
    // tuple,
    KeyPress(char),
    Paste(String),
    // 或者是结构体.
    Click { x: i64, y: i64 },
}


// 此函数将一个 `Person` enum 作为参数，无返回值。
fn inspect(p: Person) {
    // `enum` 的使用必须覆盖所有情形（无可辩驳的），所以使用 `match`
    // 以分支方式覆盖所有类型。
    match p {
        Person::Engineer    => println!("Is engineer!"),
        Person::Scientist       => println!("Is scientist!"),
        // 从 `enum` 内部解构 `i`
        Person::Height(i) => println!("Has a height of {}.", i),
        Person::Weight(i) => println!("Has a weight of {}.", i),
        // 将 `Info` 解构成 `name` 和 `height`。
        Person::Info { name, height } => {
            println!("{} is {} tall!", name, height);
        },
    }
}

fn main() {
    let person   = Person::Height(18);
    let amira    = Person::Weight(10);
    // `to_owned()` 从一个字符串 slice 创建一个具有所有权的 `String`。
    let dave     = Person::Info { name: "Dave".to_owned(), height: 72 };
    let rebecca  = Person::Scientist;
    let rohan    = Person::Engineer;

    inspect(person);
    inspect(amira);
    inspect(dave);
    inspect(rebecca);
    inspect(rohan);
}
```

### 参见：

[`attributes`][attributes], [`match`][match], [`fn`][fn], 和 [`String`][str]

[attributes]: ./attribute.html
[c_struct]: http://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ./flow_control/match.html
[fn]: ./fn.html
[str]: ./std/str.html
