---
aliases:
  - config.sys
tags:
  - MS-DOS
  - 起動
---
# CONFIG.SYS

MS-DOSの起動時にシステムの構成を指定するテキストファイル。デバイスドライバーの読み込みや、開けるファイル数などの設定に使う。通常、起動ドライブのルートディレクトリに置き、[[AUTOEXEC.BAT]]より先に処理される。[MS-DOS 6.22 User's Manual](https://www.bitsavers.org/pdf/microsoft/msdos_6.22/DOS_6.22_Users_Manual_1994.pdf)

## 例

```ini
DEVICE=C:\DOS\HIMEM.SYS
FILES=40
```

- `DEVICE`：指定したデバイスドライバーを読み込む。例の `HIMEM.SYS` は拡張メモリを管理する。
- `FILES`：同時に開くことができるファイル数を設定する。

これはMS-DOS環境での例であり、ドライバーの配置や必要な値は環境によって異なる。

## AUTOEXEC.BATとの違い

| ファイル | 主な役割 |
| --- | --- |
| `CONFIG.SYS` | ドライバーの読み込みやDOSのシステム構成 |
| `AUTOEXEC.BAT` | 起動後に実行するコマンドやプログラム |

## 関連

- [[AUTOEXEC.BAT]]
- [[バックアップ起動ディスク]]
