# skim

**[skim](https://github.com/skim-rs/skim)** は Rust 製のコマンドライン用ファジーファインダー。実行コマンドは **`sk`**。候補を絞り込みながら選び、選択した行を標準出力に渡す。プログラムに組み込むライブラリとしても利用できる。

## 基本的な使い方

```sh
printf '%s\n' 'Obsidian' 'CodeMirror' 'Zed' 'navi' | sk
```

候補の一部を入力すると一覧を絞り込める。上下キーで選び、Enter で決定すると、選択した行が標準出力に出る。Esc でキャンセルできる。

```sh
find . -type f | sk
```

こちらは現在のディレクトリ以下のファイルを候補として選ぶ例。選択結果を表示するだけで、ファイルの編集や削除はしない。大量のファイルがある場所では列挙に時間がかかることがある。

## navi・fzf との関係

- [[navi]] はコマンドの説明や引数を含むチートシートを扱う。候補選択に `fzf` または skim を利用できる。
- **fzf** も同じ種類のファジーファインダーで、Go 製。skim は Rust で別途実装されている。検索アルゴリズムやオプションには差があり、すべてのコマンドで完全互換とは限らない。[skim: Differences from fzf](https://github.com/skim-rs/skim#differences-from-fzf)
- [[KRunner]] と異なり、skim 自体は候補の選択部品であり、デスクトップ全体のアプリや操作を自動で管理するものではない。

## fzf より skim が向くところ

**常に skim の方が優れているわけではない。** 選ぶ理由は、必要な機能や組み込み先によって変わる。

1. **Rust プログラムに組み込みたい**：skim は CLI だけでなく Rust のライブラリとして提供され、候補の表示・比較などをカスタマイズできる。Rust アプリ内で選択画面を作りたい場合に便利。[skim: Use as a library](https://github.com/skim-rs/skim#use-as-a-library)
2. **検索アルゴリズムを選びたい**：公式資料には、入力ミスへの耐性を意識した `frizbee` や `arinae` など複数のアルゴリズムが記載されている。候補の並びや入力ミスへの対応が好みに合えば利点になる。利用できる設定は手元の版の `sk --help`・`man sk` で確認する。[skim: Algorithms](https://github.com/skim-rs/skim#algorithms)
3. **外部コマンドを入力に応じて実行したい**：skim の `-i`・`-c` を使う専用のインタラクティブモードでは、検索語に応じて `rg` などの結果を更新できる。ただし **fzf にも `reload` による同様の方法がある**ため、skim だけができる機能ではなく、設定方法と操作感の違いとして比較する。[skim: Interactive mode](https://github.com/skim-rs/skim#interactive-mode)、[fzf: Interactive Ripgrep launcher](https://github.com/junegunn/fzf/blob/master/ADVANCED.md#using-fzf-as-interactive-ripgrep-launcher)

### 気をつけること

- **速さは条件次第**：候補数、検索語、バージョン、マシンによる。Rust 製だから必ず速いとはいえない。skim の公式ベンチマークも測定手法に限界があると明記している。
- **fzf と完全互換ではない**：オプションやマッチ結果が異なることがある。既存スクリプトや [[navi]] との組み合わせは、利用する両方のバージョンで試す。
- **Rust 製であること自体は使用時の優位性ではない**。CLI として使うだけなら、普段の候補や連携ツールで使いやすい方を選べばよい。

## 導入

公式リポジトリには各種パッケージマネージャーや Cargo による導入方法がある。たとえば Rust の開発環境があれば `cargo install skim` を使える。利用可能なパッケージ・バージョンや `PATH` は環境ごとに確認する。[公式インストール手順](https://github.com/skim-rs/skim#installation)

この環境へのインストールや動作確認は行っていない。
