---
aliases:
  - sin の導関数
  - sin x の微分
  - (sin x)' = cos x
  - derivative of sine
date: 2026-10-03
tags:
  - 数学
  - 微分
---

# $(\sin x)'=\cos x$ の証明

$$
\boxed{\frac{d}{dx}\sin x=\cos x}
$$

（角は **ラジアン** で測る。度で測ると $\dfrac{\pi}{180}$ 倍がつく。理由は最後に）

いろいろな証明があり、それぞれ **sin をどう定義するか**（単位円・級数・指数関数）と、**何を前提にするか** が違う。

## 証明 1：加法定理と $\dfrac{\sin h}{h}\to1$
導関数の定義と加法定理 $\sin(x+h)=\sin x\cos h+\cos x\sin h$ から

$$
\frac{\sin(x+h)-\sin x}{h}
=\sin x\cdot\frac{\cos h-1}{h}+\cos x\cdot\frac{\sin h}{h}
$$

したがって、次の 2 つの極限がわかれば、$h\to0$ で $\sin x\cdot0+\cos x\cdot1=\cos x$ になる。

$$
\lim_{h\to0}\frac{\sin h}{h}=1,\qquad \lim_{h\to0}\frac{\cos h-1}{h}=0
$$

**1 つめ（はさみうち）**：単位円で、$0<h<\dfrac{\pi}{2}$ の角について 3 つの図形の面積を比べる。

<svg viewBox="0 0 420 290" width="420" role="img" aria-label="単位円で、角 h の 3 つの図形の面積を比べる図。三角形 OAP（面積 sin h / 2）は、扇形 OAP（面積 h / 2）に含まれ、扇形は三角形 OAT（面積 tan h / 2）に含まれる。だから sin h ≤ h ≤ tan h" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <path d="M60 250 L360.0 47.6 L360 250 Z" fill="currentColor" fill-opacity="0.08" stroke="currentColor" stroke-width="1.2"/>
  <path d="M60 250 L360 250 A300 300 0 0 0 308.7 82.2 Z" fill="currentColor" fill-opacity="0.12" stroke="none"/>
  <path d="M60 250 L360 250 L308.7 82.2 Z" fill="currentColor" fill-opacity="0.2" stroke="currentColor" stroke-width="1.6"/>
  <path d="M360 250 A300 300 0 0 0 112.1 -45.4" fill="none" stroke="currentColor" stroke-width="2"/>
  <path d="M308.7 82.2 V250" stroke="currentColor" stroke-width="1" stroke-dasharray="4 3"/>
  <path d="M105 250 A45 45 0 0 0 97.3 224.8" fill="none" stroke="currentColor" stroke-width="1.4"/>
  <circle cx="60.0" cy="250.0" r="3.5" fill="currentColor"/>
  <circle cx="360.0" cy="250.0" r="3.5" fill="currentColor"/>
  <circle cx="308.7" cy="82.2" r="3.5" fill="currentColor"/>
  <circle cx="360.0" cy="47.6" r="3.5" fill="currentColor"/>
  <text x="50.0" y="268.0" fill="currentColor" font-size="15" text-anchor="middle" font-style="italic" font-family="serif">O</text>
  <text x="368.0" y="268.0" fill="currentColor" font-size="15" text-anchor="middle" font-style="italic" font-family="serif">A</text>
  <text x="300.7" y="72.2" fill="currentColor" font-size="15" text-anchor="middle" font-style="italic" font-family="serif">P</text>
  <text x="374.0" y="47.6" fill="currentColor" font-size="15" text-anchor="middle" font-style="italic" font-family="serif">T</text>
  <text x="120.0" y="240.0" fill="currentColor" font-size="15" text-anchor="middle" font-style="italic" font-family="serif">h</text>
  <text x="292.7" y="166.1" fill="currentColor" font-size="13" text-anchor="end" font-style="italic" font-family="serif">sin h</text>
  <text x="370.0" y="148.8" fill="currentColor" font-size="13" text-anchor="start" font-style="italic" font-family="serif">tan h</text>
  <text x="210.0" y="270.0" fill="currentColor" font-size="14" text-anchor="middle" font-style="italic" font-family="serif">1</text>
</svg>

$$
\underbrace{\frac{1}{2}\sin h}_{\triangle OAP}\ \le\ \underbrace{\frac{1}{2}h}_{\text{扇形 }OAP}\ \le\ \underbrace{\frac{1}{2}\tan h}_{\triangle OAT}
$$

（扇形の面積は、半径 1・中心角 $h$ ラジアンで $\frac{1}{2}h$）。$\sin h>0$ で割って逆数をとると

$$
\cos h\ \le\ \frac{\sin h}{h}\ \le\ 1
$$

$h\to+0$ で $\cos h\to1$ なので、はさまれた $\dfrac{\sin h}{h}\to1$。$\dfrac{\sin h}{h}$ は偶関数なので $h\to-0$ でも同じ。

**2 つめ**：分子と分母に $\cos h+1$ を掛けて $1-\cos^2h=\sin^2h$ を使う。

$$
\frac{\cos h-1}{h}=\frac{\cos^2h-1}{h(\cos h+1)}=-\frac{\sin h}{h}\cdot\frac{\sin h}{\cos h+1}\ \to\ -1\cdot\frac{0}{2}=0
$$

## 証明 2：和積の公式
$\sin A-\sin B=2\cos\dfrac{A+B}{2}\sin\dfrac{A-B}{2}$ を使う（$A=x+h$、$B=x$）。

$$
\frac{\sin(x+h)-\sin x}{h}
=\frac{2\cos\!\left(x+\frac{h}{2}\right)\sin\frac{h}{2}}{h}
=\cos\!\left(x+\frac{h}{2}\right)\cdot\frac{\sin(h/2)}{h/2}
\ \to\ \cos x\cdot1
$$

$\dfrac{\cos h-1}{h}$ の極限がいらず、**$\dfrac{\sin h}{h}\to1$ と $\cos$ の連続性だけ** で済む。いちばん短い証明。

## 証明 3：単位円の上の小さな三角形（図形的）

<svg viewBox="0 0 430 290" width="430" role="img" aria-label="単位円の上の点が角 θ から θ + Δθ まで動くときの図。動いた弧の長さは Δθ。弧はほぼまっすぐで半径 OP と直角なので、小さな直角三角形ができる。その斜辺 Δθ と縦の辺のなす角は θ に等しく、縦の変化は cos θ・Δθ、横の変化は −sin θ・Δθ になる" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <path d="M70 260 H350 M70 260 V-15" stroke="currentColor" stroke-width="1" stroke-opacity="0.6"/>
  <path d="M330 260 A260 260 0 0 0 70 0" fill="none" stroke="currentColor" stroke-width="1.2" stroke-opacity="0.5"/>
  <path d="M70 260 L274.9 99.9 M70 260 L222.8 49.7" stroke="currentColor" stroke-width="1.4"/>
  <path d="M274.9 99.9 A260 260 0 0 0 222.8 49.7" fill="none" stroke="currentColor" stroke-width="3"/>
  <path d="M274.9 99.9 L274.9 49.7 L222.8 49.7" fill="none" stroke="currentColor" stroke-width="1.4" stroke-dasharray="4 3"/>
  <path d="M274.9 99.9 V260" stroke="currentColor" stroke-width="0.8" stroke-dasharray="2 3" stroke-opacity="0.6"/>
  <path d="M110 260 A40 40 0 0 0 101.5 235.4" fill="none" stroke="currentColor" stroke-width="1.4"/>
  <circle cx="70.0" cy="260.0" r="3.5" fill="currentColor"/>
  <circle cx="274.9" cy="99.9" r="3.5" fill="currentColor"/>
  <circle cx="222.8" cy="49.7" r="3.5" fill="currentColor"/>
  <text x="60.0" y="278.0" fill="currentColor" font-size="15" text-anchor="middle" font-style="italic" font-family="serif">O</text>
  <text x="286.9" y="105.9" fill="currentColor" font-size="15" text-anchor="start" font-style="italic" font-family="serif">P</text>
  <text x="216.8" y="39.7" fill="currentColor" font-size="15" text-anchor="end" font-style="italic" font-family="serif">P′</text>
  <text x="122.0" y="250.0" fill="currentColor" font-size="15" text-anchor="start" font-style="italic" font-family="serif">θ</text>
  <text x="284.9" y="78.8" fill="currentColor" font-size="12" text-anchor="start" font-style="italic" font-family="serif">Δ(sin θ) ≈ cos θ·Δθ</text>
  <text x="248.9" y="39.7" fill="currentColor" font-size="12" text-anchor="middle" font-style="italic" font-family="serif">−Δ(cos θ)</text>
  <text x="224.9" y="86.8" fill="currentColor" font-size="13" text-anchor="end" font-style="italic" font-family="serif">Δθ</text>
  <text x="194.7" y="188.0" fill="currentColor" font-size="14" text-anchor="start" font-style="italic" font-family="serif">1</text>
</svg>

単位円の上の点 $P=(\cos\theta,\sin\theta)$ が、角が $\Delta\theta$ だけ増えて $P'$ まで動く。

- 動いた弧の長さは、半径 1 なので $\Delta\theta$（ラジアンの定義）。$\Delta\theta$ が小さければ、弧はほぼまっすぐな線分
- この線分は半径 $OP$ と直角（円の接線は半径と直角）
- 半径 $OP$ は $x$ 軸と角 $\theta$ をなすので、それと直角な小さな線分は、**縦の線と角 $\theta$ をなす**
- よって小さな直角三角形の縦の辺（$\sin$ の増え方）と横の辺（$\cos$ の減り方）は

$$
\Delta(\sin\theta)\approx\cos\theta\cdot\Delta\theta,\qquad \Delta(\cos\theta)\approx-\sin\theta\cdot\Delta\theta
$$

$\Delta\theta$ で割って $\Delta\theta\to0$ とすれば $(\sin\theta)'=\cos\theta$、ついでに $(\cos\theta)'=-\sin\theta$ も出る。「≈」をきちんとするには証明 1 の極限が要るが、**なぜ cos になるのか** がいちばんよく見える証明。

## 証明 4：等速円運動の速度（ベクトル）
$\boldsymbol{r}(t)=(\cos t,\sin t)$ は、単位円の上を **速さ 1** で回る点（$t$ ラジアン進むと弧の長さも $t$）。

- $|\boldsymbol{r}|^2=\boldsymbol{r}\cdot\boldsymbol{r}=1$ を $t$ で微分すると $2\,\boldsymbol{r}\cdot\boldsymbol{r}'=0$。**速度は位置と直角**
- 弧の長さで進むので、**速度の大きさは 1**
- 位置 $(\cos t,\sin t)$ と直角で長さ 1 のベクトルは $\pm(-\sin t,\cos t)$ の 2 つ。角が増える向き（反時計回り）に進むので $+$ のほう

$$
\boldsymbol{r}'(t)=(-\sin t,\ \cos t)
\quad\Rightarrow\quad
(\cos t)'=-\sin t,\quad (\sin t)'=\cos t
$$

証明 3 を、極限を使わずにベクトルの言葉で言いかえたもの（ただし「速さ 1」の部分で、弧長の微分を前提にしている）。

## 証明 5：べき級数
$\sin x$ と $\cos x$ を、べき級数で定義する（すべての $x$ で収束する）。

$$
\sin x=x-\frac{x^3}{3!}+\frac{x^5}{5!}-\frac{x^7}{7!}+\cdots,\qquad
\cos x=1-\frac{x^2}{2!}+\frac{x^4}{4!}-\frac{x^6}{6!}+\cdots
$$

べき級数は収束する範囲で **項ごとに微分してよい**。$\dfrac{d}{dx}\dfrac{x^{n}}{n!}=\dfrac{x^{n-1}}{(n-1)!}$ なので

$$
(\sin x)'=1-\frac{3x^2}{3!}+\frac{5x^4}{5!}-\cdots=1-\frac{x^2}{2!}+\frac{x^4}{4!}-\cdots=\cos x
$$

図形を使わず、**定義からほぼ計算だけ** で出る。解析学の教科書ではこちらを sin の定義にすることが多い（その場合、$\sin$ が周期 $2\pi$ をもつことや単位円との関係のほうを後で証明する）。

## 証明 6：オイラーの公式
指数関数を $e^z=\displaystyle\sum_{n=0}^{\infty}\frac{z^n}{n!}$ で定義すると、$(e^{iz})'=ie^{iz}$ で、**オイラーの公式**

$$
e^{ix}=\cos x+i\sin x
$$

が成り立つ（レオンハルト・オイラー〈Leonhard Euler、スイス〉）。両辺を $x$ で微分する。

$$
\begin{aligned}
\text{左辺}&=i\,e^{ix}=i(\cos x+i\sin x)=-\sin x+i\cos x\\
\text{右辺}&=(\cos x)'+i(\sin x)'
\end{aligned}
$$

実部と虚部を比べると $(\cos x)'=-\sin x$、$(\sin x)'=\cos x$。**微分すると $i$ が掛かる ＝ 複素平面で 90° 回る** ことが、証明 3・4 の「速度は位置と直角」に対応している。

## なぜラジアンでないといけないのか
- 証明 1 の扇形の面積 $\frac{1}{2}h$、証明 3・4 の「弧の長さ ＝ 角」は、どちらも **ラジアンの定義（弧の長さ ÷ 半径）** そのもの
- 角を度で測る関数 $\mathrm{sind}(x)=\sin\dfrac{\pi x}{180}$ を微分すると、合成関数の微分で

$$
\frac{d}{dx}\sin\frac{\pi x}{180}=\frac{\pi}{180}\cos\frac{\pi x}{180}
$$

  と、余計な係数 $\dfrac{\pi}{180}$ がつく。この係数が 1 になるように角の測り方を選んだのがラジアン

## 注意：循環論法にならないか
- 証明 1 の面積の比べ方は、「扇形の面積が $\frac{1}{2}h$」という事実を使っている。扇形の面積や弧の長さを厳密に定義するには積分が要り、その積分の計算に $\sin$ の微分を使うと循環になる。高校の教科書の証明は、面積を直観的に認めたうえでのもの
- 厳密には、証明 5・6 のように級数で $\sin$・$\cos$ を **定義** してから、その性質（周期、単位円、加法定理）を導く。あるいは、弧の長さを積分 $\displaystyle\int\frac{dt}{\sqrt{1-t^2}}$ で定義して $\arcsin$ を作り、その逆関数として $\sin$ を定義する方法もある
- どの道をとっても、たどり着く $\sin$ は同じ関数になる

## 術語まとめ

| 術語 | 英語 |
| --- | --- |
| 導関数 | derivative |
| 加法定理 | angle addition formula |
| 和積の公式 | sum-to-product formula |
| はさみうちの原理 | squeeze theorem |
| ラジアン（弧度法） | radian |
| 扇形 | sector |
| べき級数 | power series |
| 項別微分 | term-by-term differentiation |
| オイラーの公式 | Euler's formula |
| 循環論法 | circular reasoning |
