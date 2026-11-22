# Plasma 6

**Plasma 6** は、KDE コミュニティが開発するデスクトップ環境 **KDE Plasma** の第6世代。パネル、ウィンドウ管理、システム設定、ウィジェット、[[KRunner]] などを提供する。Linux ディストリビューション上で使われ、OS 全体そのものではない。

## Plasma 5 からの主な変更

- **Qt 6・KDE Frameworks 6** を基盤に移行。2024年2月28日の KDE MegaRelease 6 で、Plasma 6.0 などが公開された。[KDE MegaRelease 6](https://kde.org/announcements/megarelease/6/)
- **Wayland** が既定のセッションになった。ただし実際の既定値はディストリビューションや設定によって異なる。
- パネルを浮かせる表示や、ファイルをダブルクリックで開く動作など、初期設定が変更された。設定で好みに合わせられる。
- Plasma 5 用のウィジェットやテーマは、Plasma 6 向けの対応が必要なものがある。[ウィジェットの移植](https://develop.kde.org/docs/plasma/widget/porting_kf6/)

## Wayland と X11

Plasma 6 の初期には Wayland と X11 の両セッションがあったが、**Plasma 6.8 では Plasma 自体の X11 セッションが廃止された**。X11 用アプリがすべて動かなくなるという意味ではなく、多くは Wayland 上の **XWayland** を通して実行できる。[KDE: Plasma 6.8](https://kde.org/announcements/plasma/6/6.8.0/)

ただし、X11 向けのウィンドウ操作やキー送信、画面共有などはそのまま同じように動くとは限らない。たとえば [[KRunner]] のノートにある `xdotool` の例は X11 向けで、Wayland ネイティブのウィンドウ操作にはそのまま使えない。IME も環境ごとに確認する。

## 移行前に確認すること

1. **バージョンとセッション**：`plasmashell --version` と `printf '%s\n' "$XDG_SESSION_TYPE"` で現在の状態を確認する。
2. **ディストリビューションの対応**：Plasma の更新方法・提供バージョン・サポート期間は OS ごとに異なる。公式のアップグレード手順を確認する。
3. **自作設定と追加ウィジェット**：テーマ、KRunner プラグイン、ショートカット、パネル設定などの Plasma 6 対応を確認する。
4. **X11 依存の操作**：`xdotool` や IME、画面共有、リモート操作など、普段使うものを Wayland で試す。
5. **バックアップと復旧手段**：重要なデータや設定を保存し、更新に失敗した場合の手順を用意する。

この保管庫の [[KRunner]] には Plasma 5.27・X11 と記録されているが、現在の実機の状態を確認したものではない。ここに記した更新や設定変更は行っていない。

## 関連

- [[KRunner]]
- [[アプリ横断のコマンドパレット]]
- [[Unix 盆栽]]
- [[Zed]]
