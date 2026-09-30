---
aliases:
  - ソフトマックス関数
  - softmax
date: 2026-09-29
tags:
  - 情報理論
  - 機械学習
related:
  - "[[交差エントロピー]]"
---

# Softmax

任意の実数 $z_i$ を確率分布へ変換する。

$$
\boxed{p_i=\frac{e^{z_i}}{\sum_j e^{z_j}}}
$$

各 $p_i>0$ かつ $\sum_i p_i=1$。

正解クラスを $k$ とすると cross entropy loss は、

$$
L=-\log p_k
$$
