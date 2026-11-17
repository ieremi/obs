---
aliases:
  - Obsidian のノートを公開する
  - vault をブログにする
date: 2026-11-18
tags:
  - ブログ
  - Obsidian
---

# vault の一部をブログにする

**おすすめは Quartz で、公開したいノートにだけ `publish: true` を付ける方法である。** Quartz は Obsidian の vault をそのままサイトにするための静的サイトジェネレーターである。ウィキリンク、バックリンク、グラフ、コールアウトがそのまま使える。一般的なブログの構成は [[AIで書くブログのテックスタック]] を参照。

## 方法の比較

| 方法 | 費用 | 手間 | ウィキリンク | 公開するノートの選び方 |
| --- | --- | --- | --- | --- |
| **Quartz** | 無料（ホスティングも無料枠） | 中 | そのまま使える | `publish: true` |
| Obsidian Publish | 年払いで月 8 ドル、月払いで月 10 ドル（1 サイトあたり） | 小 | そのまま使える | Obsidian の画面で選ぶ |
| Digital Garden（Obsidian のプラグイン） | 無料 | 中 | 使える | `dg-publish: true` |
| Astro など一般の SSG | 無料 | 大 | 変換が必要 | 自分でスクリプトを書く |

- **Obsidian Publish** は公式の有料サービスで、いちばん手軽である。ノートを選んでボタンを押すだけで公開できる（[Obsidian Publish](https://obsidian.md/publish)、[料金](https://obsidian.md/pricing)）。
- **Quartz** は無料で、見た目や機能を自由に変えられる。この vault はすでに GitHub で管理しているので、相性がよい（[Quartz](https://quartz.jzhao.xyz/)）。

## Quartz でのやり方

### 1. 公開するノートに印を付ける
公開したいノートのフロントマターに `publish: true` を書く。

```yaml
---
publish: true
---
```

- Quartz の **ExplicitPublish** フィルターを有効にすると、`publish: true` のノートだけがサイトになる。初期設定では無効なので、自分で有効にする（[ExplicitPublish](https://quartz.jzhao.xyz/plugins/ExplicitPublish)）。
- 公開はするが一覧・検索・グラフには出したくないノートには、`unlisted: true` を付ける。
- 書きかけのノートは `draft: true` にすると公開されない（[Private Pages](https://quartz.jzhao.xyz/features/private-pages)）。

### 2. 添付ファイルに注意する
- **初期設定（`publishAssets: "all"`）では、画像や PDF などの Markdown 以外のファイルは、フィルターに関係なくすべて公開される。**
- `publishAssets: "referenced"` にすると、公開するノートがリンク・埋め込みしているファイルだけが公開される。**必ずこちらにする**（[Private Pages](https://quartz.jzhao.xyz/features/private-pages)）。

### 3. リポジトリの構成
- ブログ用に、別のリポジトリを Quartz から作る。
- ビルドのときに、`obs` リポジトリの中身を Quartz の `content/` に入れる。GitHub Actions で `obs` をチェックアウトする方法がわかりやすい。
- こうすると、ノートは今までどおり `obs` で書き、ブログの設定やデザインは別に管理できる。

### 4. 公開する
- ビルドしたサイトを Cloudflare Pages か GitHub Pages に置く（[Quartz: Hosting](https://quartz.jzhao.xyz/hosting)）。
- `obs` に push したらブログも作り直されるように、GitHub Actions でつなぐ。

## 気をつけること
- **`obs` リポジトリはすでに GitHub で公開（public）になっている。** ブログで公開しないノートも、GitHub では誰でも読める。ブログに出すノートだけを公開したいなら、`obs` を非公開（private）にし、ブログのビルドからだけ読むようにする。
- **公開しないノートへのリンク**は、行き先のページがなくなる。公開するノートのリンク先も公開するか、リンクを外す。
- **引用・転載**：本や論文の文章を長く写したノート（`文選` など）は、著作権を確かめてから公開する。
- **個人情報**：住所・病歴・他人の名前などが書かれていないか、公開する前に読み返す。
- **ファイル名**：日本語のファイル名はそのまま URL になる（エンコードされて長くなる）。短い英語の URL にしたい場合は、ファイル名を英語にするのが確実である。
- **ノートの数**：`history/` だけで 1 万を超えるノートがある。全部を `content/` に入れてもフィルターで絞れるが、ビルドに時間がかかる。公開するフォルダだけを入れるほうが速い。

## AI に任せられること
- 公開してよさそうなノートの候補を挙げさせ、`publish: true` を付けさせる。
- 公開するノートに、個人情報や長い引用がないか確かめさせる。
- 公開しないノートへのリンクを一覧にさせる。
- GitHub Actions の設定ファイルを書かせる。
