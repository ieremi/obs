---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのNilClass]
date: 2026-10-21
---
# NilClass

**`nil` のクラス。値の不在や、検索で対象が見つからないことなどを表す。**

## 基本の使い方

```ruby
nil.class             # => NilClass
nil.nil?              # => true
nil.to_s              # => ""
[1, 2][10]            # => nil
{name: "Ruby"}[:age]  # => nil
nil == false          # => false
```

## nilの判定と安全な呼び出し

```ruby
name = nil
name.nil?        # => true
name&.upcase     # => nil
name || "未設定" # => "未設定"
```

`&.` はレシーバーが `nil` の場合にメソッド呼び出しを省略して `nil` を返す。`false` には同じ働きをしない。

条件式では `nil` は偽。ただし、`false` と同じ値ではない。欠けてはいけない値なら、既定値で補うだけでなく、入力の検証やHashの `fetch` を使うことも検討する。

関連：[[FalseClass]]、[[Hash]]、[[Array]]

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：NilClass](https://docs.ruby-lang.org/en/3.4/NilClass.html)

作成日：2026-10-21
