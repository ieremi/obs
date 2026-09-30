---
aliases:
  - Rust の所有権
  - ownership
date: 2026-09-27
tags:
  - プログラミング
  - プログラミング/Rust
related:
  - "[[Rustの借用]]"
  - "[[Rustの可変借用]]"
---

# Rust の所有権

```rust
let a = String::from("hello");
let b = a;
```

`String` の所有権は `a` から `b` へ move する。これにより二重解放をコンパイル時に防ぐ。

複製したい場合：

```rust
let b = a.clone();
```

核心：

$$
\boxed{\text{値には原則として所有者が一つ}}
$$
