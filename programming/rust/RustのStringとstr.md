---
aliases:
  - "Rust の String と &str"
  - "String と &str"
date: 2026-09-30
tags:
  - プログラミング
  - プログラミング/Rust
related:
  - "[[Rustの借用]]"
  - "[[Rustのスライス]]"
---

# Rust の String と &str

`String` は文字列データを所有し、`&str` は文字列スライスとして参照する。

```rust
fn print_name(name: &str) {
    println!("{name}");
}

fn main() {
    let name = String::from("Taro");
    print_name(&name);
}
```

読むだけの関数では `&String` より `&str` をまず検討すると柔軟。
