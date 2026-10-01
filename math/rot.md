---
aliases:
  - 回転
  - curl
  - rotation
date: 2026-09-30
tags:
  - 数学
  - ベクトル解析
related:
  - "[[grad]]"
  - "[[div]]"
---

# rot

rot（回転、curl ともいう）は、**ベクトル場が、その点の近くでどの向きに、どれだけ回転する傾向を持つか**を表すベクトル。

水の流れに小さな羽根車を置くイメージで考える。羽根車がその場で回ろうとするかを見る。流れに乗って移動することと、羽根車自身が回転することは別。

rot の向きは回転軸の向きで、右手の指を回転方向へ曲げたときの親指の方向。大きさは局所的な回転の強さを表す。流速場では、局所的な回転の角速度の2倍に対応する。

**定義**

3次元のベクトル場 $\mathbf{F}=(F_x,F_y,F_z)$ に対して、右手系の直交座標では、

$$
\boxed{\operatorname{rot}\mathbf{F}=\nabla\times\mathbf{F}
=\left(
\frac{\partial F_z}{\partial y}-\frac{\partial F_y}{\partial z},\;
\frac{\partial F_x}{\partial z}-\frac{\partial F_z}{\partial x},\;
\frac{\partial F_y}{\partial x}-\frac{\partial F_x}{\partial y}
\right)}
$$

たとえば $z$ 成分は、$xy$ 平面内での回転を調べる。小さな閉曲線に沿って流れを一周分足し合わせた「循環」を、その面積で割り、面積を限りなく小さくした値に対応する。

**計算例**

$z$ 軸のまわりを回る場 $\mathbf{F}=(-y,x,0)$ を考える。点 $(1,0,0)$ では $+y$ 方向、点 $(0,1,0)$ では $-x$ 方向へ流れるので、$+z$ 側から原点を見ると反時計回りになる。

$$
\operatorname{rot}\mathbf{F}
=\left(0,0,\frac{\partial x}{\partial x}-\frac{\partial(-y)}{\partial y}\right)
=(0,0,2)
$$

回転軸は $+z$ 方向。この場の [[div]] はゼロなので、湧き出し・吸い込みがなくても回転はありうる。

一方、一定の流れ $\mathbf{F}=(1,0,0)$ は rot がゼロ。羽根車は流されるが、流れの場所による違いがないため、その場で回転する傾向はない。

**grad との関係**

2階の偏微分が連続なスカラー場 $f$ では、

$$
\operatorname{rot}(\operatorname{grad}f)=\nabla\times(\nabla f)=\mathbf{0}
$$

[[grad]] で作ったベクトル場には局所的な回転がない。静電場は $\mathbf{E}=-\nabla V$ と書けるため、$\nabla\times\mathbf{E}=\mathbf{0}$ になる。

一方、時間変化する磁場がある場合、ファラデーの法則は、

$$
\nabla\times\mathbf{E}=-\frac{\partial\mathbf{B}}{\partial t}
$$

と書ける。$\mathbf{B}$ は磁束密度で、その時間変化に応じて電場に循環が生じることを表す。

**練習問題**

1. $\mathbf{F}=(2y,-2x,0)$ の rot を求めよ。$+z$ 側から原点を見ると、回転は時計回りか反時計回りか。
2. $\mathbf{F}=(y,z,x)$ の rot を求めよ。
3. $\mathbf{F}=(y,0,0)$ の rot と div を求めよ。湧き出しがなくても、局所的な回転はありうるか。
4. 【応用】$f=xy+z^2$ に対して、$\mathbf{F}=\operatorname{grad}f$ を求め、その rot がゼロになることを計算で確かめよ。

**こたえと解説**

**問1：$(0,0,-4)$。時計回り。**

$$
\operatorname{rot}\mathbf{F}
=\left(0,0,\frac{\partial(-2x)}{\partial x}-\frac{\partial(2y)}{\partial y}\right)
=(0,0,-2-2)=(0,0,-4)
$$

回転軸が $-z$ 方向なので、右手の規則より、$+z$ 側から見て時計回りになる。

**問2：$(-1,-1,-1)$。**

各成分を順に計算すると、

$$
\operatorname{rot}\mathbf{F}
=\left(
\frac{\partial x}{\partial y}-\frac{\partial z}{\partial z},\;
\frac{\partial y}{\partial z}-\frac{\partial x}{\partial x},\;
\frac{\partial z}{\partial x}-\frac{\partial y}{\partial y}
\right)
=(0-1,0-1,0-1)=(-1,-1,-1)
$$

**問3：rot は $(0,0,-1)$、div は $0$。回転はありうる。**

$$
\operatorname{rot}\mathbf{F}=(0,0,0-1)=(0,0,-1),
\qquad
\operatorname{div}\mathbf{F}=0
$$

流れは $x$ 方向だけだが、$y$ が大きい場所ほど $+x$ 方向の速度が大きい。この速度差が、羽根車を回そうとする。流線が直線でも、rot がゼロとは限らない。

**問4：$\mathbf{F}=(y,x,2z)$、その rot は $\mathbf{0}$。**

$$
\operatorname{rot}\mathbf{F}=(0-0,\;0-0,\;1-1)=(0,0,0)
$$

勾配で作った場の回転がゼロになることを確認できる。一方、この場の div は $2$ であり、rot と div は異なる性質を調べている。


**発展問題：局所の回転と、一周したときの循環**

**問5：rot がゼロなら、一周する仕事もゼロ？**

$z$ 軸を除いた空間で、

$$
\mathbf{F}=\left(-\frac{y}{x^2+y^2},\frac{x}{x^2+y^2},0\right)
$$

を考える。

1. この領域で $\nabla\times\mathbf{F}=\mathbf{0}$ を示せ。
2. $xy$ 平面の単位円を反時計回りに一周する循環 $\oint_C\mathbf{F}\cdot d\mathbf{r}$ を求めよ。$\mathbf{r}(t)=(\cos t,\sin t,0)$、$0\le t\le2\pi$ とおける。
3. この場を、領域全体で一価なスカラー関数 $f$ の勾配 $\nabla f$ として表せるか。

**問6：回転しない流体は、変形もしない？**

$0<a$ として、流速場 $\mathbf{v}=(ax,-ay,0)$ を考える。div と rot を求めよ。さらに、時刻 $0$ に $(x_0,y_0,z_0)$ にいた粒子の位置を求め、$xy$ 平面に置いた小さな正方形の流体要素がどう変形するか説明せよ。

**発展問題のこたえと解説**

**問5：rot はゼロだが、循環は $2\pi$。領域全体の一価なポテンシャルは存在しない。**

$z$ に依存せず第3成分もゼロなので、rot の第1・第2成分はゼロ。第3成分は、

$$
\frac{\partial}{\partial x}\frac{x}{x^2+y^2}
=\frac{y^2-x^2}{(x^2+y^2)^2},\qquad
\frac{\partial}{\partial y}\frac{-y}{x^2+y^2}
=\frac{y^2-x^2}{(x^2+y^2)^2}
$$

の差なのでゼロになる。一方、単位円上では、

$$
\mathbf{F}=(-\sin t,\cos t,0),\qquad
\frac{d\mathbf{r}}{dt}=(-\sin t,\cos t,0)
$$

より、

$$
\oint_C\mathbf{F}\cdot d\mathbf{r}
=\int_0^{2\pi}1\,dt=2\pi
$$

一価な $f$ の勾配なら、この積分は終点と始点の $f$ の差であり、一周するとゼロになるはず。したがって、そのような $f$ は領域全体には存在しない。

ストークスの定理「循環＝張った面を通る rot の流束」を円板に使おうとしても、円板の中心で場が未定義なので適用できない。局所的には角度 $\theta$ の勾配で表せるが、角度は一周すると $2\pi$ 増えてしまう。

**rot がゼロという局所的な条件だけでは、大域的な循環は決まらない。** 滑らかな場について「rot がゼロなら勾配で表せる」と結論するには、領域が単連結であることなど、領域の形に関する条件が必要になる。

**問6：div も rot もゼロだが、正方形は長方形に変形する。**

$$
\nabla\cdot\mathbf{v}=a-a=0,\qquad
\nabla\times\mathbf{v}=\mathbf{0}
$$

粒子の運動方程式を解くと、

$$
\frac{dx}{dt}=ax,\quad\frac{dy}{dt}=-ay,\quad\frac{dz}{dt}=0
\quad\Longrightarrow\quad
(x,y,z)=(x_0e^{at},y_0e^{-at},z_0)
$$

座標軸に平行な正方形は、横に $e^{at}$ 倍、縦に $e^{-at}$ 倍の長方形になる。面積は変わらないが形は変わる。

div は体積変化、rot は局所的な回転を捉えるが、**体積を保つ伸び縮みまでゼロだとは言っていない。** この場は $f=\tfrac{a}{2}(x^2-y^2)$ の勾配でもあり、勾配の場にも流体を変形させる働きがある。
