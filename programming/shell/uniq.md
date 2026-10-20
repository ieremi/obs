---
tags: [プログラミング, シェル, コマンド, テキスト処理]
aliases: [uniqコマンド, uniq command]
date: 2026-10-20
---
# uniq

**`uniq` は、隣り合う同じ行をまとめたり、連続する重複行を数えたりするコマンド。** 名前は英語の *unique*（一意の・重複しない）を連想すると覚えやすい。

重要なのは、**比較するのが隣接する行だけ**という点。ファイル全体の重複をまとめたい場合は、通常 `sort` と組み合わせる。

## 基本形

```sh
uniq input.txt
sort input.txt | uniq
```

入力ファイルを省略すると標準入力を読む。出力先を省略すると標準出力へ書くため、パイプと組み合わせられる。

## 連続していない重複は残る

次の内容を例にする。

```text
apple
apple
banana
apple
cherry
cherry
```

`uniq input.txt` の出力：

```text
apple
banana
apple
cherry
```

最初の連続する `apple` は一行にまとまるが、`banana` の後の `apple` は残る。`uniq` 自体は行を並べ替えない。

## 主なオプション

| オプション | 動作 |
| --- | --- |
| なし | 同じ行の連続ごとに一行を出す |
| `-c` | 連続する同じ行の件数を付ける |
| `-d` | 2行以上連続するグループだけ、一行ずつ出す |
| `-u` | 1行だけのグループを出す |
| `-i` | 大文字・小文字を区別せず比較する |
| `-f N` | 比較時に先頭のNフィールドを無視する |
| `-s N` | 比較時に先頭のN文字を無視する |

`-u` は「重複を一つにまとめる」指定ではない。例の入力で `uniq -u input.txt` を実行すると、`banana` と、離れて現れた一行の `apple` が出る。こちらもファイル全体の出現回数ではなく、連続するグループを見ている。

## ファイル全体で重複を除く

```sh
sort input.txt | uniq
```

```text
apple
banana
cherry
```

完全な行の一致で重複を除く基本用途なら、次の書き方もできる。

```sh
sort -u input.txt
```

どちらも並べ替えるので、元の出現順序は保たれない。`sort` にキー指定や数値比較などを加えた場合は、`sort -u` と `sort | uniq` の比較条件が同じとは限らない。

## 出現回数を数える

```sh
sort input.txt | uniq -c
```

```text
   3 apple
   1 banana
   2 cherry
```

件数の多い順に並べるには、さらに数値の降順でソートする。

```sh
sort input.txt | uniq -c | sort -nr
```

```text
   3 apple
   2 cherry
   1 banana
```

件数の前の空白幅は実装によって異なる。

## 重複行だけ・一度しか出ない行だけ

```sh
# ファイル全体で2回以上出る行を、一行ずつ表示
sort input.txt | uniq -d

# ファイル全体で一度しか出ない行を表示
sort input.txt | uniq -u
```

例の入力では、前者は `apple` と `cherry`、後者は `banana` になる。

## 大文字・小文字を無視する

```sh
sort -f input.txt | uniq -i
```

`uniq -i` だけでは、離れた場所にある同一視すべき行はまとめられない。ソート側も大文字・小文字を無視して並べる。グループから出力される文字列の表記を、必ず小文字へ変換するコマンドではない。

## 注意点

- 比較は行単位。行内の単語の重複を除く処理ではない。
- 通常は先頭・末尾の空白も比較に関わる。
- 並び順や大文字・小文字の扱いはロケールの影響を受ける。
- GNU版とmacOSなどのBSD系では、追加オプションや細部が異なる。手元の `man uniq` を確認する。

再現性のため、バイト単位の並び・比較にそろえたい場合は、例えば次のように両方へロケールを指定する。

```sh
LC_ALL=C sort input.txt | LC_ALL=C uniq -c
```

## 関連

- [[awk]]：列の抽出・集計、出現順を保つ重複除去

## 出典・確認

- macOSの `man uniq`：基本動作とオプション。掲載した基本例は手元の `uniq` でも確認。
- [GNU Coreutils：uniq invocation](https://www.gnu.org/software/coreutils/manual/html_node/uniq-invocation.html)
- [POSIX：uniq](https://pubs.opengroup.org/onlinepubs/9799919799/utilities/uniq.html)

確認日：2026-10-20
