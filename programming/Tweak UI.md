---
aliases:
  - TweakUI
  - トゥイークUI
tags:
  - コンピュータ史
  - Windows
  - レガシー技術
確認日: 2026-10-31
---
# Tweak UI

**Windowsの細かい設定を、レジストリを直接編集せずに変えられるMicrosoft製の無料ツール。** Windows 95からXPの時代に、サポート対象外のツール集「PowerToys」の1つとして配布された。中身は「レジストリを書き換える画面」で、OSにない機能を足すものではない。

| 項目 | 内容 |
| --- | --- |
| 作者 | レイモンド・チェン（Windowsシェルチームの開発者。ブログ「The Old New Thing」の著者） |
| 初公開 | 1996年ごろ。Windows 95の発売の少し後。 |
| 配布 | Microsoftのサイトから無料でダウンロード。Windows 98ではインストールCDにも入った。 |
| 対応OS | Windows 95・98・Me・NT 4.0・2000・XP・Server 2003。OSごとに別の版がある。 |
| 最終版 | 2.10（Windows XP SP1以降とServer 2003用、2003年） |
| サポート | なし。Microsoft製だが、使うのは自己責任。 |

## なぜ作られたか

- Windows 95の開発中、開発者たちは機能の確認や試作のために、ちょっとした補助プログラムを書いていた。発売後にそれを集めて配ったのが、最初の **Windows 95 PowerToys**。
- Tweak UIは第2弾のPowerToysの1つで、はじめからPowerToyとして作られた。チェンによれば、苦情に応えたわけではなく、**「書きたかったから書いた」**。
- チェン自身、Tweak UIは「すでにある機能に画面を付けただけ」と説明している。どの設定も、レジストリの値を知っていれば手で変えられた。

## 版の移り変わり

| 対象 | 形式 | 主な出来事 |
| --- | --- | --- |
| Windows 95・NT 4.0 | コントロールパネルの項目（tweakui.cpl） | Windows 95 PowerToysの第2弾で公開。タブで設定を切り替える画面。 |
| Windows 98 | 同上 | 新しい版が **Windows 98のCD-ROMに入った**（付属ツールのフォルダー）。 |
| Windows 2000など | 同上 | 旧系統の最終版は1.33。XPやServer 2003では使わないよう注意されていた。 |
| Windows XP | 単独のアプリ（TweakUI.exe） | PowerToys for Windows XPの1つとして作り直された。左のツリーで項目を選ぶ画面になった。 |
| Windows XP SP1以降・Server 2003 | 同上 | **2.10**が最終版。SP1がないXPでは2.00を使う。 |
| Windows Vista | ― | チェンはVista版を書いたが、「サポートしないソフトは配らない」という社の方針に反するため、公開されなかった。 |
| Windows XP x64 | ― | 公式版はなく、NeoSmart Technologiesが非公式の64ビット版を作った。 |

## できたこと

### Windows 95・98の版

設定はタブごとに分かれていた。主なもの：

| タブ | 内容 |
| --- | --- |
| Mouse | メニューが開く速さ、ダブルクリックやドラッグと判定する範囲 |
| General | ウィンドウのアニメーション、スムーズスクロール、特殊フォルダーの場所 |
| Explorer | **ショートカットの矢印**を消す・変える、「ショートカット ～」という名前を付けない |
| Desktop | ごみ箱などのデスクトップのアイコンを出し入れする |
| My Computer | マイコンピュータに表示するドライブを隠す |
| Network | 起動時の自動ログオン |
| New | エクスプローラーの「新規作成」メニューの項目を整理する |
| Add/Remove | 「アプリケーションの追加と削除」に残ったごみの項目を消す |
| Boot | 起動メニューの表示や待ち時間、起動時のロゴ（MSDOS.SYSの設定） |
| Repair | アイコンのキャッシュを作り直すなど、壊れた設定を直す |
| Paranoia | ログオフ時に、最近使ったファイル、ファイル名を指定して実行、検索などの履歴を消す |

### Windows XPの版

左のツリーで項目を選ぶ。主なもの：

| 項目 | 内容 |
| --- | --- |
| Focus | ほかのアプリがウィンドウを勝手に前面に出す（フォーカスを奪う）のを止める |
| Mouse | **X-Mouse**（ポインターを乗せたウィンドウがアクティブになる）、ホイールのスクロール量、ホバーの感度 |
| Explorer | ショートカットの矢印、圧縮・暗号化したファイルの色、サムネイルの画質と大きさ |
| Common Dialogs | 「ファイルを開く」画面の左側に出す場所 |
| Taskbar | タスクバーのボタンをまとめる条件、スタートメニューに出すアプリ |
| Desktop | デスクトップのアイコンを出し入れする |
| My Computer | ドライブの表示、特殊フォルダーの場所、**ドライブごとの自動再生** |
| Control Panel | コントロールパネルの項目を隠す |
| Templates | 「新規作成」メニューの項目 |
| Internet Explorer | アドレスバーに打つキーワードで検索サイトを切り替える |
| Command Prompt | ファイル名の補完に使うキー |
| Logon | **自動ログオン**、ようこそ画面の未読メール表示 |
| Access Control | ファイルやフォルダーのアクセス権を画面から変える |
| Repair | アイコンの再作成、レジストリエディタを使えるようにする、など |

## 問題点

- **サポートの負担**：Windows 98のCDに入れたことを、チェンは「大失敗」だったと振り返っている。利用者がTweak UIで設定を変えたせいで起きた不具合まで、サポート窓口が原因を調べる羽目になったため。
- **自動ログオンのパスワード**：95・98の版では、パスワードがレジストリにそのまま保存された。XPの版では、LSA（OSの秘密情報の保管場所）に保存するよう改善された。
- **版の取り違え**：OSごとに版が違い、合わない版を入れると不具合が出た。
- **英語版のみ**：日本語版はなかった。XP用の2.10には、有志の「X-Toysを日本語化する」プロジェクトが2003年8月に日本語化ツールを公開した。

## その後

| 時期 | 出来事 |
| --- | --- |
| 2000年代 | PowerToys for Windows XPは、セキュリティの見直しのために一度すべて取り下げられた。戻ってこなかったものもある。 |
| Vista以降 | 公式のTweak UIは出なかった。同じような設定は、サードパーティのツール（Winaero Tweakerなど）や、レジストリ・グループポリシーで変える形になった。 |
| 2019年5月 | Windows 10用に **PowerToys** がオープンソースで復活すると発表された。最初のプレビュー（2019年9月）はFancyZones（ウィンドウの配置）とショートカットガイドで、Tweak UIは含まれない。 |

## 押さえどころ

- Tweak UIは「OSの隠し設定を画面から変える」ツールの元祖的な存在。今の「〇〇Tweaker」系ツールは、その役割を引き継いでいる。
- 名前は同じPowerToysでも、95・XPの時代のものと2019年以降のものは別物。
- 設定が隠されていたのには理由があった。サポートしない、という線を引いたからこそ、Microsoftは無料で配れた。

## 出典

- [Wikipedia：Tweak UI](https://en.wikipedia.org/wiki/Tweak_UI)
- [Wikipedia：Microsoft PowerToys](https://en.wikipedia.org/wiki/Microsoft_PowerToys)
- [The Old New Thing：The history of the Windows PowerToys（2005年2月2日）](https://devblogs.microsoft.com/oldnewthing/20050202-00/?p=36543)
- [The Old New Thing：Tweak UI 2.10についての記事（2003年7月21日）](https://devblogs.microsoft.com/oldnewthing/20030721-00/?p=43093)
- [Neowin：TweakUI 2.10 for Windows XP and Server 2003](https://www.neowin.net/news/tweakui-210-for-windows-xp-and-server-2003/)
- [窓の杜：TweakUI v2.10を日本語化するプログラムが公開（2003年8月25日）](https://forest.watch.impress.co.jp/article/2003/08/25/tweakuixpjpatch.html)
- [GitHub：microsoft/PowerToys](https://github.com/microsoft/PowerToys)

関連：[[Microsoft Plus!]]、[[コンピュータ関連のオワコン]]
