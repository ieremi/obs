---
tags: [プログラミング, Ruby, Integer, 型変換]
aliases: [RubyのInteger, Rubyの基本クラス, Rubyの型]
date: 2026-10-21
---
# RubyのIntegerと基本クラス

**`Integer` は整数を表すクラス。`Integer("42")` は値を整数へ変換するメソッド呼び出し。** 同じ名前だが、クラスと変換メソッドを区別して読む。

## よく使う基本クラス

各クラス名のリンク先に、使い方と注意点をまとめている。数値の共通の親クラスは[[Numeric]]。

Rubyでは、数値や文字列などの値もオブジェクトで、`class` でクラスを確認できる。

| クラス | 値の例 | 用途 |
| --- | --- | --- |
| [[Integer]] | `42`, `-3` | 整数 |
| [[Float]] | `3.14` | 浮動小数点数 |
| [[String]] | `"Ruby"` | 文字列 |
| [[Symbol]] | `:name` | 名前・識別子 |
| [[Array]] | `[1, 2, 3]` | 順序のある要素の集まり |
| [[Hash]] | `{name: "Ruby", age: 30}` | キーと値の対応 |
| [[Range]] | `1..5`, `1...5` | 範囲。`..` は終端を含み、`...` は含まない |
| [[TrueClass]] / [[FalseClass]] | `true` / `false` | 真偽値 |
| [[NilClass]] | `nil` | 値がないことなどを表す |

```ruby
42.class       # => Integer
3.14.class     # => Float
"42".class     # => String
:name.class    # => Symbol
[1, 2].class   # => Array
nil.class      # => NilClass
```

条件式では **`false` と `nil` だけが偽**。`0`、空文字列 `""`、空配列 `[]` は真として扱われる。

## Integer：整数を扱う

`Integer` と `Float` は、数値を表す `Numeric` のサブクラス。

```ruby
42.is_a?(Integer)  # => true
42.is_a?(Numeric)  # => true

1_000_000         # => 1000000：桁区切りに _ を使える
0b1010            # => 10：2進数
0xff              # => 255：16進数
```

### 計算と整数同士の割り算

```ruby
7 + 2       # => 9
7 - 2       # => 5
7 * 2       # => 14
7 ** 2      # => 49：累乗
7 / 2       # => 3：整数同士の除算
7 / 2.0     # => 3.5
7.fdiv(2)   # => 3.5：浮動小数点で除算
7 % 2       # => 1：余り
7.divmod(2) # => [3, 1]：商と余り
```

整数同士の `/` は負の無限大の方向へ丸める。`-7 / 2` は `-4`。単純に小数部分を切り捨てて `-3` にする計算とは異なる。

出典：[Ruby公式：Integer](https://docs.ruby-lang.org/ja/latest/class/Integer.html)

### 判定・繰り返し・文字列化

```ruby
4.even?       # => true
4.odd?        # => false
0.zero?       # => true
(-5).abs      # => 5
255.to_s      # => "255"
255.to_s(16)  # => "ff"

3.times { |i| puts i }       # 0, 1, 2 を順に出力
1.upto(3) { |i| puts i }     # 1, 2, 3 を順に出力
3.downto(1) { |i| puts i }   # 3, 2, 1 を順に出力
```

## Integer(...) と to_i の違い

`Integer` 単独ならクラスを指す。`Integer(...)` は、`Kernel#Integer` という変換メソッドを呼ぶ。

```ruby
Integer               # => Integer：クラス
Integer("42", 10)     # => 42：10進数として変換
"42".to_i             # => 42：文字列自身のメソッド
```

`String#to_i` は先頭から整数として読める部分を使い、読めなければ0を返す。`Integer(string, 10)` は文字列を10進整数の表記として解釈し、不正な入力には `ArgumentError` を発生させる。

| 文字列 `s` | `s.to_i` | `Integer(s, 10)` |
| --- | ---: | --- |
| `"42"` | 42 | 42 |
| `"42abc"` | 42 | `ArgumentError` |
| `"abc"` | 0 | `ArgumentError` |
| `""` | 0 | `ArgumentError` |
| `"12.9"` | 12 | `ArgumentError` |
| `" 42 "` | 42 | 42 |

進数を省略すると、`Integer("010")` は8、`Integer("0x10")` は16になる。**10進数の入力検証には `Integer(s, 10)` を使う。**

数値を渡す場合の挙動は別で、`Integer(12.9)` は12を返す。小数を許さない入力検証として、あらゆるオブジェクトにそのまま使えるわけではない。

出典：[Ruby公式：Kernel#Integer](https://docs.ruby-lang.org/en/3.4/Kernel.html#method-i-Integer)、[String#to_i](https://docs.ruby-lang.org/en/3.4/String.html#method-i-to_i)

## Float・String・Array・Hashの基本操作

```ruby
# Float：小数を扱う
Float("3.14")           # => 3.14
3.14.round(1)           # => 3.1

# String：文字列を加工する
" Ruby ".strip          # => "Ruby"
"a,b,c".split(",")      # => ["a", "b", "c"]
"ruby".upcase           # => "RUBY"

# Array：要素を変換・抽出・集計する
[1, 2, 3].map { |n| n * 2 }  # => [2, 4, 6]
[1, 2, 3].select(&:odd?)      # => [1, 3]
[1, 2, 3].sum                # => 6

# Hash：キーで値を取り出す
user = {name: "Ruby", age: 30}
user[:name]                  # => "Ruby"
user[:email]                 # => nil
user.fetch(:email, "未登録")  # => "未登録"
```

`{name: "Ruby"}` の `name:` はSymbolキー `:name` の省略記法。`user[:name]` と `user["name"]` は別のキーを参照する。

`map(&:odd?)` のような `&:メソッド名` の読み方は[[RubyのSymbolからブロックへの変換]]を参照。

## `Float(...)` などの変換メソッド

クラス名と同じ名前の変換メソッドが用意されているものがある。`Float("3.14")` は `Kernel#Float` の呼び出し。元の値を受け取り、変換結果を返す。

| 書き方 | 詳しい説明 |
| --- | --- |
| `Integer("42", 10)` | [[Integer]]：進数、`to_i`との違い、変換失敗の扱い |
| `Float("3.14")` | [[Float]]：文字列・指数表記、`to_f`との違い、入力検証 |
| `String(42)` | [[String]]：文字列化と`nil`の扱い |
| `Array(value)` | [[Array]]：配列化、`[value]`や`Array.new`との違い |
| `Hash(value)` | [[Hash]]：Hashへの変換、`Hash[...]`や`to_h`との違い |

すべてのクラスに同名の変換メソッドがあるわけではない。例えばSymbolには `"name".to_sym`、Rangeの作成には `1..5` や `Range.new(1, 5)` を使う。

出典：[Ruby公式：Kernelの変換メソッド](https://docs.ruby-lang.org/en/3.4/Kernel.html#converting)

## 関連・出典

- [[Ruby_oneliner|Ruby oneliner]]：文字列の数値変換や配列・ハッシュを使う実例
- [[RubyのSymbolからブロックへの変換]]：`map(&:to_i)` と `map(&method(:Integer))` の違い
- [Ruby公式：Numeric](https://docs.ruby-lang.org/ja/latest/class/Numeric.html)
- [Ruby公式：Float](https://docs.ruby-lang.org/en/3.4/Float.html)
- [Ruby公式：String](https://docs.ruby-lang.org/en/3.4/String.html)
- [Ruby公式：Array](https://docs.ruby-lang.org/en/3.4/Array.html)
- [Ruby公式：Hash](https://docs.ruby-lang.org/en/3.4/Hash.html)

確認日：2026-10-21
