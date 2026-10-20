---
tags: [医学, 微生物学, 検査, 薬剤感受性]
aliases: [最小発育阻止濃度, minimum inhibitory concentration, 最小阻止濃度]
date: 2026-10-20
---
# MIC

**MIC（minimum inhibitory concentration、最小発育阻止濃度）は、所定の条件で菌の目に見える発育を阻止する、最小の薬剤濃度。** 単位はmg/Lやµg/mLで、$1\,\mathrm{mg/L}=1\,\mathrm{µg/mL}$。

「どれほど低い濃度で発育を抑えられるか」を表す測定値であり、投与量や、菌をすべて殺す濃度そのものではない。[EUCAST：Broth Microdilution Reading Guide](https://www.eucast.org/fileadmin/eucast/pdf/MIC/Reading_guide_BMD_v_5.0_2024.pdf)

## 略語の意味

| 語 | 意味 |
| --- | --- |
| minimum | 最小の |
| inhibitory | 発育を阻止する |
| concentration | 濃度 |

## 具体例で読む

同じ菌と薬剤について、濃度を段階的に変えて発育を観察する。以下は読み方を示す架空例。

| 薬剤濃度（mg/L） | 観察 |
| ---: | --- |
| 0.25 | 発育あり |
| 0.5 | 発育あり |
| 1 | 発育あり |
| **2** | **発育なし** |
| 4 | 発育なし |

測定した濃度の中で、発育を認めない最小値は **2 mg/L**。したがって、この例のMICは2 mg/Lになる。

0.25、0.5、1、2、4……のような2倍希釈系列が用いられる。測定は連続的な値を無限に細かく決めるものではない。発育対照などを確認し、判読は菌種・薬剤・測定法に対応する手順で行う。[EUCAST：MIC測定の推奨法](https://www.eucast.org/fileadmin/eucast/pdf/Document_Archive/bacteria/disk_diffusion_methodology/EUCAST_recommendations_for_broth_microdilution_MIC_determination_September_2026.pdf)

## 「≤」「>」が付いた結果

測定できる濃度範囲には限りがある。

| 報告例 | 意味 |
| --- | --- |
| MIC ≤0.25 mg/L | 最低試験濃度0.25 mg/Lでも発育が抑えられた。さらに低い正確な値は分からない |
| MIC >8 mg/L | 最高試験濃度8 mg/Lでも発育した。発育を止める濃度は試験範囲の外 |

「≤0.25」を正確に0.25と同じ意味で扱わない。[EUCAST：Broth Microdilution Reading Guide](https://www.eucast.org/fileadmin/eucast/pdf/MIC/Reading_guide_BMD_v_5.0_2024.pdf)

## MICとS・I・Rは別

MICは測定値。**S・I・Rは、その値などを判定基準（ブレイクポイント）と照合した解釈**である。菌種、薬剤、感染部位、投与条件、採用する規格と版を確認する。[EUCAST：Clinical Breakpoint Tables](https://www.eucast.org/bacteria/clinical-breakpoints-and-interpretation/clinical-breakpoint-tables/)

EUCASTでの区分は次のとおり。

| 区分 | 意味 |
| --- | --- |
| S | 標準的な投与法で治療成功の可能性が高い |
| I | 投与法の調整や感染部位への集積など、曝露量の増加により治療成功の可能性が高い |
| R | 曝露量を増やしても治療失敗の可能性が高い |

EUCASTのIは「曝露量を増やした場合の感受性」であり、Rと同じではない。ほかの規格のIをそのまま同義として読まない。[EUCAST：Definition of S, I and R](https://www.eucast.org/bacteria/clinical-breakpoints-and-interpretation/definition-of-s-i-and-r/)

## 数字だけで薬剤を順位付けしない

同じ菌・同じ薬剤を同じ方法で測る場合、低いMICはより低濃度で発育を抑えられたことを示す。一方、**異なる薬剤のMICをそのまま比べて、低いほうが治療に優れるとはいえない**。各薬剤で到達濃度や判定基準が違うためである。

MICをそのまま血中濃度の目標や投与量へ置き換えることもできない。薬剤の体内での動きと、濃度・時間に応じた抗菌作用を合わせて考える。

## 阻止円との違い

| MIC | 阻止円径 |
| --- | --- |
| 発育を止める薬剤濃度 | 発育を抑えられた領域の直径 |
| mg/L、µg/mL | mm |
| 通常、低い値ほど低濃度で阻止 | 同一条件では通常、大きい円ほど広い範囲で阻止 |

関連はあるが同じ測定値ではなく、阻止円径から個々のMICを一意に換算することはできない。[EUCAST：MICと阻止円径の相関](https://www.eucast.org/bacteria/development-of-clinical-breakpoints-and-ecoffs/mic-zone-diameter-correlations/)

## 関連

- [[阻止円]]
- [[ESBL産生菌と抗菌薬耐性]]：菌名・耐性機序・感受性結果を分ける
- [[分布容積]]：薬剤の体内動態を理解する量

出典確認日：2026-10-20
