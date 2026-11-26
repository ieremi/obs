---
tags: [プログラミング, Obsidian, git]
aliases: [Obsidian で Git を使う, Obsidian Git, obsidian-git, Git プラグイン]
related:
  - "[[Obsidian を Ubuntu で使う]]"
  - "[[Obsidianのカスタマイズ]]"
確認日: 2026-11-26
---
# Obsidian で Git を使う

**使える。** Community plugin の **Git**（作者 Vinzent03、`obsidian-git`）を入れると、Obsidian の中で **コミット・プル・プッシュ・差分の確認・履歴** ができる。いまの最新は **2.43.0**（2026 年 11 月 5 日）。

- デスクトップでは、パソコンに入っている **git コマンドを呼び出して** 動く。だから、端末や VS Code で使っている git の設定（ユーザー名、SSH の鍵、`.gitignore`）がそのまま効く
- このボールトは、すでに git のリポジトリ（`origin` は `git@github.com:ieremi/obs.git`）なので、入れればすぐ使える

## ほかの人は vault をどう Git 管理しているか

調査・確認日：**2026-11-26**。公開された利用者の投稿と開発元のドキュメントから、次のような運用が確認できた。利用率の統計ではないため、どれが多数派かまでは判断できない。

### 運用は「同期も Git」か「履歴だけ Git」かで分かれる

| 運用 | 実際の使い方 | 向いている条件 |
| --- | --- | --- |
| Git を同期と履歴保存に使う | 端末ごとに clone し、編集前に pull、編集後に commit・push。Obsidian Git で自動化することもできる | 主に PC で使い、競合を自分で解決できる |
| Obsidian Sync で同期し、Git は履歴保存 | ノートの転送は Sync、Git の commit・push は代表の PC で行う | スマホでも編集しつつ、Git の差分・履歴を残したい |
| iCloud などで同期し、Git は履歴保存 | ノートはクラウド同期し、Git の管理データは同期対象外の場所に置く | すでにクラウド同期を使っている |
| Obsidian の外で Git を操作 | 端末や VS Code で変更を選び、意味のある単位でコミットする | コミットの内容・メッセージを確認して残したい |

Git プラグインは自動 commit-and-sync と差分・履歴表示に対応する。一方、開発元はモバイル版に不安定さがあることも明記している。PC と同じ安定性を前提にスマホへ広げるのは避けたい。[Git プラグインの README](https://github.com/Vinzent03/obsidian-git)

**「同期は別のサービス、Git は履歴」という構成は、プラグイン公式ドキュメントにも載っている運用**。Git を一台だけで動かすための `Disable on this device` と、別サービスが同期したファイルを pull で更新しないための `Other sync service` という merge strategy が案内されている。これは目的に応じた設定であり、通常の Git 同期にそのまま当てはめるものではない。[Git：Tips and Tricks](https://publish.obsidian.md/git-doc/Tips-and-Tricks)

### 利用者が公開している具体例

- **iCloud と Git を併用する人**：iCloud が `.git` 内の管理データまで同期して競合した経験から、管理データをクラウド外へ移し、vault 内には参照用の `.git` ファイルを置く構成を紹介している。これは本人の経験談で、あらゆる競合を防ぐ保証ではない。[本人の投稿：Using git for versioning alongside cloud for syncing](https://www.reddit.com/r/ObsidianMD/comments/1fia8yi/using_git_for_versioning_alongside_cloud_for/)
- **設定をどこまで共有するか迷う人**：`.obsidian/` 全体を無視する案に対し、開いているタブなどの workspace だけ除外し、テーマやプラグインは共有する考え方が議論されている。設定全体を除外すると端末ごとの設定になる、という違いがある。[利用者の議論：Ignore .obsidian when using git to sync?](https://www.reddit.com/r/ObsidianMD/comments/1js8b9i/ignore_obsidian_when_using_git_to_sync/)

### `.gitignore` は「ノート」と「端末の状態」を分ける

Git プラグインの公式ドキュメントは、`.obsidian/` 全体を除外する方法と、workspace だけを除外する方法を選択肢として示している。後者を使う基本例は次のとおり。[公式の Gitignore 例](https://publish.obsidian.md/git-doc/Tips-and-Tricks)

```gitignore
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.trash/
.DS_Store
```

テーマ・ショートカット・CSS も再現したければ、それらは追跡する。プラグイン設定に認証情報が入る場合は、そのファイルを個別に除外する。すでに追跡中のファイルは `.gitignore` に書くだけでは追跡が止まらない。

### この保管庫との比較と提案

2026-11-26 に確認した、このリポジトリ（`Documents/obs`）の状態：

- `obs/.git` はディレクトリではなく、`gitdir: /Users/ieremius/git/obs.git` と書かれた参照ファイル。**Git の管理データはすでに iCloud の外にある**。
- `.gitignore` で workspace、graph、ゴミ箱、OS のファイル、一部の AI プラグインの設定・生成物を除外している。
- したがって、構成は上記の「クラウド同期の対象から Git 管理データを分離する」実例に近い。ただし、他端末の同期設定や動作までは今回確認していない。

**この構成を保ち、Git に履歴を残す操作は代表の PC に寄せるのが、まず取りやすい運用**と考える。ノートを同期する役割と Git の履歴を作る役割を明確にできる。内容を確認してコミットする現在の方針なら、ほかの人が自動コミットしているからといって自動化する必要はない。復元用の細かい記録を優先したい場合は、一定間隔の自動コミットも選択肢になる。

別の PC でも Git を動かす場合、`.git` ファイルの絶対パスは各端末で有効な必要がある。その参照ファイル自体を iCloud で共有しても、参照先の Git 管理データが各端末へ用意されるわけではない。Git が管理データを別の場所に置く仕組み自体は `--separate-git-dir` として公式に用意されている。[Git：git-init](https://git-scm.com/docs/git-init)

なお、Obsidian 公式は同じ vault を複数の同期サービスで同時に同期しないよう案内している。履歴保存用の Git を追加する場合も、iCloud に加えて各端末から Git の pull でノートを書き換える運用に広げる際は、どちらが同期を担うかを決める必要がある。[Obsidian：Sync your notes across devices](https://obsidian.md/help/sync-notes)

上記は運用の提案であり、今回、Git 設定・同期設定・自動コミット設定は変更していない。

### Obsidian Sync で同期し、Git は履歴保存にする場合の点検

> [!note] この方針は同じ日に取りやめた
> 2026-11-26 のうちに、Obsidian Sync は使わず iCloud で同期する方針に変えた。現在の構成は「[[#iCloud で同期し、Git は履歴保存にする（現在の構成）]]」を参照。以下はその前の点検と作業の記録として残す。

2026-11-26 に、この Mac の保管庫の実物と Obsidian 公式ヘルプで確かめた。

**結論：いまの構成は、この運用には合っていない。** 直すべき点は次の 2 つ。

#### 1. 保管庫が iCloud Drive の中にある

- 保管庫のルートは `~/Library/Mobile Documents/iCloud~md~obsidian/Documents`、つまり iCloud Drive の Obsidian フォルダーである。`.obsidian/core-plugins.json` では Sync も有効になっている。
- Obsidian 公式は「Obsidian Sync をクラウドストレージ（iCloud、Dropbox、OneDrive、Google Drive など）と併用することはすすめない。競合の原因になる」としている。iCloud から切り替えるときは、まず保管庫を iCloud の外へ移すよう案内している。[Obsidian：Switch to Obsidian Sync](https://obsidian.md/help/sync/switch)
- 併用すると、復元したファイルが Sync からすぐ消えるといった症状が出るとトラブルシューティングに書かれている。[Obsidian：Troubleshoot Obsidian Sync](https://obsidian.md/help/sync/troubleshoot)
- macOS での置き場所の例として、公式は `/Users/<ユーザー名>/vaults` を挙げている。

#### 2. Git の範囲が保管庫の一部だけになっている

- Git の作業ツリーは `Documents/obs` で、保管庫ルートの `Documents` ではない。Obsidian Git も `basePath: "obs"` で動いている。
- そのため、ルート直下にある `.obsidian/`（設定・テーマ・スニペット）、`AGENTS.md`、`クービビック.md`、`ハイドロキノン.md`、`copilot/` などは Git の履歴に残らない。
- 2026-11-25 のコミット「Obsidian設定を保管庫ルートへ統合」で `.obsidian/` は `obs` の外へ出た。`obs/.gitignore` に書かれた `.obsidian/workspace.json`、`.claude/settings.json`、`/copilot/copilot-conversations/` などは、保管庫ルートが Git のルートでもある前提の書き方で、いまは該当するファイルが `obs` の中にない。
- `obs/Users:.fileloc` は、Finder が作った場所の参照ファイル（中身は `.obsidian/snippets` へのリンク）で、ノートではない。未追跡のまま残っている。

#### 問題ない点

- Git の管理データを `~/git/obs.git` に置き、`obs/.git` を参照ファイルにしている点は、iCloud をやめた後も使える。参照先は絶対パスなので、保管庫を移しても有効である。
- Obsidian Sync は `.` で始まるファイル・フォルダーを同期しない（例外は `.obsidian`）。公式は除外される例として `.git` と `.gitignore` を挙げている。そのため、Sync に移った後は `.git` を保管庫の中に普通のフォルダーとして置いても Sync とはぶつからない。[Obsidian：Sync settings](https://obsidian.md/help/sync/settings)
- 逆に、`.gitignore` も Sync されないので、Git を動かす Mac にだけあればよい。

#### 目標の構成

| 場所 | Obsidian Sync | Git |
| --- | --- | --- |
| 保管庫ルート（iCloud の外、例：`~/vaults/obs`） | 同期する | ここを作業ツリーのルートにする |
| `.obsidian/`（設定・プラグイン・スニペット） | 同期する | 追跡する（`workspace*.json`、`graph.json`、認証情報の入る `data.json` は除外） |
| ノートのフォルダー（`med/`、`programming/` など） | 同期する | 追跡する |
| `.git`（フォルダー、または `~/git/obs.git` への参照ファイル） | 同期されない | 代表の Mac だけに置く |

保管庫ルートと Git のルートを一致させるには、次の 2 案がある。どちらにするかはまだ決めていない（計画段階）。

- **案 A：`obs` を保管庫にする。** ルート直下の `.obsidian/`、`AGENTS.md`、2 つのノート、`copilot/` を `obs` に入れ、`obs` を iCloud の外へ移して保管庫として開き直す。Git の中のパスが変わらず、いまの `.gitignore` がそのまま当てはまる。昨日の統合の向きを戻すことになるので、`obs/AGENTS.md` とルートの `AGENTS.md` の中身は 1 つにまとめる必要がある。
- **案 B：いまのルート（`Documents`）を Git のルートにする。** Git の作業ツリーを 1 つ上へ広げる。すべてのノートのパスに `obs/` が付くので、履歴上は全ファイルの移動になる（`git log --follow` で追える）。

パスが変わらず、`.gitignore` が案 A の形で書かれていることから、**案 A のほうが手間と混乱が少ない**と考える。

#### 移すときの手順（案）

1. すべての端末で Obsidian を終了し、保管庫のバックアップをとる。
2. この Mac で、保管庫の切り替え画面の「保管庫を別のフォルダーへ移動」を使い、iCloud の外（例：`~/vaults/`）へ移す。[Obsidian：Switch to Obsidian Sync](https://obsidian.md/help/sync/switch)
3. `git rev-parse --show-toplevel` で、Git が新しい場所を作業ツリーとして認識しているか確かめる。
4. Sync の設定で、移した保管庫をリモート保管庫につなぎ直す。
5. iPhone などほかの端末では iCloud の保管庫を使わず、Sync から新しいローカル保管庫を作る。公式も、すでに Sync にデータがあるならそうするよう案内している。古い iCloud のフォルダーは、同期が済んだのを確かめてから消す。
6. `.obsidian/plugins/` は Sync で配られるので、Git のプラグインもほかの端末に届く。Git を動かすのは代表の Mac だけにし、ほかの端末ではプラグインの `Disable on this device` を入れる。[Git：Tips and Tricks](https://publish.obsidian.md/git-doc/Tips-and-Tricks)
7. 代表の Mac で Obsidian Git の pull を使うなら、merge strategy を `Other sync service` にするか、pull を切って commit・push だけにする。
8. `obs/Users:.fileloc` を消す。案 A なら、Obsidian Git の `basePath` を空に戻す。

#### 移行の記録（2026-11-26 実施、案 A）

確定したこと：

- 保管庫を `~/vaults/obs` に作り直した。元の `iCloud~md~obsidian/Documents` は消さずにバックアップとして残してある（コピーで移したため）。
- 元のルートにあった `.obsidian/`、`copilot/`、`.copilot/`、`.claude/settings.local.json` を `obs` の中へ入れた。`.claude/skills/` のシンボリックリンクは、iCloud の絶対パスから相対パス（`../../copilot/skills/…`）に張り直した。
- ルート直下の `クービビック.md` と `ハイドロキノン.md` は `med/drug/` へ移した。
- 2 つの `AGENTS.md` を 1 つにまとめ、Ohohama のスニペットの配置先を新しいパスに直した。
- Obsidian Git の `basePath` を空にした（保管庫ルートと Git のルートが一致したため）。
- `.gitignore` に `.claude/settings.local.json` と `*.fileloc` を足した。`Users:.fileloc` は消した。
- Obsidian の保管庫一覧（`~/Library/Application Support/obsidian/obsidian.json`）で、同じ保管庫 ID の場所を新しいパスに書きかえた。
- `git rev-parse --show-toplevel` が `/Users/ieremius/vaults/obs` を返すことを確かめた。

移さなかったもの：中身のない `Untitled.base`・`Untitled.canvas`、設定のバックアップ `.config-backups/`。これらは元の iCloud フォルダーに残っている。

まだ済んでいないこと（手作業が要る）：

1. Obsidian を起動し、`~/vaults/obs` が開くことを確かめる。
2. 設定 → Sync で、この保管庫をリモート保管庫に接続する（`sync.json` がなく、まだ接続されていなかった）。
3. iPhone などでは、iCloud の保管庫を開かず、Sync から新しいローカル保管庫を作る。Git のプラグインは `Disable on this device` にする。
4. 新しく Git の追跡対象になった `.obsidian/`、`copilot/skills/` の一部、移したノートを確認してコミットする。
5. すべて問題なければ、元の iCloud フォルダーを消す。

#### 元の iCloud フォルダーを消してよいか（2026-11-26 15 時ごろ点検）

**中身の面では消してよい。** 元のフォルダーにしかないものは、次のとおり不要なものだけだった。コピーの後に iCloud 側で更新されたファイルもなかった。

- `.DS_Store`（Finder が作るファイル）と `Users:.fileloc`（場所の参照ファイル）。
- 中身のない `Untitled.base`・`Untitled.canvas`。
- 統合前の設定のバックアップ `.config-backups/`。念のため残すなら、iCloud の外へ移しておく。

**ただし、消すのは次の 3 点が済んでからにする。**

1. **開いている保管庫が `~/vaults` になっている。** Obsidian の保管庫一覧で開いているのは `~/vaults/obs` ではなく、その 1 つ上の `~/vaults` で、そこに新しい `.obsidian/` ができていた。このまま使うと、保管庫ルートが Git のルートより上になり、移行前と同じずれが起きる。保管庫の切り替え画面で `~/vaults/obs` を開き直し、`~/vaults` は一覧から外す。`~/vaults/.obsidian/` は Ohohama のスニペットを入れて表示を整えただけのもので、`~/vaults/obs/.obsidian/` に同じスニペットがある。
2. **Sync にまだつながっていない。** どちらの保管庫にも Sync の接続の記録がない。`~/vaults/obs` を Sync のリモート保管庫につなぐ。
3. **ほかの端末を Sync に切り替える。** iCloud のフォルダーを消すと、iPhone などの iCloud 上の保管庫も消える。先に各端末で Sync から新しい保管庫を作り、iCloud の保管庫に未同期の変更がないことを確かめる。

消すときは、Obsidian の保管庫一覧から元の保管庫を外してから、Finder で `iCloud Drive/Obsidian/Documents` をゴミ箱に入れる。ゴミ箱を空にするまでは取り戻せる。

### iCloud で同期し、Git は履歴保存にする（現在の構成）

2026-11-26 に、Obsidian Sync は使わず、iCloud で同期する方針に決めた（確定）。

#### 構成

| 場所 | iCloud | Git |
| --- | --- | --- |
| 保管庫ルート `iCloud Drive/Obsidian/obs`（Mac では `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/obs`） | 同期する | 作業ツリーのルート |
| `.obsidian/`、ノートのフォルダー | 同期する | 追跡する（`workspace*.json`、`graph.json`、プラグイン本体 `main.js`、認証情報の入る `data.json` は除外） |
| `.git`（`gitdir: /Users/ieremius/git/obs.git` と書いた参照ファイル） | 同期される（数十バイトのテキストで、ほかの端末では使われない） | 管理データの本体は iCloud の外の `~/git/obs.git` |

- iPhone・iPad の Obsidian は、iCloud Drive の `Obsidian` フォルダーの中にあるフォルダーを保管庫として扱う。そのため、保管庫は `Documents` 直下の 1 つのフォルダー（`obs`）にし、`Documents` 自体には設定やノートを置かない。[Obsidian：Sync your notes across devices](https://obsidian.md/help/sync-notes)
- Git の管理データを iCloud の外に置くのは、iCloud が `.git` の中の小さなファイルを同期して壊したり競合させたりするのを避けるため。利用者の報告にもとづく対策で、公式の保証ではない。[本人の投稿：Using git for versioning alongside cloud for syncing](https://www.reddit.com/r/ObsidianMD/comments/1fia8yi/using_git_for_versioning_alongside_cloud_for/)
- Git を動かすのはこの Mac だけにする。`.obsidian/plugins/` は iCloud で配られるので、iPhone などでは Git のプラグインを `Disable on this device` にする。Mac で pull を使う場合は merge strategy を `Other sync service` にする。[Git：Tips and Tricks](https://publish.obsidian.md/git-doc/Tips-and-Tricks)
- 同期サービスを 2 つ重ねないよう、コアプラグインの Sync は切った。

#### 作業の記録（2026-11-26 実施）

- Obsidian を終了してから、`~/vaults/obs` を `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/obs` へ移した。`git rev-parse --show-toplevel` がこのパスを返すことを確かめた。
- 元の iCloud の `Documents` にあった古いコピー（`obs/`、`.obsidian/`、`copilot/`、`AGENTS.md`、2 つのノート、`Untitled.*`、`.config-backups/` など）は、消さずに iCloud の外の `~/vaults-backup/icloud-Documents-20261126/` へ移した。誤って `~/vaults` を保管庫として開いたときにできた `.obsidian/` も、同じ場所に `vaults-parent.obsidian` として移した。
- `.obsidian/core-plugins.json` で Sync を切った。
- Obsidian の保管庫一覧で、保管庫の場所を新しいパスに直し、`~/vaults` の項目を消した。
- Copilot プラグインが `.claude/skills/` のリンクを `~/vaults/obs` の絶対パスで作り直していたので、相対パスに戻した。
- `.gitignore` に `*.icloud`（iCloud がまだダウンロードしていないファイルの仮置き）を足した。
- `AGENTS.md` の保管庫の場所と Ohohama のコピー先を、新しいパスに直した。

#### 気をつけること

- **「Mac のストレージを最適化」が入っている**（`com.apple.bird optimize-storage` が 1）。空き容量が減ると、iCloud がノートをこの Mac から追い出して中身のない仮置きにすることがある。Git や検索が中身を読めなくなることがあるので、Finder で `obs` フォルダーを右クリックし「ダウンロードしたままにする」を選ぶか、システム設定の iCloud Drive で最適化を切るとよい。
- iCloud が競合すると、`ノート 2.md` のような名前の複製ができる。Git の差分に見慣れないファイルが出たら、まず競合を疑う。
- `~/vaults-backup/icloud-Documents-20261126/` は、iPhone などで新しい `obs` が問題なく開けるのを確かめてから消してよい。

## 入れ方
1. 設定（`Ctrl+,`）→ **Community plugins** → **Browse**
2. 「**Git**」をさがす（作者 Vinzent03）→ **Install** → **Enable**
3. 左のリボンや、コマンドパレット（`Ctrl+P`）で「Git:」から始まるコマンドが使えるようになる

### Linux での注意
- **Snap 版の Obsidian では動かない**（Snap の sandbox が git を呼べない）
- **Flatpak 版はすすめない**（システムのファイルに全部は届かない）
- **.deb か AppImage** で入れた Obsidian で使う。このパソコンは .deb なので問題ない（→ [[Obsidian を Ubuntu で使う]]）

## できること

| 画面・機能 | 中身 | 開き方 |
| --- | --- | --- |
| **Source Control View** | 変更したファイルの一覧。ステージ・アンステージ・コミット | コマンド `Open source control view` |
| **History View** | コミットの履歴と、そこで変わったファイル | `Open history view` |
| **Diff View** | 変更を左右に並べて見る。かたまり（hunk）ごとにステージ・取り消し | `Open diff view` |
| **エディターの印** | 追加・変更・削除した行に、行の横で印をつける（デスクトップだけ） | プラグインの設定でオン |
| **衝突の解決** | 衝突した所をエディターの中で色分けし、どちらを残すかボタンで選ぶ | 衝突したとき |
| **自動の commit-and-sync** | 決めた間隔で、コミット → プル → プッシュ | プラグインの設定 |
| **起動時の自動プル** | Obsidian を開いたときにプル | プラグインの設定 |
| GitHub で開く | いまのファイルや、その履歴を GitHub で開く | `Open file on GitHub` |

### Git パネルを左下に置く
Source Control View は、はじめは **右のサイドバー** に開く。**ドラッグで左下に移せる**（設定の項目はない）。

1. 左のサイドバーを開いておく（左上のサイドバーのアイコン）
2. 右のサイドバーの上にある **Source Control のアイコン**（枝分かれの形）を、マウスでつかむ
3. 左のサイドバーの **ファイル一覧の下のほう** へ持っていく。**下半分が青くなった** ところで離す
4. 左のサイドバーが上下に分かれ、**上がファイル一覧、下が Git** になる。境目はドラッグで高さを変えられる

- 下半分ではなく **タブの並び** に落とすと、ファイル一覧と同じ場所のタブになる（上下に分かれない）。そのときは、もう一度つかんで下のほうへ落としなおす
- 置き場所は **`.obsidian/workspace.json`** に保存される。このファイルは `.gitignore` で外しているので、**パソコンごとの設定** になる（ほかのパソコンでは、また右に出る）
- 一度閉じても、コマンド `Open source control view` で開きなおすと、最後に置いた場所に出る

### よく使うコマンド
| コマンド | すること |
| --- | --- |
| `Commit` | ステージしたものをコミット（なければ、設定によって全部をステージしてコミット） |
| `Commit with specific message` | メッセージを入れてコミット |
| `Commit all changes` | 全部をコミット（プッシュはしない） |
| `Commit-and-sync` | 全部をコミット → プル → プッシュ |
| `Push` / `Pull` | プッシュ・プル |
| `List changed files` | 変更したファイルの一覧 |
| `Discard all changes` | 変更を全部すてる（**注意**） |
| `Add file to .gitignore` | いまのファイルを `.gitignore` に足す |

## このボールトでのおすすめの設定
このボールトは、**コミットのメッセージを日本語で 1 つずつ書く**（「〇〇を追加」）運用なので、**自動のコミットは切っておく** のがよい。

| 設定 | おすすめ | わけ |
| --- | --- | --- |
| Auto commit-and-sync interval | **0（切る）** | 自動にすると「vault backup: 日時」というメッセージのコミットが勝手にたまる |
| Auto pull interval | 0 か、長め | ほかのパソコンでも書くなら、起動時のプルだけで足りる |
| Pull on startup | オン（ほかの所でも書くなら） | |
| Commit message | 手で書く（`Commit with specific message` を使う） | |
| Show status bar | オン | 下の帯に、変更したファイルの数が出る |
| 行の印（Signs） | 好みで | 書いたところがひと目でわかる |

- 既定のコミットメッセージは「`vault backup: {{date}}`」の形。自動で使うなら、ここを変えられる
- **Claude Code でコミットするのと、ぶつからないように**：Obsidian で自動コミットを切っておけば、Claude Code に「コミットしてください」とたのむいまのやり方と両立する

## コミットメッセージを AI に考えてもらう

### 1. Git プラグインの「Commit message script」（おすすめ）
Git プラグインの設定に **Commit message script** がある。コミットのときに、ここに書いたコマンドを **リポジトリのフォルダーで `sh -c` で動かし、その標準出力をコミットメッセージにする**（デスクトップだけ）。ここで **Claude Code を `-p`（1 回だけ答えるモード）で呼べば**、AI がメッセージを考える。

スクリプトの例（`obs-commit-msg`）：

```sh
#!/bin/sh
# Obsidian Git の「Commit message script」から呼んで、Claude にコミットメッセージを考えさせる
# Obsidian はリポジトリのフォルダーで sh -c で動かし、標準出力をメッセージにする
CLAUDE="$HOME/.local/bin/claude"   # nvm の PATH は Obsidian から見えないので、フルパスで

{
  echo "## git status"
  git status --porcelain
  echo "## 変更の量"
  git diff HEAD --stat
  echo "## 変更の中身（一部）"
  git diff HEAD | head -c 20000
} | "$CLAUDE" -p --model haiku \
  "標準入力は、Obsidian のボールト（ノートの git リポジトリ）の変更です。これに合う日本語のコミットメッセージを 1 行だけ書いてください。
形は「〇〇を追加」「〇〇を直す」「〇〇と△△を追加」のように短く。〇〇にはノートのファイル名（拡張子なし）を使う。
説明・引用符・前置きはつけず、メッセージの 1 行だけを出力してください。"
```

使い方：
1. 上のスクリプトを、たとえば `~/.local/bin/obs-commit-msg` に置き、`chmod +x` する
2. Git プラグインの設定 → **Commit message script** に、`/home/ieremius/.local/bin/obs-commit-msg` と書く
3. **Commit** や **Commit-and-sync** をすると、メッセージの欄が空でも、AI が考えたメッセージでコミットされる

- 2026-11-21 にこのパソコンで試した：約 **6 秒** で「Obsidianのカスタマイズとohohamaを追加」のような 1 行が返った
- **`claude` のログインの警告などは標準エラーに出る** ので、メッセージにはまじらない（標準出力だけを見て確かめた）
- `--model haiku` は、速くて安いモデル。もっとよいメッセージがほしければ、`--model sonnet` にする
- 変更が大きいときは、中身を 20,000 バイトで切っている（AI に送る量をおさえるため）
- ノートの変更の中身が **Anthropic に送られる** ことに注意
- Claude の代わりに Codex を使うなら、`codex exec "…"` で同じことができる（試していない）
- 「Co-Authored-By」の行をつけたいなら、スクリプトの最後で `printf '\n\nCo-Authored-By: …'` を足す

### 2. Copilot の Agent や Claude Code にたのむ
- Obsidian の Copilot の Agent（Claude Code・Codex）で「変更を見て、コミットして」とたのむ（→ [[Obsidian から AI を使う]]）
- いま VS Code の横の Claude Code にたのんでいるのと同じやり方。メッセージの形を `CLAUDE.md` に書いておくと、毎回そろう

### 3. VS Code のソース管理
- VS Code のソース管理の、コミットメッセージの欄の **✨（きらきら）のボタン** で、AI がメッセージを書く（GitHub Copilot の機能）

## `.obsidian/` の扱い
- Obsidian は、開いているだけで **`.obsidian/workspace.json`**（開いているタブなど）や **`graph.json`**（グラフの拡大率）を書きかえる。これをコミットすると、意味のない変更がたまる
- このボールトの `.gitignore` は、すでに `workspace.json`・`workspace-mobile.json`・`.trash/` を外している
- `graph.json` もいつも変わるので、2026-11-21 に `.gitignore` に `.obsidian/graph.json` を足し、`git rm --cached .obsidian/graph.json` で追跡をやめた（ファイルはパソコンに残る）
  - 一度コミットしたファイルは、`.gitignore` に書くだけでは追跡が止まらない。`git rm --cached` が要る
- プラグインを入れると `.obsidian/plugins/obsidian-git/` ができる。設定（`data.json`）をほかのパソコンと共有したいなら、コミットしてよい

### `appearance.json` は ignore しなくてよい
**外さずに、コミットしつづけるのがよい。** `workspace.json` や `graph.json` とちがって、開いているだけでは書きかわらない。設定画面の「外観」を変えたときだけ変わる。

中身（2026-11-22 に見た）：

| 項目 | 値 | 意味 |
| --- | --- | --- |
| `theme` | `moonstone` | 基本の色。`moonstone` は明るい色（light）、`obsidian` は暗い色（dark）、`system` は OS に合わせる |
| `enabledCssSnippets` | `ubuntu-ja`、`ohohama` | 有効にしている CSS snippet |
| `showRibbon` | `true` | 左のリボンを出す |
| `accentColor` | `""` | アクセントの色（空は既定） |

- **snippet とセットになっている**：`.obsidian/snippets/ohohama.css` はコミットしてある。`appearance.json` を外すと、ほかのパソコンで snippet のファイルは来るのに、有効にはならない
- **変わる回数が少ない**：見た目を変えたときに、意味のある変更として「〇〇を変更」とコミットすればよい
- ほかのパソコンでも同じ見た目にしたいなら、なおさら共有したほうがよい

#### ただし、`theme` は何度も変わっている
履歴を見ると、`theme` が 1 日で `obsidian` → `moonstone` → `obsidian` → `moonstone` と変わっている（2026-11-21〜22）。明るい色と暗い色を **時間や気分で切りかえている** なら、そのたびに差分が出る。そのときは、次のどれかにする。

1. **（おすすめ）OS に合わせる**：設定 → 外観 → **基本の配色**（Base color scheme）を「**システムに合わせる**」（Adapt to system）にする。`theme` が `system` で固定され、明るさは KDE の設定で切りかわる。ファイルはもう変わらない
2. **手元の変更として無視する**：`git update-index --skip-worktree .obsidian/appearance.json` とすると、追跡はつづけたまま、このパソコンでの変更を git が見なくなる。もどすときは `--no-skip-worktree`。ただし、ほかのパソコンからこのファイルの変更がプルされると、ぶつかることがある
3. **パソコンごとに見た目を変えたい** なら、`.gitignore` に足して `git rm --cached` する。snippet の有効・無効もパソコンごとになる

- 1 台のパソコンでしか使っていないなら、どれもしないで、変えたときにコミットするだけでもよい

#### 気づいたこと
- `enabledCssSnippets` に `ubuntu-ja` があるが、`.obsidian/snippets/` には `ohohama.css` しかない。`ubuntu-ja.css` は消したか、まだ作っていないかで、いまは何も効いていない。要らなければ、設定 → 外観 → CSS snippets で切れば、ここから消える

## `.claude/settings.json` の扱い
**このボールトでは、`.gitignore` で外す（コミットしない）のがよい。**

`.claude/settings.json` は Claude Code の **プロジェクトの設定**。本来は、チームで共有する設定（許可するコマンド、フックなど）を書いて **コミットする** ためのファイルである。自分だけの設定は **`.claude/settings.local.json`** に書き、こちらはコミットしない、という分け方になっている。

ただ、このボールトの `settings.json`（2026-11-22 に見た）は、中身が次のようになっている。

- `permissions.allow` に、Claude が **1 回だけ動かした長い Bash のコマンド** が、そのまま並んでいる。ツールの実行を「許可」したときに、自動で足されたもの
- コマンドが一字一句同じでないと効かないので、**あとで役に立たない**
- `/home/ieremius/…` のような **このパソコンのパス** が入っている
- 許可するたびに書きかわるので、コミットすると **意味のない変更がたまる**（`graph.json` と同じ）

共有したい設定は入っておらず、ほかのパソコンで同じ設定が要るわけでもない。したがって、外してよい。

```gitignore
.claude/settings.json
```

- `settings.local.json` は、パソコン全体の gitignore（`~/.config/git/ignore`）の `**/.claude/settings.local.json` で、すでに外れている
- `.claude/skills/` も、このボールトの `.gitignore` で外している。`.claude/agents/`・`.claude/commands/` は空なので、git には出てこない
- `settings.json` はまだ一度もコミットしていない（`?? .claude/`）ので、`git rm --cached` は要らない。`.gitignore` に 1 行足すだけでよい
- 2026-11-22 に、このボールトの `.gitignore` に `.claude/settings.json` を足した
- 中身は消してもかまわない。のこすなら、`"Bash(git status*)"` のように **何度も使う形** に書きなおす

### コミットしたほうがよい場合
- **いつも使う許可やフック** を、ほかのパソコンでも同じにしたいとき。たとえば「`git diff` と `git log` は聞かずに動かす」など
- そのときは、長いコマンドを消して、`Bash(git log*)` のような短い形だけを `settings.json` に残し、コミットする。その場限りの許可は `settings.local.json` に入るようにする

## Git プラグインと、ほかの方法のちがい
| 方法 | よいところ | 気をつけること |
| --- | --- | --- |
| **Git プラグイン** | Obsidian から出ずに、差分を見てコミットできる | Snap では動かない。スマホでは不安定 |
| **端末・VS Code の git** | 何でもできる | Obsidian の外 |
| **Claude Code**（いまのやり方） | メッセージも書いてくれる | Obsidian の外 |
| Obsidian Sync（有料） | スマホとも安定して同期 | 履歴は git ほど細かくない。お金がかかる |

- **スマホ（iOS・Android）では、Git プラグインは「とても不安定」** と作者自身が書いている。スマホでも使うなら、Obsidian Sync などのほうがよい

## 押さえどころ
- Obsidian で git は **使える**。Community plugin の **Git**（Vinzent03）を入れる
- デスクトップでは **パソコンの git** を使うので、SSH の鍵などの設定がそのまま効く
- Linux では **Snap 版では動かない**。.deb か AppImage で
- Source Control・History・Diff の画面、行の印、衝突の解決、自動の commit-and-sync ができる
- このボールトでは、**自動のコミットは切って**、メッセージは手で書く（または Claude Code にまかせる）

## 出典
- [obsidian-git の README（GitHub）](https://github.com/Vinzent03/obsidian-git)：できること（Source Control・History・Diff の画面、エディターの印、衝突の解決、自動の commit-and-sync、起動時のプル、GitHub で開く）、コマンドの一覧、Linux では Snap が使えず Flatpak はすすめないこと、デスクトップではパソコンの git を呼ぶこと、スマホではとても不安定なこと
- GitHub の API（`Vinzent03/obsidian-git` の latest）：2.43.0、2026 年 11 月 5 日（このパソコンで curl で調べた）
- このボールトの `origin` と `.gitignore`：このパソコンで見た
- [Obsidian：Switch to Obsidian Sync](https://obsidian.md/help/sync/switch)、[Sync settings](https://obsidian.md/help/sync/settings)、[Troubleshoot Obsidian Sync](https://obsidian.md/help/sync/troubleshoot)、[Sync FAQ](https://obsidian.md/help/sync/faq)：Sync とクラウドストレージの併用をすすめないこと、iCloud の外へ移す手順、`.` で始まるファイルが同期されないこと（2026-11-26 確認）
- 保管庫の場所、`core-plugins.json` の Sync、Obsidian Git の `basePath`、`obs/.git` の参照先：このパソコンで見た（2026-11-26）
- 設定の項目の名前（Auto commit-and-sync interval など）と、既定のコミットメッセージ「vault backup: {{date}}」：一般的な知識（ウェブでの確認はしていない）。くわしくは [プラグインのドキュメント](https://publish.obsidian.md/git-doc)
