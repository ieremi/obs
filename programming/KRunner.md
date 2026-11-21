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

## ブラウザのアドレスバー（Ctrl+L）の代わりに使えるか

**KRunnerからブラウザの `Ctrl+L` そのものを押すことはできない。** ただし、アドレスバーでやること（URLを開く、検索する、ブックマークや履歴、開いているタブを呼び出す）の多くはKRunnerでできる。`Ctrl+L` を送る操作そのものが必要なら、別のツールで作る。

以下は、この環境（Plasma 5.27、X11、KRunnerは `Meta+Q` で起動）の設定とインストール済みのプラグインに基づく。実際の動作はまだ試していない。

### KRunnerでアドレスバーの操作をする

| アドレスバーでの操作 | KRunnerでの方法 | 使うプラグイン |
| --- | --- | --- |
| URLを開く | `kde.org` や `https://…` を入力してEnter。既定のブラウザで開く | Locations（場所） |
| 検索する | `gg:検索語`（Google）、`dd:検索語`（DuckDuckGo）、`wp:検索語`（Wikipedia）、`yt:検索語`（YouTube） | Web Search Keywords（ウェブ検索キーワード） |
| ブックマークを開く | ブックマーク名の一部を入力する | Bookmarks（ブックマーク） |
| 履歴から開く | 以前開いたページのタイトルやURLの一部を入力する | Browser History（ブラウザの履歴） |
| 開いているタブに移る | タブのタイトルの一部を入力すると、そのタブに切り替わる | Browser Tabs（ブラウザのタブ） |

- 検索キーワードと区切り文字（既定は `:`）は、システム設定の「検索」→「ウェブ検索キーワード」で追加・変更できる。キーワードなしの入力をどの検索エンジンに送るかも、ここで決められる。
- 履歴とタブの検索は、Plasma Browser Integrationを使う。この環境ではシステム側のパッケージ（`plasma-browser-integration`）は入っているので、ブラウザに拡張機能「Plasma Integration」を入れれば使える。履歴の検索は、拡張機能の設定で有効にする必要がある場合がある。[KDE Community: Plasma Browser Integration](https://community.kde.org/Plasma/Browser_Integration)
- UbuntuのFirefoxはSnap版で、拡張機能とシステム側の連携（ネイティブメッセージング）がうまく動かないことがある。その場合、タブと履歴の検索は使えない。

### `Ctrl+L` そのものを送る

ブラウザを前面に出してアドレスバーにフォーカスを移す操作を、全体のショートカットに割り当てることもできる。X11では `xdotool` でウィンドウを選んでキー入力を送れる（この環境には未インストール。`sudo apt install xdotool` で入れる）。[xdotool](https://github.com/jordansissel/xdotool)

```sh
xdotool search --onlyvisible --class firefox windowactivate --sync key --clearmodifiers ctrl+l
```

このコマンドを、システム設定の「ショートカット」→「カスタムショートカット」でキーに割り当てる。KRunnerに入力して実行してもよいが、その場合は毎回コマンドを打つことになるので、ショートカットに割り当てる方が実用的である。

- `--class firefox` を `chromium` などに替えれば、ほかのブラウザにも使える。
- Waylandでは `xdotool` はほとんどのウィンドウに効かない。Waylandに移ったら、`ydotool` など別の方法が必要になる。

### 新しいタブで入力を始める

新しいタブを開くと、たいていのブラウザでアドレスバーにフォーカスが移る。したがって、次のコマンドをショートカットに割り当てると、「ブラウザを前に出してアドレスバーに入力する」に近い操作になる。追加のツールは要らない。

```sh
firefox --new-tab about:newtab
```

ただし、今のタブのURLを編集したいとき（`Ctrl+L` でURLを選択してコピーするなど）は、この方法では代わりにならない。
