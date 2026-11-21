---
aliases:
  - autoexec.bat
tags:
  - MS-DOS
  - バッチファイル
---
# AUTOEXEC.BAT

MS-DOSの起動時に自動実行されるバッチファイル。起動ドライブのルートディレクトリに置き、環境変数の設定や常駐プログラムの起動などを記述する。通常、[[CONFIG.SYS]]の処理後に実行される。[MS-DOS 6.22 User's Manual](https://www.bitsavers.org/pdf/microsoft/msdos_6.22/DOS_6.22_Users_Manual_1994.pdf)

## 例

```bat
@ECHO OFF
PATH C:\DOS
PROMPT $P$G
C:\DOS\SMARTDRV.EXE
```

- `@ECHO OFF`：コマンド自体の表示を抑える。
- `PATH`：実行ファイルを探すディレクトリを設定する。
- `PROMPT $P$G`：現在のドライブとディレクトリをプロンプトに表示する。
- `SMARTDRV.EXE`：[[SMARTDrive]]を起動する。

これはMS-DOS環境での例であり、ファイルの配置や必要な設定は環境によって異なる。

## 関連

- [[CONFIG.SYS]]
- [[バックアップ起動ディスク]]
