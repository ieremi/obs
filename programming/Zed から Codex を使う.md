# Zed から Codex を使う

Zed では、**Codex を外部エージェントとして Agent Panel から使える**。Zed と Codex は Agent Client Protocol（ACP）で連携し、会話や変更を Zed 内で確認できる。Zed 組み込みの **Zed Agent に OpenAI のモデルを設定すること**とは別の方法である。[Zed: External Agents](https://zed.dev/docs/ai/external-agents)

## 設定手順

1. Zed で作業したいプロジェクトを開く。
2. コマンドパレットで `zed: acp registry` を実行する。あるいは `agent: open settings` → **External Agents** → **Add Agent** → **Install from Registry** を開く。
3. 一覧から **Codex** を選んでインストールする。これはエディタ拡張機能の一覧とは別の ACP Registry。
4. **Agent Panel** または **Threads Sidebar** の新規スレッドメニューから Codex を選ぶ。
5. 認証を求められたら、Codex 側の画面に従ってサインインする。利用できる認証方法は導入したバージョンや環境による。ChatGPT アカウントでのログインと API キー利用は課金・利用条件が異なるので、選択時に確認する。
6. まず「このプロジェクトの構成を説明して。ファイルは変更しないで」のように依頼し、接続を確認する。編集やコマンド実行を依頼する場合は、表示される権限・承認内容と変更差分を確認する。

Zed のバージョンによって UI の名称や手順が異なる場合がある。上記は [Zed の外部エージェントの現行ドキュメント](https://zed.dev/docs/ai/external-agents)に基づく。

## 認証・設定の境界

- **Zed Agent の OpenAI API キーは Codex に自動では引き継がれない。** Codex は原則として独自の認証と課金を使う。
- Codex 側のモデル・認証・ネイティブ設定と、Zed Agent の設定は別物。Zed Agent 用のプロファイルや Skills が Codex にそのまま適用されるとは限らない。
- Codex 独自の指示や MCP 設定、Zed から ACP 経由で渡される設定の扱いは、エージェントや連携方法に依存する。`AGENTS.md` や権限設定は、実際に使う環境で確認する。
- ACP Registry からの導入と、既存の `codex` CLI が同じ実行ファイル・認証情報・バージョンを使うとは限らない。SSH やコンテナでは、どちら側で認証・実行されるかも確認する。

## ターミナルで使う方法

ACP 連携を使わず、Zed の内蔵ターミナルで `codex` を起動する方法もある。すでに Codex CLI を使える場合は、対象プロジェクトで次を実行する。

```sh
codex
```

これは通常の CLI をターミナル内で操作する方法で、Agent Panel による ACP 連携とは UI や連携範囲が異なる。Codex の導入・認証は CLI 側で行う。[OpenAI: Codex](https://developers.openai.com/learn/codex)

## うまく動かないとき

- 一覧に Codex がない場合：Zed のバージョンと ACP Registry を確認する。
- 認証エラー：Zed Agent のキーではなく、Codex スレッド自身のログイン状態・利用資格を確認する。アカウントや組織、API 課金の状態も確認する。
- 動作が CLI と異なる場合：使用しているエージェントのバージョン、作業ディレクトリ、認証先、設定と権限を確認する。
- 通信上の問題：コマンドパレットから `dev: open acp logs` を開く。ログを共有する前に秘密情報が含まれていないか確認する。

このノートは公式ドキュメントに基づく手順であり、この環境でのインストールや動作確認は行っていない。
