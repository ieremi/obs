# Markdown の歴史

Markdown は、記号を使って見出しやリンクなどを表す、プレーンテキストのための軽量マークアップ言語である。もともとはウェブ向けの文章を HTML に変換するために生まれたが、開発文書、チャット、ノート、本などにも広がった。

## 誕生

2004 年、John Gruber は Aaron Swartz の協力を得て Markdown を開発した。Gruber が書いた `Markdown.pl` は、Markdown 形式のテキストを HTML に変換する Perl のプログラムだった。「Markdown」は記法と変換プログラムの両方を指す名前だった。 [Gruber による紹介](https://daringfireball.net/2004/03/introducing_markdown) · [Markdown の説明](https://daringfireball.net/projects/markdown/)

発想の源には、プレーンテキストの電子メールで使われてきた、引用の `>` や強調の `*` といった書き方がある。変換前のテキスト自体も読みやすいことが重視された。

## 主なできごと

| 時期 | できごと |
| --- | --- |
| 2004 年 | Gruber が Markdown を公開。8 月に 1.0 がベータを抜け、12 月にオリジナルの変換プログラム 1.0.1 が公開された。 [1.0 の告知](https://daringfireball.net/linked/2004/08/20/markdown-10) · [プロジェクトページ](https://daringfireball.net/projects/markdown/) |
| 2000 年代後半〜2010 年代 | さまざまな言語で変換プログラムがつくられ、GitHub、Reddit、Stack Overflow などでも使われるようになった。表や脚注などを加えた方言も増えた。 [CommonMark 仕様の背景](https://spec.commonmark.org/current/) |
| 2014 年 | 解釈の違いを減らすため、明確な仕様とテストを整える CommonMark の取り組みが始まった。当初の名称は Standard Markdown だったが、CommonMark に変更された。 [名称変更の告知](https://talk.commonmark.org/t/standard-markdown-is-now-commonmark/434) · [仕様の履歴](https://spec.commonmark.org/) |
| 2016 年 | Markdown ファイルのメディアタイプ `text/markdown` が RFC 7763 で登録され、RFC 7764 で Markdown の利用に関する指針が示された。特定の一方言を唯一の標準に定めたわけではない。 [RFC 7763](https://www.rfc-editor.org/rfc/rfc7763) · [RFC 7764](https://www.rfc-editor.org/rfc/rfc7764) |
| 2017 年 | GitHub が CommonMark を基礎とする GitHub Flavored Markdown（GFM）の正式な仕様を公開した。 [GitHub の告知](https://github.blog/news-insights/product-news/a-formal-spec-for-github-flavored-markdown/) |
| 2020 年代 | Markdown ファイルを用いるノートアプリ、文書作成ツール、開発ツールなどが引き続き使われている。用途ごとに拡張が加えられる一方、方言の違いは残っている。 |

## 方言と互換性

オリジナルの説明には細部があいまいな箇所があり、実装ごとに解釈が分かれた。また、それぞれのアプリが必要な機能を追加した。そのため、同じ Markdown ファイルでも、使うアプリによって表示が異なることがある。 [CommonMark の背景](https://commonmark.org/)

| 記法・仕様 | 特徴 |
| --- | --- |
| オリジナルの Markdown | 見出し、強調、リスト、リンク、引用などを備える。表やタスクリストは含まれない。 |
| CommonMark | 基本的な記法の解釈を明確にし、実装間で共通の動作を目指す仕様。 |
| GitHub Flavored Markdown | CommonMark を基礎に、表、取り消し線、タスクリストなどを加えた GitHub の方言。 [GFM 仕様](https://github.github.com/gfm/) |
| Obsidian の Markdown | Markdown に加え、`[[ノート名]]` のようなウィキリンクや埋め込みなどを使える。これらは一般的な Markdown で必ず使えるわけではない。 [Obsidian の内部リンク](https://help.obsidian.md/links) |

Markdown はテキストなので別のアプリへ持ち運びやすいが、**ファイルを開けることと、すべての拡張記法が同じように表示されることは別**である。

## 関連

- [[programming/Obsidianの歴史|Obsidian の歴史]]
- [[programming/VS Code で Markdown をプレビューで開く|VS Code で Markdown をプレビューで開く]]
