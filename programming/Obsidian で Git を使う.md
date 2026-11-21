---
tags: [プログラミング, Obsidian, git]
aliases: [Obsidian で Git を使う, Obsidian Git, obsidian-git, Git プラグイン]
related:
  - "[[Obsidian を Ubuntu で使う]]"
  - "[[Obsidianのカスタマイズ]]"
確認日: 2026-11-21
---
# Obsidian で Git を使う

**使える。** Community plugin の **Git**（作者 Vinzent03、`obsidian-git`）を入れると、Obsidian の中で **コミット・プル・プッシュ・差分の確認・履歴** ができる。いまの最新は **2.43.0**（2026 年 11 月 5 日）。

- デスクトップでは、パソコンに入っている **git コマンドを呼び出して** 動く。だから、端末や VS Code で使っている git の設定（ユーザー名、SSH の鍵、`.gitignore`）がそのまま効く
- このボールトは、すでに git のリポジトリ（`origin` は `git@github.com:ieremi/obs.git`）なので、入れればすぐ使える

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
- 設定の項目の名前（Auto commit-and-sync interval など）と、既定のコミットメッセージ「vault backup: {{date}}」：一般的な知識（ウェブでの確認はしていない）。くわしくは [プラグインのドキュメント](https://publish.obsidian.md/git-doc)
