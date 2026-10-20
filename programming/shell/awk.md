---
tags: [プログラミング, シェル, コマンド, テキスト処理]
aliases: [awkコマンド, AWK, awk command]
date: 2026-10-20
---
# awk

**`awk` は、テキストを行ごとに読み、条件に合う行から列を取り出したり、計算・集計したりする言語と、その実行コマンド。** 空白やタブで区切られた表、ログなどを短いプログラムで処理できる。

## 名前の由来

開発者 **Alfred Aho、Peter Weinberger、Brian Kernighan** の姓の頭文字を並べた名前。GNUによる実装は `gawk` と呼ばれる。[GNU Awk User’s Guide：History](https://www.gnu.org/s/gawk/manual/html_node/History.html)

## 基本形：条件と処理

```sh
awk '条件 { 処理 }' input.txt
```

- 条件を省略すると、すべての入力行に処理を行う。
- 処理を省略すると、条件に合う行全体を表示する。
- ファイルを省略すると標準入力を読む。

```sh
# すべての行の第1フィールドを表示
awk '{ print $1 }' input.txt

# ERRORを含む行全体を表示
awk '/ERROR/' app.log
```

プログラムは通常シングルクォートで囲む。これにより `$1` などをシェルが展開するのを防ぐ。

## 行とフィールド

標準では一行が一つのレコードになり、空白・タブの並びでフィールドに分かれる。先頭・末尾の空白は、標準の空白区切りでは空フィールドを作らない。

| 表記 | 意味 |
| --- | --- |
| `$0` | 現在の行全体 |
| `$1`、`$2` | 第1・第2フィールド |
| `$NF` | 最後のフィールド |
| `NF` | 現在の行のフィールド数 |
| `NR` | 入力全体で何番目のレコードか |
| `FNR` | 現在のファイルで何番目のレコードか |

複数ファイルを読むとき、`NR` は通算し、`FNR` はファイルごとに数え直す。[GNU Awk User’s Guide：Input Summary](https://www.gnu.org/software/gawk/manual/html_node/Input-Summary.html)

## 表の列を取り出す

以下を `scores.txt` とする。

```text
name score team
Alice 80 red
Bob 65 blue
Carol 90 red
```

```sh
awk 'NR > 1 { print $1 }' scores.txt
```

```text
Alice
Bob
Carol
```

`NR > 1` で最初のヘッダー行を除く。複数ファイルそれぞれの先頭行を除きたい場合は、`FNR > 1` を使う。

## 条件で抽出する

```sh
awk 'NR > 1 && $2 >= 80 { print $1, $2 }' scores.txt
```

```text
Alice 80
Carol 90
```

`&&` は「かつ」。ほかに `||`（または）、`!`（否定）、`==`（等しい）、`!=`（等しくない）がある。`=` は代入なので、比較の `==` と区別する。

フィールドを正規表現で調べるには `~` を使う。

```sh
awk 'NR > 1 && $3 ~ /^r/ { print $1 }' scores.txt
```

## 合計と平均

```sh
awk 'NR > 1 { sum += $2; n++ }
     END { if (n > 0) printf "average=%.2f\n", sum / n }' scores.txt
```

```text
average=78.33
```

`sum += $2` は加算、`n++` は件数を一つ増やす処理。未初期化変数は数値演算では0として扱われる。`n > 0` を確認して、データがないときの0除算を防ぐ。

| ブロック | 実行する時点 |
| --- | --- |
| `BEGIN { ... }` | 入力を読み始める前 |
| 条件 `{ ... }` | 各入力レコードの処理中 |
| `END { ... }` | 入力の処理後 |

`print` は通常末尾に改行を付ける。`printf` は書式を指定できるが、改行も `\n` などで明示する。`%.2f` は小数点以下2桁。[GNU Awk User’s Guide：BEGIN/END](https://www.gnu.org/software/gawk/manual/html_node/Using-BEGIN_002fEND.html)

## グループ別に集計する

```sh
awk 'NR > 1 { total[$3] += $2 }
     END { for (team in total) print team, total[team] }' scores.txt
```

`total["red"]` のように、文字列をキーにする**連想配列**を使う。結果は `red 170` と `blue 65`。配列の走査順は保証されないため、順番が必要なら出力を `sort` へ渡す。

## 区切り文字を変える

```sh
# 単純なカンマ区切り
awk -F ',' '{ print $1, $3 }' input.csv

# 入力も出力もタブ区切り
awk -F '\t' 'BEGIN { OFS = "\t" } { print $1, $3 }' input.tsv
```

`-F` は入力の区切り、`OFS` は `print` で複数の値を出すときの区切り。`print $1, $3` と、行全体をそのまま出す `print $0` は異なる。

**`-F ','` だけでは、引用符内にカンマや改行がある一般的なCSVを正しく扱えない。** その場合はCSVパーサーや、対応する実装のCSV機能を使う。

## シェルの値を渡す

```sh
threshold=80
awk -v min="$threshold" 'NR > 1 && $2 >= min { print $1, $2 }' scores.txt
```

シェルの値をプログラム本文へ連結するより、`-v` で変数として渡すと、引用符やコードとの境界を管理しやすい。

## 出現順を保って重複を除く

```sh
awk '!seen[$0]++' input.txt
```

初めて現れた行だけを出力する。`seen[$0]++` は増やす前の値を返すので、初回の0を `!` が真にし、処理省略時の「行全体を表示」が実行される。

[[uniq]]は隣接する行だけを比較するが、この例は配列に既出の行を記憶する。離れた重複も除ける一方、異なる行が増えるほどメモリーを使う。

## 長いプログラムはファイルへ

```sh
awk -f script.awk scores.txt
```

`gawk`、macOSの `awk`、`mawk` などは追加機能に違いがある。移植する場合は、使用先の `man awk` と実装の資料を確認する。

## 関連

- [[Ruby_oneliner|Ruby oneliner]]：Rubyによる行処理・列抽出・集計

## 出典・確認

- 手元のmacOSの `man awk`。列抽出・条件抽出・平均・グループ集計・順序を保つ重複除去の例は実行確認。
- [GNU Awk User’s Guide](https://www.gnu.org/software/gawk/manual/)
- [[uniq]]

確認日：2026-10-20
