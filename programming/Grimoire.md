---
tags:
  - Obsidian
  - AI
---
# Grimoire

**Grimoire**は、CodexやClaude CodeなどのCLIエージェントをObsidianの中から使うためのコミュニティプラグイン。チャットでノートやフォルダーを参照し、エージェントに検索や編集を依頼できる。デスクトップ版Obsidian用で、モバイル版はない。[Grimoire公式リポジトリ](https://github.com/sandsaber/Grimoire)

## 導入

1. Obsidianの「設定」→「コミュニティプラグイン」→「閲覧」で **Grimoire** を検索してインストールし、有効にする。
2. リボンまたはコマンドパレットからGrimoireを開く。
3. 使いたいCLIを別途インストールし、端末で認証する。Grimoireの「Providers」で利用するものを有効にする。Codexは初回から有効。

Grimoire自体は各CLIのアカウント、モデルの利用権、利用制限に代わるものではない。[[Obsidian から AI を使う]]も参照。

## Antigravity CLIを使う

[[Obsidian から AI を使う#Ubuntu に agy を入れる|agyをインストール]]してログインし、Grimoireの設定でAntigravityを有効にする。`agy` はPATHから自動検出され、見つからない場合はプロバイダー設定でCLIのパスを指定できる。

公式READMEによると、対応する `agy` ではACPを使って会話を続けられ、許可要求をチャットに表示できる。古いCLIではprintモードに切り替わり、自動承認が必要になる。使える機能はCLIとGrimoireのバージョンによって異なる。[Antigravity CLIの設定](https://github.com/sandsaber/Grimoire#antigravity-cli)

## データと権限

Grimoireの設定やセッション情報は、ボールト内の `.grimoire/` に保存される。公式READMEでは、Grimoire独自のサーバーへの送信やテレメトリーはないと説明している。一方、選択したプロバイダーのCLIには指示や必要なノートなどが渡り、外部サービスに送信される場合がある。

エージェントによるファイル編集やコマンド実行の範囲は、プロバイダーと作業モードによって異なる。利用前に権限を確認し、変更の前にGitで保存しておくと戻しやすい。
