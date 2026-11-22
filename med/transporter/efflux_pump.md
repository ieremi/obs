---
name: efflux pump
name_ja: 排出ポンプ
aliases:
  - efflux pump
  - efflux pumps
  - 排出ポンプ
  - 薬剤排出ポンプ
  - multidrug efflux pump
tags:
  - transporter
  - 薬剤耐性
related:
  - "[[Acinetobacter]]"
  - "[[Pseudomonas]]"
  - "[[Escherichia]]"
  - "[[P糖蛋白]]"
---

# efflux pump

## 概要
- 細胞膜にあって、**細胞の中に入った物質を外へくみ出す輸送体**。細菌では、抗菌薬を外へ出して効きにくくする、耐性のしくみの一つになる
- 抗菌薬の耐性のしくみは大きく 4 つある: **薬の分解・修飾**(β-lactamase など)、**標的の変化**、**透過性の低下**(porin の減少)、**efflux**。efflux pump は最後のもの
- 1 つの pump が、形の違う多くの薬をくみ出すことがある(**multidrug efflux pump**)。そのため、1 つの変異で、いくつもの系統の抗菌薬がまとめて効きにくくなる
- もともと菌にあって、胆汁酸・界面活性剤・毒素など、環境の有害物質を出すのが本来の役目と考えられている
- ヒトの [[P糖蛋白|P-glycoprotein]] (ABCB1) も、ABC family の efflux pump

## 名前の由来
| 語 | 由来 | 意味 |
| --- | --- | --- |
| efflux | Latin *effluxus*(*effluere*「流れ出る」の完了分詞)から | 流れ出ること |
| *effluere* | *ex-*「外へ」+ *fluere*「流れる」 | 流れ出る |
| pump | 中世オランダ語 *pompe* などから | 液体をくみ上げる器械 |

- 反対は influx(*in-*「中へ」+ *fluere*)。英語の fluid、flux、influence と同じ語根

## 主な family
| family | energy | 主にいる菌 | 例 |
| --- | --- | --- | --- |
| **RND** (resistance-nodulation-division) | H<sup>+</sup> の濃度勾配 | Gram 陰性菌 | AcrAB-TolC(*E. coli*)、MexAB-OprM(*P. aeruginosa*)、AdeABC(*A. baumannii*) |
| **MFS** (major facilitator superfamily) | H<sup>+</sup> の濃度勾配 | Gram 陽性・陰性 | NorA(*S. aureus*、fluoroquinolone)、Tet(A)・Tet(K)(tetracycline)、Mef(A)(*Streptococcus*、macrolide) |
| **ABC** (ATP-binding cassette) | ATP の分解 | 広く | MacAB-TolC(*E. coli*、macrolide)、ヒトの P-gp |
| **MATE** (multidrug and toxic compound extrusion) | Na<sup>+</sup> または H<sup>+</sup> の濃度勾配 | 広く | NorM、AbeM(*A. baumannii*) |
| **SMR** (small multidrug resistance) | H<sup>+</sup> の濃度勾配 | 広く | EmrE(*E. coli*)、消毒薬の第四級 ammonium |

- ABC だけが ATP を直接使う。ほかは、膜をはさんだ H<sup>+</sup> や Na<sup>+</sup> の勾配を使う(二次輸送)
- 臨床で最も問題になるのは、Gram 陰性菌の **RND family**

## Gram 陰性菌の RND 型 pump
Gram 陰性菌には内膜と外膜がある。RND 型 pump は **3 つの部品が内膜から外膜までつながった管** になっていて、薬を periplasm や細胞質から、菌の外へ直接出す。

| 部品 | 場所 | *E. coli* の例 | *A. baumannii* の例 |
| --- | --- | --- | --- |
| RND 輸送体 | 内膜 | AcrB | AdeB |
| membrane fusion protein (adaptor) | periplasm | AcrA | AdeA |
| outer membrane factor (channel) | 外膜 | TolC | AdeC |

- 外膜の透過性が低いことと組み合わさると、とても効く。外膜でゆっくりしか入らない薬を、入ったそばから出すので、菌の中の濃度が上がらない
- この組み合わせが、*P. aeruginosa* や *Acinetobacter* が多くの薬にもともと効きにくい理由の一つ

## efflux pump をもつ細菌
**ほとんどすべての細菌が、何かしらの efflux pump をもつ。** 染色体の pump は種のもともとの性質で、plasmid の pump は菌から菌へうつる。以下は、臨床で耐性に関わる主なもの。

### Gram 陰性菌
| 菌                                             | pump (family)                    | 主に出す薬・意味                                                                                         |
| --------------------------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------ |
| *[[Escherichia\|E. coli]]*                    | **AcrAB-TolC** (RND)             | fluoroquinolone、tetracycline、chloramphenicol、一部の β-lactam など。調節因子 MarA・SoxS・Rob で発現が上がる          |
|                                               | MacAB-TolC (ABC)、EmrE (SMR)      | macrolide、第四級 ammonium など                                                                        |
| *[[Klebsiella\|K. pneumoniae]]*               | AcrAB-TolC (RND)、**OqxAB** (RND) | OqxAB は *K. pneumoniae* では染色体にある。fluoroquinolone、tigecycline、nitrofurantoin など。調節因子 RamA で発現が上がる |
| *[[Enterobacter\|Enterobacter]]*、*Salmonella* | AcrAB-TolC (RND)                 | 腸内細菌目に共通。fluoroquinolone の耐性に加わる                                                                 |
| *[[Pseudomonas\|P. aeruginosa]]*              | **MexAB-OprM** (RND)             | 多くの β-lactam(meropenem を含む)、fluoroquinolone。もともとの耐性の中心                                           |
|                                               | **MexXY-OprM** (RND)             | **aminoglycoside**、cefepime                                                                      |
|                                               | MexCD-OprJ、MexEF-OprN (RND)      | fluoroquinolone など。変異で発現が上がる                                                                     |
| *[[Acinetobacter\|A. baumannii]]*             | **AdeABC** (RND)                 | aminoglycoside、tigecycline、fluoroquinolone、tetracycline など。二成分制御系 AdeRS の変異で発現が上がる               |
|                                               | AdeIJK (RND)                     | 多くの薬。もともとの耐性に関わる                                                                                 |
|                                               | AdeFGH (RND)、AbeM (MATE)         | fluoroquinolone、chloramphenicol など                                                               |
| *Stenotrophomonas maltophilia*                | SmeDEF (RND) など                  | 多くの薬にもともと効きにくい理由の一つ。fluoroquinolone、tetracycline、chloramphenicol                                 |
| *[[Neisseria\|N. gonorrhoeae]]*               | **MtrCDE** (RND)                 | macrolide(azithromycin)、penicillin、脂肪酸・抗菌 peptide。抑制因子 MtrR の変異で発現が上がる                           |
| *[[Campylobacter\|Campylobacter jejuni]]*     | **CmeABC** (RND)                 | fluoroquinolone、macrolide、胆汁酸。腸で胆汁の中を生きのびるのにも要る                                                  |
| *[[Haemophilus\|H. influenzae]]*              | AcrAB-TolC (RND)                 | macrolide がもともと効きにくい理由の一つ                                                                        |

- *P. aeruginosa* の imipenem 耐性は、主に porin **OprD の減少** による。meropenem は MexAB-OprM でも出されるので、両方が効く

### Gram 陽性菌
Gram 陽性菌には外膜がないので、RND 型の 3 部品の管はない。**MFS** を中心に、1 つの膜の pump が働く。

| 菌 | pump (family) | 主に出す薬・意味 |
| --- | --- | --- |
| *[[Staphylococcus\|S. aureus]]* | **NorA** (MFS) | 染色体。親水性の fluoroquinolone(norfloxacin、ciprofloxacin)、消毒薬 |
| | NorB、NorC (MFS)、MepA (MATE) | fluoroquinolone、tigecycline(MepA)など |
| | **QacA・QacB** (MFS)、Smr (SMR) | plasmid。chlorhexidine、第四級 ammonium などの**消毒薬** |
| | Tet(K) (MFS) | plasmid。tetracycline(minocycline には効きにくい) |
| *[[Streptococcus\|S. pneumoniae]]* | **Mef(E)/Mel** | macrolide の **M 型耐性**(14・15 員環の macrolide だけに耐性。clindamycin は効く) |
| *[[Streptococcus\|S. pyogenes]]* | **Mef(A)** (MFS) | 同じく macrolide の M 型耐性 |

- macrolide 耐性には、ribosome を methyl 化する *erm*(MLS<sub>B</sub> 型、clindamycin にも耐性)もある。*mef* は pump なので、clindamycin は出されない

### *Mycobacterium*
| 菌 | pump (family) | 主に出す薬・意味 |
| --- | --- | --- |
| *Mycobacterium tuberculosis* | **MmpS5-MmpL5** (RND) | 調節因子 Rv0678 の変異で発現が上がり、**bedaquiline と clofazimine に同時に**効きにくくなる |
| | Tap (Rv1258c) (MFS) など | 多くの薬の効きを少し下げる |

- 多剤耐性結核の治療で bedaquiline を使うときに、Rv0678 の変異は問題になる

## 臨床での意味
- **もともとの耐性**: Gram 陰性菌に macrolide や penicillin G などが効きにくい理由の一部は、AcrAB-TolC などの pump
- **獲得耐性**: 調節遺伝子の変異で pump が増えると、**いくつもの系統に同時に耐性** になる。ただ、pump だけでは耐性の程度は低いことが多い
- **ほかのしくみと足し算になる**: 標的の変異(DNA gyrase など)や β-lactamase と組み合わさると、耐性が強くなる。pump による低い耐性が、さらに強い耐性の変異が選ばれる足場になる
- **遺伝子が plasmid にのることもある**: Tet(A)、QepA(fluoroquinolone)、OqxAB など。ほかの菌へうつる
- **消毒薬**: 第四級 ammonium 塩(benzalkonium など)や chlorhexidine も、pump で出されることがある

## pump を止める薬
- efflux pump inhibitor (EPI) は研究されている。PAβN (phenylalanine-arginine β-naphthylamide) は RND 型 pump を止める研究用の物質
- 2026 年の時点で、抗菌薬と組み合わせて臨床で使える EPI はない(一般的な知識による。ウェブでは確かめていない)

## 関連
- [[Acinetobacter]]: AdeABC、AdeIJK
- [[Pseudomonas]]: MexAB-OprM、MexXY-OprM
- [[Escherichia]]: AcrAB-TolC
- [[Klebsiella]]: OqxAB
- [[Neisseria]]: MtrCDE
- [[Campylobacter]]: CmeABC
- [[Staphylococcus]]: NorA、QacA/B
- [[Streptococcus]]: Mef(A)、Mef(E)
- [[P糖蛋白]]: ヒトの ABC 型 pump
- [[ESBL]]: 分解による耐性(efflux とは別のしくみ)

## 出典
- この note の内容は、一般的な微生物学・感染症学の知識による。個々の pump の基質は、菌株や文献によって違うことがある
