---
aliases:
  - Git の includeIf
  - Git で匿名をデフォルトにする
date: 2026-11-18
tags:
  - プログラミング
  - プログラミング/Git
---

# Git の名前をディレクトリごとに変える

**ふだんは匿名の名前を設定しておき、特定のディレクトリの下でだけ本名を読み込む。** これには `~/.gitconfig` の `includeIf "gitdir:..."` を使う。条件に合うリポジトリでだけ、別の設定ファイルが読み込まれる（[git-config: Conditional includes](https://git-scm.com/docs/git-config#_conditional_includes)）。

## 設定

`~/.gitconfig`：

```ini
[user]
	name = anonymous
	email = anonymous@example.invalid
	useConfigOnly = true

# ~/real/ の下のリポジトリでだけ、本名の設定を読む
[includeIf "gitdir:~/real/"]
	path = ~/.gitconfig-real
```

`~/.gitconfig-real`：

```ini
[user]
	name = 本名
	email = real@example.com
```

- **後に書いた設定が勝つ。** `includeIf` は、デフォルトの `[user]` より **後ろ** に書く。
- `gitdir:` のパターンは **`/` で終える**。`~/real/` と書くと、その下のすべてのリポジトリ（`~/real/a/b/` なども）にあてはまる。
- パスに空白があってもよい。`"gitdir:~/Library/Mobile Documents/"` のように、引用符の中にそのまま書ける。
- macOS は大文字と小文字を区別しないことが多い。区別せずに合わせたいときは `gitdir/i:` を使う。
- `useConfigOnly = true` にすると、名前やメールが設定されていないときに、Git がホスト名などから **勝手に推測しない**。推測されたメールアドレス（`ユーザー名@マシン名.local` など）から身元がわかるのを防げる。

## 確かめ方

```bash
cd ~/real/some-repo
git config user.name                    # 本名
git config --show-origin user.name      # どのファイルの設定かも表示

cd ~/other-repo
git config user.name                    # anonymous
```

この設定を一時的な `HOME` で試し、`~/real/` の下では本名、それ以外では anonymous でコミットされることを確かめた（git 2.50.1）。

## ディレクトリではなく、リモートの URL で分ける
置き場所ではなく、push 先で分けたい場合は `hasconfig:remote.*.url:` を使う（git 2.36 以降）。

```ini
[includeIf "hasconfig:remote.*.url:git@github.com:real-account/**"]
	path = ~/.gitconfig-real
```

`real-account` のリポジトリをどこに clone しても、本名が使われる。

## includeIf を使わないやり方

| 方法 | 効く範囲 | よい点 | 弱い点 |
| --- | --- | --- | --- |
| ① リポジトリごとに設定 | そのリポジトリ | いちばん単純 | clone するたびに設定を忘れやすい |
| ② グローバルに名前を置かない | すべて | 設定し忘れるとコミットできないので、うっかりがない | 新しいリポジトリでは毎回設定がいる |
| ③ direnv で環境変数 | ディレクトリの下 | includeIf とほぼ同じことができる | direnv（外部のツール）が必要 |
| ④ コミットのときだけ指定 | その 1 回 | 設定ファイルを変えない | 毎回打つ必要がある |

### ① リポジトリごとに設定する
グローバル（`~/.gitconfig`）は匿名にしておき、本名を出したいリポジトリの中でだけ `--global` なしで設定する。

```bash
cd ~/real/some-repo
git config user.name "本名"
git config user.email real@example.com
```

この設定はそのリポジトリの `.git/config` に書かれ、グローバルの設定より優先される。

### ② グローバルに名前を置かない
`~/.gitconfig` には `useConfigOnly` だけを書き、名前とメールは置かない。

```ini
[user]
	useConfigOnly = true
```

名前を設定していないリポジトリでコミットすると、`Author identity unknown` というエラーで止まる。そのたびに ① で匿名か本名かを決める。**どちらで出すかを毎回自分で選ぶ** ので、まちがえて本名を出すことがない。

### ③ direnv で環境変数を設定する
Git は、環境変数 `GIT_AUTHOR_NAME`・`GIT_AUTHOR_EMAIL`・`GIT_COMMITTER_NAME`・`GIT_COMMITTER_EMAIL` があると、設定ファイルより **環境変数を優先** する（[Pro Git: Environment Variables](https://git-scm.com/book/en/v2/Git-Internals-Environment-Variables)）。

[direnv](https://direnv.net/) は、そのディレクトリに入ったときだけ `.envrc` の環境変数を読み込むツールである。`~/real/.envrc` に次のように書く。

```bash
export GIT_AUTHOR_NAME="本名"
export GIT_AUTHOR_EMAIL=real@example.com
export GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
export GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
```

- 初回は `direnv allow` で許可する。
- **AUTHOR と COMMITTER の両方** を設定する。AUTHOR だけだと、コミッターは匿名の名前のまま残る。
- ターミナルの外（エディタの Git 機能など）から操作すると、環境変数が読み込まれないことがある。

### ④ コミットのときだけ指定する

```bash
# 作者もコミッターも本名にする
git -c user.name="本名" -c user.email=real@example.com commit

# 作者だけを変える（コミッターは設定ファイルの名前のまま）
git commit --author="本名 <real@example.com>"
```

`--author` は作者（author）だけを変え、コミッター（committer）は変えない（[git-commit](https://git-scm.com/docs/git-commit)）。両方を変えたいなら `-c` を使う。

①〜④の動作は、一時的な `HOME` で確かめた。② ではエラーで止まった。③ の環境変数は設定ファイルより優先された。④ の `--author` では作者だけが変わった。

## GitHub で使うメールアドレス
- 匿名用には、存在しないドメイン（`example.invalid` など）か、GitHub の **noreply アドレス**（`ID+ユーザー名@users.noreply.github.com`）を使う。
- noreply アドレスは、GitHub の Settings → Emails で確認できる。「Keep my email addresses private」を有効にすると、Web 上の操作でも本当のアドレスが使われない（[GitHub Docs: Setting your commit email address](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address)）。
- GitHub は、コミットのメールアドレスでアカウントを結びつける。匿名のコミットを本名のアカウントに結びつけたくないなら、匿名用には本名のアカウントのアドレスを使わない。

## 注意
- **すでにあるコミットは変わらない。** 設定は、これから作るコミットにだけ効く。過去のコミットの名前を変えるには履歴の書き換え（`git filter-repo` など）が必要で、push 済みなら force push になる。
- **リポジトリ内の設定は、グローバルや includeIf より優先される。** リポジトリの `.git/config` に `user.name` があると、そちらが使われる（ただし ③ の環境変数はさらに優先される）。`git config --show-origin user.name` で確かめる。
- **名前以外の手がかり**：コミットには時刻とタイムゾーン（`+0900` など）も記録される。ほかにも、書いた内容や push に使う SSH 鍵・アカウントから、本人がわかることがある。
