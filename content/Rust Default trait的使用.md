---
title: 
date: 2024-11-22T16:10
tags:
  - Rust
---

在 Rust 中，`#[derive(Default)]`  是一个派生宏（derive macro），它允许你为自定义的结构体或枚举自动实现 `Default` trait。`Default` trait 提供了一个默认的实例，通常用于初始化结构体或枚举的默认值。Rust 已经为内置的大部分类型实现了 Default

```rust
#[derive(Default)]
struct MyStruct {
    field1: i32,
    field2: String,
    field3: Option<bool>,
}

fn main() {
    let default_instance = MyStruct::default();
    println!("{:?}", default_instance);
}
```

在这个例子中，`MyStruct`  的所有字段都实现了  `Default` trait：

- `i32`  实现了  `Default`，默认值为  `0`。
- `String`  实现了  `Default`，默认值为空字符串  `""`。
- `Option<bool>`  实现了  `Default`，默认值为  `None`。
  因此，`MyStruct::default()`  会返回一个  `MyStruct`  实例，其中  `field1`  为  `0`，`field2`  为空字符串，`field3`  为  `None`。

如果希望为某些字段提供自定义的默认值，你可以手动实现  `Default` trait，而不是使用  `#[derive(Default)]`。

```rust
struct MyStruct {
    field1: i32,
    field2: String,
    field3: Option<bool>,
}

impl Default for MyStruct {
    fn default() -> Self {
        MyStruct {
            field1: 42,
            field2: String::from("Hello, world!"),
            field3: Some(true),
        }
    }
}

fn main() {
    let default_instance = MyStruct::default();
    println!("{:?}", default_instance);
}
```
