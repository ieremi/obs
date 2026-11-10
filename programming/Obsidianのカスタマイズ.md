---
aliases:
  - Obsidian のカスタマイズ
  - Obsidian の見た目
  - Obsidian と Claude
tags:
  - Obsidian
  - CSS
  - Claude
related:
  - "[[VS Code で Markdown をプレビューで開く]]"
確認日: 2026-11-10
---
# Obsidian のカスタマイズ

Obsidian の **見た目の変え方** と、**Claude とつなぐ方法** のまとめ。

## 見た目

**Settings**（⌘,）→ **Appearance** で変える。

| 何を変えるか | 場所 | メモ |
| --- | --- | --- |
| ライト / ダーク | Appearance → **Base color scheme** | **Adapt to system** で OS に合わせる |
| アクセントカラー | Appearance → **Accent color** | リンクやボタンの色 |
| テーマ | Appearance → **Themes** → **Manage** | 人気は **Minimal**、**AnuPpuccin**、**Things** など |
| フォント | Appearance → **Font** | **Interface font**・**Text font**・**Monospace font** を別々に指定できる |
| 文字の大きさ | Appearance → **Font size** | |
| 細かい調整 | Appearance → **CSS snippets** | `.obsidian/snippets/` に `.css` を置いて、トグルでオンにする |

### テーマを細かく設定する

- **Style Settings**（Community plugin）を入れると、テーマが用意した項目を画面で変えられる
- Minimal には専用の **Minimal Theme Settings** プラグインもある
- Community plugin は **Settings → Community plugins → Browse** から入れる。はじめは **Turn on community plugins** を押す（Restricted mode を切る）

### CSS snippets

1. **Settings → Appearance → CSS snippets** のフォルダのアイコンを押して、`snippets` フォルダを開く
2. `.css` ファイルを置く
3. 更新のアイコン（**Reload snippets**）を押し、トグルをオンにする

例：日本語の本文を読みやすくし、見出しと引用を整える。

```css
/* .obsidian/snippets/custom.css */
body {
  --font-text-theme: "Hiragino Sans", "Noto Sans JP", sans-serif;
  --line-height-normal: 1.8;
  --file-line-width: 46rem;
}
.markdown-rendered h2 {
  border-bottom: 1px solid var(--background-modifier-border);
}
.markdown-rendered blockquote {
  font-size: 0.95em; /* 条文の引用など */
}
```

- 色は `var(--text-accent)` などの **CSS 変数** を使うと、ライトとダークの両方で自然になる
- 変数の一覧は、**View → Toggle Developer Tools**（⌥⌘I）で調べられる

### 注意：vault が二つある

- `Documents/.obsidian` と `Documents/obs/.obsidian` があり、別の vault になっている
- 設定は **ふだん開いている vault の `.obsidian`** に入る

## Claude とつなぐ

### 1. Claude Code

- VS Code やターミナルで vault のフォルダを開いて使う
- ノートの読み書き、調べもの、git のコミットまでできる
- vault に `CLAUDE.md` を置くと、書き方のルールを毎回守らせられる。たとえば：
  - ファイル名にスペースを使わない
  - frontmatter に `確認日` を入れる
  - 条文は引用ブロックで書き、出典をつける

### 2. Claude Desktop と MCP

Claude のデスクトップアプリから vault を読み書きする方法。

- **Filesystem の MCP サーバー**：vault のフォルダを指定するだけ。いちばんかんたん
- **Local REST API**（Community plugin）＋ Obsidian 用の MCP サーバー：Obsidian の検索などの機能も使える。Obsidian を起動しておく必要がある

### 3. Obsidian の中で Claude と話す

- **Copilot for Obsidian** などの Community plugin に、Anthropic の API キーを入れる
- サイドバーで Claude と話せる
- API の料金は Claude の契約とは別にかかる

### どれを使うか

| 方法 | よいところ | 気をつけること |
| --- | --- | --- |
| Claude Code | ファイル操作も git もできる。`CLAUDE.md` でルールを決められる | Obsidian の外で使う |
| Claude Desktop と MCP | ふだんの Claude のチャットから使える | 設定ファイルを書く必要がある |
| プラグイン | Obsidian の中で完結する | API の料金。プラグインごとに機能がちがう |
