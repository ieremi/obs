---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのArray]
date: 2026-10-21
---
# Array

**順序のある要素の集まりを表すクラス。添字は0から始まる。**

## 基本の使い方

```ruby
values = [10, 20, 30]
values[0]                     # => 10
values[-1]                    # => 30
values[10]                    # => nil
values.length                 # => 3
values.map { |n| n * 2 }       # => [20, 40, 60]
values.select { |n| n >= 20 }  # => [20, 30]
values.sum                    # => 60
[1, 1, 2].uniq                # => [1, 2]
[1, nil, 2].compact           # => [1, 2]
["a", "b"].join(",")         # => "a,b"
```

## 要素の追加と繰り返し

```ruby
values = [1, 2]
values << 3                    # values 自体が [1, 2, 3] になる
values.each { |n| puts n }      # 各要素を出力
values.map { |n| n * 2 }        # 新しい配列を返す
```

`each` は各要素について処理を行い、通常は元の配列を返す。`map` はブロックの戻り値を集めた新しい配列を返す。

関連：[[Hash]]、[[Range]]、[[RubyのSymbolからブロックへの変換]]

## `Array(value)`：値を配列として扱う

```ruby
Array(42)             # => [42]
Array("a,b")          # => ["a,b"]
Array(nil)            # => []
Array([1, 2])         # => [1, 2]
Array(1..3)           # => [1, 2, 3]
Array({name: "Ruby"}) # => [[:name, "Ruby"]]
```

`Array(...)` は `Kernel#Array` という変換メソッド。対象の `to_ary`、次に `to_a` を使い、変換できない値は一要素の配列に包む。`nil` は空配列になる。

### `[value]` や `Array.new` との違い

```ruby
value = [1, 2]
Array(value)  # => [1, 2]
[value]       # => [[1, 2]]

Array(3)      # => [3]：値を配列化
Array.new(3)  # => [nil, nil, nil]：要素数を指定して作成
"a,b".split(",") # => ["a", "b"]：文字列の分割は別の操作
```

`Array(value)` は複製を保証しない。既存の配列を渡すとその配列自体が返るため、戻り値を変更すると元の配列にも反映される。

### 一つの値または配列を受け取る例

```ruby
def normalize_tags(tags)
  Array(tags).map { |tag| tag.to_s.strip }
end

normalize_tags("ruby")          # => ["ruby"]
normalize_tags(["ruby", " cli "]) # => ["ruby", "cli"]
normalize_tags(nil)             # => []
```

Hashもキーと値のペアの配列へ変換されるため、受け付ける入力の種類は用途に合わせて決める。

出典：[Ruby公式：Kernel#Array](https://docs.ruby-lang.org/en/3.4/Kernel.html#method-i-Array)

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：Array](https://docs.ruby-lang.org/en/3.4/Array.html)

作成日：2026-10-21
