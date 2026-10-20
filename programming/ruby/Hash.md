---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのHash]
date: 2026-10-21
---
# Hash

**キーと値の対応を表すクラス。名前を指定して値を取り出す。**

## 基本の使い方

```ruby
user = {name: "Ruby", age: 30}
user[:name]                    # => "Ruby"
user["name"]                   # => nil：Symbolとは別のキー
user[:email]                   # => nil
user.fetch(:email, "未登録")    # => "未登録"
user.key?(:name)               # => true
user.keys                     # => [:name, :age]
user.values                   # => ["Ruby", 30]
user[:age] = 31                # 値を更新
user.each { |key, value| puts "#{key}: #{value}" }
```

## キーがない場合とnilを区別する

```ruby
settings = {token: nil}
settings[:token]        # => nil
settings[:missing]      # => nil
settings.key?(:token)   # => true
settings.key?(:missing) # => false
settings.fetch(:missing) # => KeyError
```

既定のHashでは、`[]` だけではキーがない場合と値が `nil` の場合を区別できない。存在確認には `key?`、必須のキーには `fetch` を使う。

## 件数を数える

```ruby
counts = Hash.new(0)
["a", "b", "a"].each { |word| counts[word] += 1 }
counts  # => {"a"=>2, "b"=>1}
```

`Hash.new([])` の既定値は、存在しないキーの間で同じ配列を共有する。キーごとに配列を作るなら `Hash.new { |hash, key| hash[key] = [] }` と書く。

関連：[[Symbol]]、[[Array]]、[[NilClass]]

## `Hash(value)`：値をHashに変換する

```ruby
Hash({name: "Ruby"}) # => {:name=>"Ruby"}
Hash(nil)            # => {}
Hash([])             # => {}
Hash("name=Ruby")    # TypeError
Hash([[:name, "Ruby"]]) # TypeError
```

`Hash(...)` は `Kernel#Hash` という変換メソッド。対象の `to_hash` を使う。`nil` と空配列は特別に空のHashになるが、キーと値のペアを並べた配列を一般に変換するメソッドではない。

### ペアの配列には `to_h` または `Hash[...]`

```ruby
pairs = [[:name, "Ruby"], [:age, 30]]
pairs.to_h   # => {:name=>"Ruby", :age=>30}
Hash[pairs]  # => {:name=>"Ruby", :age=>30}
```

| 書き方 | 目的 |
| --- | --- |
| `Hash(value)` | Hashへの変換。`nil` は `{}` |
| `pairs.to_h` | キーと値のペアの配列からHashを作る |
| `Hash[pairs]` | ペアの配列からHashを作るクラスメソッド |
| `Hash.new(0)` | キーがないときの既定値を0にして作成 |

`Hash(...)` と `Hash[...]` は別のメソッド。括弧の種類で意味が変わる。

### nilなら空の設定として扱う例

```ruby
def read_timeout(options)
  options = Hash(options)
  options.fetch(:timeout, 30)
end

read_timeout(nil)            # => 30
read_timeout({timeout: 10})  # => 10
```

`Hash(existing_hash)` は複製を保証しない。また、キーの型や値の正当性まで検証するものではない。

出典：[Ruby公式：Kernel#Hash](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/Hash.html)、[Hash.\[\]](https://docs.ruby-lang.org/en/3.4/Hash.html#method-c-5B-5D)

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：Hash](https://docs.ruby-lang.org/en/3.4/Hash.html)

作成日：2026-10-21
