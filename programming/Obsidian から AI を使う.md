---
tags: [プログラミング, Obsidian, AI, Claude, ChatGPT]
aliases: [Obsidian から AI を使う, Obsidian で Claude, Obsidian で ChatGPT, Obsidian で Antigravity, Obsidian Copilot]
related:
  - "[[Obsidianのカスタマイズ]]"
  - "[[Obsidian で Git を使う]]"
  - "[[Obsidian を Ubuntu で使う]]"
確認日: 2026-11-21
---
# Obsidian から AI を使う

**Claude・ChatGPT・Antigravity は、どれも Obsidian の中から使える。** やり方は、Community plugin で **パソコンに入っている AI の CLI を呼び出す** のが中心。

| 使いたいもの | おすすめの方法 | このパソコンの準備 |
| --- | --- | --- |
| **Claude** | **Copilot** プラグインの Agent で **Claude Code** をつなぐ | `claude` 2.1.215 が入っている |
| **ChatGPT** | **Copilot** プラグインの Agent で **Codex** をつなぐ（ChatGPT のアカウントでログイン） | `codex` 0.160.0 が入っている |
| **Antigravity** | **Antigravity** プラグイン（kyc）か **Antigravity CLI** プラグイン（jsun2020） | **`agy` の CLI が入っていない**（VS Code の拡張機能だけ）→ 先に `agy` を入れる |

- どれも **デスクトップだけ**。プラグインが、パソコンの中のプログラム（CLI）を動かすため
- **契約は、それぞれの AI のもの** を使う（Claude Code は Claude のログイン、Codex は ChatGPT のログイン、agy は Google のアカウント）。プラグインに別の料金はかからない（Copilot の有料版 Plus を使わない場合）

## 1. Copilot プラグイン（Claude と ChatGPT）
**Copilot**（作者 logancyang、`obsidian-copilot`）は、いちばん多く入れられている Obsidian の AI プラグイン。いまは **4.0.20**（2026 年 11 月 13 日）。V4 から、**Claude Code・Codex・OpenCode をエージェントとして Obsidian の中で動かせる**。

### 入れ方
1. 設定（`Ctrl+,`）→ Community plugins → Browse → 「**Copilot**」（logancyang）→ Install → Enable
2. **Settings → Copilot → Basic → Agents** を開く
3. **Claude Code**：「**Auto-detect**」を押す。見つからなければ、パスを手で入れる（下）
4. **Codex**：Copilot が、Codex 用のアダプター（`@agentclientprotocol/codex-acp`）を入れる
5. 左のリボンの **Agent** のアイコンか、コマンド「**Open Copilot Agent Chat window**」で開く

### このパソコンでの注意：パスを手で入れる
`claude` と `codex` は **nvm の Node.js の中** に入っている。

```text
/home/ieremius/.nvm/versions/node/v24.18.0/bin/claude
/home/ieremius/.nvm/versions/node/v24.18.0/bin/codex
```

デスクトップのメニューから起動した Obsidian は、端末の `.zshrc` を読まないので、**nvm の PATH を知らない**。Auto-detect で見つからないときは、上のパスを設定に入れる。Node.js の版を上げると、パスが変わるので入れなおす。

### 「Update required」と出たとき
Agent の選択の画面で **Claude** に「**Update required**」と出たら、`claude` の版が古い。2026-11-21 にこのパソコンで見たときは、

| 場所 | 版 |
| --- | --- |
| `~/.local/bin/claude`（ネイティブ版。`~/.local/share/claude/versions/2.1.215` へのリンク） | 2.1.215 |
| `~/.nvm/versions/node/v24.18.0/bin/claude`（npm 版） | 2.1.215 |
| npm の最新（`npm view @anthropic-ai/claude-code version`） | **2.1.330** |

どちらも 7 月の版のままだった。端末で更新する：

```sh
~/.local/bin/claude update                      # ネイティブ版
npm install -g @anthropic-ai/claude-code@latest # npm 版（nvm の Node.js で）
```

- **Copilot 4.0.20 が求めるのは Claude Code 2.1.281 以上**（設定の画面に「Claude Code 2.1.215 is not supported. Copilot requires Claude Code 2.1.281 or newer.」と出た）
- Copilot は **nvm の方**（`~/.nvm/versions/node/v24.18.0/bin/claude`）を見つけた。だから、**npm 版を更新する**（ネイティブ版だけ更新しても、Copilot は古い方を見たまま）。または、ネイティブ版を更新してから、Copilot の設定の **Configure** でパスを `~/.local/bin/claude` に変える
- 2 つ入っているのは、まぎらわしい。どちらか 1 つにまとめるとよい（端末の `which claude` は、いまは nvm の方を指す）
- 更新したら、Copilot の設定で **Auto-detect** を押しなおす

### Codex（ChatGPT）をつなぐ
Codex は、`codex` の CLI を **そのまま** 呼ぶのではなく、**`@agentclientprotocol/codex-acp`** というアダプター（Codex を ACP〔Agent Client Protocol〕で動かすためのもの）を通す。Configure Codex の画面には 2 つの道がある。

| 道 | 中身 |
| --- | --- |
| **Managed by Copilot**（おすすめ） | Copilot が、**試験ずみの版の codex-acp** を入れて、更新も管理する |
| My own installation | 自分で入れた codex-acp（**2.0.0 以上**）のパスを指定する。更新は自分で。Copilot は「ほかの版では正しく動かないかもしれない」と注意を出す |

- このパソコンには、2026-11-21 の時点で **codex-acp は入っていなかった**（`codex` の CLI 0.160.0 だけ。npm の codex-acp の最新は 2.8.0）。だから **Managed by Copilot** を選ぶのがいちばん楽
- 手順：**Managed by Copilot** のタブ → 入れる → 下の **Authentication** で **ChatGPT のアカウントでサインイン** → **Done**
- 自分で入れるなら：`npm install -g @agentclientprotocol/codex-acp` のあと、**Auto-detect**（npm のいつもの場所と PATH をさがす）か、パス（`~/.nvm/versions/node/v24.18.0/bin/codex-acp`）を入れて **Apply**

### できること
| 機能 | 中身 |
| --- | --- |
| **Agent** | ノートを読み、ツールを使い、Obsidian のファイルを作る。何回かやりとりしながら進める。**権限は自分で決める** |
| Projects | 仕事ごとに、指示・資料・チャットの履歴をまとめる |
| Skills | Obsidian の Markdown・Bases・Canvas・CLI の書き方などを、エージェントに教える |
| Commands | よく使うたのみ方を保存し、`/` で呼ぶ |
| Quick Chat | エージェントを使わない、ふつうのチャット（API キーが要る） |

- **Claude Code と Codex は、それぞれの CLI のログイン** を使う。Copilot の BYOK（自分の API キー）の設定は要らない
- API キーを使う場合は、キーは **このパソコンの Obsidian のキーチェーン** に入り、ボールトの `data.json` には入らない
- **OpenCode の無料モデル（Zen）** は、送った内容が記録・学習に使われることがある、と注意が出る。ノートの中身を送るので気をつける

## 2. Antigravity（Google）
Google の Antigravity を Obsidian から使うプラグインは 2 つある。どちらも **`agy` という CLI** を呼び出す。

| | **Antigravity**（kyc） | **Antigravity CLI**（jsun2020） |
| --- | --- | --- |
| 版 | 1.0.15（Obsidian 1.13.0 以上） | 0.2.1（Obsidian 1.7.2 以上） |
| できること | ボールトの整理：リンクの修正、frontmatter の点検、フォルダーの目次（`_MOC.md`）作り、選んだ文・ノート・ボールト全体へのタスク。`agy --hub` のウェブ画面をタブに出す | ノートの処理：要約・翻訳・書きなおし・要点・タイトルとタグ。ノートをつけたチャット。フォルダーごとの一括処理 |
| モデル | `gemini-3.8-flash-high` など。`claude-sonnet-4-6`、`gpt-oss-120b-medium` も選べる | `gemini-3.8-flash-high`（`-medium`・`-low` は考える深さ） |
| 権限 | はじめは **制限つき**。「Allow unrestricted tasks」で無制限 | はじめは **ネイティブの許可の規則**。「Full access」で無制限 |
| 決まりのファイル | ボールトに **`AGENTS.md`** を作って、指示として読ませる | — |

### このパソコンの状態
- **VS Code の拡張機能**（`google.google-antigravity` 1.13.0）は入っているが、**`agy` の CLI は入っていない**。プラグインは CLI がないと動かない
- `agy` の入れ方は、どちらのプラグインのページにも書かれていない。Google の Antigravity の公式の案内で入れ、端末で `agy` を一度起動してログインし、`agy --version` と `agy models` で確かめる
- プラグインが `agy` をさがす場所：`~/.local/bin/agy`、`/usr/local/bin/agy` など。見つからなければ、設定にパスを入れる

### Ubuntu に agy を入れる

[Google の公式手順](https://antigravity.google/docs/getting-started?tab=cli)では、端末で次を実行する。

```sh
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

既定のインストール先は `~/.local/bin/agy`。新しい端末を開き、次で確認する。

```sh
agy --version
agy
```

初回起動時の案内に従って設定し、求められたらGoogleアカウントでログインする。`agy` が見つからない場合は `~/.local/bin/agy --version` を試し、動くなら `~/.local/bin` をPATHに追加する。Obsidianのプラグインから見つからない場合は、プラグイン設定に `/home/ieremius/.local/bin/agy` を指定する。

## 3. Obsidian の外から使う（いまのやり方）
いま VS Code の横で使っている **Claude Code・ChatGPT（Codex）・Antigravity の拡張機能** は、ボールトのフォルダーを開けば、ノートを直接読み書きできる。Obsidian のノートはただの Markdown のファイルなので、**Obsidian の中に入れなくても、外からで十分なことが多い**。

| やり方 | よいところ | 気をつけること |
| --- | --- | --- |
| **Obsidian の中**（Copilot・Antigravity のプラグイン） | ノートを見ながら、その場でたのめる。選んだ文だけ渡せる | プラグインの設定、CLI のパス |
| **VS Code の横**（いまのやり方） | git、端末、ほかのファイルも使える。慣れている | Obsidian と画面を行き来する |
| **MCP**（Claude Desktop などから） | ふだんのチャットアプリから、ボールトを検索・編集 | MCP サーバーの設定が要る（→ [[Obsidianのカスタマイズ#Claude とつなぐ]]） |

## 安全のための注意
- **エージェントには、ボールトのファイルを書きかえる力がある**。とくに「Full access」「Allow unrestricted tasks」（`--dangerously-skip-permissions` をつけて動かす設定）は、**確認なしでファイルの書きかえやコマンドの実行** をさせる。ふだんは切っておく
- 大きな変更をたのむ前に、**git でコミットしておく**（→ [[Obsidian で Git を使う]]）。おかしくなっても戻せる
- AI に守らせたい書き方は、ボールトの **`CLAUDE.md`**（Claude Code）や **`AGENTS.md`**（Codex・Antigravity）に書く。このボールトには、まだどちらもない
- ノートの中身は、それぞれの AI の会社のサーバーに送られる。人に見せたくないノートは、渡さない

## 押さえどころ
- **Claude と ChatGPT**：**Copilot** プラグイン（4.0.20）の Agent で、**Claude Code** と **Codex** をつなぐ。どちらもこのパソコンに入っている。nvm の中にあるので、**パスを手で入れる** ことになりそう
- **Antigravity**：**Antigravity** プラグインか **Antigravity CLI** プラグイン。ただし **`agy` の CLI を先に入れる**（いまは VS Code の拡張機能だけ）
- どれもデスクトップだけ。権限は制限つきのままにし、**大きな変更の前に git でコミット**

## 出典
- [Copilot の README（GitHub）](https://github.com/logancyang/obsidian-copilot)：V4 の Agent（OpenCode・Claude Code・Codex）、設定の場所、Auto-detect、Codex のアダプター、Projects・Skills・Commands、キーの保存場所、OpenCode Zen の注意、デスクトップだけであること、無料で使える範囲
- GitHub の API（`logancyang/obsidian-copilot` の latest）：4.0.20、2026 年 11 月 13 日（このパソコンで curl で調べた）
- [Obsidian のプラグインのページ：Antigravity](https://community.obsidian.md/plugins/antigravity)・[Antigravity CLI](https://community.obsidian.md/plugins/antigravity-cli)：作者、版、できること、`agy` が要ること、さがす場所、モデル、権限の設定、`AGENTS.md`（ページを読む道具を通して読んだ）
- `claude`・`codex` の版とパス、`agy` がないこと、VS Code の拡張機能の一覧、ボールトに `CLAUDE.md`・`AGENTS.md` がないこと：このパソコンで調べた
- デスクトップから起動したアプリが `.zshrc`（nvm の PATH）を読まないこと：一般的な知識（このパソコンでは試していない）
