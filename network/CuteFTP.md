---
aliases:
  - Cute FTP
tags:
  - Windows
  - FTP
  - ファイル転送
---
# CuteFTP

**手元のコンピューターとサーバーの間でファイルを転送する、GUIのファイル転送クライアント**。Globalscapeの商用ソフトウェアで、Webサイトのファイルのアップロードや、サーバーからのダウンロードなどに使う。[Globalscape公式：CuteFTP](https://www.globalscape.com/cuteftp)

## 主な用途・機能

- 接続先を登録し、サーバーのファイル一覧を表示する。
- ファイルやフォルダーをアップロード・ダウンロードする。
- 転送処理をスクリプトなどで自動化する。
- 暗号化された接続方式でファイルを転送する。

公式資料では、FTP・FTPS・SFTPなどへの対応が説明されている。使える機能は製品の版によって確認する。[公式製品ページ](https://www.globalscape.com/cuteftp)、[CuteFTP 9.4ユーザーガイド](https://hstechdocs.helpsystems.com/manuals/globalscape/pdfs/cuteftp/cuteftp_9_4_user_guide.pdf)

## FTP・FTPS・SFTPの違い

| 方式 | 内容 |
| --- | --- |
| FTP | ファイル転送用のプロトコル。通常のFTP自体には通信の暗号化がない |
| FTPS | FTPをTLSで保護する方式 |
| SFTP | SSHを利用するファイル転送プロトコル。FTPSとは別方式 |

接続先のホスト名や認証情報に加え、サーバーが指定する方式とポート番号を合わせて設定する。**FTPSとSFTPは、名前が似ていても相互に置き換えられない。** [CuteFTP公式ユーザーガイド](https://hstechdocs.helpsystems.com/manuals/globalscape/pdfs/cuteftp/cuteftp_9_4_user_guide.pdf)

## FFFTPとの関係

[[FFFTP]]もGUIでファイルを転送するクライアント。CuteFTPは商用製品、FFFTPは無償で利用できるオープンソースのソフトウェアである。いずれも転送先のサーバーそのものではなく、サーバーへ接続して操作する側の道具。

## 参考資料

- [CuteFTP公式製品ページ](https://www.globalscape.com/cuteftp)
- [公式リリースノート](https://hstechdocs.helpsystems.com/releasenotes/Content/_ProductPages/Globalscape/cuteftp.htm)
