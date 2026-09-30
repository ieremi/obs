---
aliases:
  - Rust のクロージャ
  - closure
date: 2026-09-26
tags:
  - プログラミング
  - プログラミング/Rust
---

# Rust のクロージャ

クロージャは無名関数のように使える。

```rust
let square = |x: i32| x * x;
```

周囲の変数を取り込むこともできる。

```rust
fn main() {
    let n = 10;
    let add_n = |x| x + n;
    println!("{}", add_n(5));
}
```

iterator の `map` や `filter` でも頻繁に使う。
