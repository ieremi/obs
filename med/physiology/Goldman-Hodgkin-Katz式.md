---
aliases:
  - Goldman-Hodgkin-Katz 式
  - GHK 式
  - ゴールドマンの式
  - Goldman equation
date: 2026-09-28
tags:
  - physiology
  - physiology/electrophysiology
related:
  - "[[Nernst式]]"
  - "[[リドカイン]]"
---

# Goldman-Hodgkin-Katz 式

実際の膜は複数のイオンを通すため、膜電位は各イオンの濃度差を透過性で重みづけして決まる。

一価イオンを単純化すると、

$$
\boxed{
V_m=\frac{RT}{F}\ln
\frac{P_K[K]_o+P_{Na}[Na]_o+P_{Cl}[Cl]_i}
{P_K[K]_i+P_{Na}[Na]_i+P_{Cl}[Cl]_o}
}
$$

静止時は $P_K\gg P_{Na}$ なので膜電位は $E_K$ に近い。活動電位では $P_{Na}$ が急増し、膜電位は $E_{Na}$ 方向へ動く。
