---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのFloat]
date: 2026-10-21
---
# Float

**浮動小数点数を表すクラス。小数を含む計算に使い、`Numeric` を継承する。**

## 基本の使い方

```ruby
3.14.class       # => Float
7 / 2.0          # => 3.5
7.fdiv(2)        # => 3.5
Float("3.14")    # => 3.14
3.14.round(1)    # => 3.1
3.14.floor       # => 3
3.14.ceil        # => 4
3.99.to_i        # => 3
(-3.99).to_i     # => -3
```

## 小数の誤差

```ruby
0.1 + 0.2 == 0.3  # => false
```

多くの10進小数は2進浮動小数点で正確に表せない。計算途中で小さな誤差が生じるため、近似値の比較では用途に応じた許容誤差を決める。

`Float("abc")` は `ArgumentError`。`"abc".to_f` は `0.0` を返すので、入力検証では違いに注意する。

関連：[[Integer]]、[[Numeric]]

## `Float(value)`：値を浮動小数点数に変換する

```ruby
text = "3.14"          # 文字列。まだ計算に使う数値ではない
number = Float(text)   # 文字列を解釈して、Floatの値を返す
number                # => 3.14
number.class          # => Float
number * 2            # => 6.28
text                  # => "3.14"：元の変数は変わらない
```

`Float` はメソッド名、括弧内の `text` は引数、変換された `3.14` は戻り値。`# =>` は結果を説明するコメントであり、出力する命令ではない。画面に出すなら `puts number` と書く。

`Float` 単独はクラスを指し、`Float(...)` は `Kernel#Float` の呼び出し。`Float.new(...)` という書き方で生成するものではない。

### どのような値を渡せるか

```ruby
Float("3.14")    # => 3.14
Float("42")      # => 42.0
Float(42)        # => 42.0
Float(3.14)      # => 3.14
Float(" 3.14 ")  # => 3.14：前後の空白は許される
Float("-2.5")    # => -2.5
Float("1e3")     # => 1000.0：指数表記
Float("1e-2")    # => 0.01
```

### `to_f` との違いと失敗時の扱い

| 入力 `s` | `Float(s)` | `s.to_f` |
| --- | --- | --- |
| `"3.14"` | `3.14` | `3.14` |
| `"3.14kg"` | `ArgumentError` | `3.14` |
| `"abc"` | `ArgumentError` | `0.0` |
| `""` | `ArgumentError` | `0.0` |

`Float(nil)` は `TypeError`。表の例外は戻り値ではなく、その場で処理が中断されることを示す。`to_f` は数値として読める先頭部分を使うため、不正な入力と本当の0を区別したい処理には `Float(...)` が向いている。

```ruby
Float("abc", exception: false)  # => nil
Float(nil, exception: false)    # => nil
Float("0", exception: false)    # => 0.0
```

`exception: false` はキーワード引数。通常の変換失敗を例外ではなく `nil` として受け取る。

### 入力を受けて計算する例

```ruby
input = "12.5"  # フォームやファイルから読んだ文字列を想定
weight = Float(input, exception: false)

if weight.nil?
  puts "数値を入力してください"
elsif !weight.finite? || weight < 0
  puts "有限の0以上の数値を入力してください"
else
  puts weight * 2
end
```

変換の成功と、用途に合う値かどうかは別に確認する。極端に大きい値は無限大になりうるため、この例では `finite?` も確認している。

出典：[Ruby公式：Kernel#Float](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/Float.html)

## 有効数字・小数点以下の桁数を指定する

**表示する有効数字は `format("%.3g", value)` のように指定できる。Float自体の保存精度を設定する引数はない。**

### 有効数字を3桁にして表示する

有効数字は、最初の0でない数字から数える桁数。小数点以下の桁数とは異なる。

```ruby
x = Float("3.141592")
format("%.3g", x)        # => "3.14"
format("%.3g", 12345.0)  # => "1.23e+04"
format("%.3g", 1.2)      # => "1.2"
format("%#.3g", 1.2)     # => "1.20"：末尾の0も残す
```

`g` の `.3` は有効数字3桁を意味する。値の大きさによって指数表記になる。末尾の0は通常省略され、`#` を付けると残せる。

`format` の戻り値は[[String]]。元の `x` の値や計算精度は変わらない。表示するには `puts format("%.3g", x)` と書く。

### 小数点以下を3桁にそろえる

```ruby
format("%.3f", 3.141592)  # => "3.142"
format("%.3f", 1.2)       # => "1.200"
```

`f` の `.3` は小数点以下3桁。有効数字3桁とは指定する基準が違う。

出典：[Ruby公式：書式指定](https://docs.ruby-lang.org/en/3.4/format_specifications_rdoc.html)

### 計算に使う値を丸める

```ruby
x = 3.141592
rounded = x.round(3)
rounded        # => 3.142
rounded.class  # => Float
x              # => 3.141592
```

`round(3)` は小数点以下3桁に丸めた数値を返す。有効数字3桁の指定ではない。Floatは `1.200` の末尾の0のような表示上の桁数を保持しないため、桁をそろえる表示には `format` を使う。

### Float自体の精度

Floatは通常、倍精度浮動小数点で、10進数の有効数字はおよそ15〜16桁。`Float::DIG` で保証される10進有効桁数の目安を確認でき、一般的には15を返す。この定数は精度を変更する設定ではない。

`Float("3.14", 3)` のように桁数を渡すことはできない。より多くの10進桁を扱う計算には `BigDecimal` などを検討する。

出典：[Ruby公式：Float・DIG・round](https://docs.ruby-lang.org/en/3.4/Float.html)

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：Float](https://docs.ruby-lang.org/en/3.4/Float.html)

作成日：2026-10-21
