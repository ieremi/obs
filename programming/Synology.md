---
aliases:
  - シノロジー
  - DSM
  - DiskStation Manager
tags:
  - NAS
  - Linux
確認日: 2026-10-30
---
# Synology

**台湾のNASメーカー。** 家庭・中小企業向けのNAS（ネットワーク接続のストレージ）で大きなシェアを持つ。強みはハードウェアより、専用OSの **DSM**（DiskStation Manager）とその上で動くアプリにある。

| 項目 | 内容 |
| --- | --- |
| 創業 | 2000年、台北。元Microsoftの技術者が設立。 |
| 主な製品 | DiskStation（据え置き型NAS）、RackStation（ラック型）、BeeStation（初心者向けの個人用クラウド）、ルーター |
| OS | DSM。Linuxベースで、ブラウザーから操作する。 |
| 競合 | QNAP（台湾）、ASUSTOR、TrueNAS（自作向けOS）、UGREEN など |

## DSMでできること

| 機能 | 主なアプリ |
| --- | --- |
| ファイル共有 | SMB・NFS・AFPでの共有、Synology Drive（Dropbox風の同期） |
| バックアップ | Hyper Backup（NASの外へ）、Active Backup for Business（PCやサーバーをNASへ）、スナップショット |
| 写真・動画 | Synology Photos（顔認識やスマホからの自動アップロード） |
| 監視カメラ | Surveillance Station |
| 仮想化・コンテナ | Virtual Machine Manager、Container Manager（Docker） |
| 外からの接続 | QuickConnect（ポート開放なしでの中継接続）、DDNS |

ブラウザーの中にデスクトップのような画面が出て、アプリを追加していく作り。Linuxの知識がなくても、サーバーの機能を一通り使える。

## 独自の技術

| 技術 | 内容 |
| --- | --- |
| **SHR**（Synology Hybrid RAID） | 容量の違うHDDを混ぜても無駄が少なくなるRAID。HDDを後から大きいものに入れ替えて増やしやすい。 |
| **Btrfs** | スナップショットやデータの破損検出ができるファイルシステム。 |

## 型番の読み方

例：**DS925+**

| 部分 | 意味 |
| --- | --- |
| DS | DiskStation |
| 9 | 拡張ユニットを含めた最大ベイ数 |
| 25 | 発売年（2025年） |
| + | シリーズ |

| シリーズ | 対象 |
| --- | --- |
| FS / XS | 企業向けの上位機 |
| **Plus（+）** | 中小企業・上級者向け。Docker、仮想マシン、SSDキャッシュに対応する機種が多い。 |
| Value | 一般向け |
| J | 入門向け |

最大ベイ数は本体だけのベイ数とは限らない。DS923+は本体4ベイで、拡張ユニットを付けると9ベイ。

## HDDの制限問題（2025年）

| 時期 | 出来事 |
| --- | --- |
| 2025年 | Plusシリーズの2025年モデル（DS925+など）で、ストレージプールを作れるHDDを、Synology純正品と認定品に限った。他社製HDDでは警告が出たり、機能が制限されたりした。 |
| 2025年 | 他社製HDDより割高な純正品を強いる囲い込みだとして強く反発され、販売も落ち込んだと報じられた。 |
| 2025年10月 | **DSM 7.3**で方針を撤回し、他社製のHDDと2.5インチSATA SSDを警告なしで使えるようにした。M.2 SSDの制限は残る。 |

互換性リスト（HCL）自体は続いているので、リストにない機種では、初期化のときに一度だけ警告が出ることがある。

## 押さえどころ

- Synologyの価値は主にソフトウェア（DSM）にある。同じ値段なら、自作やほかのメーカーのほうがハードウェアの性能は高いことが多い。
- NASのRAIDやスナップショットはバックアップの代わりにならない。NASそのものの故障、ランサムウェア、火災に備えて、別の場所へのバックアップが必要。
- インターネットに公開したNASを狙うランサムウェアの被害が過去に起きている。QuickConnectやポート開放は必要なときだけ使い、DSMを最新に保つ。
- かつての自作NASキット（[[玄箱と白箱]]）が担っていた「家庭のLinuxサーバー」の役割を、完成品として引き継いだ製品の1つといえる。

## 出典

- [Synology公式サイト](https://www.synology.com/)
- [Wikipedia：Synology](https://en.wikipedia.org/wiki/Synology)
- [Thurrott.com：Synology Reverses Drive Validation Policy](https://www.thurrott.com/cloud/328060/synology-reverses-drive-validation-policy)
- [Dong Knows Tech：Synology DSM 7.3 Now Available](https://dongknows.com/synology-dsm-7-3-removes-storage-lock-in-hcl-policy/)
- [WinBuzzer：Synology Reverses Controversial NAS Hard Drive Restriction（2025年10月8日）](https://winbuzzer.com/2025/10/08/synology-reverses-controversial-nas-hard-drive-restriction-after-sales-plummet-xcxwbn/)
- [Michael Tsai：Synology Reverses Ban on Third-Party Hard Drives](https://mjtsai.com/blog/2025/10/09/synology-reverses-ban-on-third-party-hard-drives/)

関連：[[玄箱と白箱]]、[[RAID]]
