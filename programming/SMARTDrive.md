---
aliases:
  - smartdrv
  - SMARTDRV
  - SMARTDRV.EXE
  - SmartDrive
tags:
  - MS-DOS
  - Windows
  - キャッシュ
---
# SMARTDrive

Microsoftが提供した、**ディスクアクセスを高速化するためのキャッシュプログラム**。DOS時代の資料では、実行ファイル名の `SMARTDRV.EXE` やコマンド名の `smartdrv` で登場する。[Microsoft MASM 6.1 Getting Started：Using SMARTDRV.EXE](https://www.bitsavers.org/pdf/microsoft/masm/Microsoft_MASM_6.1_1992/MASM_6.1_Getting_Started_1992.pdf#page=36)

## 仕組み

ディスクから読み出した内容の一部をRAMに保持する。同じ内容を再び必要としたときに、低速なディスクへのアクセスを省き、メモリ上のコピーを返す。

書き込みキャッシュが有効な場合は、書き込む内容をいったんメモリに蓄え、後からディスクに反映する。**プログラム側で書き込みが終わっても、ディスクへの反映が完了していない時間がありうる。**

## 起動とキャッシュの書き出し

以下は `SMARTDRV.EXE` 4.0の資料に基づく例。DOSのコマンドラインや `AUTOEXEC.BAT` から起動する。

```bat
C:\DOS\SMARTDRV.EXE
```

パスは実際の配置に合わせる。起動済みの状態で `SMARTDRV` を実行すると、キャッシュの状態を確認できる。

保留中の書き込みをディスクへ反映させるには、次を使う。

```bat
SMARTDRV /C
```

Microsoftの資料は、独自の再起動ユーティリティーをバッチファイルから使う場合、再起動の前にこの書き出しを行うよう説明している。[Microsoft公式マニュアルの保存版、本文27〜29ページ](https://www.bitsavers.org/pdf/microsoft/masm/Microsoft_MASM_6.1_1992/MASM_6.1_Getting_Started_1992.pdf#page=36)

## RAMディスクとの違い

| 機能 | 役割 |
| --- | --- |
| ディスクキャッシュ | 実際のディスクとの間でデータを保持・再利用し、アクセスを速くする |
| RAMディスク | メモリの一部を、独立したディスクドライブのように扱う |

キャッシュはバックアップではない。SMARTDriveを使っても、データの別媒体への複製が保存されるわけではない。

## 関連

- [[バックアップ起動ディスク]]
- [[QBasic]]
