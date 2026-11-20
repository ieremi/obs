---
aliases:
  - 独自ドメインを取らずに短いURLを使う
  - 短縮URL
  - カスタムエイリアス
tags:
  - Web
  - URL
---

# 独自ドメインなしでシンプルなURLを使う

確認日：**2026年11月20日**。サービスの無料枠・機能・利用条件は変更される。以下のURLは形式の例であり、名前の空きや取得を確認したものではない。

**既存ページへの覚えやすい入口が欲しいなら、名前を指定できる短縮URL。自作サイトの公開先も欲しいなら、ホスティングサービスの標準URL**が使える。

`example.com/name` のような形は、ドメイン所有者が提供するサービスで `/name` を確保する仕組みになる。検索するときのキーワードは「カスタムエイリアス」「カスタム短縮URL」「無料サブドメイン」。

## 候補の比較

| 目的 | 候補 | URLの形式例 | 要点 |
| --- | --- | --- | --- |
| すでにあるページへ短い名前で転送 | TinyURL | `tinyurl.com/my-project` | 無料プランでカスタムエイリアスに対応。作成後のリンク編集は有料機能として案内されている [1] |
| 短いドメインで固定の転送先を作る | is.gd | `is.gd/mytool` | 無料。名前は5〜30文字の英数字とアンダースコア。作成後の転送先変更・削除は不可 [2] |
| プロフィールや複数リンクの入口 | Linktree | `linktr.ee/myname` | 無料で開始でき、リンク集を作れる。通常は中間ページを表示する [3] |
| 自作のHTML・JavaScriptを公開 | Cloudflare Pages | `mytool.pages.dev` | 自分のファイルをアップロードして公開できる。ドメイン購入は不要 [4] |
| GitHubで管理する静的サイトを公開 | GitHub Pages | `username.github.io/mytool/` | 公開リポジトリならGitHub Freeで利用可能。末尾はリポジトリ名 [5] |
| コードを書かずに1ページ作成 | Carrd | `myname.carrd.co` | 無料のBasicプランがあり、サービスのサブドメインで公開できる [6] |

## 今回の希望に近い選び方

以下は用途に基づく提案。

- **「長いURLを、人に伝えやすいURLにしたい」**：TinyURL。好きな末尾を指定して、すでにあるページに転送する。
- **「短さを優先し、転送先は固定でよい」**：is.gd。ただし `name` は4文字なので、そのままでは5文字以上という条件を満たさない。
- **「自分の窓口を1つ用意し、リンクを後から追加・差し替えたい」**：Linktree。公開URLを保ってリンク集の内容を更新する運用に向く。
- **「Geminiなどで作った小さなWebアプリを公開したい」**：Cloudflare Pages。`mytool.pages.dev` をそのまま案内すれば、短縮サービスを挟む必要がない。
- **「すでにGitHubを使っている」**：GitHub Pages。`username.github.io/tool/` の形でプロジェクトをまとめられる。

## 短縮URLと公開URLの違い

短縮URLは、ページ本体の置き場所とは別の「転送用の入口」。アクセスすると通常は転送先のURLに移る。**ブラウザのアドレス欄にも短いURLを残したい場合は、そのURLでページを配信するサービスを選ぶ。**

例えば、長い共有URLへの案内ならTinyURLで足りる。一方、自作アプリを `mytool.pages.dev` で表示したいならCloudflare Pagesにアプリ本体を置く。

Linktreeはリンク集ページを表示するサービス。自動で1つのリンクへ転送する「Redirect」は有料プランの機能なので、無料の短縮URLと同じものとして選ばない。[3]

## 小さなWebアプリならCloudflare Pagesで始める例

1. `index.html` と必要なCSS・JavaScriptを用意する。ビルドが必要な構成なら、ビルド後の出力フォルダを使う。
2. CloudflareのダッシュボードでPagesのDirect Uploadを選ぶ。
3. プロジェクト名を決め、フォルダまたはZIPをアップロードする。
4. 発行された `プロジェクト名.pages.dev` を共有する。

名前が使用済みの場合は文字が追加されることがある。Direct Uploadで作ったプロジェクトは後からGit連携へ切り替えられないため、Gitからの自動公開を使いたければ最初からGit連携で作る。[4]

これはブラウザで動く小さなアプリを想定した例。Pythonサーバーやデータベースなどが必要なアプリは、別途その実行・保存環境も選ぶ。

## 名前と継続利用で確認すること

- 短い名前・一般的な単語は取得済みの場合がある。サービスが提供する範囲で名前を選ぶ。
- 「好きな末尾を指定できる」と「後から転送先を変えられる」は別の機能。印刷物などに載せるなら、更新できるかを先に確認する。
- サービスのドメインを使うため、そのURLはサービスの継続提供に依存する。長期的な移転の自由度を重視する段階になったら、独自ドメインを検討する。

## 出典

いずれも2026年11月20日確認。

1. [TinyURL：無料プランに含まれる機能](https://tinyurl.com/blog/what-included-tinyurl-free/)
2. [is.gd：サービス説明](https://www.is.gd/description.php)、[FAQ（名前の制約・変更不可）](https://www.is.gd/faq.php)
3. [Linktree：無料での作成案内](https://linktr.ee/blog/how-to-make-a-linktree)、[ユーザー名とURL](https://linktr.ee/help/articles/5434143-about-linktree-username)、[Redirectと独自ドメインについて](https://linktr.ee/help/articles/6571689-about-custom-domains)
4. [Cloudflare Pages：Direct Upload](https://developers.cloudflare.com/pages/get-started/direct-upload/)
5. [GitHub：What is GitHub Pages?](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages)
6. [Carrd：利用規約（Basicプランとサービスのサブドメイン）](https://carrd.com/docs/general/terms)、[公開先URLについて](https://carrd.com/docs/sites/using-a-custom-domain)

## 関連

- [[Cloudflare]]
- [[AIで書くブログのテックスタック]]
- [[vaultの一部をブログにする]]
- [[Geminiでプログラミングする方法]]
