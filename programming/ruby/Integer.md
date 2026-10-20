---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのInteger]
date: 2026-10-21
---
# Integer

**整数を表すクラス。`Numeric` を継承する。**

## 基本の使い方

```ruby
42.class       # => Integer
7 / 2          # => 3
7 / 2.0        # => 3.5
-7 / 2         # => -4
7 % 2          # => 1
7.divmod(2)    # => [3, 1]
2 ** 10        # => 1024
4.even?        # => true
(-5).abs       # => 5
255.to_s(16)   # => "ff"
3.times { |i| puts i }  # 0, 1, 2 を出力
```

## 文字列から整数に変換する

```ruby
Integer("42", 10)     # => 42
"42abc".to_i          # => 42
Integer("42abc", 10)  # => ArgumentError
```

`Integer` はクラス名だが、`Integer(...)` は `Kernel#Integer` メソッドの呼び出し。入力を10進整数として検証するなら `Integer(s, 10)` を使う。進数を省略すると `Integer("010")` は8になる。

整数同士の `/` は負の無限大方向へ丸める。小数の商には `fdiv` またはFloatの引数を使う。

関連：[[Float]]、[[Numeric]]、[[RubyのSymbolからブロックへの変換]]

変換の出典：[Kernel#Integer](https://docs.ruby-lang.org/en/3.4/Kernel.html#method-i-Integer)

## `Integer(value, base = 0, exception: true)` を詳しく読む

```ruby
text = "42"
number = Integer(text, 10)
number          # => 42
number.class    # => Integer
number + 8      # => 50
text            # => "42"：元の文字列は変わらない
```

`Integer` は変換メソッド名、`text` は変換対象、`10` は文字列を読む進数。戻り値の整数を `number` に代入して計算している。`# =>` は結果を示すコメントで、表示するには `puts number` と書く。

### 引数と戻り値

| 引数 | 意味 |
| --- | --- |
| `value` | 変換する文字列や数値 |
| `base` | 文字列用の進数。0または2〜36。省略時は0で、接頭辞から判断 |
| `exception:` | 既定は `true`。`false` にすると通常の変換失敗で `nil` を返す |

```ruby
Integer("42", 10)     # => 42
Integer("  -42 ", 10) # => -42
Integer("1010", 2)    # => 10
Integer("ff", 16)     # => 255
Integer("010")        # => 8：進数を自動判定
Integer("010", 10)    # => 10：10進数を明示
Integer("0x10")       # => 16
Integer("08")         # ArgumentError：8進数として解釈できない
Integer("08", 10)     # => 8
```

通常の10進入力には `Integer(text, 10)` と書くと意図が明確。`base` は文字列用なので、数値を渡す `Integer(42)` には進数を付けない。

### 数値と文字列では小数の扱いが違う

```ruby
Integer(12.9)       # => 12
Integer(-12.9)      # => -12：0の方向へ切り捨て
Integer("12.9", 10) # ArgumentError
```

数値の変換では小数部を落とすため、`Integer(value)` の成功だけで「元の値に小数部がなかった」とは判断できない。

### 不正な値を検出する

```ruby
Integer("42abc", 10)  # ArgumentError
Integer("", 10)       # ArgumentError
Integer(nil)          # TypeError

Integer("abc", 10, exception: false) # => nil
Integer(nil, exception: false)       # => nil
Integer("0", 10, exception: false)   # => 0
```

`exception: false` なら、変換失敗の `nil` と正しい入力の `0` を区別できる。`"abc".to_i` は0なので、この区別が失われる。

### 件数の入力を検証する例

```ruby
input = "3"
count = Integer(input, 10, exception: false)

if count.nil?
  puts "整数を入力してください"
elsif count < 1
  puts "1以上を入力してください"
else
  puts "合計: #{count * 500}円"
end
```

変換できても負数などが許されるとは限らないため、用途に応じて範囲を検証する。

```ruby
["10", "20", "30"].map { |s| Integer(s, 10) }
# => [10, 20, 30]
```

配列の各文字列にも使える。不正な要素があれば、その要素の変換時に例外が発生する。

出典：[Ruby公式：Kernel#Integer](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/Integer.html)

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：Integer](https://docs.ruby-lang.org/en/3.4/Integer.html)

作成日：2026-10-21
