# Carbon Design System

**Carbon Design System** は、IBM が開発するオープンソースのデザインシステム。IBM Design Language に基づき、デジタル製品の画面を一貫して設計・実装するための指針と部品を提供する。[Carbon 公式サイト](https://www.carbondesignsystem.com/getting-started/about-carbon)

## 構成

- **デザインの基礎**：色、余白、グリッド、アイコン、タイポグラフィなど。
- **コンポーネント**：ボタン、フォーム、データテーブルなど、再利用可能な UI 部品。
- **デザイントークン**：背景色や文字色などを役割で表し、テーマごとに値を切り替える仕組み。
- **アクセシビリティ**：設計・実装の指針とコンポーネントごとの検証状況。

書体には IBM Plex を使う。[[IBM Plex Sans]] はそのファミリーのサンセリフ体である。[タイポグラフィのガイド](https://www.carbondesignsystem.com/building-blocks/foundations/typography/overview)

## 配色テーマ

Carbon は単一のエディタ配色ではなく、UI 部品や設計指針も含むデザインシステム。標準では背景を基準に、次の4テーマがある。[色のガイド](https://www.carbondesignsystem.com/building-blocks/foundations/color/overview)

| テーマ | 種類 | 基本背景色 |
| --- | --- | --- |
| White | ライト | `#ffffff` |
| Gray 10 | ライト | `#f4f4f4` |
| Gray 90 | ダーク | `#262626` |
| Gray 100 | ダーク | `#161616` |

[[エディタやターミナルの配色テーマ|Tokyo Night や Catppuccin などの配色テーマ]]とは対象が異なるが、Carbon の色に基づくエディタ用テーマもある。たとえば VS Code の [IBM Carbon Design System Theme](https://marketplace.visualstudio.com/items?itemName=achkasov.ibm-carbon-design-system-theme) は第三者による実装で、Carbon 本体とは別の拡張機能である。

## 開発

公式リポジトリには React と Web Components のライブラリ、Sass、トークン、アイコンなどが含まれる。他のフレームワーク向けにはコミュニティによる実装もある。[開発者向け概要](https://www.carbondesignsystem.com/getting-started/developing/overview)

- [Carbon Design System 公式サイト](https://www.carbondesignsystem.com/)
- [Carbon リポジトリ — GitHub](https://github.com/carbon-design-system/carbon)
