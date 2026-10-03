---
aliases:
  - CSS の ::after
  - CSS の :after
  - "::after"
  - after 擬似要素
date: 2026-10-03
tags:
  - プログラミング
  - プログラミング/CSS
---

# CSS の ::after

```html
<p class="note">保存しました</p>
```

```css
.note::after {
  content: " ✓";
  color: green;
}
```

表示：

```text
保存しました ✓
```

`::after` は、要素の **中身の最後** に、HTML には書いていない子要素を 1 つ CSS だけで足す。足されるのは `<p>` の **後ろ** ではなく、`<p>` の **中の末尾**。

$$
\boxed{\texttt{<p>}\ \text{中身}\ \underbrace{\text{::after}}_{\text{ここに入る}}\ \texttt{</p>}}
$$

`::before` は同じものを中身の先頭に足す。

## 決まりごと

- **`content` がないと何も出ない**。文字を出さないときも `content: ""` が要る
- 既定では **インライン要素**。幅・高さを指定するなら `display: block` や `inline-block` にする
- `<img>`、`<input>`、`<br>` など、**中身をもたない要素（置換要素・空要素）にはふつう使えない**
- 1 つの要素につき `::before` と `::after` は 1 つずつ
- `:after`（コロン 1 つ）は CSS2 の古い書き方。いまのブラウザではどちらも動くが、擬似クラス（`:hover` など）と区別するため `::after` と書く

## content に書けるもの

```css
.a::after { content: "→"; }                 /* 文字列 */
.b::after { content: "\2192"; }             /* Unicode のコード（→）*/
.c::after { content: attr(data-unit); }     /* 要素の属性の値 */
.d::after { content: url(icon.svg); }       /* 画像 */
.e::after { content: counter(item) "."; }   /* カウンター */
.f::after { content: ""; }                  /* 空：形だけ描く */
```

`attr()` の例：

```html
<span class="price" data-unit="円">1200</span>
```

```css
.price::after { content: attr(data-unit); }
```

表示：`1200円`

## よく使う例

### 必須項目の印

```css
label.required::after {
  content: " *";
  color: red;
}
```

### 外部リンクの印

```css
a[href^="http"]::after {
  content: " ↗";
}
```

### 形だけ描く（下線のアニメーション）

```css
.link {
  position: relative;      /* ::after の位置の基準にする */
}
.link::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: -2px;
  width: 100%;
  height: 2px;
  background: currentColor;
  transform: scaleX(0);
  transition: transform 0.2s;
}
.link:hover::after {
  transform: scaleX(1);
}
```

`position: absolute` の `::after` は、いちばん近い `position` が `static` 以外の祖先を基準に置かれる。親に `position: relative` をつけるのが定番。

### float の回り込みを止める（clearfix）

```css
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
```

いまは `display: flow-root` やフレックスボックス・グリッドで足りることが多い。

## 注意

- **文字は選択・コピーできない**。本文として必要な情報は HTML に書く
- スクリーンリーダーは `content` の文字を **読み上げることが多い**。飾りの記号なら、代替テキストを空にできる：`content: "★" / "";`
- JavaScript から `::after` 自体は DOM の要素として取れない。クリックは親要素のイベントとして届く。値を読むだけなら `getComputedStyle(el, "::after").content`
- 状態を組み合わせるときは、擬似クラスが先、擬似要素が最後：`a:hover::after`（`a::after:hover` は誤り）

$$
\boxed{\texttt{::after}=\text{要素の中の末尾に足す、CSS だけの子要素}\quad(\texttt{content}\ \text{必須})}
$$
