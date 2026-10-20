---
tags: [プログラミング, Ruby, ブロック, Symbol, Proc]
aliases: [Symbolからブロックへの変換, Symbol#to_proc, Rubyのアンパサンドコロン, "&:method", "map(&:chomp)"]
date: 2026-10-20
---
# RubyのSymbolからブロックへの変換

**`map(&:chomp)` は、各要素に `chomp` メソッドを呼ぶブロックを渡す書き方。** Rubyワンライナーで出てくる `&:` は、`&` と `:メソッド名` を組み合わせたもの。

```ruby
lines = ["apple\n", "banana\n"]

lines.map(&:chomp)
# => ["apple", "banana"]

# このmapの例は、次のように書ける
lines.map { |line| line.chomp }
```

## `&` と `:` を分けて読む

| 部分 | 意味 |
| --- | --- |
| `:chomp` | メソッド名を表すSymbolオブジェクト |
| `&` | メソッド呼び出しの引数位置で、渡す値をブロックとして扱う指定 |
| `&:chomp` | SymbolをProcへ変換し、ブロックとして渡す |

`&:` 全体が一つの専用演算子なのではない。Proc以外の値をこの形で渡すと、Rubyは `to_proc` を使って変換する。Symbolの場合は **`Symbol#to_proc`** が呼ばれる。[Ruby公式：Calling Methods](https://docs.ruby-lang.org/en/3.4/syntax/calling_methods_rdoc.html)

## SymbolからProcへ

```ruby
operation = :upcase.to_proc
operation.call("ruby")
# => "RUBY"
```

`:upcase.to_proc` が返すProcは、渡された最初の引数を**レシーバー（メソッドを呼ばれる対象）**として、`upcase` を呼ぶ。

`map` は要素ごとにブロックを呼ぶため、次の流れになる。

1. `:upcase` がProcに変換される。
2. `map` が各要素をブロックへ渡す。
3. 各要素に `upcase` が呼ばれる。
4. 戻り値が新しい配列の要素になる。

```ruby
["ruby", "shell"].map(&:upcase)
# => ["RUBY", "SHELL"]
```

出典：[Ruby公式：Symbol#to_proc](https://docs.ruby-lang.org/en/3.4/Symbol.html#method-i-to_proc)

## よく使う例

| 短い書き方 | 一要素を受け取るブロックで書いた場合 |
| --- | --- |
| `values.map(&:to_s)` | `values.map { \|value\| value.to_s }` |
| `lines.map(&:chomp)` | `lines.map { \|line\| line.chomp }` |
| `words.reject(&:empty?)` | `words.reject { \|word\| word.empty? }` |
| `words.sort_by(&:length)` | `words.sort_by { \|word\| word.length }` |

```ruby
[1, 2, 3].map(&:to_s)
# => ["1", "2", "3"]

["a", "", "bc"].reject(&:empty?)
# => ["a", "bc"]

["banana", "kiwi", "fig"].sort_by(&:length)
# => ["fig", "kiwi", "banana"]
```

## 引数や複数の処理を加えるとき

各文字列をカンマで分割したい場合、呼び出す `split` へ引数を渡すので、通常のブロックで書く。

```ruby
lines.map { |line| line.split(",") }

# 前後の空白を除き、大文字へ変換
words.map { |word| word.strip.upcase }
```

`map(&:split(","))` という書き方ではない。`&:split` 自体には、カンマを固定引数として指定する機能がない。

ただし、Symbol由来のProcが引数を一切扱えないという意味ではない。複数の引数を渡すと、先頭をレシーバー、残りをメソッドの引数として使う。

```ruby
:+.to_proc.call(2, 3)
# => 5：2.+(3) に相当

[1, 2, 3].reduce(&:+)
# => 6
```

`map` の一引数ブロックへの書き換えを、複数引数を渡すすべてのメソッドへ機械的に当てはめない。

## `&method(...)` との違い

```ruby
["10", "20"].map(&:to_i)
# 各要素にto_iを呼ぶ

["10", "20"].map(&method(:Integer))
# 現在の呼び出し元に結びついたIntegerメソッドへ、各要素を引数として渡す
```

後者はMethodオブジェクトを `to_proc` でブロックへ変換する。**要素自身のメソッドを呼ぶか、別のメソッドへ要素を渡すか**が違う。`to_i` と `Integer` は不正な文字列の扱いも異なる。

### `to_i` は先頭を読み、`Integer` は整数として検証する

`String#to_i` は、先頭の空白と符号を扱い、整数として読める部分を読む。途中で読めない文字が来ると、そこまでを数値にする。最初から読めなければ0を返す。

`Integer(string)` は、前後の空白を除いた文字列を、整数の表記として解釈する。不正な場合は、通常 **`ArgumentError`** を発生させる。

| 入力文字列 `s` | `s.to_i` | `Integer(s)` | `Integer(s, 10)` |
| --- | ---: | --- | --- |
| `"123"` | 123 | 123 | 123 |
| `"123abc"` | 123 | `ArgumentError` | `ArgumentError` |
| `"abc"` | 0 | `ArgumentError` | `ArgumentError` |
| `""` | 0 | `ArgumentError` | `ArgumentError` |
| `"12.9"` | 12 | `ArgumentError` | `ArgumentError` |
| `" 42 "` | 42 | 42 | 42 |
| `"010"` | 10 | 8 | 10 |
| `"0x10"` | 0 | 16 | `ArgumentError` |
| `"08"` | 8 | `ArgumentError` | 8 |

`to_i` は既定で10進数として読む。一方、進数を省略した `Integer` は表記から進数を判断するため、先頭が `0` の `"010"` は8進数、`"0x10"` は16進数になる。**10進数の入力として検証したいなら `Integer(s, 10)` と明示する。**

出典：[Ruby公式：String#to_i](https://docs.ruby-lang.org/en/3.4/String.html#method-i-to_i)、[Kernel#Integer](https://docs.ruby-lang.org/en/3.4/Kernel.html#method-i-Integer)。

### 配列で変換すると違いが見える

```ruby
["10", "abc", "20"].map(&:to_i)
# => [10, 0, 20]

["10", "abc", "20"].map(&method(:Integer))
# => "abc" の変換時にArgumentError。配列の結果は返らない
```

点数の集計で `"abc"` を0点にしてしまうと、不正な入力と本当の0点を区別できない。不正な入力を検出したい処理では `Integer` が役立つ。

10進数を明示する場合は、引数を渡せる通常のブロックで書く。

```ruby
["010", "20"].map { |value| Integer(value, 10) }
# => [10, 20]
```

ここで比較しているのは**文字列の変換**。`Integer(12.9)` のようにFloatを渡す場合は整数部分の12を返すので、`Integer("12.9")` と区別する。

## ワンライナーでの読み方

```sh
ruby -e 'puts ARGF.each_line.map(&:chomp).sort' input.txt
```

`each_line` で行を読み、`map(&:chomp)` で各行の改行を除き、`sort` で並べ、`puts` で出力する。詳しい使用例は[[Ruby_oneliner|Ruby oneliner]]へ。

## 出典・確認

- [Ruby公式：Symbol#to_proc](https://docs.ruby-lang.org/en/3.4/Symbol.html#method-i-to_proc)
- [Ruby公式：Calling Methods](https://docs.ruby-lang.org/en/3.4/syntax/calling_methods_rdoc.html)
- 掲載例は手元のRuby 2.6.10で実行確認。

確認日：2026-10-20
