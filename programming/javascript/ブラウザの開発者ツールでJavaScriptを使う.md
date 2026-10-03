---
aliases:
  - DevTools の Console
  - 開発者ツールのコンソール
  - ブラウザのコンソール
  - Chrome DevTools
date: 2026-10-03
tags:
  - プログラミング
  - プログラミング/JavaScript
---

# ブラウザの開発者ツールで JavaScript を使う

開いているページの上で、JavaScript をその場で実行できる。

```js
document.title
```

出力：

```text
'Example Domain'
```

コンソールで書いたコードは、**そのページのスクリプトと同じ環境**（同じ `window`、同じ DOM）で動く。ページの変数を読んだり、要素を書き換えたりできる。ただし変更はそのタブの中だけで、再読み込みすれば消える。

## 開きかた

| 操作 | Chrome・Edge | Firefox |
| --- | --- | --- |
| 開発者ツールを開く | F12、Ctrl+Shift+I（Mac：Cmd+Option+I） | F12、Ctrl+Shift+I |
| コンソールを直接開く | Ctrl+Shift+J（Mac：Cmd+Option+J） | Ctrl+Shift+K（Mac：Cmd+Option+K） |
| 要素を選んで調べる | 右クリック →「検証」 | 右クリック →「調査」 |

- 改行して複数行を書くときは **Shift+Enter**。Enter だけだと実行される
- 上下の矢印キーで、前に実行したコードを呼び出せる
- Chrome では、はじめてコードを貼り付けようとすると止められ、`allow pasting` と入力すると貼り付けられるようになる。**意味のわからないコードは貼り付けない**（下の「注意」）

## 式を書くと値が表示される

```js
1 + 2              // 3
[3, 1, 2].sort()   // [1, 2, 3]
location.href      // 今のページの URL
```

- 最後の式の値が表示される。`console.log` を書かなくてよい
- 入力中から結果が薄く表示される（Chrome の **eager evaluation**。副作用のある式は先に評価しない）
- `const` や `let` で宣言した変数は、次の入力でも使える

```js
const links = document.querySelectorAll('a')
links.length       // 12
```

## コンソールだけで使える便利な関数

ページのスクリプトからは使えない、コンソール専用の関数（Console Utilities）。

| 書き方 | 意味 |
| --- | --- |
| `$_` | 直前の式の値 |
| `$0` | 「要素」パネルで選んでいる要素（`$1`〜`$4` は、その前に選んだ要素） |
| `$('セレクタ')` | `document.querySelector` と同じ（最初の 1 つ） |
| `$$('セレクタ')` | `document.querySelectorAll` と同じ。ただし **配列** で返る |
| `$x('XPath')` | XPath で要素を探す |
| `copy(値)` | 値をクリップボードにコピー（オブジェクトは JSON に） |
| `inspect(要素)` | その要素を「要素」パネルで表示 |
| `keys(obj)`・`values(obj)` | オブジェクトのキー・値の一覧 |
| `monitorEvents(要素, 'click')` | その要素のイベントが起きるたびに表示 |
| `getEventListeners(要素)` | その要素に登録されたイベントリスナー（Chrome） |
| `clear()` | コンソールを消す |

例：ページのリンクの URL を全部コピーする。

```js
copy($$('a').map(a => a.href).join('\n'))
```

`$$` は配列を返すので、そのまま `map` が使える（`querySelectorAll` の結果は `NodeList` で、`map` がない）。

例：要素パネルで選んだ要素を書き換える。

```js
$0.textContent = '書き換えた'
$0.style.outline = '2px solid red'
```

## console の表示を使い分ける

```js
console.log('ふつう', { a: 1 })
console.warn('警告')                  // 黄色
console.error('エラー')               // 赤。呼び出し元も表示
console.table([{ x: 1, y: 2 }, { x: 3, y: 4 }])   // 表にする
console.dir($0)                       // 要素を HTML ではなくオブジェクトとして見る
console.time('t'); /* 処理 */ console.timeEnd('t') // かかった時間
```

- 表示されたオブジェクトを右クリック →「**グローバル変数として保存**」で、`temp1` という名前で使えるようになる
- ページを移動するとログは消える。残すには設定の「**ログを保持**」（Preserve log）をオンにする

## await がそのまま使える

コンソールでは、関数の外でも `await` が書ける。

```js
const res = await fetch('/api/items')
const data = await res.json()
console.table(data)
```

`fetch` はそのページと同じオリジンとして送られ、ログインの cookie もつく。API の動きを確かめるのに便利。

## 長いコードはスニペットに

コンソールに毎回貼るのが面倒なコードは、**スニペット** として保存できる（Chrome：「ソース」パネル →「スニペット」）。

- Ctrl+Enter（Mac：Cmd+Enter）で、開いているページの上で実行される
- 保存したスニペットは、どのページでも使える

Firefox では、コンソールの **複数行エディタ**（Ctrl+B）で長いコードを書ける。

## コードを止めて調べる

```js
function total(items) {
  debugger          // 開発者ツールが開いていれば、ここで止まる
  return items.reduce((s, x) => s + x.price, 0)
}
```

- 止まっている間、コンソールではその関数の中の変数（`items` など）が使える
- 「ソース」パネルで行番号をクリックしても止められる（ブレークポイント）。右クリックで
  - **条件付きブレークポイント**：条件が真のときだけ止める
  - **ログポイント**：止めずに値をコンソールに出す。コードに `console.log` を書き足さなくてよい
- 何度も見たい式は、コンソール上部の目のアイコン（**ライブ式**）に登録すると、値が自動で更新され続ける

## どのページの中で動くか

- ページに `<iframe>` があると、コンソールはどのフレームの中で実行するかを選べる（コンソール上部の「top」と書かれたメニュー）。iframe の中の要素が `$()` で見つからないときは、ここを切り替える
- ブラウザの拡張機能のコードも、このメニューで選べる

## 注意
- 「このコードをコンソールに貼ると〇〇できる」という指示は、**ほぼ詐欺**。コンソールのコードはログイン中のページと同じ権限で動くので、cookie や個人情報を送られたり、勝手に操作されたりする（**Self-XSS**）。Chrome の貼り付け防止や、Facebook などのコンソールに出る警告はこのため
- コンソールでの変更は保存されない。直したい内容は、元のソースに反映する

$$
\boxed{\text{コンソール}=\text{ページと同じ環境で動く、その場かぎりの JavaScript 実行環境}}
$$
