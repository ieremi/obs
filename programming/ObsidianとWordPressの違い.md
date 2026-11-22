# Obsidian と WordPress の違い

**Obsidian は手元のノートを作成・整理するアプリ、WordPress はウェブサイトを作成・運営するための CMS である。** どちらも文章を扱えるが、出発点が異なる。

## 比較

| 項目 | Obsidian | WordPress |
| --- | --- | --- |
| 主な目的 | ノートを書き、知識や資料を整理する | ブログや企業サイトなどを作り、ウェブで公開する |
| 扱うもの | 保管庫の中のノートや添付ファイル | 投稿、固定ページ、メディア、コメントなど |
| 保存 | 基本的に端末内の Markdown ファイル | 投稿や設定などは主にサーバーのデータベース。画像などはファイルとして保存 |
| 編集 | デスクトップ・モバイルアプリで、主に Markdown を編集 | 主にブラウザの管理画面で、ブロックを使って編集 |
| 公開 | 通常のノートは自動公開されない。Obsidian Publish などを別途利用する | 公開を前提とした機能が中心。下書きや非公開の状態でも管理できる |
| リンク | ノート間のリンクやバックリンクで関係をたどりやすい | 投稿や固定ページをリンクでき、カテゴリーやタグでも整理できる |
| サイト運営 | Obsidian Publish でノートをサイトとして公開できる | 投稿・固定ページ、利用者、コメントなどの管理を備え、サイト運営向けに拡張できる |
| 拡張と見た目 | アプリ用のプラグイン、テーマ、CSS スニペット | サイト用のプラグインとテーマ。利用可能な範囲はホスティングやプランによる |
| オフライン | 基本的なノートの読み書きはオフラインで可能 | 通常はウェブサーバーに接続して編集。ローカル環境に WordPress を設置することもできる |
| ソースコード | アプリ本体はプロプライエタリ | WordPress 本体はオープンソース |
| 費用 | アプリ本体は無料。公式の同期・公開サービスは別料金 | ソフトウェア本体は無料。公開用のホスティングや有料テーマなどに費用がかかることがある |

[Obsidian の料金とデータの保存](https://obsidian.md/pricing) · [WordPress とは](https://make.wordpress.org/support/user-manual/about-wordpress/what-is-wordpress/) · [WordPress のデータベース](https://learn.wordpress.org/lesson/the-wordpress-database/)

## Obsidian Publish と比べると

Obsidian Publish を使えば、Obsidian のノートから公開するものを選び、ウェブサイトにできる。リンクでつながったノート、資料集、個人の知識ベースを公開したいときに向く。公開サイト用の CSS も使える。 [Obsidian Publish](https://obsidian.md/publish) · [サイトのカスタマイズ](https://obsidian.md/help/publish/customize)

WordPress は、ブログの記事や固定ページを管理し、複数の利用者やコメントを扱うなど、サイト運営を中心に設計されている。テーマやプラグインを選び、用途に合わせてサイトを拡張できる。 [WordPress とは](https://make.wordpress.org/support/user-manual/about-wordpress/what-is-wordpress/)

つまり、**ノートを育てて必要なものを公開する**なら Obsidian と Publish、**公開サイトを中心に記事や読者とのやり取りを管理する**なら WordPress がわかりやすい選択である。

## WordPress.org と WordPress.com

- **WordPress.org**：オープンソースの WordPress を入手できる場所。自分でホスティングを選んで設置・運営できる。
- **WordPress.com**：WordPress を利用できる、ホスティング込みのサービス。サーバーの用意や管理の負担を減らせるが、使える機能はプランによって異なる。

同じ WordPress のソフトウェアを使うが、ホスティングや管理の分担が違う。 [WordPress.com と WordPress.org の比較](https://wordpress.com/support/com-vs-org/)

## 併用するなら

Obsidian で調査や下書きを行い、公開用の記事を WordPress に移す方法もある。ただし、Obsidian 固有のウィキリンク、埋め込み、プラグインの表示や画像の参照先が、WordPress でそのまま再現されるとは限らない。公開前にリンクや画像、書式を確認する。

## 関連

- [[programming/Obsidianの歴史|Obsidian の歴史]]
- [[programming/Markdownの歴史|Markdown の歴史]]
- [[programming/Obsidianのテーマを公開する|Obsidian のテーマを公開する]]
