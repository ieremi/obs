# Obsidian の CSS スニペット

Obsidian の見た目は CSS スニペットで調整できる。ここでは書き方とデスクトップ・iOS での使い方をまとめる。

## デスクトップで CSS スニペットを使う

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

## iOS で CSS スニペットを使う

**iPhone・iPad でも CSS スニペットを使える。** 既定の保存先は保管庫内の `.obsidian/snippets/`。CSS ファイルを配置するだけではなく、iOS 版 Obsidian の **設定 → 外観 → CSS スニペット**で有効にする。[Obsidian Help: CSS snippets](https://obsidian.md/help/snippets)

### 方法1：パソコンで作って同期する

1. パソコン側の保管庫の `.obsidian/snippets/` に CSS ファイルを置く。
2. 利用している同期サービスで、その設定フォルダーと CSS ファイルが iPhone 側に届くようにする。設定フォルダーやスニペットが同期対象に含まれるかは、サービスと設定によって異なる。
3. iPhone の Obsidian で同じ保管庫を開き、**設定 → 外観 → CSS スニペット**へ進む。
4. 再読み込みボタンで一覧を更新し、目的のスニペットをオンにする。既にオンなら表示を確認する。

設定フォルダーを端末ごとに変更している場合、保存先もそのフォルダー内の `snippets` になる。ファイルの同期とオン／オフ設定の同期は別なので、必要に応じて各端末で確認する。[Obsidian Help: Configuration folder](https://obsidian.md/help/Files%2Band%2Bfolders/Configuration%2Bfolder)

### 方法2：iPhone だけで作る

標準の「ファイル」アプリでは `.obsidian` のような隠しフォルダーにアクセスしにくい場合がある。Obsidian の公式ヘルプは、隠しファイルを扱えるファイル管理アプリ、または Obsidian 内でスニペットを作るコミュニティプラグインを案内している。[設定フォルダーについて](https://obsidian.md/help/Files%2Band%2Bfolders/Configuration%2Bfolder)

たとえば **CSS Editor** プラグインを使う方法：

1. **設定 → コミュニティプラグイン → 閲覧**で `CSS Editor` を検索し、インストールして有効にする。コミュニティプラグインを使うには制限モードの解除が必要。
2. コマンドパレットから **CSS Editor: Create CSS snippet** を実行し、名前を付けて CSS を入力・保存する。
3. **設定 → 外観 → CSS スニペット**で一覧を再読み込みし、そのスニペットをオンにする。[CSS Editor](https://community.obsidian.md/plugins/css-editor)

コミュニティプラグインは第三者製なので、権限や信頼性を確認してから導入する。別の方法として、隠しフォルダーを扱えるファイル管理アプリで `.obsidian/snippets/` に `.css` ファイルを作成してもよい。

### 動作確認と注意

たとえば見出し 1 の色を青にするテスト用スニペット：

```css
body {
  --h1-color: #3366aa;
}
```

見出し 1 のあるノートで確認し、不要になったらスニペットをオフにする。反映されない場合は、ファイルの拡張子が `.css` か、正しい保管庫・設定フォルダーにあるか、スニペットがオンか、使用中のテーマが値を上書きしていないかを確認する。iOS とデスクトップでは画面構造やテーマの対応が異なり、同じ CSS が同じ見た目になるとは限らない。

この保管庫の `ohohama.css` は生成物なので直接編集しない。変更が必要な場合は、PC 側の `~/prd/src/ohohama` で元の設定・CSS を編集して生成し、配置したものを同期する。

## 関連

- [[Obsidianのカスタマイズ]]
- [[Obsidian を Ubuntu で使う]]
