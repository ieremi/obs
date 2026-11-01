---
tags: [プログラミング, VSCode, Markdown, 設定]
aliases: [VS Code で Markdown をプレビューで開く, VSCode Markdown プレビュー, editorAssociations, workbench.editorAssociations, vscode.markdown.preview.editor]
date: 2026-11-01
---
# VS Code で Markdown をプレビューで開く

**`settings.json` に `workbench.editorAssociations` を書くと、`*.md` を開いたとき、はじめからプレビューで開く。** 拡張機能は要らない。

```json
{
  "workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
  }
}
```

- 書く場所：
  - **ユーザー設定**（`~/.config/Code/User/settings.json`。Linux の場合）に書くと、すべてのフォルダーで効く
  - **ワークスペース設定**（そのフォルダーの `.vscode/settings.json`）に書くと、そのフォルダーだけで効く
- 画面からなら：設定（`Ctrl+,`）で「**Editor Associations**」を検索 → 「項目の追加」→ 項目 `*.md`、値 `vscode.markdown.preview.editor`
- 効いたかどうか：md を開いて、コマンドパレット（`Ctrl+Shift+P`）の「**表示: エディターを再度開く…**」（View: Reopen Editor With…）を見る。「Markdown Preview」に「既定」とついていれば効いている

## 書きなおしたいとき
- プレビューは **読むだけ** で、書けない
- 書くときは、コマンドパレットの「**エディターを再度開く…**」で「**テキスト エディター**」を選ぶ
- 横に並べて見るなら、テキストで開いてから `Ctrl+K V`（プレビューを横に開く）。プレビューだけにするなら `Ctrl+Shift+V`

## 注意
- 開くのが **プレビューだけ** になるので、md を書くことが多いなら、かえって不便になる。**書くことが多い人は、この設定はせず、`Ctrl+Shift+V` を使う** ほうがよいこともある
- VS Code をはじめて起動したときに開いた 1 つ目の md は、テキストで開くことがある、という報告がある（2025 年 3 月、VS Code 1.98.2）。2 つ目からはプレビューで開く
- git の差分の画面など、ほかの所で開く md にも効いてしまう。困るときは、パターンを `"{git,gitlens}:/**/*.md": "default"` のように分けて、そこだけふつうのエディターにする方法がある

## 押さえどころ
- `"workbench.editorAssociations": { "*.md": "vscode.markdown.preview.editor" }` で、md がひとりでにプレビューで開く
- 書くときは「エディターを再度開く… → テキスト エディター」

## 出典
- [GitHub：microsoft/vscode の issue 244597（goodfirstissue.org）](https://www.goodfirstissue.org/Microsoft/vscode/issues/244597)：`*.md` に `vscode.markdown.preview.editor` を割りあてるやり方、「Reopen editor with…」で既定を確かめること、はじめての起動で効かないことがある報告（検索結果の要約による）
- [GitHub：microsoft/vscode の issue 84520](https://www.github.com/microsoft/vscode/issues/84520)：昔は `workbench.experimental.editorAssociations` という名前だったこと（検索結果の要約による）
- 書きなおすときの手順、`Ctrl+K V`・`Ctrl+Shift+V`、git の差分のパターン：一般的な知識（ウェブでの確認はしていない）

関連：[[Obsidian]]
