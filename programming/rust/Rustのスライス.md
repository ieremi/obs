---
aliases:
  - Rust のスライス
  - slice
date: 2026-10-01
tags:
  - プログラミング
  - プログラミング/Rust
related:
  - "[[RustのStringとstr]]"
  - "[[Rustの借用]]"
---

# Rust のスライス

```rust
fn first_word(s: &str) -> &str {
    match s.find(' ') {
        Some(i) => &s[..i],
        None => s,
    }
}

fn main() {
    let text = String::from("hello world");
    println!("{}", first_word(&text));
}
```

出力：

```text
hello
```

`&s[..i]` は新しい文字列をコピーしているのではなく、元の文字列の一部分を

$$
\boxed{\text{開始位置}+\text{長さ}}
$$

という形で参照している。これが slice の発想。

ただし Rust の文字列インデックスは**バイト境界**なので、日本語文字列を単純に `&s[..1]` と切ることはできない（UTF-8 で 1 文字 3 バイトなので panic する）。

$$
\boxed{String=\text{所有する文字列},\qquad \&str=\text{文字列へのビュー}}
$$
