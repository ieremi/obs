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
確認日: 2026-11-21
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

### Ubuntu では

Mac の書き方（⌘、Hiragino）は、Ubuntu ではこう読みかえる（→ [[Obsidian を Ubuntu で使う]]）。

| Mac | Ubuntu |
| --- | --- |
| ⌘,（設定） | **Ctrl+,** |
| ⌥⌘I（開発者ツール） | **Ctrl+Shift+I** |
| Hiragino Sans | **Noto Sans CJK JP**（Ubuntu にはじめから入っている） |
| Hiragino Mincho | **Noto Serif CJK JP** |

このボールトには、Ubuntu 用の snippet **`.obsidian/snippets/ohohama.css`** を置いた（2026-11-21）。

- オンにする：**Settings → Appearance → CSS snippets** で、更新のアイコンを押してから **ohohama** のトグルをオン
- 中身：
  - フォント：本文と画面は **Noto Sans CJK JP**、コードは **Hack Nerd Font Mono**（日本語は Noto Sans Mono CJK JP）。VS Code の設定とそろえた
  - 行間 1.8、本文の幅 48rem
  - h2 に下線、h1 を少し大きく
  - **表**：文字を少し小さく、見出し行に背景色、すきまを整える（このボールトは表が多いため）
  - 引用とインラインのコードを少し小さく
- 明朝体で読みたいときは、`--font-text-theme` を `"Noto Serif CJK JP", serif` に変える

#### 色：ライトグレーと #0B8BEE

同じ snippet に、**ライトグレーの背景** と **アクセント #0B8BEE** の配色を入れた。**Base color scheme を Light** にして使う。

| 役わり | 色 | 変数 |
| --- | --- | --- |
| 本文の背景 | **#ECEEF1** | `--background-primary` |
| サイドバー・表の見出し行 | #E1E5EA・#DAE0E7 | `--background-secondary`・`--table-header-background` |
| 線 | #C8CED6 | `--background-modifier-border` |
| 本文の文字 | #222831（濃いグレー） | `--text-normal` |
| うすい文字 | #5B6573・#8A94A2 | `--text-muted`・`--text-faint` |
| **アクセント**（ボタン、チェックボックス、h1、引用の線、h2 の下線） | **#0B8BEE** | `--accent-h/s/l`（206・91%・49%）、`--interactive-accent` |
| **リンク** | **#0966B0**（#0B8BEE を少し暗く） | `--text-accent` |
| 選んだ文字・マウスを乗せたところ | #0B8BEE を透かしたもの | `--text-selection`・`--background-modifier-hover` |

- **リンクだけ少し暗くした わけ**：#0B8BEE は、#ECEEF1 の背景とのコントラストが **3.0:1** で、小さい文字には足りない（WCAG の AA は 4.5:1）。#0966B0 なら **5.1:1**。大きい文字の h1 は 3:1 でよいので #0B8BEE のまま（このパソコンで計算した）
- Settings → Appearance → **Accent color** で色を選ぶと、snippet の `--accent-h/s/l` と食いちがうことがある。そこは **空（既定）** のままにしておく
- 使えるフォントの名前は、端末で `fc-list : family | grep -i noto` で調べる
- フォントは **Settings → Appearance → Font** でも指定できる。そこで指定すると、snippet より優先される

#### ダーク：Ohohama に合わせる

**Base color scheme を Dark** にすると、VS Code で使っているテーマ **Ohohama**（[github.com/ieremi/ohohama](https://github.com/ieremi/ohohama)）の色になる。Ohohama は、静岡の **大浜海岸** の海と空をイメージした、**青とグレーだけ** のダークテーマ。

色は、このパソコンに入っている拡張機能（`~/.vscode/extensions/ieremius.ohohama-0.3.12`）の `palette.ts` と `vscode/themes/Ohohama-color-theme.json` から取った。

| 役わり | 色 | Ohohama でのもと |
| --- | --- | --- |
| 背景（本文もサイドバーも） | **#080D10** | `palette.black`（editor・sideBar の背景） |
| 線 | #1A2327（ほとんど見えない） | Ohohama は線を透明にしている。Obsidian では区切りが要るので、ごくうすく |
| 本文の文字 | **#E6EDF9** | `palette.white`（foreground） |
| うすい文字 | #A4ADB0・#899296 | neutral のグレー |
| **アクセント**（ボタン、チェックボックス、引用の線） | **#0B8BEE** | `palette.city.t` |
| マウスを乗せたアクセント | #00BBDF | statusBar・選択の色 |
| **見出し**（h1〜h6） | **#259BCD** | `markup.heading.markdown` |
| リンク | #99CBFF | badge の色 |
| 選んだ文字 | #00BBDF を透かしたもの | `editor.selectionBackground` |
| コード | 文字 #BFC8CC、キーワード #57B1FF、関数・コメント #4CB6E9、文字列 #899296、数 #0097ED | `tokenColors` |

- 背景 #080D10 とのコントラスト（このパソコンで計算）：本文 16.6:1、見出し 6.2:1、リンク 11.5:1、うすい文字 8.5:1・6.2:1。どれも 4.5:1 をこえる
- ボタンの文字は、Ohohama の #E6EDF9 だと #0B8BEE の上で読みにくいので、**#080D10（黒）** にした（5.5:1）

#### コールアウトの色

Obsidian のコールアウト（`> [!caution]` など）は、はじめは種類ごとに **オレンジ・赤・緑・紫** などの色がつく。Ohohama の「青とグレーだけ」に合わないので、snippet で **すべて青系（とグレー）** に置きかえた（`--callout-color` を種類ごとに上書き）。警告も青にした（黄色も試したが、青系でそろえることにした）。

| 種類 | ダーク | ライト |
| --- | --- | --- |
| note・info・todo | #0B8BEE | #0966B0 |
| tip・hint・important・success・check・done | #00BBDF | #00708C |
| **warning・caution・attention**（もとはオレンジ） | **#57B1FF** | #145AA0 |
| danger・error・failure・fail・missing・bug（もとは赤） | #99CBFF | #00205B（Ohohama の city.k） |
| example | #4CB6E9 | #1A6E96 |
| question・help・faq | #259BCD | #166487 |
| quote・cite | #899296 | #5B6573 |
| abstract・summary・tldr | #A4ADB0 | #5B6573 |

- タイトルの文字の色も、この色になる。背景とのコントラストは、ダークで 5.5〜11.5:1、ライトで 4.9〜13.3:1（このパソコンで計算した）
- 色で種類を見分けにくくなるので、種類は **アイコン** で見分ける

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
