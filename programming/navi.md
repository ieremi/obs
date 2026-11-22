# navi

**[navi](https://github.com/denisidoro/navi)** は、ターミナルでコマンドのチートシートを検索し、必要な引数を指定して使うための対話型ツール。Rust で開発され、候補の絞り込みには `fzf` または [[skim]] を使う。

長いコマンドやオプションをすべて暗記する代わりに、説明文から目的の操作を探せる。自分で `.cheat` ファイルを育てる使い方は [[Unix 盆栽]] にも近い。

## 使い方

1. navi と検索用の `fzf` または `skim` を導入する。導入方法は環境により異なるので、[公式インストール手順](https://github.com/denisidoro/navi/blob/master/docs/installation/README.md)を確認する。
2. ターミナルで `navi` を起動し、説明やタグからコマンドを検索する。
3. 候補を選び、必要な変数を入力・選択する。実行されるコマンドと引数を必ず確認する。

初回起動時にはチートシートの導入案内がある。自分の `.cheat` ファイルを配置する方法やリポジトリから取り込む方法もある。[チートシートの説明](https://github.com/denisidoro/navi/blob/master/docs/cheatsheet/README.md)

## 自分のチートシート

例として、`network.cheat` に次のように書く。

```text
% network, diagnostics

# IP アドレスを確認
ip -br address

# IPv4 の経路を確認
ip route

# DNS の状態を確認
resolvectl status
```

`%` はタグ、`#` は操作の説明、次の行はコマンド。`ip` や `resolvectl` が使える Linux 環境向けの例で、`resolvectl` は systemd-resolved に依存する。これらは設定を変更せず状態を表示するが、結果には内部 IP アドレスなどが含まれ得る。

`.cheat` の保存先は設定やバージョンによって異なる。公式ドキュメントでは既定の保存先を、2.25.0 より前は `navi info cheats-path`、それ以降は `navi info default-cheats-path` で確認する方法を示している。手元の `navi info --help` と併せて確認する。[チートシートの配置](https://github.com/denisidoro/navi/blob/master/docs/cheatsheet/README.md)

## シェルと連携する

Zsh の場合、公式ドキュメントでは `~/.zshrc` に次を追加する方法が紹介されている。

```sh
eval "$(navi widget zsh)"
```

新しいシェルでウィジェットが有効になると、既定では `Ctrl+G` で navi を開ける。選んだコマンドはシェルの入力行に入り、実行前に編集できる。キーの競合やシェル設定を確認すること。[ウィジェットの設定](https://github.com/denisidoro/navi/blob/master/docs/widgets/README.md)

## KRunner やアプリのパレットとの違い

| ツール | 主な対象 |
| --- | --- |
| **navi** | ターミナルのチートシートに登録されたシェルコマンド |
| [[KRunner]] | アプリの起動、ファイル検索、Desktop Actions など |
| [[アプリ横断のコマンドパレット\|アプリ内パレット・メニュー検索]] | 対象アプリが提供・公開する操作 |

navi は GUI アプリのメニューやコマンドを自動収集するものではない。CLI やスクリプトとして実行できる操作を自分で登録し、ターミナルから探す用途に向く。

## 安全面

外部のチートシートには実行可能なコマンドが含まれる。**実行前に内容を確認するだけでなく、取り込み前に変数候補を生成する `$` 行も確認する。** navi は候補生成のためにシェルコマンドを実行することがある。[変数とシェルの設定](https://github.com/denisidoro/navi/blob/master/docs/configuration/README.md)

この環境へのインストール、シェル設定の変更、動作確認は行っていない。
