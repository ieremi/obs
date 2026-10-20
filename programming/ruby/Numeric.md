---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのNumeric]
date: 2026-10-21
---
# Numeric

**数値クラスに共通する親クラス。`Integer`、`Float`、`Rational`、`Complex` などが継承する。**

## 基本の使い方

```ruby
42.is_a?(Numeric)       # => true
3.14.is_a?(Numeric)     # => true
"42".is_a?(Numeric)     # => false
Integer.superclass     # => Numeric
Float.superclass       # => Numeric
(-3).abs               # => 3
0.zero?                # => true
```

## 具体的な数値クラスを使う

通常の計算では `Numeric` 自体を直接使うより、[[Integer]] や[[Float]]などの具体的な値を使う。

`is_a?(Numeric)` は数値クラスに属するかの確認であり、整数だけか、誤差のない値か、大小比較が可能かまで保証するものではない。用途に応じて具体的なクラスや値を確認する。

関連：[[Integer]]、[[Float]]

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：Numeric](https://docs.ruby-lang.org/en/3.4/Numeric.html)

作成日：2026-10-21
