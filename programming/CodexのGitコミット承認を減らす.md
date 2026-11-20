---
aliases: [コミットのたびにAllowしなくてよくするには, Codexのgit承認, Codexの永続許可]
tags: [Codex, Git, 設定]
---

# CodexのGitコミット承認を減らす

確認日：2026年11月20日。

**`git add` と `git commit` のコマンド接頭辞を永続許可すれば、ファイル名やコミットメッセージが変わるたびの承認を減らせる。** この会話では、こちらが提案した許可範囲にファイル名やメッセージまで含めていたため、毎回の操作が別のコマンドとして扱われていた。

## この保管庫で承認が必要になる理由

保管庫の `obs/.git` はディレクトリではなく、次の外部Git管理領域を指すファイルになっている。

```text
gitdir: /Users/ieremius/git/obs.git
```

このセッションで通常書き込めるのはObsidianのDocumentsなどで、上記のGit管理領域は含まれない。そのため、`git add` のインデックス更新や `git commit` の書き込みには、サンドボックス外実行の承認が必要になる。これは会話内の実行結果と `.git` の内容で確認した事実。

## 手軽な方法：コマンドの接頭辞を永続許可する

次回のコミット時、Codex側から次の範囲で永続許可を提案し、承認画面に「今後このコマンドを許可する」相当の選択肢が表示される場合はそれを選ぶ。画面の文言は利用中のクライアントによって異なる。

```text
git -C obs add
git -C obs commit
```

**ファイル名や `-m` 以降のメッセージを許可の接頭辞に含めない**のがポイント。これなら、同じ形式のコマンドで対象ファイルやメッセージが変わってもルールに一致する。ルールは引数の並び順にも依存するので、`git -C obs commit` と `git commit` は別に扱われる。[出典：OpenAI公式 Rules](https://learn.chatgpt.com/docs/agent-configuration/rules)

## ルールファイルに手動で設定する場合

公式ドキュメントでは、ユーザーのルールを `~/.codex/rules/` 以下の `.rules` ファイルに保存できる。例えば `~/.codex/rules/default.rules` に、既存の内容を残して次を追記する。

```python
prefix_rule(
    pattern = ["git", "-C", "obs", "add"],
    decision = "allow",
)

prefix_rule(
    pattern = ["git", "-C", "obs", "commit"],
    decision = "allow",
)
```

これはこの会話の作業ディレクトリから実行するコマンド形式に合わせた例。`obs` は相対パスなので、あらゆる作業ディレクトリで同じ保管庫を指す制限ではない。別のプロジェクトでも同名のディレクトリに一致し得る。

対象を絶対パスで明示したい場合は、コマンドとルールの両方を次の形式にそろえる。

```python
prefix_rule(
    pattern = ["git", "-C", "/Users/ieremius/Library/Mobile Documents/iCloud~md~obsidian/Documents/obs", "add"],
    decision = "allow",
)

prefix_rule(
    pattern = ["git", "-C", "/Users/ieremius/Library/Mobile Documents/iCloud~md~obsidian/Documents/obs", "commit"],
    decision = "allow",
)
```

手動変更後は新しいセッションで読み込ませる。管理者側の制限や、より優先される禁止・承認ルールがある場合は、許可ルールだけでは承認をなくせない。`allow` はサンドボックス外実行の許可判定に使われるもので、通常のファイル書き込み許可範囲を広げる設定とは異なる。[出典：OpenAI公式 Rules](https://learn.chatgpt.com/docs/agent-configuration/rules)

## この会話での今後の扱い

今後、コミットの承認を求める際は、ファイル名・コミットメッセージまで固定したルールではなく、対象保管庫の `add` と `commit` をそれぞれ再利用できる範囲で提案する。永続許可の保存操作自体はユーザー側で行う。

このページは設定方法の説明であり、実際の承認ルールや権限設定は変更していない。
