---
tags: [プログラミング, Obsidian, Ubuntu, Linux]
aliases: [Obsidian を Ubuntu で使う, Obsidian Ubuntu, Obsidian Linux, Obsidian のインストール]
related:
  - "[[Obsidianのカスタマイズ]]"
  - "[[VS Code で Markdown をプレビューで開く]]"
確認日: 2026-11-21
---
# Obsidian を Ubuntu で使う

**Obsidian は Linux 版も公式に出ている（無料）。** Ubuntu では **.deb** で入れるのがいちばん手間が少ない。いまの最新は **1.15.1**（2026 年 11 月 12 日）。

## 入れ方の比べ

| 形 | 入れ方 | 更新 | 一言 |
| --- | --- | --- | --- |
| **.deb**（公式） | `sudo apt install ./obsidian_1.15.1_amd64.deb` | アプリの中で自動（下の「更新」） | **おすすめ**。メニューに出る、`/opt/Obsidian` に入るので **AppArmor の問題が起きない** |
| **AppImage**（公式） | ダウンロードして実行権をつける | アプリの中で自動 | 入れずに動かせる。ただし Ubuntu 24.04 では **FUSE と sandbox の問題** が出やすい |
| **Snap**（公式） | `sudo snap install obsidian --classic` | Snap が自動で | 楽。ただし **Ubuntu 26.04 で起動しない不具合** の報告がある |
| **Flatpak**（有志がまとめたもの） | `flatpak install flathub md.obsidian.Obsidian` | Flatpak が自動で | 公式ではない。ファイルへのアクセスが制限されることがある |

- ダウンロードは **https://obsidian.md/download** か、GitHub の **obsidianmd/obsidian-releases** のリリース
- ARM（aarch64）用の AppImage と tar.gz もある

## .deb で入れる（おすすめ）

```sh
cd ~/Downloads
curl -LO https://github.com/obsidianmd/obsidian-releases/releases/download/v1.15.1/obsidian_1.15.1_amd64.deb
sudo apt install ./obsidian_1.15.1_amd64.deb
obsidian            # またはアプリのメニューから
```

- `apt install ./ファイル名` と **`./` をつける**（つけないと、パッケージの名前として探してしまう）
- 大きさ：.deb が **108 MB**、入れたあとは **356 MB**
- 入れると、`update-alternatives` で **`/usr/bin/obsidian` → `/opt/Obsidian/obsidian`** が作られるので、端末から `obsidian` で起動できる
- 最後に **`N: Download is performed unsandboxed as root, as file '…/obsidian_1.15.1_amd64.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: 許可がありません)`** と出ることがある。**エラーではなく、ただのお知らせ（N: は Notice）で、無視してよい**
  - apt は、ふだんはファイルを **`_apt`** という権限の弱いユーザーで読む（安全のため）。ホームフォルダー（`/home/ユーザー名`）は、ほかのユーザーが入れない設定のことが多いので、`_apt` が .deb を読めず、かわりに root で読んだ、という意味
  - 出したくなければ、.deb を `/tmp` に置いてから入れる（`sudo apt install /tmp/obsidian_1.15.1_amd64.deb`）
- 足りないライブラリがあれば、apt がいっしょに入れる（`libxss1` が要った、という報告がある）
- アンインストール：`sudo apt remove obsidian`

## AppImage で使うとき

```sh
sudo apt install libfuse2t64          # Ubuntu 24.04 では名前が libfuse2t64
chmod +x Obsidian-1.15.1.AppImage
./Obsidian-1.15.1.AppImage
```

Ubuntu 24.04 で起きやすい 2 つの問題：

| 症状 | わけ | 直し方 |
| --- | --- | --- |
| `dlopen(): error loading libfuse.so.2` | AppImage が使う **FUSE 2** が、24.04 には入っていない | `sudo apt install libfuse2t64` |
| `The SUID sandbox helper binary was found, but is not configured correctly` | 24.04 から、AppArmor が **ふつうのユーザーの user namespace** を制限する。Electron のアプリ（Obsidian など）の sandbox がこれを使う | ① **.deb にする**（いちばん楽）<br>② AppImage を **`/opt/Obsidian/obsidian`** に置く（Ubuntu が用意した AppArmor のプロファイル `/etc/apparmor.d/obsidian` が、このパスのときだけ userns を許す）<br>③ `--no-sandbox` をつけて起動（安全の仕組みを切るので、おすすめしない） |

- このパソコン（Ubuntu 24.04）の `/etc/apparmor.d/obsidian` は、`profile obsidian /opt/Obsidian/obsidian flags=(unconfined) { userns, ... }` となっていた。.deb は `/opt/Obsidian/` に入るので、このプロファイルがそのまま効く
- 1.15.1 の .deb を入れると、.deb の中の `/opt/Obsidian/resources/apparmor-profile` で、`/etc/apparmor.d/obsidian` が書きかえられた（中身はほぼ同じで、名前とパスに引用符がつき、はじめのコメントがなくなった）。このファイルは、もとは Ubuntu の `apparmor` パッケージのもの

### このパソコンでの結果（2026-11-21）
- Ubuntu 24.04.5 に **1.15.1 の .deb** を入れ、起動できた。sandbox のエラーは出なかった

## 更新
- .deb と AppImage は、**アプリの中で新しい版を知らせて、自分で更新する**（設定 → 一般 → 自動更新）
- ただし、中身（アプリの本体）だけ更新される形なので、**インストーラーの版が古くなりすぎると** 「インストーラーを入れなおして」と言われる。そのときは新しい .deb を入れなおす
- Snap・Flatpak は、それぞれのしくみで更新される

## 使いはじめる
1. 起動すると、**新しいボールトを作る** か **フォルダーをボールトとして開く** かを聞かれる
2. このボールトなら「**フォルダーをボールトとして開く**」で `~/prd/src/obs` を選ぶ。`.obsidian/` の設定もそのまま使われる
3. 複数のボールトは、左下のボールトの名前から切りかえる

### Ubuntu でのこつ
| こと | どうする |
| --- | --- |
| 日本語入力 | fcitx5 や IBus で入る。入らないときは、環境変数 `GTK_IM_MODULE`・`QT_IM_MODULE`・`XMODIFIERS` を確かめる（→ [[IME の自作]]） |
| 日本語のフォント | 設定 → 外観 → フォントで **Noto Sans CJK JP** などを指定（→ [[Obsidianのカスタマイズ]]） |
| Wayland で文字がぼやける | Electron のオプション `--ozone-platform=wayland` をつけて起動すると直ることがある |
| ショートカット | Mac の `⌘` は **`Ctrl`** になる（例：設定は `Ctrl+,`、コマンドパレットは `Ctrl+P`） |
| `obsidian://` のリンク | .deb で入れると、ブラウザーからのリンクでアプリが開くように登録される |
| 同期 | 公式の **Obsidian Sync**（有料）、または **git**（このボールトのやり方。コミュニティプラグインの **Obsidian Git** もある）、Syncthing など |

## 押さえどころ
- Ubuntu では **公式の .deb**（`sudo apt install ./obsidian_*.deb`）がいちばん楽で、問題が少ない
- AppImage は 24.04 で **libfuse2t64** と **sandbox（AppArmor）** の問題が出る。`/opt/Obsidian/obsidian` に置けば AppArmor の問題は消える
- Snap は Ubuntu 26.04 で起動しない報告がある。Flatpak は公式ではない
- 最新は 1.15.1（2026 年 11 月）

## 出典
- [Obsidian ヘルプ：Download and install Obsidian](https://obsidian.md/help/install)：Linux 版の形（AppImage・Snap・Deb・ARM 用 AppImage、Flatpak は有志）、Flatpak の ID（検索結果の要約による）
- GitHub の API（`obsidianmd/obsidian-releases` の latest）：1.15.1、2026 年 11 月 12 日、ファイルの一覧（このパソコンで curl で調べた）
- [Snapcraft：obsidian](https://snapcraft.io/obsidian)：`snap install obsidian --classic`（検索結果の要約による）
- [Obsidian フォーラム：Snap doesn't start with Ubuntu 26.04](https://forum.obsidian.md/t/obsidian-snap-doesnt-start-open-with-ubuntu-26-04/113569)、[Installation Issues on Ubuntu 26.04](https://forum.obsidian.md/t/installation-issues-on-ubuntu-26-04/115607)：26.04 の Snap の不具合、.deb で直った報告、AppImage の sandbox の問題（検索結果の要約による）
- [Obsidian フォーラム：AppImage not work in Kubuntu 24.04](https://forum.obsidian.md/t/obsidian-appimage-not-work-in-kubuntu-24-04/80969)、[It's FOSS：Can't Run AppImage on Ubuntu](https://itsfoss.com/cant-run-appimage-ubuntu)、[Ubuntu Discourse](https://discourse.ubuntu.com/t/problem-runing-appimage-files-without-no-sandbox/78361)：libfuse2t64、user namespace の制限、`/opt/Obsidian/obsidian` に置くやり方、`--no-sandbox`、`libxss1`（検索結果の要約による）
- `/etc/apparmor.d/obsidian` の中身：このパソコンで見た
- アプリの中での更新とインストーラーの入れなおし、日本語入力、Wayland、ショートカット、`obsidian://`、同期の方法：一般的な知識（ウェブでの確認はしていない）
