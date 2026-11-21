---
tags:
  - KDE
  - ランチャー
---
# KRunner

KRunnerは、KDE Plasmaの検索・実行ツール。通常は `Alt+Space` または `Alt+F2` で開き、文字を入力して候補を選ぶ。アプリの起動、Webページやフォルダーを開く操作、計算などに使える。利用できる検索対象や機能はプラグインで設定できる。[KDE: KRunner](https://docs.kde.org/trunk_kf6/en/plasma-desktop/plasma-desktop/krunner.html)

## Stream DeckやSpacemacsのように使えるか

**よく使う操作をキーボードから呼び出すことはできる。** ただし、%%操作の選び方はそれぞれ異なる%%。

| ツール | 主な操作方法 |
| --- | --- |
| KRunner | 検索欄に名前やコマンドを入力し、候補を選ぶ |
| [[Stream Deck]] | 操作を割り当てたボタンを押す |
| Spacemacs | リーダーキーから始まるキー列を入力する |

たとえば、`Alt+Space` でKRunnerを開き、`spectacle` と入力してEnterを押すと、スクリーンショットツールを起動できる。アプリが提供するDesktop Actionsも検索できるので、Spectacleの特定の撮影操作などを直接選べる。[KDE: Starting Spectacle](https://docs.kde.org/trunk_kf6/en/spectacle/spectacle/starting.html)

KRunnerは検索候補を表示するが、Spacemacsのリーダーキーによる階層型のキー操作や、Stream Deckの常設ボタンをそのまま再現する機能ではない。Spacemacsでは、通常 `SPC` をリーダーキーとして後続のキーを入力する。[Spacemacs documentation](https://www.spacemacs.org/doc/DOCUMENTATION.html)

## 近い操作を作る

- **検索して実行する**：KRunnerでアプリ名やDesktop Actionを検索する。繰り返し使う検索は履歴からも呼び出せる。
- **キーで直接実行する**：Plasmaのシステム設定のショートカットで、アプリやデスクトップの操作にキーを割り当てる。利用できる設定項目はPlasmaのバージョンによって異なる。[KDE: Shortcuts](https://docs.kde.org/stable_kf6/en/plasma-desktop/kcontrol/keys/index.html)
- **複数操作をまとめる**：必要なコマンドをスクリプトにまとめ、KRunnerから実行する。実行前にスクリプトの内容と権限を確認する。
- **画面上のボタンを使う**：[[Stream Deck#ソフトウェアで再現する|ソフトウェア版の操作パネル]]を使う。LinuxではBitfocus Companionが選択肢になる。

アプリ内部の任意の操作までKRunnerで扱えるとは限らない。アプリがDesktop Action、コマンドライン、APIなどを提供しているかによって、実行できる範囲が決まる。
