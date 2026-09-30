---
aliases:
  - RC 回路の充電
date: 2026-09-28
tags:
  - 電気
  - 回路
  - RC回路
related:
  - "[[RC回路の放電]]"
  - "[[細胞膜の時定数]]"
---

# RC 回路の充電

抵抗 $R$ とコンデンサ $C$ の直列回路に電圧 $V_0$ を加える。

$$
V_0=R\frac{dQ}{dt}+\frac{Q}{C}
$$

これを解くと、

$$
\boxed{Q(t)=CV_0(1-e^{-t/RC})}
$$

$$
\boxed{V_C(t)=V_0(1-e^{-t/RC})}
$$

時定数は、

$$
\boxed{\tau=RC}
$$

$t=RC$ で最終値の約63%まで充電される。
