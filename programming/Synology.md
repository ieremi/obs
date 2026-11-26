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

## USB 接続で使う

確認日：**2026-11-26**。

### PC と USB ケーブルでつなぐことはできない

**Synology の NAS を USB ケーブルで PC や Mac につなぎ、外付けドライブのように使うことはできない。** Synology は、NAS と PC の間で USB ケーブルを使ってデータを転送することはできず、NAS の USB ポートは外付けの USB ストレージなど対応機器をつなぐためのものだと説明している。[Synology ナレッジセンター：USBケーブルを使ってSynology NASとコンピュータの間でファイルを転送できますか？](https://kb.synology.com/ja-jp/DSM/tutorial/Transfer_files_between_Synology_NAS_and_a_computer_using_a_USB_cable)

NAS の USB ポートは、機器をぶら下げる側（ホスト）としてしか働かない。PC につながれる側（デバイス）にはなれないので、NAS どうし、または NAS と PC を USB でつないでも通信できない。

### 代わりに：LAN ケーブルで PC と直接つなぐ

ルーターやスイッチがなくても、**LAN ケーブル1本で PC と NAS を直接つなげば**、ネットワーク経由で普段どおりに使える。

1. PC の Wi-Fi を切り、PC と NAS を LAN ケーブルでつなぐ。いまの LAN ポートは配線の向きを自動で切り替えるので、普通のケーブルでよい（昔はクロスケーブルが必要だった）。[Synology Community：Connect directly to computer with ethernet for video editing](https://community.synology.com/enu/forum/17/post/118618)
2. PC の有線 LAN を「IP アドレスを自動で取得（DHCP）」にしておく。[Synology ナレッジセンター：How do I find my Synology storage system via Web Assistant or Synology Assistant?](https://kb.synology.com/en-global/DSM/tutorial/Unable_to_Locate_NAS)
3. DHCP サーバーがないので、PC も NAS も `169.254.x.x` のアドレス（リンクローカルアドレス）を自分で付ける。見つからないときは、両方に同じ範囲の固定アドレス（例：NAS を `192.168.1.2`、PC を `192.168.1.1`、サブネットマスク `255.255.255.0`）を手で設定する。[Synology Community：DS212j can't connect](https://community.synology.com/enu/forum/1/post/136172)、[Synology Forum：DS1010+ Direct Connection to Laptop via Ethernet Cable?](https://forum.synology.com/enu/viewtopic.php?t=22026)
4. PC に入れた **Synology Assistant** で NAS を探し、アドレスを確かめる。
5. ファイル共有につなぐ。
   - Mac：Finder で ⌘K を押し、`smb://NASのアドレス` を開く。
   - Windows：エクスプローラーのアドレス欄に `\\NASのアドレス` と入れる。

注意点：直結している間、NAS はインターネットにつながらない。DSM の更新やパッケージの追加は、手でファイルを入れて行うことになる。ほかの機器からも NAS を使えない。[Synology Community：DS213 - how to setup nas using network cable to pc](https://community.synology.com/enu/forum/17/post/95939)

### PC に LAN ポートがないとき：USB の LAN アダプターを使う

最近のノート PC や Mac には LAN ポートがないことが多い。その場合は、PC 側に **USB（USB-C）接続の LAN アダプター** を付けて、そこから LAN ケーブルで NAS につなぐ。「USB でつなぐ」に最も近いのはこの形である。

- NAS の LAN ポートが 2.5GbE の機種なら、アダプターも 2.5GbE のものにすると速さを活かせる。1GbE なら、理論上の上限は毎秒約125MB である（1バイトは8ビットなので、125MB × 8 ＝ 1000Mb）。
- 速さは USB の規格ではなく、LAN の規格（1GbE、2.5GbE、10GbE）で決まる。

### NAS の USB ポートでできること

NAS の USB ポートには、NAS が使う側として機器をつなぐ。[Synology ナレッジセンター：External Devices](https://kb.synology.com/en-global/DSM/help/DSM/AdminCenter/system_externaldevice_devicelist?version=7)

| つなぐもの | できること |
| --- | --- |
| 外付け HDD・SSD、USB メモリ | NAS から読み書きする。NAS のバックアップ先（Hyper Backup）にもできる。 |
| 同上 | **USB Copy** で、USB 機器と NAS の間でファイルをコピーする。カメラのカードの中身を NAS に取り込むときなどに使う。[Synology ナレッジセンター：USB Copy](https://kb.synology.com/en-global/DSM/help/USBCopy/usbcopy_general?version=7) |
| UPS（無停電電源装置） | 停電のときに NAS を安全に止める。 |

PC のデータを NAS に移したいだけなら、いったん外付けドライブにコピーしてから NAS の USB ポートにつなぎ、USB Copy で取り込む方法もある。

### NAS が壊れて起動しないとき

NAS のドライブを取り出し、PC で Linux（Ubuntu）を起動して中身を読み出す方法を、Synology が案内している。[Synology ナレッジセンター：How can I use a PC to recover data when my Synology NAS malfunctions?](https://kb.synology.com/en-global/DSM/tutorial/How_can_I_recover_data_from_my_DiskStation_using_a_PC) ふだんの使い方ではなく、故障したときの最後の手段である。

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
