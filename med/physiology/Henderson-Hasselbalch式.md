---
aliases:
  - Henderson–Hasselbalch式
  - ヘンダーソン・ハッセルバルヒの式
  - Henderson-Hasselbalch equation
date: 2026-10-01
tags:
  - physiology
  - physiology/acid-base
related:
  - "[[肺胞換気とPaCO2]]"
  - "[[アセタゾラミド]]"
  - "[[代謝性アシドーシス]]"
---

# Henderson-Hasselbalch 式

## 導出

弱酸を

$$
HA \rightleftharpoons H^+ + A^-
$$

とする。酸解離定数の定義は、

$$
K_a=\frac{[H^+][A^-]}{[HA]}
$$

$[H^+]$ について解くと、

$$
[H^+]=K_a\frac{[HA]}{[A^-]}
$$

両辺の常用対数を取る。

$$
\log[H^+]=\log K_a+\log\frac{[HA]}{[A^-]}
$$

$pH=-\log[H^+]$、$pK_a=-\log K_a$ なので、両辺に $-1$ を掛けると、

$$
pH=pK_a-\log\frac{[HA]}{[A^-]}
$$

分数を逆にすれば、

$$
\boxed{pH=pK_a+\log\frac{[A^-]}{[HA]}}
$$

## 重炭酸緩衝系

$$
CO_2+H_2O \rightleftharpoons H_2CO_3 \rightleftharpoons H^++HCO_3^-
$$

溶存 CO₂ 濃度はおおよそ $0.03\times P_{CO_2}$ なので、

$$
\boxed{pH=6.1+\log\frac{[HCO_3^-]}{0.03P_{CO_2}}}
$$

$$
\boxed{pH\sim\frac{\text{腎臓が調節する }HCO_3^-}{\text{肺が調節する }CO_2}}
$$

酸塩基平衡は、**腎臓と肺の共同作業**として式から理解できる。

$$
K_a\rightarrow \text{Henderson-Hasselbalch}\rightarrow HCO_3^-\rightarrow \text{アセタゾラミド}\rightarrow \text{代謝性アシドーシス}
$$
