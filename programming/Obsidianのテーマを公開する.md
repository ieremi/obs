# Obsidian のテーマを公開する

「テーマを公開する」には、主に二つの意味がある。

1. **コミュニティテーマとして公開する**：ほかの人が Obsidian のテーマ一覧からインストールできるようにする。
2. **Obsidian Publish に反映する**：自分の公開サイトの見た目をテーマや CSS で変える。

## 1. コミュニティテーマとして公開する

### 準備

GitHub アカウントと Obsidian アカウントを用意し、テーマのリポジトリを GitHub に作成する。[公式のサンプルテーマ](https://github.com/obsidianmd/obsidian-sample-theme)をひな形にできる。

主なファイルは次のとおり。

| ファイル | 内容 |
| --- | --- |
| `theme.css` | テーマ本体の CSS |
| `manifest.json` | テーマ名、バージョン、作者など |
| `README.md` | テーマの説明 |
| `LICENSE` | 利用条件を示すライセンス |
| スクリーンショット | テーマ一覧用の画像。推奨は 512 × 288 ピクセル、16:9 |
| `versions.json` | テーマのバージョンと対応する Obsidian の最低バージョンの対応表 |

[公式の申請手順](https://docs.obsidian.md/themes/app-themes/submit-theme) · [サンプルテーマの説明](https://github.com/obsidianmd/obsidian-sample-theme)

`manifest.json` の例：

```json
{
  "name": "ExampleBlue",
  "version": "1.0.0",
  "minAppVersion": "1.10.6",
  "author": "Your Name",
  "authorUrl": "https://example.com"
}
```

`minAppVersion` は例であり、実際に動作を確認した最低バージョンに合わせる。テーマ名は既存のものと重複できず、`Obsidian` や `Theme` を含めないなどの規則がある。申請後にテーマ名は変更できないので、先に確認する。 [マニフェストの仕様](https://docs.obsidian.md/Reference/Manifest)

### 手順

1. **テーマを作成して試す。** 開発用の保管庫の `.obsidian/themes/テーマ名/` に `theme.css` と `manifest.json` を置き、設定の「外観」から選ぶ。フォルダ名は `manifest.json` の `name` と一致させる。ライト・ダークやモバイルなど、対応すると決めた環境で確認する。 [テーマの作り方](https://docs.obsidian.md/Themes/App%20themes/Build%20a%20theme)
2. **GitHub に公開する。** ソース、`README.md`、`LICENSE`、スクリーンショット、最新の `manifest.json` をリポジトリの既定ブランチにコミットして push する。
3. **GitHub Release を作る。** `manifest.json` の `version` を `1.0.0` のような `x.y.z` にし、それと**完全に同じタグ**の Release を作成する。`manifest.json` と `theme.css` を Release の添付ファイルとして追加し、下書きのままにせず公開する。リポジトリにファイルを置くだけでは足りない。
4. **コミュニティディレクトリに申請する。** [Obsidian Community](https://community.obsidian.md/) にサインインし、GitHub アカウントを連携する。**Themes → New theme** から、リポジトリ URL、スクリーンショットの相対パス、対応するライト・ダークモードなどを入力する。
5. **レビュー結果に対応する。** 自動レビューのエラーを確認し、必要なら修正してバージョンを上げ、新しい Release を公開する。審査を通って公開されると、Obsidian のテーマ一覧からインストールできる。

ディレクトリは既定ブランチの `manifest.json` を読み、利用者がインストールするときには、そのバージョンと同じタグの Release に添付されたファイルを取得する。 [公式の申請手順](https://docs.obsidian.md/themes/app-themes/submit-theme)

### 更新するとき

初回の申請は一度だけでよい。その後はバージョンを上げ、既定ブランチの内容と必要な `versions.json` を更新し、同じバージョンのタグで `manifest.json` と `theme.css` を添付した新しい Release を公開する。 [公式サンプル](https://github.com/obsidianmd/obsidian-sample-theme)

コミュニティ公開用のテーマはネットワーク通信を行えないため、外部フォントなどの扱いにも注意する。 [テーマのガイドライン](https://docs.obsidian.md/Themes/App%20themes/Theme%20guidelines)

### CSS スニペットとの違い

CSS スニペットは既存のテーマに重ねる部分的な変更であり、そのままではコミュニティテーマとして登録するための一式にはならない。テーマとして配布するには、CSS を整理し、`manifest.json`、ライセンス、スクリーンショット、Release などを用意する。既存テーマを流用する場合は、そのライセンスも確認する。

Ohohama のスニペットは生成物なので、変更は元の `~/prd/src/ohohama` 側で行う。このノートでは生成物を直接編集しない。

## 2. Obsidian Publish のサイトに反映する

こちらはテーマを他人に配布する手順ではなく、有料サービス **Obsidian Publish** で公開している自分のサイトの見た目を変える方法である。

1. 利用したいテーマの `theme.css` を、保管庫のルートに `publish.css` という名前でコピーする。自分で Publish 用の CSS を書いてもよい。
2. Obsidian の **Publish: Publish changes** から `publish.css` を公開する。ファイルエクスプローラーには通常表示されなくても、公開ダイアログから選べる。
3. 公開サイトで表示を確認する。反映されない場合はブラウザのキャッシュも確認する。

アプリ用と Publish 用では画面の構造や CSS が異なるため、コピーしたテーマがアプリと同じ見た目になるとは限らない。また、アプリの設定フォルダにある CSS スニペットや Style Settings の設定が、そのままサイトに反映されるわけではない。 [サイトのカスタマイズ](https://obsidian.md/help/publish/customize) · [Publish の CSS に関する注意](https://obsidian.md/help/publish/troubleshoot)

## 関連

- [[programming/Obsidian の CSS スニペット|Obsidian の CSS スニペット]]
- [[programming/Obsidianのカスタマイズ|Obsidian のカスタマイズ]]
- [[programming/エディタやターミナルの配色テーマ|エディタやターミナルの配色テーマ]]
