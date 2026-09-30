---
aliases:
  - Rust の借用
  - borrowing
date: 2026-09-28
tags:
  - プログラミング
  - プログラミング/Rust
related:
  - "[[Rustの所有権]]"
  - "[[Rustの可変借用]]"
  - "[[RustのStringとstr]]"
---

# Rust の借用

所有権を渡さずに値を参照するには借用を使う。

```rust
fn length(s: &String) -> usize {
    s.len()
}

fn main() {
    let text = String::from("hello");
    let n = length(&text);
    println!("{text}: {n}");
}
```

核心：

$$
\boxed{\text{所有権が不要なら }T\text{ ではなく }&T}
$$
