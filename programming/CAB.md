---
aliases:
  - cab
  - CABファイル
  - Cabinetファイル
  - キャビネットファイル
tags:
  - Windows
  - ファイル形式
  - 圧縮
---
# CAB

**複数のファイルをまとめて格納する、Microsoftのアーカイブ形式。** Cabinetの略で、通常は拡張子 `.cab` を使う。圧縮にも対応し、Windowsのインストールやソフトウェア配布などで利用される。[Microsoft Learn：Cabinet Files](https://learn.microsoft.com/en-us/windows/win32/msi/cabinet-files)

## 特徴

- 複数のファイルを一つにまとめられる。
- ファイルの境界をまたいで圧縮でき、個別に圧縮する場合より効率がよくなることがある。
- 大きな内容を複数のキャビネットに分割できる。
- Windows Installerでは、CABをインストールパッケージの内部に格納したり、外部ファイルとして配置したりできる。

[Microsoft Learn：Cabinet Files](https://learn.microsoft.com/en-us/windows/win32/msi/cabinet-files)

## 内容の確認と展開

以下はWindowsの `expand` コマンドの例。古いDOS・Windowsの展開ツールとは、対応形式やオプションが異なる場合がある。

内容の一覧を表示する。

```bat
expand -d example.cab
```

すべてのファイルを、あらかじめ作成した `C:\Temp\cab-out` に展開する。

```bat
expand example.cab -f:* C:\Temp\cab-out
```

`-d` は一覧表示、`-f:*` はすべてのファイルを指定する。特定のファイルだけなら `-f:名前` とする。[Microsoft Learn：expand](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/expand)

## CABを作る

Windowsの `makecab` では、たとえば次のようにファイルを圧縮できる。

```bat
makecab example.txt example.cab
```

複数ファイルの配置などを細かく指定する場合は、指示ファイル（DDF）を使う。[Microsoft Learn：makecab](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/makecab)

## バックアップ・起動ディスクとの違い

**CABは格納形式であり、それだけで起動可能になるわけではない。** また、CABを一つ保存しただけでは、OS全体のバックアップになるとは限らない。[[バックアップ起動ディスク]]から復旧環境を起動し、別媒体に保存した配布ファイルを使う、といった役割分担がある。

## 関連

- [[バックアップ起動ディスク]]
- [[QBasic]]
