---
tags: [プログラミング, Ruby, シェル, テキスト処理]
aliases: [Ruby oneliner, Rubyワンライナー, Rubyのワンライナー, ruby one-liner]
date: 2026-10-20
---
# Ruby oneliner

**Rubyのワンライナーは、`ruby -e 'コード'` で短いRubyプログラムをシェルから実行する書き方。** 行の抽出・置換から、配列・ハッシュを使った集計、CSV・JSONの処理まで書ける。

## まず `-e`

```sh
ruby -e 'puts 1 + 2'
```

```text
3
```

Rubyコードは通常シングルクォートで囲み、`$_` や `$F` などをシェルが展開しないようにする。

## 行処理に使うオプション

| 指定 | 動作 |
| --- | --- |
| `-e 'コード'` | 指定したコードを実行 |
| `-n` | 入力を一行ずつ読み、各行にコードを実行 |
| `-p` | `-n` と同様に処理し、各回の最後に `$_` を自動出力 |
| `-a` | `-n` / `-p` と組み合わせ、行を分割して `$F` に格納 |
| `-Fパターン` | `-a` の分割用パターンを指定 |
| `-l` | `-n` / `-p` で行末を自動処理し、出力側の区切りも設定 |
| `-rライブラリ` | 実行前にライブラリを読み込む |
| `-i.bak` | 指定ファイルを直接編集し、元の内容を `.bak` に保存 |

例えば `-ane` は `-a -n -e` をまとめた指定。まずは **抽出なら `-n`、各行を変換して出すなら `-p`、列を使うなら `-a`** と覚える。

出典：[Ruby公式：Command-Line Options](https://docs.ruby-lang.org/en/3.4/ruby/options_md.html)

## `-n`：条件に合う行を出す

```sh
ruby -ne 'print if /ERROR/' app.log
```

`$_` が現在の入力行。ここでの `/ERROR/` は `$_` に対する正規表現マッチになり、引数なしの `print` は `$_` を出力する。

ファイルを指定しない場合は標準入力を読むため、パイプでも使える。

```sh
some_command | ruby -ne 'print if /ERROR/'
```

## `-p`：置換して各行を出す

```sh
ruby -pe 'gsub(/red/, "green")' input.txt
```

`-n` / `-p` の行処理では、この形の `gsub` は `$_` を置換する。`-p` が処理後の行を自動で出力するので、さらに `print` を書くと二重出力になりうる。

明示的に書くなら、次の形も使える。

```sh
ruby -pe '$_.gsub!(/red/, "green")' input.txt
```

## `-a`：列を取り出す

以下を `scores.txt` とする。

```text
name score team
Alice 80 red
Bob 65 blue
Carol 90 red
```

```sh
ruby -ane 'puts $F[0] if $. > 1' scores.txt
```

```text
Alice
Bob
Carol
```

| Rubyでの表記 | 意味 | awkとの比較 |
| --- | --- | --- |
| `$_` | 現在の行全体 | `$0` |
| `$F[0]` | 第1フィールド | `$1` |
| `$F[1]` | 第2フィールド | `$2` |
| `$F[-1]` | 最後のフィールド | `$NF` |
| `$F.length` | 分割したフィールドの数 | `NF` |
| `$.` | 現在の入力行番号 | 単一ファイルなら `NR` に対応 |

**Rubyの配列の添字は0始まり。** `$. > 1` は、この単一ファイル例でヘッダーを除く条件。標準では空白で分割する。

```sh
# 単純なカンマ区切りの第1列
ruby -F, -ane 'puts $F[0]' input.txt
```

`-F,` だけでは、引用符付きの一般的なCSVを正しく扱えない。

## 数値で条件を付ける

```sh
ruby -ane 'puts $F[0] if $. > 1 && $F[1].to_i >= 80' scores.txt
```

```text
Alice
Carol
```

フィールドは文字列なので、整数として比較するには `to_i`、小数なら `to_f` などを使う。`to_i` は不正な入力を厳密に検証する関数ではないため、入力の正当性も確認したい場合は `Integer(...)` などを検討する。

## 全行の合計を出す

```sh
ruby -ane 'BEGIN { total = 0 }; total += $F[1].to_i if $. > 1; END { puts total }' scores.txt
```

```text
235
```

`BEGIN` は入力処理前、`END` は入力処理後に実行する。初期化・各行の処理・最後の出力を分けると、[[awk]]の集計と対応させやすい。

## 出現順を保つ重複除去

```sh
ruby -ne 'BEGIN { seen = {} }; unless seen[$_]; print; seen[$_] = true; end' input.txt
```

ハッシュに既出の行を記憶し、初めての行だけを出力する。[[uniq]]と違い、離れた重複も扱える。異なる行が増えるほどメモリーを使い、この例では改行も比較対象になる。

## sort・uniq・cut・grepをRubyで書く

以下は、各コマンドの**基本的なテキスト処理をRubyで書いた例**。通常の改行区切りのテキストを想定する。ロケール、最終行の改行、正規表現、終了ステータスなどを含め、全オプションを互換にするものではない。

ファイル名を省略すれば、いずれも標準入力を処理できる。

### sort：行を並べ替える

```sh
# sort input.txt に相当する基本的な文字列ソート
ruby -e 'puts ARGF.each_line.map(&:chomp).sort' input.txt

# sort -r：逆順
ruby -e 'puts ARGF.each_line.map(&:chomp).sort.reverse' input.txt

# 単純な数値だけの行を、数値として昇順にする
ruby -e 'puts ARGF.each_line.map(&:chomp).sort_by { |line| line.to_f }' numbers.txt

# sort -u：並べ替えて重複除去
ruby -e 'puts ARGF.each_line.map(&:chomp).sort.uniq' input.txt
```

`map(&:chomp)`（[[RubyのSymbolからブロックへの変換]]）で行末の改行を外し、`puts` で行として出力する。Rubyの文字列比較は、OSの `sort` がロケールに従って行う照合と同じとは限らない。

この例は全行をメモリーに載せる。外部ソートを使える専用の `sort` と、大量データでのメモリー使用量は異なる。数値の例の `to_f` も、`sort -n` の数値解釈すべてを再現するものではない。

### uniq：隣り合う同じ行だけをまとめる

```sh
# uniq：直前の行と比較
ruby -ne 'BEGIN { previous = nil }; key = $_.chomp; print if key != previous; previous = key' input.txt
```

入力が `apple, apple, banana, apple` の順なら、出力は `apple, banana, apple` の順。最後の `apple` は隣接していないため残る。

**`Array#uniq` は入力全体の重複を除くので、コマンドの `uniq` とは違う。** 隣接するグループ単位の処理には、`chunk` も使える。

```sh
# uniq -c：連続するグループの件数
ruby -e 'ARGF.each_line.chunk { |line| line.chomp }.each { |line, group| printf "%7d %s\n", group.size, line }' input.txt

# uniq -d：2行以上連続するグループだけ一行出す
ruby -e 'ARGF.each_line.chunk { |line| line.chomp }.each { |line, group| puts line if group.size > 1 }' input.txt

# uniq -u：1行だけのグループを出す
ruby -e 'ARGF.each_line.chunk { |line| line.chomp }.each { |line, group| puts line if group.size == 1 }' input.txt
```

`chunk` は同じキーが続く部分をまとめる。この例では一つの連続グループを配列として保持する。ファイル全体の出現数で判断したい場合は、先に並べ替えるか、ハッシュで集計する。[Ruby公式：Enumerable#chunk](https://docs.ruby-lang.org/en/3.4/Enumerable.html#method-i-chunk)

### cut：列や文字の範囲を取り出す

まず、単純なカンマ区切りから第1・第3フィールドを出す。

```sh
ruby -ne 'puts $_.chomp.split(",", -1).values_at(0, 2).compact.join(",")' input.txt
```

`split(",", -1)` は末尾の空フィールドも残す。`values_at(0, 2)` は第1・第3フィールドを選び、`compact` は存在しないフィールドの `nil` を除く。最後にカンマで連結する。

`cut -d, -f1,3` は、カンマのない行を通常そのまま出す。この挙動も入れるなら次の形になる。

```sh
ruby -ne 'puts($_.include?(",") ? $_.chomp.split(",", -1).values_at(0, 2).compact.join(",") : $_.chomp)' input.txt
```

例えば `Alice,80,red` は `Alice,red`、`solo` はそのまま `solo` になる。引用符付きCSVの処理には、前述の `CSV` ライブラリを使う。

第2〜第4文字の抽出は、0始まりの位置と長さで書ける。

```sh
# cut -c2-4 に相当する文字範囲の抽出
ruby -ne 'puts $_.chomp[1, 3].to_s' input.txt
```

Rubyの文字列スライスは文字列のエンコーディングに従う。`cut -b` のバイト抽出や、実装による `cut -c` の挙動と同一とは限らない。[Ruby公式：String](https://docs.ruby-lang.org/en/3.4/String.html)

### grep：一致する行を出す

```sh
# grep -E 'ERROR'：正規表現に一致する行
ruby -ne 'print if /ERROR/' app.log

# grep -Ei 'error'：大文字・小文字を無視
ruby -ne 'print if /error/i' app.log

# grep -Ev 'ERROR'：一致しない行
ruby -ne 'print unless /ERROR/' app.log

# grep -En 'ERROR'：行番号付き（単一ファイルの例）
ruby -ne 'print "#{$.}:#{$_}" if /ERROR/' app.log

# grep -F 'a.b'：正規表現ではなく固定文字列
ruby -ne 'print if $_.include?("a.b")' app.log
```

件数を数えるなら、カウンターを使う。

```sh
# grep -c 'ERROR' に相当する一致行数の出力（単一ファイル）
ruby -ne 'BEGIN { count = 0 }; count += 1 if /ERROR/; END { puts count }' app.log
```

Rubyと `grep` では正規表現の仕様が異なる。複数ファイル時のファイル名表示や行番号も別途実装が必要。また、これらのRuby例は、一致する行がなくても通常は終了ステータス0となる。`grep` の「一致なしは1」を前提にしたシェル条件式へ、そのまま置き換えない。

## JSONを処理する

```sh
ruby -rjson -e 'JSON.parse(STDIN.read).each { |row| puts row.fetch("name") }' < data.json
```

入力例：

```json
[{"name":"Alice"},{"name":"Bob"}]
```

出力は `Alice` と `Bob`。JSON全体を読み込む例なので、巨大な入力ではメモリー使用量に注意する。[Ruby公式：JSON](https://docs.ruby-lang.org/en/3.4/JSON.html)

## CSVを処理する

```sh
ruby -rcsv -e 'CSV.new(ARGF, headers: true).each { |row| puts row["name"] }' data.csv
```

`CSV` に入力を渡すことで、引用符内のカンマや改行もCSVとして解釈する。`ARGF` は、指定された入力ファイルや標準入力を読むためのオブジェクト。この例は `name` ヘッダーのある単一のCSVを想定する。[Ruby CSV：CSV.new](https://ruby.github.io/csv/CSV.html)

## ファイルを直接編集する

```sh
# 先に標準出力で結果を見る
ruby -pe 'gsub(/old/, "new")' input.txt

# 元ファイルをinput.txt.bakに残して編集
ruby -i.bak -pe 'gsub(/old/, "new")' input.txt
```

`-i` は元ファイルを書き換える。バックアップの拡張子を付けない場合はバックアップを作らない。同じファイルを入力とシェルの `>` の出力先に指定すると、読み込み前に空になることがあるため、直接編集には上記の仕組みを使う。

## 実装・確認

掲載した抽出・置換・合計・重複除去・JSONの基本例は、手元のRuby 2.6.10で実行確認。利用できるオプションやライブラリは環境によって異なるため、`ruby --version`・`ruby --help`・対応する版の公式資料を確認する。

sort・uniq・cut・grepの基本例は、改行付きの入力で手元の各コマンドと出力を比較した。`uniq -c` は件数前の空白幅を除いて確認。

## 関連・出典

- [[RubyのSymbolからブロックへの変換]]：`map(&:chomp)` の仕組み
- [[awk]]：列の抽出・集計との比較
- [[uniq]]：連続する重複行の処理
- [Ruby公式：Command-Line Options](https://docs.ruby-lang.org/en/3.4/ruby/options_md.html)

確認日：2026-10-20
