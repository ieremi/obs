---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのString]
date: 2026-10-21
---
# String

**文字列を表すクラス。文字列の検索・分割・置換・連結に使う。**

## 基本の使い方

```ruby
"Ruby".class             # => String
"Ruby".length            # => 4
" Ruby ".strip           # => "Ruby"
"ruby".upcase            # => "RUBY"
"a,b,c".split(",")       # => ["a", "b", "c"]
"apple".gsub("p", "P")   # => "aPPle"
"Ruby".include?("ub")    # => true
"42".to_i               # => 42
"".empty?                # => true
```

## 展開と破壊的変更

```ruby
name = "Ruby"
"Hello, #{name}"  # => "Hello, Ruby"
'Hello, #{name}'  # => "Hello, #{name}"

text = "ruby"
text.upcase      # => "RUBY"：text は変わらない
text.upcase!     # => "RUBY"：text 自体を変更
```

`!` 付きメソッドは、対応するメソッドより注意が必要な操作を示す慣習。すべてのメソッドに `!` 版があるわけではなく、`<<` のように `!` がなくても元の文字列を変更するものがある。

関連：[[Symbol]]、[[Array]]、[[Integer]]

## `String(value)`：値を文字列に変換する

```ruby
String(42)     # => "42"
String(3.14)   # => "3.14"
String(:name)  # => "name"
String(true)   # => "true"
String(nil)    # => ""
```

`String(...)` は `Kernel#String` の呼び出し。文字列を返すので、数値の42と文字列の `"42"` を区別する。

```ruby
price = 42
text = String(price)
text + "円"  # => "42円"
price        # => 42：元の値は変わらない
42.to_s      # => "42"：数値自身にも変換メソッドがある
```

通常の表示には `to_s` や `"#{price}円"` もよく使う。`String(nil)` は空文字列になるため、必須入力の欠落を検出したい場合は変換前に `nil?` を調べる。

`String(...)` はJSONのシリアライズではない。HashやArrayをJSON形式にしたい場合はJSONライブラリを使う。

出典：[Ruby公式：Kernel#String](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/String.html)

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：String](https://docs.ruby-lang.org/en/3.4/String.html)

作成日：2026-10-21
