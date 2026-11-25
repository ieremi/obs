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

## 現在のディレクトリ構成の確認

確認日：2026-11-25。ローカルのファイルと設定を確認した結果。

**`obs` を保管庫として開くなら、`obs/.obsidian/snippets/ohohama.css` は正しい配置であり、そのままでよい。** 質問の `ohama.css` に相当する実ファイル名は `ohohama.css`。`obs/.obsidian/appearance.json` の `enabledCssSnippets` にも `ohohama` があり、ファイル名と一致している。公式の配置先は、各保管庫の設定フォルダー内の `snippets`。[Obsidian Help: CSS snippets](https://obsidian.md/help/snippets)

### 現状と判断

```text
Documents/
├── .obsidian/                   ← 親を保管庫として開いた場合の設定
└── obs/                         ← 日常の保管庫に統一する候補
    ├── .obsidian/
    │   ├── appearance.json      ← ohohama が有効
    │   └── snippets/
    │       └── ohohama.css       ← 生成済みCSSの配置先（現状でよい）
    ├── programming/
    ├── med/
    ├── geography/
    └── elec/
        └── .obsidian/           ← elec 用の設定フォルダーも存在
```

- 分野別のノート用ディレクトリは、そのままでよい。今回の確認では、全体を組み替える必要性は見つからなかった。
- `Documents/.obsidian/appearance.json` は `Paper Blue` テーマの設定で、`ohohama` の有効化指定はない。親の `Documents` を開くと、`obs/.obsidian` の設定は使われない。実際にアプリで開いている保管庫は今回確認していないため、設定画面のスニペットフォルダーから確認する。
- `obs/elec/.obsidian` も存在する。これは設定フォルダーの存在を示すもので、現在別の保管庫として利用中かは未確認。用途を確認するまでは残す。
- `enabledCssSnippets` には `ubuntu-ja` もあるが、今回 `obs/.obsidian/snippets` に見つかったCSSは `ohohama.css` だけだった。`ubuntu-ja` を使っていないなら、有効化指定の整理候補になる。

### Ohohama の管理方法

生成元と配置先を分ける現在の方針は適切。`ohohama.css` の先頭コメントと `obs/AGENTS.md` に、生成物を直接編集しない旨がある。配色やフォント、見出し、プラグイン向けの調整を含むが、長いことだけを理由に生成済みファイルを手作業で分割する必要はない。分割するなら生成元で行う。

ただし、`obs/AGENTS.md` に記載された配置先 `~/prd/src/obs/.obsidian/snippets` は、このMacでは親の `~/prd/src/obs` 自体が存在しなかった。生成元の `~/prd/src/ohohama` は存在する。次回の配置時には、このMacの実際の保存先を指定する。

```sh
cd ~/prd/src/ohohama
OBSIDIAN_SNIPPETS_DIR="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/obs/.obsidian/snippets" npm run deploy:obsidian
```

これは既存の運用指示に基づき保存先を修正したコマンド例であり、今回実行したものではない。

**推奨は、普段開く保管庫を `obs` に統一し、CSSは現在の場所に残すこと。** 親と `elec` の設定を整理する場合は、それぞれを保管庫として使っていないことを確認してから行う。今回は調査結果のみ追記し、CSS・設定・ディレクトリの移動や削除は行っていない。

ローカルの確認元：`Documents/.obsidian/appearance.json`、`obs/.obsidian/appearance.json`、`obs/.obsidian/snippets/ohohama.css`、`obs/elec/.obsidian/appearance.json`、`obs/AGENTS.md`、生成元・配置先ディレクトリの存在確認。

### `obs` というディレクトリ自体は必要か

**Obsidianの仕組み上、`obs` という名前のディレクトリは必須ではない。ただし、現在の構成では保管庫とGitの境界になっているので、残すのが扱いやすい。** 前述の推奨は、この現状を踏まえたもの。

`Documents` は保管庫を入れる親フォルダー、`obs` はノートと設定をまとめる保管庫、と考えれば自然な構成になる。`obs` を開けば、その直下の分野別フォルダーが見えるため、Obsidian内で余分な一階層をたどる必要もない。CSSも保管庫からの相対位置は `.obsidian/snippets/ohohama.css` であり、`obs` という名前には依存しない。

2026-11-25の追加確認では、Gitのルートも `Documents/obs` だった。また、`obs/.git` はディレクトリではなくファイルなので、単純に中身を親へ移すとGitの参照関係が壊れる可能性がある。移動するなら、その参照先も確認する必要がある。

`obs` をなくして `Documents` 自体を保管庫にすることもできるが、これは中身を親へ移す構成変更になる。親にも `.obsidian` とノートがあるため、設定や同名ファイルを統合し、Gitと配置スクリプト、Obsidianで開く場所も合わせて変更する必要がある。階層を一つ減らすだけの目的なら、その作業をする利点は小さい。

したがって、今回のおすすめは **`obs` を残し、Obsidianで `Documents/obs` を開くこと**。親の `Documents/.obsidian` は、親を別の保管庫として使っているかを確認したうえで整理する候補になる。今回、移動や削除は行っていない。

追加の確認元：`git -C obs rev-parse --show-toplevel` の結果と `obs/.git` のファイル種別。

### `.obsidian` が親と子に二つあるのはどうか

**存在するだけなら問題はないが、保管庫を一つだけ使うつもりなら、設定が分散して紛らわしい構成。** Obsidianは、開いた保管庫の設定フォルダーを使う。親と子の設定を自動で合成したり、親の設定を子が引き継いだりはしない。[Obsidian Help: Configuration folder](https://obsidian.md/help/Files%2Band%2Bfolders/Configuration%2Bfolder)

| 開く保管庫 | 通常使われる設定 | 今回確認した外観設定 |
| --- | --- | --- |
| `Documents` | `Documents/.obsidian` | Paper Blue |
| `Documents/obs` | `Documents/obs/.obsidian` | ohohama スニペットが有効 |

この表は既定の設定フォルダー名を使う場合。設定フォルダーの変更機能を使っている場合は、その指定先を確認する。

**現在の整理方針としては、`obs/.obsidian` を残す。** ノート群とGitのルートが `obs` にあり、`ohohama.css` もそこに配置されているため。親の `Documents/.obsidian` は、`Documents` 自体を保管庫として使わないなら不要になる。ただし、親には独自のテーマ・プラグイン・ワークスペース設定が入っている可能性があるため、用途を確認せず削除はしない。

整理する場合は、まず `Documents/obs` を保管庫として開いて、ノートとOhohamaの表示を確認する。その後、親の `.obsidian` は保管庫の外へバックアップしてから取り除く。親に残っているノートは別途 `obs` に移すか判断する。設定フォルダーを取り除いてもノート自体は削除されないが、親を保管庫として再び開くと設定フォルダーが再作成され得る。

なお、厳密には今回の確認では `obs/elec/.obsidian` もあり、設定フォルダーは計三か所にあった。`elec` を独立した保管庫として使わないなら、こちらも同じ判断で整理する候補。2026-11-25時点では、実際に開いている保管庫と各設定の利用状況は未確認で、削除や移動は行っていない。

### 方針の修正：root の `.obsidian` を残す

2026-11-25、ユーザーから「root/.obsidian を残すべきでは」と指摘。ここでの root は `/` ではなく、この作業フォルダーの `Documents` を指す。

**`Documents` を保管庫のルートとして使う方針なら、残す設定は `Documents/.obsidian`。** 上の「`obs/.obsidian` を残す」という推奨は、`obs` を保管庫として開く前提に基づくものだった。Gitのルートが `obs` であることは、Obsidianの保管庫も `obs` にすべき理由にはならない。Gitと保管庫の境界は別に決められる。以後は、この節の方針を優先する。

この場合、`obs` は保管庫内のノート用サブフォルダーとして残してもよい。`obs` 自体をなくしてノートを直下に移す作業と、設定フォルダーを一つにする作業は別なので、一度に行う必要はない。

Ohohamaを使うには、生成済みCSSを `Documents/.obsidian/snippets/ohohama.css` に配置し、root側の外観設定で有効にする。現状のroot側はPaper Blueの設定なので、CSSをコピーするだけで子側と同じ表示になるとは限らず、使用するテーマも合わせて判断する。子側の `appearance.json` で有効になっているだけでは、root側では有効にならない。

設定を統合するときは、root側の既存設定を保ち、必要なスニペットやプラグイン設定を個別に引き継ぐ。動作確認とバックアップの後、使わなくなる `obs/.obsidian` と、独立保管庫として使わない場合の `obs/elec/.obsidian` を整理する。Ohohamaの生成・配置手順の出力先もroot側の `snippets` に変更する。

今回は方針の訂正のみを記録し、設定の統合・CSSのコピー・削除はまだ実施していない。

## rootへの設定統合（実施済み）

確認日：2026-11-25。ユーザーの指示により、上記の検討後に次の作業を実施した。この節が現在の状態を示す。

- 保管庫の設定を `Documents/.obsidian` に統合し、Ohohamaの生成済みCSSをバイト単位で同一のまま `Documents/.obsidian/snippets/ohohama.css` にコピーした。
- rootの外観を標準テーマ＋Ohohamaに変更。Paper Blueのテーマファイルは保持し、存在しない `ubuntu-ja` の有効化指定は引き継がなかった。
- rootの既存Copilot本体・設定、ワークスペース、コアプラグイン設定を保持。子側のアプリ設定（インラインタイトル非表示・PDF設定）と、未配置だったchem・obsidian-git・grimoireを引き継いで有効化指定を統合した。
- Gitプラグインの `basePath` は `obs` に設定。Gitのルートとノートの配置は変えていない。
- `obs/.obsidian` と `obs/elec/.obsidian` は削除せず、`.config-backups/obsidian-consolidation-20261125-143111/` に移動。変更前のroot設定と `obs/AGENTS.md` も同じ場所にバックアップした。
- `obs/AGENTS.md` のCSS配置先をrootへ修正した。

ローカルのJSON整合性・CSS一致・配置とGitルートを確認。Obsidian画面での表示・プラグイン動作は未確認。`Documents` を保管庫として開き直すか、既に開いていればアプリを再読み込みして反映する。子フォルダーを独立保管庫として開くと、子側の設定が再作成される可能性がある。

## 関連

- [[Obsidianのカスタマイズ]]
- [[Obsidian を Ubuntu で使う]]
