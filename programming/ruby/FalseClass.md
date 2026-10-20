---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのFalseClass]
date: 2026-10-21
---
# FalseClass

**真偽値 `false` のクラス。比較が成立しない場合などに使う。**

## 基本の使い方

```ruby
false.class        # => FalseClass
1 > 2              # => false
3.even?            # => false
false.to_s         # => "false"
!false             # => true
```

## falseとnil

条件式では `false` と `nil` のどちらも偽として扱われる。ただし、`false` は否定的な判定結果、`nil` は値がないことなどを表すために使い分ける。

```ruby
false.nil?        # => false
false == nil      # => false
false || "既定値" # => "既定値"
```

`||` や `||=` は `nil` だけでなく `false` も既定値に置き換える。設定値で `false` を保持したいときは、`nil?` やHashの `fetch` などで意図を明示する。

関連：[[TrueClass]]、[[NilClass]]、[[Hash]]

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：FalseClass](https://docs.ruby-lang.org/en/3.4/FalseClass.html)

作成日：2026-10-21
