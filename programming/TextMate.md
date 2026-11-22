# TextMate

**TextMate** は、macOS 向けのグラフィカルなテキストエディタ。プログラミング言語やマークアップの編集に向けて、構文強調、スニペット、コマンド、マクロなどを備える。[公式サイト](https://macromates.com/)

## 歴史

- **2004年**：TextMate 1.0 を公開。当初は有料ソフトウェアだった。[公開時の告知](https://macromates.com/blog/2004/hello-world/)
- **2006年**：Wimer Hazenberg が TextMate 向けに **Monokai** の配色を作成。後に多くのエディタへ移植された。[Monokai の Vim 移植版](https://www.vim.org/scripts/script.php?script_id=2340)
- **2012年**：TextMate 2 のソースコードが GPL で公開された。[変更履歴](https://github.com/textmate/textmate/blob/master/Applications/TextMate/about/Changes.md)

現在公開されている TextMate のソースコードは GNU GPL バージョン3以降で提供される。[公式リポジトリ](https://github.com/textmate/textmate)

## バンドルと構文強調

**バンドル**は、言語定義、スニペット、コマンドなどをまとめる仕組み。言語定義はテキストの各部分に `string` や `comment` などの**スコープ**を割り当て、テーマがそのスコープに色やスタイルを対応させる。

TextMate の言語定義とスコープの仕組みは他のエディタにも使われている。たとえば VS Code は構文強調に TextMate 文法を利用し、テーマがスコープを色に対応づける。VS Code では、さらにセマンティック強調が重なる場合もある。[VS Code の構文強調ガイド](https://code.visualstudio.com/api/language-extensions/syntax-highlight-guide)、[セマンティック強調ガイド](https://code.visualstudio.com/api/language-extensions/semantic-highlight-guide)

## 関連

- [[エディタやターミナルの配色テーマ]] — Monokai を含む配色テーマの一覧と歴史。
