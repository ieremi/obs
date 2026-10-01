---
name: 高Na血症
name_en: hypernatremia
aliases:
  - 高 Na 血症
  - 高ナトリウム血症
  - hypernatremia
icd10: E87.0
date: 2026-10-01
tags:
  - disease
  - disease/electrolyte
related:
  - "[[Na]]"
  - "[[Naの生理]]"
  - "[[低Na血症]]"
  - "[[バソプレシン]]"
---

# 高 Na 血症

## 定義
- 血清 Na 145 mmol/L を超えるもの
- 血漿は必ず **高浸透圧** になる（低 Na 血症と違い、偽性はない）

## なぜ起こるか

ほとんどは **水の不足**。口渇が正常で水を飲めれば、ふつうは起こらない。

- **飲めない**：高齢者・意識障害・乳児、寝たきり
- **水を失う**：尿崩症（ADH の不足・無効）、浸透圧利尿（高血糖など）、発熱・発汗、下痢
- まれに **Na の過剰**：高張食塩水・炭酸水素ナトリウムの大量投与

## 症状
- 口渇、脱力、意識障害、けいれん
- 細胞外液が濃くなると脳細胞から水が出て、**脳が縮む**。脳と頭蓋骨をつなぐ血管が引っぱられて切れ、出血することがある

## 水の不足量

体内の Na・K の量が変わらず、水だけが失われたとすると、[[Naの生理]] の Edelman の関係から $[\mathrm{Na}]\cdot\mathrm{TBW}$ は一定。正常時の Na を 140 とすると、

$$
[\mathrm{Na}]\cdot\mathrm{TBW}_\text{今}=140\cdot\mathrm{TBW}_\text{正常}
$$

$$
\boxed{\text{水の不足量}=\mathrm{TBW}_\text{正常}-\mathrm{TBW}_\text{今}=\mathrm{TBW}_\text{今}\left(\frac{[\mathrm{Na}]}{140}-1\right)}
$$

最後に、体重 70 kg の高齢男性（$\mathrm{TBW}=0.5\times70=35$ L）、$[\mathrm{Na}]=160$ を代入すると、

$$
35\times\left(\frac{160}{140}-1\right)=35\times\frac{1}{7}=5\ \text{L}
$$

<svg viewBox="0 0 560 210" width="560" role="img" aria-label="高 Na 血症での水の不足。体内の Na・K の量は同じまま、水が 40 L から 35 L に減ると、Na は 140 から 160 mmol/L に上がる。不足量は 5 L" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <text x="140" y="62" fill="currentColor" font-size="13" text-anchor="end">正常時</text>
  <g><title>正常時：体水分量 40 L、Na 140</title><rect x="150" y="40" width="340.0" height="34" rx="4" fill="currentColor" fill-opacity="0.3"/></g>
  <text x="320.0" y="62" fill="currentColor" font-size="12" text-anchor="middle">体水分量 40 L</text>
  <text x="502.0" y="62" fill="currentColor" font-size="13">Na 140</text>
  <text x="140" y="132" fill="currentColor" font-size="13" text-anchor="end">今</text>
  <g><title>今：体水分量 35 L、Na 160</title><rect x="150" y="110" width="297.5" height="34" rx="4" fill="currentColor" fill-opacity="0.55"/></g>
  <text x="298.75" y="132" fill="currentColor" font-size="12" text-anchor="middle">体水分量 35 L</text>
  <text x="502.0" y="132" fill="currentColor" font-size="13">Na 160</text>
  <rect x="447.5" y="110" width="42.5" height="34" rx="4" fill="none" stroke="currentColor" stroke-dasharray="4 3"/>
  <text x="468.75" y="166" fill="currentColor" font-size="12" text-anchor="middle">不足 5 L</text>
  <text x="550" y="200" fill="currentColor" font-size="11" text-anchor="end" opacity="0.7">Na・K の量は同じ。水だけが減ると濃くなる</text>
</svg>

## 治療
- 不足している水を、5% ブドウ糖液や飲水で補う。さらに、続いている喪失分も足す
- 慢性の高 Na 血症では脳が適応しているので、**急に下げると脳がむくむ**。一般に 24 時間に 10 mmol/L 程度までにする

## 出典
- 一般的な知識
