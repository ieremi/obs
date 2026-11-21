---
tags: [プログラミング, AI, AIエージェント, オープンソース]
aliases: [OpenCode, opencode, opencode.ai, OpenCode Zen, OpenCode Go]
related:
  - "[[Obsidian から AI を使う]]"
  - "[[Muse（Meta の AI）]]"
確認日: 2026-11-21
---
# OpenCode

**オープンソースの「AI のコーディングエージェント」。** Claude Code や Codex（ChatGPT）と同じように、端末でたのむと、AI がファイルを読み、書きかえ、コマンドを動かして作業を進める。ちがいは、**特定の AI の会社のものではなく、いろいろな会社のモデルを選んで使える** こと。

| 項目 | 内容 |
| --- | --- |
| 何か | 端末（TUI）で動く AI エージェント。デスクトップアプリ（ベータ）もある |
| ライセンス | **MIT**（オープンソース） |
| リポジトリ | GitHub の **anomalyco/opencode**（もとは SST の `sst/opencode`）。スター 22 万 8 千あまり |
| 始まり | 2025 年 4 月 |
| いまの版 | **v1.19.6**（2026 年 11 月 17 日） |
| ウェブ | **opencode.ai** |
| 使えるモデル | **75 以上の会社**（Anthropic・OpenAI・Google・Grok・Qwen など）と、**ローカルのモデル** |

## Claude Code・Codex とのちがい
| | **OpenCode** | Claude Code | Codex |
| --- | --- | --- | --- |
| 作った所 | オープンソースのチーム | Anthropic | OpenAI |
| モデル | **どの会社のものでも**（自分の API キー、Zen、Go、ローカル） | Claude だけ | OpenAI のモデルだけ |
| 料金 | OpenCode 自体は **無料**。モデルの代金は、使うモデルの会社へ（または Zen・Go） | Claude の契約か API | ChatGPT の契約か API |
| ソース | 公開（MIT） | 公開していない | CLI は公開 |

- **一つの道具で、モデルを取りかえられる** のがいちばんの特徴。同じたのみごとを、Claude でも GPT でも Gemini でもやらせて比べられる
- 自分のパソコンで動くモデル（Ollama など）を使えば、**ノートの中身を外に出さずに** 使うこともできる

## モデルの使い方（3 つの道）
| 道 | 中身 | 料金 |
| --- | --- | --- |
| **自分の API キー** | Anthropic・OpenAI などのキーを入れる | 各社に、使った分だけ |
| **OpenCode Zen** | OpenCode のチームが「OpenCode でうまく動く」と確かめたモデルの一覧。OpenCode の API キー 1 つで使える | **使った分だけ** |
| **OpenCode Go** | オープンソースのコーディング用モデルを、定額で使う | **月 10 ドル**（はじめの月 5 ドル、という案内もある） |
| ローカル | 自分のパソコンで動くモデル | 無料（パソコンの力が要る） |

- **Zen の中の無料モデル** は、送った内容がモデルの会社に **記録されたり、学習に使われたりすることがある**。Copilot プラグインもこの注意を出す。見せたくないノートは送らない

## 入れ方
```sh
curl -fsSL https://opencode.ai/v2/install | bash   # $HOME/.opencode/bin に入る
# または
npm i -g @opencode/cli@latest
brew install anomalyco/tap/opencode-v2             # macOS・Linux
```

- デスクトップアプリ（ベータ）：Linux 用は **.deb・.rpm・AppImage**（opencode.ai/download）
- このパソコンには、まだ入っていない
- [[Obsidian から AI を使う|Obsidian の Copilot プラグイン]] では、**「Configure」を押すと Copilot が OpenCode を自動で入れて管理する**。自分で入れなくてもよい

## 使い方
- プロジェクトのフォルダーで `opencode` と打つと、端末の画面（TUI）が開く。そこでたのむ
- **2 つのエージェント** を、**`Tab` キー** で切りかえる：

| エージェント | すること |
| --- | --- |
| **build**（はじめの設定） | なんでもできる。ファイルの書きかえも、コマンドの実行も |
| **plan** | **読むだけ**。ファイルの書きかえは断り、コマンドを動かす前には聞く。知らないコードを調べるとき、計画を立てるときに |

- 複雑な調べものには、`@general` というサブエージェントを呼べる

## Obsidian の Copilot での位置づけ
Copilot プラグイン（V4）の Agent では、**OpenCode が「Recommended（おすすめ）」** になっている。わけ：

- Copilot がダウンロードから管理までしてくれる
- **Copilot Plus のモデル**（有料）も、**自分の API キーのモデル** も、**ローカルのモデル** も使える
- Claude Code（Claude の契約）や Codex（ChatGPT の契約）を持っていない人でも使える

**すでに Claude や ChatGPT の契約があるなら**、Copilot で **Claude**（Claude Code）や **Codex** を選べば、その契約の中で使える。OpenCode を選ぶ必要はない。

## 押さえどころ
- OpenCode は、**オープンソース（MIT）の AI コーディングエージェント**。Claude Code・Codex の仲間
- **どの会社のモデルでも使える**（75 以上＋ローカル）。OpenCode 自体は無料
- モデルは、自分の API キー、**Zen**（使った分だけ）、**Go**（月 10 ドル）、ローカルから選ぶ。Zen の無料モデルは、送った内容が使われることがある
- `Tab` で **build**（なんでも）と **plan**（読むだけ）を切りかえる
- Obsidian の Copilot では「おすすめ」だが、Claude や ChatGPT の契約があるなら、そちらを選べばよい

## 出典
- GitHub の API（`anomalyco/opencode`）：説明、MIT、スターの数、2025 年 4 月 30 日の作成、opencode.ai、最新 v1.19.6（2026 年 11 月 17 日）（このパソコンで curl で調べた）
- [OpenCode の README](https://github.com/anomalyco/opencode)：入れ方、デスクトップアプリ、`$HOME/.opencode/bin`、build と plan のエージェント、`Tab`、`@general`
- [OpenCode のドキュメント：Providers](https://opencode.ai/docs/providers)、[Docker のドキュメント：OpenCode Zen](https://docs.docker.com/ai/docker-agent/providers/opencode-zen/)・[OpenCode Go](https://docs.docker.com/ai/docker-agent/providers/opencode-go/)：75 以上の会社、Zen と Go のしくみと料金（検索結果の要約による）
- [Copilot の README](https://github.com/logancyang/obsidian-copilot)：Copilot で OpenCode がおすすめであること、Zen の無料モデルの注意
- 「もとは SST の `sst/opencode`」：一般的な知識（`sst/opencode` は API でいまは見つからなかった）。ローカルのモデルに Ollama を使えること：一般的な知識（ウェブでの確認はしていない）
