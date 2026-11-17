---
aliases:
  - AI driven blog
  - AI ブログのテックスタック
date: 2026-11-18
tags:
  - ブログ
  - AI
  - 自動化
---

# AI で書くブログのテックスタック

**おすすめは「Markdown ファイル＋静的サイトジェネレーター＋Git＋無料ホスティング」である。** 記事がただのテキストファイルなので、AI が読み書きしやすい。また、API の有無や規約に縛られない。note のように公式 API がないサービスとの違いは [[note_comにAIで投稿する]] を参照。

## おすすめの構成

| 役割 | おすすめ | 理由 |
| --- | --- | --- |
| 下書き・管理 | Obsidian | いまのボールトの Markdown をそのまま記事にできる。 |
| AI | Claude Code | ファイルを直接読み書きし、Git の操作やビルドもできる。 |
| サイト生成 | Astro | Markdown をそのまま記事にでき、表示が速い。 |
| 置き場所 | GitHub | 履歴が残るので、AI の変更を確認して戻せる。 |
| 公開 | Cloudflare Pages | GitHub に push すると自動でビルド・公開される。個人ブログなら無料枠で足りる。 |

### 流れ
1. Obsidian でメモや構成を書く。
2. Claude Code に下書き・推敲・タグ付け・要約（description）を任せる。
3. 自分で読んで直す。
4. `git push` すると Cloudflare Pages が自動で公開する。

**公開の前に必ず人が読む工程を入れる。** AI はもっともらしい誤りを書くことがある。

## 各部品
- **Astro**：コンテンツ向けのフレームワーク。`src/content/` に Markdown を置くと記事になり、Content Collections でタイトル・日付・タグなどのフロントマターを型でチェックできる。AI が書いた記事の項目漏れをビルド時に見つけられる（[Astro Docs: Content collections](https://docs.astro.build/en/guides/content-collections/)）。
- **Cloudflare Pages**：Git リポジトリとつなぐと、push ごとにビルド・公開される（[Cloudflare Pages docs](https://developers.cloudflare.com/pages/)）。
- **Claude Code**：ターミナルや VS Code で動く。リポジトリに `CLAUDE.md` を置き、文体・記事の型・禁止事項を書いておくと、毎回同じルールで書かせられる（[Claude Code docs](https://code.claude.com/docs/en/overview)）。

## ほかの選択肢

| 構成 | よい点 | 気をつける点 |
| --- | --- | --- |
| Hugo | ビルドがとても速い。Go 製で単体で動く。 | テンプレートの書き方にくせがある。 |
| Next.js | 動的な機能（ログイン・検索・AI チャット）を足しやすい。 | ブログだけには大げさ。 |
| Ghost | 公式の Admin API があり、AI から投稿まで自動化できる（[Ghost Admin API](https://docs.ghost.org/admin-api)）。 | サーバーの運用か、有料のホスティングが必要。 |
| WordPress | REST API で投稿できる（[WordPress REST API Handbook](https://developer.wordpress.org/rest-api/)）。 | 更新やセキュリティ対策の手間がかかる。 |
| note | 読者が最初からいる。 | 個人向けの公式投稿 API がない。 |

## 選び方
- **書いた記事を自分で持ちたく、手間も費用もかけたくない** → Astro＋Cloudflare Pages。
- **管理画面がほしく、投稿まで API で自動化したい** → Ghost。
- **読者を集めることを優先する** → note や Zenn に投稿し、原稿は Obsidian で管理する。

## AI に任せるとよいこと
- 構成案、下書き、推敲、誤字のチェック。
- タイトル・description・タグ・OGP 画像の文言。
- 過去記事への内部リンクの提案。
- 英語版などへの翻訳。

**事実の確認と、公開するかどうかの判断は人がする。**
