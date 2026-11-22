# ユーザーの好み・執筆ルール

## 1. 回答・出力の形式
- ユーザーがトピックを提示したときや質問をしたときは、チャット上で回答を完結させず、Obsidian内の適切なページ（ノート）を作成または追記して記録する。
- チャットでは完了報告および該当ページへのファイルリンク（`file://` 形式）のみを簡潔に伝える。

## 2. 図・ビジュアル表現の配色
- ノート内に掲載する図（SVG、Mermaid、ダイアグラム等）には、**無彩色（白、黒、グレー、`currentColor`）と青系（ブルー、ネイビー、スレートブルー等）のみ**を使用する。
- 赤、オレンジ、黄、緑などの暖色系やその他の色相は使用しない。

## 3. Ohohama のスニペット
- `.obsidian/snippets/ohohama.css` は `~/prd/src/ohohama` の `obsidian/` から生成したものを、そのままコピーしている。このファイルは直接編集しない。
- 見た目を変えるときは `~/prd/src/ohohama` の `obsidian/config.ts`・`obsidian/rules.css` を編集し、`~/prd/src/ohohama` で `OBSIDIAN_SNIPPETS_DIR=~/prd/src/obs/.obsidian/snippets npm run deploy:obsidian` を実行してコピーする。
