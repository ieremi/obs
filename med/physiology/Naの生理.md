---
aliases:
  - Na の生理
  - ナトリウムの生理
  - 体内の Na
  - Edelman の関係
  - 血漿浸透圧
date: 2026-10-01
tags:
  - physiology
  - physiology/renal
related:
  - "[[Na]]"
  - "[[低Na血症]]"
  - "[[高Na血症]]"
  - "[[バソプレシン]]"
  - "[[アルドステロン]]"
---

# Na の生理

## 体内の Na

<svg viewBox="0 0 580 215" width="580" role="img" aria-label="体重に占める体液の割合（成人男性の目安）。体液は体重の 60%。細胞内液 40%、細胞外液 20%（間質液 15%、血漿 5%）。細胞外液のおもな陽イオンは Na、細胞内液では K" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <g><title>細胞内液：体重の 40%</title><rect x="31.0" y="60" width="210.0" height="44" rx="3" fill="currentColor" fill-opacity="0.55"/></g>
  <text x="136.0" y="122" fill="currentColor" font-size="12" text-anchor="middle">細胞内液</text>
  <text x="136.0" y="138" fill="currentColor" font-size="12" text-anchor="middle" opacity="0.75">40%</text>
  <g><title>間質液：体重の 15%</title><rect x="243.0" y="60" width="77.5" height="44" rx="3" fill="currentColor" fill-opacity="0.35"/></g>
  <text x="281.8" y="122" fill="currentColor" font-size="12" text-anchor="middle">間質液</text>
  <text x="281.8" y="138" fill="currentColor" font-size="12" text-anchor="middle" opacity="0.75">15%</text>
  <g><title>血漿：体重の 5%</title><rect x="322.5" y="60" width="24.5" height="44" rx="3" fill="currentColor" fill-opacity="0.75"/></g>
  <g><title>水以外（蛋白質・脂肪・骨など）：体重の 40%</title><rect x="349.0" y="60" width="210.0" height="44" rx="3" fill="currentColor" fill-opacity="0.08"/></g>
  <text x="454.0" y="122" fill="currentColor" font-size="12" text-anchor="middle">水以外（蛋白質・脂肪・骨など）</text>
  <text x="454.0" y="138" fill="currentColor" font-size="12" text-anchor="middle" opacity="0.75">40%</text>
  <text x="334.8" y="52" fill="currentColor" font-size="12" text-anchor="middle">血漿 5%</text>
  <path d="M32.0 30 V22 H346.0 V30" fill="none" stroke="currentColor" stroke-width="1.2"/>
  <text x="189.0" y="16" fill="currentColor" font-size="13" text-anchor="middle">体液（総体水分量）60%</text>
  <path d="M32.0 150 V158 H240.0 V150" fill="none" stroke="currentColor" stroke-width="1.2"/>
  <path d="M244.0 150 V158 H346.0 V150" fill="none" stroke="currentColor" stroke-width="1.2"/>
  <text x="136.0" y="176" fill="currentColor" font-size="12" text-anchor="middle">K⁺ が多い</text>
  <text x="295.0" y="176" fill="currentColor" font-size="13" text-anchor="middle">細胞外液 20%</text>
  <text x="295.0" y="193" fill="currentColor" font-size="12" text-anchor="middle">Na⁺ が多い</text>
  <text x="560" y="211" fill="currentColor" font-size="11" text-anchor="end" opacity="0.7">成人男性の目安。女性・高齢者は体液の割合が小さい</text>
</svg>

| | 細胞外液 | 細胞内液 |
| --- | ---: | ---: |
| Na⁺（mmol/L） | 約 140 | 約 10〜15 |
| K⁺（mmol/L） | 約 4 | 約 140 |

細胞膜の Na⁺/K⁺-ATPase が、Na⁺ を細胞の外へ、K⁺ を中へくみ入れて、この差を保っている。Na⁺ は **細胞外液のおもな陽イオン** で、細胞外液の量と浸透圧を決める。

## 血清 Na は何を表すか

水は細胞膜を自由に通るので、細胞内液と細胞外液の浸透圧は等しい。体内の交換可能な Na の量を $\mathrm{Na_e}$、K の量を $\mathrm{K_e}$、総体水分量を $\mathrm{TBW}$ とする。細胞外液の浸透圧のほとんどは Na⁺ とそれにともなう陰イオン、細胞内液では K⁺ とそれにともなう陰イオンがつくるので、

$$
P_\mathrm{osm}\approx\frac{2(\mathrm{Na_e}+\mathrm{K_e})}{\mathrm{TBW}}
$$

一方、血漿では $P_\mathrm{osm}\approx2[\mathrm{Na}]$ なので、

$$
\boxed{[\mathrm{Na}]\approx\frac{\mathrm{Na_e}+\mathrm{K_e}}{\mathrm{TBW}}}
$$

（Edelman の関係）。

- 血清 Na は体内の Na の **量** ではなく、Na（と K）と **水の比** を表す
- 血清 Na が下がるのは、**分母の水が増える** か、**分子の Na・K が減る** とき。[[低Na血症]] の多くは前者
- K が減っても血清 Na は下がる（低 K 血症の補正で Na も上がる）

## 血漿浸透圧

$$
\boxed{P_\mathrm{osm}\approx2[\mathrm{Na}]+\frac{\text{血糖}}{18}+\frac{\mathrm{BUN}}{2.8}}
$$

- $2[\mathrm{Na}]$：Na⁺ とともにある陰イオン（Cl⁻、HCO₃⁻）の分を 2 倍で見積もる
- 血糖（mg/dL）を mmol/L にするには、グルコースの分子量 180 で割って 10 倍（dL→L）するので $\div18$
- BUN（尿素窒素、mg/dL）も同様に、窒素 2 原子の分子量 28 で割って 10 倍するので $\div2.8$

最後に、$[\mathrm{Na}]=140$、血糖 $90$、BUN $14$ を代入すると、

$$
P_\mathrm{osm}\approx280+5+5=290\ \text{mOsm/kg}
$$

尿素は細胞膜を自由に通るので、水を動かさない。水の移動を決める **有効浸透圧**（張度）は $2[\mathrm{Na}]+\text{血糖}/18$ である。

## 調節

| 調節するもの | しくみ | 何を変えるか |
| --- | --- | --- |
| **水** | [[バソプレシン]]（ADH）、口渇 | 血清 Na の **濃度**。浸透圧が上がると ADH が出て尿が濃くなり、のどが渇く |
| **Na の量** | [[アルドステロン]]（レニン・アンジオテンシン系）、ANP | 細胞外液の **量**（体液量・血圧） |

**濃度の異常は水の異常、量の異常は Na の異常** と考えると整理しやすい。

- 浸透圧が 1〜2% 変わるだけで ADH の分泌が大きく変わる。浸透圧の調節はとても鋭敏
- 体液量が大きく減ると、浸透圧が低くても ADH が出る（体液量の維持が優先される）

## 出典
- 一般的な知識
