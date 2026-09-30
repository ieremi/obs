---
aliases:
  - 発散
  - divergence
date: 2026-09-30
tags:
  - 数学
  - ベクトル解析
related:
  - "[[grad]]"
  - "[[rot]]"
---

# div

div（発散）は、**ある点のまわりで、流れがどれだけ湧き出しているか、または吸い込まれているか**を表す数値。

水の流れの中に小さな箱を置くイメージで考える。箱から出る流れが入る流れより多ければ正、少なければ負、釣り合っていればゼロになる。正確には、差し引きの流出量を箱の体積で割り、箱を限りなく小さくした値。

**定義**

流速のように、各点に向きと大きさを持つものを **ベクトル場** と呼ぶ。3次元のベクトル場 $\mathbf{F}=(F_x,F_y,F_z)$ に対して、直交座標では、

$$
\boxed{\operatorname{div}\mathbf{F}=\nabla\cdot\mathbf{F}
=\frac{\partial F_x}{\partial x}
+\frac{\partial F_y}{\partial y}
+\frac{\partial F_z}{\partial z}}
$$

たとえば $\partial F_x/\partial x>0$ なら、$x$ 方向について、箱の右面から出る流れが左面から入る流れより多い。それを3方向について足し合わせる。

- $\operatorname{div}\mathbf{F}>0$：局所的な湧き出し。
- $\operatorname{div}\mathbf{F}<0$：局所的な吸い込み。
- $\operatorname{div}\mathbf{F}=0$：流入と流出が釣り合う。流れ自体がないという意味ではない。

**計算例**

原点から外向きに広がる場 $\mathbf{F}=(x,y,z)$ では、

$$
\operatorname{div}\mathbf{F}=1+1+1=3
$$

どの点でも正で、局所的な湧き出しがある。逆向きの $\mathbf{F}=(-x,-y,-z)$ なら $-3$ になる。

一方、一定の流れ $\mathbf{F}=(1,0,0)$ では、どの成分も位置によって変わらないため div はゼロ。水は流れていても、小さな箱への流入量と流出量は等しい。

**電気とのつながり**

真空中の電場について、ガウスの法則は、

$$
\nabla\cdot\mathbf{E}=\frac{\rho}{\varepsilon_0}
$$

と書ける。$\rho$ は電荷密度、$\varepsilon_0$ は真空の誘電率。正の電荷が電場の湧き出し、負の電荷が吸い込みに対応する。

[[grad]] はスカラー場の「増える方向」、[[rot]] はベクトル場の「回転」を調べる。div がゼロでも rot はゼロとは限らない。たとえば $\mathbf{F}=(-y,x,0)$ は div がゼロでも回転している。

**練習問題**

1. $\mathbf{F}=(2x,-3y,4z)$ の div を求め、湧き出しか吸い込みかを答えよ。
2. $\mathbf{F}=(x^2,xy,-2z)$ の div を求めよ。また、点 $(1,2,0)$ と原点での値と意味を答えよ。
3. $\mathbf{F}=(y,0,0)$ の div を求めよ。div がゼロなら、流れもゼロと言えるか。
4. 【応用】$f=x^2+y^2+z^2$ に対して、まず $\operatorname{grad}f$ を求め、次に $\operatorname{div}(\operatorname{grad}f)$ を求めよ。

**こたえと解説**

**問1：$3$。湧き出し。**

$$
\operatorname{div}\mathbf{F}=2-3+4=3
$$

$y$ 方向には吸い込みの寄与があるが、3方向を足すと正になる。

**問2：$3x-2$。点 $(1,2,0)$ では $1$、原点では $-2$。**

$$
\operatorname{div}\mathbf{F}
=\frac{\partial x^2}{\partial x}
+\frac{\partial(xy)}{\partial y}
+\frac{\partial(-2z)}{\partial z}
=2x+x-2=3x-2
$$

$xy$ を $y$ で微分するとき、$x$ は定数として扱う。点 $(1,2,0)$ では湧き出し、原点では吸い込みになる。**先に微分し、後から座標を代入する。** 原点で $\mathbf{F}=\mathbf{0}$ でも、その周囲の変化を表す div はゼロとは限らない。

**問3：div は $0$。流れがゼロとは言えない。**

$$
\operatorname{div}\mathbf{F}
=\frac{\partial y}{\partial x}+0+0=0
$$

第1成分 $y$ は、$x$ に関して微分するのでゼロ。たとえば点 $(0,1,0)$ では $\mathbf{F}=(1,0,0)$ であり、流れはある。

**問4：$\operatorname{grad}f=(2x,2y,2z)$、その div は $6$。**

$$
\operatorname{div}(\operatorname{grad}f)=2+2+2=6
$$

このように grad の後に div をとる演算を **ラプラシアン** といい、$\nabla^2f$ や $\Delta f$ と書く。結果はスカラーになる。


**発展問題：局所の変化から、全体の流れを考える**

**問5：外向きの場なのに、発散がゼロ？**

3次元で、原点以外に定義された場

$$
\mathbf{F}(\mathbf{r})=\frac{\mathbf{r}}{r^3},\qquad
\mathbf{r}=(x,y,z),\quad r=\sqrt{x^2+y^2+z^2}
$$

を考える。大きさは $1/r^2$ で、常に外向きである。

1. $r>0$ で $\nabla\cdot\mathbf{F}=0$ を示せ。
2. 原点を中心とする半径 $R$ の球面を通る外向きの流束 $\iint \mathbf{F}\cdot\mathbf{n}\,dS$ を求めよ。$\mathbf{n}$ は外向き単位法線とする。
3. 発散定理「境界から出る流束＝内部の発散の体積積分」と矛盾しない理由を説明せよ。

**問6：流れが収束したら、密度はどうなる？**

質量密度 $\rho$、流速 $\mathbf{v}$ は、質量の生成・消滅がなければ連続の式

$$
\frac{\partial\rho}{\partial t}+\nabla\cdot(\rho\mathbf{v})=0
$$

を満たす。積の微分を用い、流体とともに動いて測る密度変化が

$$
\frac{D\rho}{Dt}=-\rho\nabla\cdot\mathbf{v},\qquad
\frac{D}{Dt}=\frac{\partial}{\partial t}+\mathbf{v}\cdot\nabla
$$

となることを示せ。さらに $\mathbf{v}=-a(x,y,z)$（$a>0$ は定数）のとき、流体粒子が持つ初期密度 $\rho_0$ は時間とともにどう変わるか。

**発展問題のこたえと解説**

**問5：原点以外の div はゼロだが、球面の流束は $4\pi$。**

各成分について、

$$
\frac{\partial}{\partial x}\left(\frac{x}{r^3}\right)
=\frac{1}{r^3}-\frac{3x^2}{r^5}
$$

なので、3方向を足すと、

$$
\nabla\cdot\mathbf{F}
=\frac{3}{r^3}-\frac{3(x^2+y^2+z^2)}{r^5}=0
\quad(r>0)
$$

球面では $\mathbf{F}\cdot\mathbf{n}=1/R^2$ が一定だから、

$$
\iint_{r=R}\mathbf{F}\cdot\mathbf{n}\,dS
=\frac{1}{R^2}\,4\pi R^2=4\pi
$$

**原点では場が定義されず、球の内部全体で滑らかという発散定理の条件を満たさない。** 原点を小さな球でくり抜いた領域なら定理を使える。その領域の内側境界の外向き法線は原点に向くため、内側の流束は $-4\pi$。外側との合計は $0$ となり、発散の体積積分と一致する。

外向きに流れていても、球面積が $r^2$ に比例して増える分だけ流れの強さが $1/r^2$ に減れば、途中で新たに湧き出す必要はない。点電荷の電場と同じ構造であり、湧き出しは原点に集中している。

**問6：流体粒子の密度は $\rho(t)=\rho_0e^{3at}$。**

積の微分から、

$$
\nabla\cdot(\rho\mathbf{v})
=\mathbf{v}\cdot\nabla\rho+\rho\nabla\cdot\mathbf{v}
$$

これを連続の式へ代入すれば、指定された式が得られる。今回の速度場では $\nabla\cdot\mathbf{v}=-3a$ なので、粒子に沿って

$$
\frac{d\rho}{dt}=3a\rho
\quad\Longrightarrow\quad
\rho(t)=\rho_0e^{3at}
$$

となる。粒子の位置は $\mathbf{r}(t)=e^{-at}\mathbf{r}(0)$ となり、流体の小さな塊の体積は $e^{-3at}$ 倍になる。その分だけ密度が増え、質量は保存される。

つまり、**流速の負の div は、質量が消えることではなく、流体の圧縮を表しうる。** 質量保存が直接制約するのは、流速 $\mathbf{v}$ だけでなく質量流束 $\rho\mathbf{v}$ と密度の時間変化である。
