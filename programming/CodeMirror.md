# CodeMirror

**CodeMirror** は、Web ページや Web 技術を使ったアプリに組み込めるテキスト・コードエディタの部品。単体のデスクトップアプリではなく、アプリの編集画面を構成するライブラリである。MIT ライセンスで公開されている。[CodeMirror 公式サイト](https://codemirror.net/)

## 主な機能

構文強調、行番号、入力補完、検索・置換、コードの折りたたみなどに対応する。必要な機能や言語サポートを拡張として組み合わせ、アプリごとに見た目や操作を調整できる。[拡張機能一覧](https://codemirror.net/docs/extensions/)

## CodeMirror 5 と 6

**CodeMirror 6** は、状態・表示・言語サポートなどを複数のパッケージと拡張機能に分けた設計。**CodeMirror 5** とは API や拡張方法が異なり、5 用の拡張をそのまま 6 で使えるとは限らない。[5 から 6 への移行ガイド](https://codemirror.net/docs/migration/)

## Obsidian・Zed との関係

- [[Obsidian の技術構成|Obsidian]] は Markdown の編集基盤に CodeMirror を使う。公式 API の `Editor` は CodeMirror 6 と、デスクトップの旧エディタである 5 の差を吸収する。[Obsidian: Editor](https://docs.obsidian.md/Plugins/Editor/Editor)
- [[Zed]] は Rust 製の独自 UI フレームワーク **GPUI** を使うエディタで、Obsidian の CodeMirror とは編集画面の基盤が異なる。[Zed 1.0](https://zed.dev/blog/zed-1-0)

日本語 IME の変換中表示などの挙動は、エディタ部品だけでなく OS、入力方式、表示環境、アプリ側の実装にも左右される。Zed での報告をそのまま CodeMirror や Obsidian に当てはめることはできない。
