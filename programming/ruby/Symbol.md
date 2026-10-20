---
tags: [プログラミング, Ruby, 基本クラス]
aliases: [RubyのSymbol]
date: 2026-10-21
---
# Symbol

**名前や識別子を表すクラス。ハッシュのキーやメソッド名の指定によく使う。**

## 基本の使い方

```ruby
:name.class       # => Symbol
:name == :name    # => true
:name.to_s        # => "name"
"name".to_sym     # => :name
user = {name: "Ruby"}
user[:name]       # => "Ruby"
user["name"]      # => nil
["a", "b"].map(&:upcase)  # => ["A", "B"]
```

## Stringとの使い分け

文章など加工するテキストには[[String]]、プログラム内の固定の名前にはSymbolを使うことが多い。`:name` と `"name"` は異なるオブジェクトで、Hashのキーとしても区別される。

`{name: "Ruby"}` は `{:name => "Ruby"}` と同じ意味。

`&:upcase` は `Symbol#to_proc` による変換を使う。詳しくは[[RubyのSymbolからブロックへの変換]]。

関連：[[Hash]]、[[String]]

## 関連・出典

- [[RubyのIntegerと基本クラス]]：基本クラスの一覧
- [Ruby公式：Symbol](https://docs.ruby-lang.org/en/3.4/Symbol.html)

作成日：2026-10-21
