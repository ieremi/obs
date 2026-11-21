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
  - 見出しをモダンに（下の「見出しの見せ方」）
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
| 見出し | h1・h2 は本文と同じ #E6EDF9、h3 は #57B1FF、h4 以下は #A4ADB0（下の「見出しの見せ方」） | はじめは Ohohama の `markup.heading.markdown` の #259BCD にしていたが、モダンにするときに変えた |
| リンク | #99CBFF | badge の色 |
| 選んだ文字 | #00BBDF を透かしたもの | `editor.selectionBackground` |
| コード | 文字 #BFC8CC、キーワード #57B1FF、関数・コメント #4CB6E9、文字列 #899296、数 #0097ED | `tokenColors` |

- 背景 #080D10 とのコントラスト（このパソコンで計算）：本文と h1・h2 16.6:1、h3 8.5:1、リンク 11.5:1、うすい文字 8.5:1・6.2:1。どれも 4.5:1 をこえる
- ボタンの文字は、Ohohama の #E6EDF9 だと #0B8BEE の上で読みにくいので、**#080D10（黒）** にした（5.5:1）

#### 見出しの見せ方（モダンに）

見出しを **角のまるい枠** でかこむ形にした。大きさ・太さ・色でも階層を見せる。

| 見出し | 形 | 大きさ・太さ | 文字の色（ダーク／ライト） |
| --- | --- | --- | --- |
| h1 | **うすい青の角丸の帯**（#0B8BEE の 14%、角の丸み 12px）＋ **1 文字目の後ろに水色の円**（#00BBDF の 45%、直径 1.6em で、帯より上下にはみ出す。`::before` で描き、文字の後ろに回す） | 2em・700 | 本文と同じ #E6EDF9／#222831 |
| h2 | **左に太い縦の線（7px）＋斜めのしま模様の背景**（-45 度、5px おき）。角は四角 | 1.5em・700 | ダークは白 #E6EDF9 で線は #0B8BEE、ライトは **紺 #00205B**（Ohohama の `city.k`）で線も紺 |
| h3 | **文字の長さだけの、丸い「ピル」**（角の丸み 999px、1px の白っぽい枠線） | 1.2em・700 | 青 #57B1FF／#0966B0 |
| h4 | 前に **小さな丸い点**（#0B8BEE） | 1.05em・500 | うすいグレー #A4ADB0／#5B6573 |
| h5・h6 | かざりなし | 1〜0.95em・500 | うすいグレー |

- **背景は本文とほとんど同じ** にし（#0B8BEE を 3〜6% だけ透かす）、**白っぽい、はっきりした枠線** で見出しを見せる（ダークは Ohohama の白 #E6EDF9 の 45〜70%、ライトは白 #FFFFFF）。はじめは背景を 12〜28% にして h1 をグラデーションにしたが、本文との差が大きすぎてやぼったかったので、うすくした
- 見出しの上の余白を広く（`--heading-spacing: 2.2em`）、行間をつめた（1.3〜1.4）
- **h1・h2 のあと** は、すきまを広くした（読む画面は h1 に `margin-bottom: 1.6em`、h2 に `1.3em`。編集の画面は、見出しの次の行に `padding-top`：h1 のあと 1.3em、h2 のあと 1em）
  - 見出しの **すぐ次の行がリスト**（空の行なし）だと、すきまが出なかった（`cleaning/尿石.md` の「できるしくみ」）。そこで、見出しの次のかたまり（`h2 + ol`、`div:has(> h2) + div > :first-child` など）の上にも `margin-top` を `!important` でつけ、編集の画面の `padding-top` にも `!important` をつけた
- **読む画面**（`.markdown-rendered hN`）と **編集の画面**（ライブプレビューの `.cm-line.HyperMD-header-N`）の両方につけた。ただし編集の画面では、h3 も行いっぱいの角丸になる（CodeMirror の行は、文字の長さに合わせられないため）。編集の画面の枠線は、`border` ではなく `box-shadow: inset`（内側の影）で描いた。`border` だと行の高さがずれるため
- Obsidian の変数 `--h1-size`〜`--h6-size`、`--h1-weight`〜、`--h1-color`〜、`--h1-line-height`〜 を使った
- 背景とのコントラスト：h3 は 8.5:1（ダーク）・5.1:1（ライト）、h4 以下は 8.5:1・5.1:1（このパソコンで計算した。枠の中は少し色がつくので、実際は少しだけ下がる）
- Noto Sans CJK JP は、太さ 500（Medium）と 700（Bold）を持っている

#### スペルチェックの赤い波線を消す

英語の単語（`CONFIG.SYS`、`AUTOEXEC.BAT` など）の下に出る **赤い波線** は、Obsidian の **スペルチェック**。日本語のノートが中心のこのボールトでは、ほとんど役に立たない。

- 消し方：**Settings → Editor → Spellcheck** をオフ（`Ctrl+,` → Editor → Spellcheck）
- 設定は `.obsidian/app.json` に `"spellcheck": false` として入る
- **このボールトでは、スペルチェックは残して、波線の色だけ青にした**（snippet に足した。Chromium の疑似要素 `::spelling-error`・`::grammar-error` を使う）：

  ```css
  ::spelling-error {
    text-decoration: underline wavy var(--interactive-accent);
    text-decoration-thickness: 1px;
    text-underline-offset: 3px;
  }
  ```

  - `::spelling-error` で使えるのは、文字の色や `text-decoration` など一部のプロパティだけ
  - Electron（Chromium）の版が古いと効かない。効かなければ、スペルチェックをオフにする

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

#### ハイライトの色

アウトラインや検索で飛んだ先が **黄色く点滅** し、`==文字==` のハイライトも黄色になる。これは `--text-highlight-bg`（と、検索で今いる所の `--text-highlight-bg-active`）の色。snippet で **#0B8BEE を透かした青** にした。

| | ダーク | ライト |
| --- | --- | --- |
| ハイライト・点滅 | #0B8BEE の 35% | #0B8BEE の 25% |
| 検索で今いる所 | #00BBDF の 45% | #0B8BEE の 40% |

#### 警告の色（黄色・オレンジ）

Copilot プラグインの設定の **⚠ の黄色** など、Obsidian やプラグインの「警告」は `--text-warning` の色を使う。ほかにも `--color-yellow`・`--color-orange`（と、その `-rgb`）を使う所がある。snippet で、これらを **全体で青系** にした。

| 変数 | ダーク | ライト |
| --- | --- | --- |
| `--text-warning`・`--color-yellow` | #57B1FF | #145AA0 |
| `--color-orange` | #4CB6E9 | #1A6E96 |

- 緑（`--color-green`・`--color-green-rgb`・`--text-success`）も、全体で **水色**（ダーク #00BBDF、ライト #00708C）にした。Copilot のチャットの「+65」のような、差分の追加の数が緑だったため
- 赤（`--text-error`・`--color-red`）は、全体ではまだ変えていない（Git の画面の中だけ青にした）

#### Git プラグインの色

[[Obsidian で Git を使う|Git プラグイン]]（obsidian-git）は、変更の一覧の **M をオレンジ**、**D を赤** で出し、差分や行の印には **緑・黄・赤** を使う。これも snippet で **青系** にした。

| 意味 | 一覧の文字 | ダーク | ライト |
| --- | --- | --- | --- |
| 追加・新しいファイル | A・U・? | #00BBDF | #00708C |
| 変更 | M・R・C | #57B1FF | #145AA0 |
| 削除 | D | #0B8BEE | #00205B |

- プラグインの CSS（`.obsidian/plugins/obsidian-git/styles.css`）を読んで、上書きする所を決めた：
  - 一覧の文字：`.git-tools .type[data-type="M"]` などに、じかに `orange`・`red` と書いてある
  - 行の印・下の帯・差分：`var(--color-green)`・`--color-yellow`・`--color-red` を使っている。snippet では、**Git の画面と部品の中だけ** これらの変数を青に置きかえた（ほかの所の赤や緑は変えない）
  - 差分の画面（diff2html）：`--git-insert-bg` などの変数
  - 左右に並べる差分：`.cm-deletedLine`・`.cm-insertedLine` の背景

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
