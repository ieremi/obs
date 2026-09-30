---
aliases:
  - KL ダイバージェンス
  - Kullback-Leibler divergence
  - 相対エントロピー
date: 2026-09-26
tags:
  - 情報理論
related:
  - "[[交差エントロピー]]"
  - "[[通信路容量]]"
---

# KLダイバージェンス

2つの確率分布 $P,Q$ の差を、

$$
\boxed{D_{\mathrm{KL}}(P\|Q)=\sum_xP(x)\log_2\frac{P(x)}{Q(x)}}
$$

で表す。

相互情報量は、

$$
I(X;Y)=D_{\mathrm{KL}}(P_{XY}\|P_XP_Y)
$$

と書ける。つまり、実際の同時分布が「独立だった場合の分布」からどれほど離れているかを測っている。
