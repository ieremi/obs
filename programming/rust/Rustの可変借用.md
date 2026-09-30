---
aliases:
  - Rust の可変借用
  - mutable borrow
date: 2026-09-29
tags:
  - プログラミング
  - プログラミング/Rust
related:
  - "[[Rustの借用]]"
---

# Rust の可変借用

```rust
fn add_world(s: &mut String) {
    s.push_str(" world");
}

fn main() {
    let mut text = String::from("hello");
    add_world(&mut text);
    println!("{text}");
}
```

同じ値への可変参照は原則として同時に一つ。

$$
\boxed{\text{共有するなら読み取り、変更するなら排他的}}
$$
