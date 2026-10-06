---
aliases:
  - 肺胞換気と PaCO₂
  - 肺胞換気式
  - alveolar ventilation equation
date: 2026-09-26
tags:
  - physiology
  - physiology/respiratory
related:
  - "[[気管支喘息]]"
  - "[[Henderson-Hasselbalch式]]"
---

# 肺胞換気と PaCO₂

## 記号の定義

| 記号 | 意味・単位 |
| --- | --- |
| $\dot V_{CO_2}$ | 単位時間あたりの CO₂ 産生量。通常は STPD 条件の L/min |
| $\dot V_A$ | 肺胞換気量：ガス交換に参加する肺胞へ届く空気の量。通常は BTPS 条件の L/min |
| $F_{ACO_2}$ | 肺胞気中の CO₂ の体積分率（無次元）。以下の換算では水蒸気を除いた乾燥気体中の分率 |
| $P_{ACO_2}$ | 肺胞 CO₂ 分圧（mmHg） |
| $P_{aCO_2}$ | 動脈血 CO₂ 分圧（mmHg）。通常は $P_{ACO_2}$ に近く、臨床ではその近似値として用いる |
| $P_B$ | 大気圧（mmHg）。$P$ は Pressure（圧力）、$B$ は Barometric（気圧の）の頭文字で、Barometric pressure＝大気圧 |
| $P_{H_2O}$ | 水蒸気分圧。37℃の飽和水蒸気では約47 mmHg |
| $P_{AO_2}$ | 肺胞 O₂ 分圧（mmHg） |
| $P_{IO_2}$ | 加湿後の吸気 O₂ 分圧（mmHg） |
| $R$ | 呼吸交換比：$\dot V_{CO_2}/\dot V_{O_2}$。$\dot V_{O_2}$ は O₂ 消費量で、安静時の $R$ は通常約0.8 |

上のドットは「単位時間あたり」を表す。添字の $A$ は肺胞（alveolar）、$a$ は動脈血（arterial）、$I$ は吸気（inspired）を表す。

肺胞換気量は $\dot V_A=(V_T-V_D)f$。$V_T$ は一回換気量、$V_D$ は一回の呼吸における生理学的死腔量、$f$ は呼吸数である（体積を L、呼吸数を回/min とすれば L/min）。

## 肺胞換気式の導出

定常状態では、体内で産生された CO₂ と肺胞から排出される CO₂ が等しい。吸気中の CO₂ を無視し、体積を同じ条件にそろえれば、

$$
\dot V_{CO_2}=\dot V_A F_{ACO_2}
$$

したがって、

$$
P_{ACO_2}\propto \frac{\dot V_{CO_2}}{\dot V_A}
$$

### 体積の基準条件（STPD・BTPS）

CO₂ 産生量は **STPD**（0℃＝273 K、760 mmHg、乾燥）、肺胞換気量は **BTPS**（体温37℃＝310 K、その場の大気圧、水蒸気で飽和）で表すため、体積の換算が必要になる。

**STPD（Standard Temperature and Pressure, Dry）** は、気体の体積を表すための基準条件である。

- **温度：0℃（273.15 K。以下の式では約273 K）**
- **圧力：1気圧（760 mmHg）**
- **乾燥：水蒸気を含まない**

気体の体積は温度・圧力・水蒸気量によって変わるため、同じ基準条件に換算して比較する。CO₂ 産生量や O₂ 消費量は通常、STPD 条件で表す。

たとえば「CO₂ 産生量200 mL/min（STPD）」は、毎分産生される CO₂ をこの基準条件に換算すると200 mLになる、という意味である。

**BTPS（Body Temperature and Pressure, Saturated）** は、肺内の状態に合わせて気体の体積を表す条件である。

- **B：Body（体の）**
- **T：Temperature（温度）**
- **P：Pressure（圧力）**
- **S：Saturated（水蒸気で飽和した）**

BTPS の B は Body に由来し、大気圧を表す $P_B$ の B（Barometric）とは由来が異なる。

- **温度：体温37℃（310.15 K。以下の式では約310 K）**
- **圧力：その場の大気圧（$P_B$）**。760 mmHgに固定するわけではない
- **飽和：水蒸気で飽和している**。37℃での水蒸気分圧は約47 mmHg

吸い込んだ空気は気道で温められ、加湿されるため、肺内の気体量を扱う肺気量や肺胞換気量は通常、BTPS 条件で表す。

たとえば「肺胞換気量4.3 L/min（BTPS）」は、体温37℃・その場の大気圧・水蒸気飽和の条件で、毎分4.3 Lの空気がガス交換に参加する肺胞へ届く、という意味である。STPD は標準条件での体積、BTPS は肺内の条件での体積を表すため、両者を式で組み合わせる際には換算が必要になる。

### 単位補正と863の導出

理想気体の状態方程式より、同じ量の乾燥気体について、

$$
V_{\mathrm{STPD}}
=V_{\mathrm{BTPS}}\frac{P_B-P_{H_2O}}{760}\frac{273}{310}
$$

したがって、CO₂ の収支は、

$$
\dot V_{CO_2,\mathrm{STPD}}
=\dot V_{A,\mathrm{BTPS}}F_{ACO_2}
\frac{P_B-P_{H_2O}}{760}\frac{273}{310}
$$

乾燥気体中の CO₂ 分率を用いると $P_{ACO_2}=F_{ACO_2}(P_B-P_{H_2O})$ なので、代入して整理すると、

$$
P_{ACO_2}
=\underbrace{760\frac{310}{273}}_{\approx863\ \mathrm{mmHg}}
\frac{\dot V_{CO_2,\mathrm{STPD}}}{\dot V_{A,\mathrm{BTPS}}}
$$

つまり **863 は標準圧760 mmHgに絶対温度の比310/273を掛けた換算係数**である。水蒸気分圧と大気圧の項は導出の途中で相殺される。

## 結論

単位補正を含めると、

$$
\boxed{P_{ACO_2}=863\frac{\dot V_{CO_2}}{\dot V_A}}
$$

係数863を使うときは、両方の流量を L/min（または両方を mL/min）にそろえる。CO₂ 産生量を mL/min、肺胞換気量を L/min で表す場合は係数が **0.863** になる。たとえば $\dot V_{CO_2}=200$ mL/min、$\dot V_A=4.3$ L/min なら、$P_{ACO_2}\approx0.863\times200/4.3\approx40$ mmHg。

よって CO₂ 産生量が一定なら、

$$
\boxed{P_{ACO_2}\propto\frac{1}{\dot V_A}}
$$

肺胞換気量が半分になれば、肺胞 CO₂ 分圧はおよそ2倍になる。低換気で高 CO₂ 血症になる基本原理である。

## 関連

肺胞気方程式：

$$
P_{AO_2}\approx P_{IO_2}-\frac{P_{ACO_2}}{R}
$$

## 参考

- [Teaching an intuitive derivation of the clinical alveolar equations（Advances in Physiology Education, 2019）](https://journals.physiology.org/doi/full/10.1152/advan.00064.2019)
