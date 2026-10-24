---
aliases:
  - QBASIC
  - Qbasic
tags:
  - プログラミング言語
  - BASIC
  - MS-DOS
---
# QBasic

Microsoftが提供した、**MS-DOS上でBASICのプログラムを編集・実行するための開発環境とインタープリター**。ソースコードを書き、その場で動作を確かめられる。MS-DOSに付属していたため、プログラミングの入門環境としても使われた。[FreeBASIC公式マニュアル：FreeBASIC and QBasic](https://www.freebasic.net/wiki/CompilerQB)

## 何ができるか

- 数値計算、文字列処理、キーボード入力、画面出力
- 条件分岐・繰り返し・配列を使った処理
- ファイルの読み書き
- DOS環境での簡単な描画や音の出力

保存したBASICのソースファイルには、通常 `.BAS` という拡張子を使う。

## 簡単なプログラム

```basic
CLS
INPUT "Number"; n
FOR i = 1 TO n
    PRINT i; i * i
NEXT i
END
```

入力した数まで、整数とその平方を表示する。`CLS` は画面消去、`INPUT` は入力、`PRINT` は表示、`FOR`〜`NEXT` は繰り返しを表す。

## QBasicとQuickBASICの違い

| 名前 | 主な位置付け |
| --- | --- |
| QBasic | インタープリターでプログラムを実行する。単独の実行ファイルを作るコンパイラーは備えない |
| QuickBASIC | 編集・実行環境に加え、DOS用の実行ファイルを作るコンパイラーを備える製品 |

名前は似ているが、**QBasicとQuickBASICは同一の製品ではない**。[FreeBASIC公式マニュアル](https://www.freebasic.net/wiki/CompilerQB)

## DOS・Windowsとの関係

QBasicはプログラムを作る道具であり、[[CAB]]のような圧縮形式や、[[バックアップ起動ディスク]]のような復旧用媒体とは役割が異なる。DOS時代の資料では同じ環境の話題として登場するが、通常のOS起動にQBasic自体が必須という意味ではない。

## 参考資料

- [FreeBASIC公式マニュアル：FreeBASIC and QBasic](https://www.freebasic.net/wiki/CompilerQB) — 互換言語側から見たQBasic・QuickBASICの位置付け
