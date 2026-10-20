---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのTrueClass]
date: 2026-10-21
---
# TrueClass

**真偽値 `true` のクラス。比較や判定メソッドの結果に現れる。**

## 基本の使い方

```ruby
true.class         # => TrueClass
1 < 2              # => true
4.even?            # => true
true.to_s          # => "true"
!true              # => false
```

## 条件式の真とtrueは区別する

Rubyの条件式では `false` と `nil` 以外は真として扱われる。`0` や `""` も条件を満たすが、値そのものが `true` になるわけではない。

```ruby
0 == true  # => false
if 0
  puts "実行される"
end
```

関連：[[FalseClass]]、[[NilClass]]

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：TrueClass](https://docs.ruby-lang.org/en/3.4/TrueClass.html)

作成日：2026-10-21
