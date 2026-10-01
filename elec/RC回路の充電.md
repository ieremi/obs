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

<svg viewBox="0 0 360 220" width="360" role="img" aria-label="RC 充電回路: 電源 V0、スイッチ S、抵抗 R、コンデンサ C の直列回路" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <g fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
    <!-- 左: 電源 -->
    <path d="M60 40 V100 M60 112 V180"/>
    <path d="M42 100 H78" stroke-width="3"/>
    <path d="M51 112 H69"/>
    <!-- 上: スイッチ -->
    <path d="M60 40 H100 M140 40 H170"/>
    <path d="M100 40 L136 22"/>
    <!-- 上: 抵抗 -->
    <path d="M170 40 L176 30 L188 50 L200 30 L212 50 L224 30 L236 50 L240 40 H300"/>
    <!-- 右: コンデンサ -->
    <path d="M300 40 V100 M300 112 V180"/>
    <path d="M280 100 H320 M280 112 H320" stroke-width="3"/>
    <!-- 下 -->
    <path d="M300 180 H60"/>
  </g>
  <g fill="currentColor" stroke="none">
    <circle cx="100" cy="40" r="3"/>
    <circle cx="140" cy="40" r="3"/>
    <!-- 電流の向き -->
    <path d="M262 34 L274 40 L262 46 Z"/>
  </g>
  <g fill="currentColor" font-size="16" font-family="serif" font-style="italic" text-anchor="middle">
    <text x="22" y="112">V<tspan font-size="11" dy="4">0</tspan></text>
    <text x="88" y="96" font-style="normal" font-size="14">+</text>
    <text x="120" y="20">S</text>
    <text x="205" y="20">R</text>
    <text x="268" y="26">I</text>
    <text x="340" y="112">C</text>
    <text x="330" y="96" font-style="normal" font-size="14">+</text>
    <text x="330" y="130" font-style="normal" font-size="14">−</text>
    <text x="180" y="205" font-style="normal" font-size="12">t = 0 でスイッチ S を閉じる</text>
  </g>
</svg>

- 電源 $V_0$(長い線が +)、スイッチ $S$、抵抗 $R$、コンデンサ $C$ を直列につなぐ
- $t=0$ で $S$ を閉じると電流 $I$ が流れ、コンデンサの上の極板に + の電荷がたまっていく
- [[キルヒホッフの法則|キルヒホッフの第 2 法則]]から、電源の電圧 = 抵抗の電圧 $RI$ + コンデンサの電圧 $Q/C$。$I=dQ/dt$ なので次の式になる

$$
V_0=R\frac{dQ}{dt}+\frac{Q}{C}
$$

初期条件は、スイッチを閉じた瞬間にコンデンサに電荷がないこと:

$$
Q(0)=0
$$

## 微分方程式の解き方(変数分離)

### 1. $\dfrac{dQ}{dt}$ について解く
両辺から $\dfrac{Q}{C}$ を引いて $R$ で割る。

$$
\frac{dQ}{dt}=\frac{V_0}{R}-\frac{Q}{RC}
$$

右辺を $\dfrac{1}{RC}$ でくくると、

$$
\frac{dQ}{dt}=\frac{CV_0-Q}{RC}
$$

- $CV_0$ は、十分に時間がたって充電が終わったときの電荷(最終値)
- 右辺の分子 $CV_0-Q$ は「**あとどれだけ充電できるか**」(残りの電荷)を表す。残りが多いほど速く充電され、残りが少なくなるほどゆっくりになる

### 2. 変数を分ける
$Q$ を含むものを左辺に、$t$ を含むものを右辺に集める。

$$
\frac{dQ}{CV_0-Q}=\frac{dt}{RC}
$$

### 3. 両辺を積分する
左辺は $u=CV_0-Q$ と置くと $du=-dQ$ なので、

$$
\int\frac{dQ}{CV_0-Q}=-\int\frac{du}{u}=-\ln|u|=-\ln|CV_0-Q|
$$

右辺は $RC$ が定数なので、

$$
\int\frac{dt}{RC}=\frac{t}{RC}
$$

積分定数をまとめて $K$ とすると、

$$
-\ln|CV_0-Q|=\frac{t}{RC}+K
$$

### 4. 対数を外す
両辺に $-1$ をかけて、

$$
\ln|CV_0-Q|=-\frac{t}{RC}-K
$$

両辺を $e$ の指数にすると、

$$
|CV_0-Q|=e^{-K}\,e^{-t/RC}
$$

充電中は $Q<CV_0$ なので $0<CV_0-Q$ で、絶対値はそのまま外せる。$e^{-K}$ は正の定数なので $A$ と置くと、

$$
CV_0-Q=Ae^{-t/RC}
$$

$$
Q(t)=CV_0-Ae^{-t/RC}
$$

### 5. 初期条件で定数を決める
$t=0$ を代入すると $e^0=1$ なので、

$$
Q(0)=CV_0-A=0
\qquad\therefore\quad A=CV_0
$$

よって、

$$
\boxed{Q(t)=CV_0\left(1-e^{-t/RC}\right)}
$$

## 電流と電圧
**コンデンサの電圧**は $V_C=Q/C$ なので、

$$
\boxed{V_C(t)=V_0\left(1-e^{-t/RC}\right)}
$$

**電流**は $I=dQ/dt$ なので、$Q(t)$ を微分する。$\dfrac{d}{dt}e^{-t/RC}=-\dfrac{1}{RC}e^{-t/RC}$ だから、

$$
I(t)=CV_0\cdot\frac{1}{RC}e^{-t/RC}
\qquad\Rightarrow\qquad
\boxed{I(t)=\frac{V_0}{R}e^{-t/RC}}
$$

**抵抗の電圧**は $V_R=RI$ なので、

$$
\boxed{V_R(t)=V_0e^{-t/RC}}
$$

- $V_C$ は 0 から $V_0$ へ増えていき、$I$ と $V_R$ は最大値から 0 へ減っていく
- 電流は[[RC回路の放電|放電]]のときと同じ形で、指数関数的に減る

## 答えを確かめる
### 元の式に代入する
$$
RI+\frac{Q}{C}
=V_0e^{-t/RC}+V_0\left(1-e^{-t/RC}\right)
=V_0
$$

どの時刻でも元の式 $V_0=R\dfrac{dQ}{dt}+\dfrac{Q}{C}$ を満たす。

### 始まりと終わり
| | $t=0$(閉じた直後) | $t\to\infty$(十分に時間がたったあと) |
| --- | --- | --- |
| $Q$ | $0$ | $CV_0$ |
| $V_C$ | $0$ | $V_0$ |
| $I$ | $V_0/R$(最大) | $0$ |
| コンデンサのふるまい | ただの**導線**と同じ(電圧 0) | **断線**と同じ(電流が流れない) |

- 閉じた直後はコンデンサに電荷がなく電圧が 0 なので、電源の電圧がすべて抵抗にかかり、電流は $V_0/R$ になる
- 十分に時間がたつとコンデンサの電圧が $V_0$ になり、抵抗にかかる電圧が 0 になるので、電流が止まる

## 別の解き方
### 定常解 + 同次解
1. 十分に時間がたったあとの「変化しない解」(**定常解**)を探す。$dQ/dt=0$ と置くと $V_0=Q/C$ なので $Q=CV_0$
2. 右辺を 0 にした式 $R\dfrac{dQ}{dt}+\dfrac{Q}{C}=0$(**同次方程式**、放電の式と同じ)の解は $Ae^{-t/RC}$
3. 一般解は 2 つの和: $Q=CV_0+Ae^{-t/RC}$
4. $Q(0)=0$ から $A=-CV_0$。上と同じ答えになる

線形の微分方程式では、「最終的な状態」と「そこへ近づいていく指数関数」の和として考えると見通しがよい。

### 積分因子
両辺を $R$ で割って $\dfrac{dQ}{dt}+\dfrac{1}{RC}Q=\dfrac{V_0}{R}$ とし、両辺に $e^{t/RC}$ をかけると、左辺が積の微分の形になる。

$$
\frac{d}{dt}\left(Qe^{t/RC}\right)=\frac{V_0}{R}e^{t/RC}
$$

両辺を $0$ から $t$ まで積分すると、$Q(0)=0$ なので、

$$
Qe^{t/RC}=\frac{V_0}{R}\cdot RC\left(e^{t/RC}-1\right)=CV_0\left(e^{t/RC}-1\right)
$$

両辺を $e^{t/RC}$ で割ると、同じ $Q(t)=CV_0\left(1-e^{-t/RC}\right)$ が得られる。電源の電圧が時間で変わる場合にも使える方法。

## 時定数
時定数は、

$$
\boxed{\tau=RC}
$$

$t=RC$ で最終値の約63%まで充電される。

$$
V_C(RC)=V_0\left(1-e^{-1}\right)\approx V_0\,(1-0.368)=0.632\,V_0
$$

| 時間 | 充電された割合 $1-e^{-t/RC}$ |
| --- | --- |
| $RC$ | 約 63% |
| $2RC$ | 約 86% |
| $3RC$ | 約 95% |
| $5RC$ | 約 99.3% |

[[RC回路の放電]]で残る割合($e^{-t/RC}$)と足すと、どの時刻でも 100% になる。
