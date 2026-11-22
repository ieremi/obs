# Obsidian の技術構成

**Obsidian のデスクトップ版は、Rust 製のネイティブアプリではなく Electron を基盤としている。** Electron は Chromium と Node.js を利用して、Web 技術でデスクトップアプリを構築するフレームワーク。Obsidian 公式ヘルプも、デスクトップ版の基盤が Electron であると説明している。[Obsidian: Update](https://obsidian.md/help/updates)

## 使われている技術

- **画面と実行環境**：Electron 上で JavaScript や HTML、CSS などの Web 技術を利用する。
- **テキストエディタ**：Markdown の編集基盤として [[CodeMirror]] を使用する。[Obsidian Developer Documentation: Editor](https://docs.obsidian.md/Plugins/Editor/Editor)
- **プラグイン**：JavaScript で動作し、TypeScript から開発することもできる。プラグインが利用する言語と Obsidian 本体の実装言語は別の話。[Obsidian Sample Plugin](https://github.com/obsidianmd/obsidian-sample-plugin)

Electron 製であることは、すべての構成要素が JavaScript だけで書かれていることを意味しない。Obsidian 本体のソースコード全体は公開されていないため、**内部のすべての構成要素で Rust が一切使われていないとまでは断定できない**。少なくとも「Obsidian 全体が Rust 製」と捉えるのは正確ではない。

## Zed との違い

Zed は Rust を中核に開発されたエディタ。一方、Obsidian のデスクトップ版は Electron を基盤としている。どちらも編集機能を提供するが、アプリケーションの実装基盤は異なる。[Zed のソースコード](https://github.com/zed-industries/zed)

## 関連

- [[Obsidianのカスタマイズ]]
- [[Obsidian を Ubuntu で使う]]
- [[Zed から Codex を使う]]
