---
tags:
  - Windows
  - FTP
  - ファイル転送
  - オープンソース
---
# FFFTP

**Windows用の、GUIで操作するFTPクライアントソフトウェア**。手元とサーバー側のファイルを見比べながら、アップロードやダウンロードを行う。無償で利用でき、ソースコードはBSD 2-Clauseライセンスで公開されている。[公式リポジトリ](https://github.com/ffftp/ffftp)、[付属説明書](https://github.com/ffftp/ffftp/blob/master/doc/ffftp.en.txt)

## 主な用途

- WebサイトのHTML・画像などをサーバーにアップロードする。
- サーバー上のファイルを手元にダウンロードする。
- 接続先を登録し、繰り返し同じサーバーへ接続する。
- ローカルとサーバーのフォルダーを比較し、必要なファイルを転送する。

## 基本的な接続情報

| 項目 | 意味 |
| --- | --- |
| ホスト名・アドレス | 接続先サーバーの名前やIPアドレス |
| ユーザー名・パスワード | サーバーが発行した認証情報 |
| 接続方式 | FTP・FTPSなど、サーバーに対応した方式 |
| ポート番号 | 接続方式とサーバー設定に応じた番号 |
| 初期フォルダー | 接続後に開く、手元またはサーバー側のフォルダー |

FTPS接続では、ホスト設定の暗号化に関する項目を設定する。サーバー事業者の手順では、`FTPS(Explicit)` を指定する例がある。[IDCフロンティア：FFFTPの設定手順](https://www.idcf.jp/rentalserver/support/manual/ftp/w-ffftp/)

**FTPSとSFTPは別の方式**であり、SFTP専用サーバーにFTPSの設定で接続することはできない。利用する版の対応方式と、サーバー側の指定を確認する。

## 開発の経緯と入手先

Sota氏による開発から、FFFTP Project、さらに後の開発者へと引き継がれてきた。現在の開発元リポジトリと配布先は、以下から確認できる。[原作者の案内](https://www2.biglobe.ne.jp/~sota/ffftp.html)、[公式説明書の著作権表示](https://github.com/ffftp/ffftp/blob/master/doc/ffftp.en.txt)

- [公式リポジトリ](https://github.com/ffftp/ffftp)
- [公式リリース一覧](https://github.com/ffftp/ffftp/releases)

## CuteFTPとの違い

| 項目 | FFFTP | CuteFTP |
| --- | --- | --- |
| 配布形態 | 無償・オープンソース | 商用製品 |
| 主な用途 | GUIでのファイル転送 | GUIでのファイル転送、自動化など |
| 詳細な対応機能 | 使用する版の説明書で確認 | 製品版ごとの公式資料で確認 |

[[CuteFTP]]と同じく、FTPサーバーへ接続するクライアントであり、サーバーを公開するためのソフトウェアではない。
