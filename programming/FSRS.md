---
tags: [プログラミング, 学習, 暗記, アルゴリズム, Anki]
aliases: [FSRS, Free Spaced Repetition Scheduler, FSRS-6, FSRS-5, FSRS-4.5, DSR モデル, 忘却曲線, desired retention, 目標の正答率]
date: 2026-11-01
---
# FSRS

**FSRS**（Free Spaced Repetition Scheduler）は、間隔反復で **つぎにいつ復習するか** を決めるアルゴリズム。記憶を数式のモデルで表し、**自分の復習の記録から、そのモデルのパラメーターを学習する**。[[Anki]] に標準で入っている。

- 作った人：**叶峻峣**（Jarrett Ye、中国）。もとは、中国の単語学習アプリ **墨墨背单词**（MaiMemo）の研究（DHP モデル）から生まれた
- 開発は **open-spaced-repetition**（GitHub）。Anki が使うのは Rust で書かれた **fsrs-rs**
- Anki の昔からの方式（SM-2 系）は、カードごとの「易しさ」を掛けて間隔をのばすだけだった。FSRS は、**思い出せる確率** を計算し、**決めた正答率** になる日に復習させる

## 記憶の 3 つの量（DSR モデル）

| 量 | 意味 |
| --- | --- |
| **R**：想起可能性（Retrievability） | いま思い出せる確率 |
| **S**：安定度（Stability） | **R が 90% に下がるまでの日数**。大きいほど忘れにくい |
| **D**：難易度（Difficulty） | カードの難しさ。1〜10 |
| **G**：評価（Grade） | 答えたボタン。1：Again、2：Hard、3：Good、4：Easy |

- 1 枚のカードの記憶の状態を、**S と D** の 2 つで表す。R は、S と前の復習からの日数 t から計算する

## 忘却曲線

前の復習から t 日たったときの思い出せる確率 R は、

$$
R(t,S)=\left(1+\mathit{factor}\cdot\frac{t}{S}\right)^{-w_{20}},\qquad \mathit{factor}=0.9^{-1/w_{20}}-1
$$

（FSRS-6）。factor は、**t = S のとき R = 90%** になるように決まる。

- **FSRS-4.5・FSRS-5**：減り方が決まっていて、$R=(1+\tfrac{19}{81}\cdot\tfrac{t}{S})^{-0.5}$（DECAY = −0.5、FACTOR = 19/81）
- **FSRS-6**：減り方（$w_{20}$）も学習する。既定値は $w_{20}=0.1542$（factor ≒ 0.980）
- **FSRS v3 まで**：指数関数 $R=0.9^{t/S}$

<svg viewBox="0 0 560 300" width="560" role="img" aria-label="安定度 S が 10 日のときの忘却曲線。横軸は前の復習からの日数（0〜100 日）、縦軸は思い出せる確率。3 本とも 10 日目に 90% を通る。指数関数（FSRS v3 まで）は 100 日で約 35% まで下がり、FSRS-4.5・5 のべき関数は約 55%、FSRS-6 の既定値は約 69% で、あとになるほどゆっくり下がる" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <line x1="50" y1="260.0" x2="540" y2="260.0" stroke="currentColor" stroke-width="0.5" opacity="0.25"/><text x="44" y="264.0" font-size="10" text-anchor="end" fill="currentColor">30%</text><line x1="50" y1="191.4" x2="540" y2="191.4" stroke="currentColor" stroke-width="0.5" opacity="0.25"/><text x="44" y="195.4" font-size="10" text-anchor="end" fill="currentColor">50%</text><line x1="50" y1="122.9" x2="540" y2="122.9" stroke="currentColor" stroke-width="0.5" opacity="0.25"/><text x="44" y="126.9" font-size="10" text-anchor="end" fill="currentColor">70%</text><line x1="50" y1="54.3" x2="540" y2="54.3" stroke="currentColor" stroke-width="0.5" opacity="0.25"/><text x="44" y="58.3" font-size="10" text-anchor="end" fill="currentColor">90%</text><line x1="50" y1="20.0" x2="540" y2="20.0" stroke="currentColor" stroke-width="0.5" opacity="0.25"/><text x="44" y="24.0" font-size="10" text-anchor="end" fill="currentColor">100%</text>
  <line x1="50" y1="260" x2="540" y2="260" stroke="currentColor" stroke-width="1"/>
  <text x="50.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">0</text><text x="99.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">10</text><text x="148.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">20</text><text x="246.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">40</text><text x="344.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">60</text><text x="442.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">80</text><text x="540.0" y="276" font-size="10" text-anchor="middle" fill="currentColor">100</text>
  <line x1="99.0" y1="20" x2="99.0" y2="260" stroke="currentColor" stroke-width="0.8" stroke-dasharray="3 3" opacity="0.6"/>
  <text x="103.0" y="254" font-size="10" fill="currentColor">t = S</text>
  <path d="M50.0 20.0 L69.6 34.1 L89.2 47.7 L108.8 60.7 L128.4 73.2 L148.0 85.1 L167.6 96.6 L187.2 107.6 L206.8 118.1 L226.4 128.2 L246.0 137.9 L265.6 147.2 L285.2 156.1 L304.8 164.6 L324.4 172.8 L344.0 180.6 L363.6 188.2 L383.2 195.4 L402.8 202.3 L422.4 208.9 L442.0 215.3 L461.6 221.4 L481.2 227.2 L500.8 232.8 L520.4 238.2 L540.0 243.3" fill="none" stroke="currentColor" stroke-width="1.2" stroke-dasharray="6 4"/>
  <path d="M50.0 20.0 L69.6 35.0 L89.2 48.3 L108.8 60.0 L128.4 70.5 L148.0 80.0 L167.6 88.6 L187.2 96.5 L206.8 103.7 L226.4 110.4 L246.0 116.6 L265.6 122.3 L285.2 127.7 L304.8 132.7 L324.4 137.4 L344.0 141.9 L363.6 146.1 L383.2 150.0 L402.8 153.8 L422.4 157.3 L442.0 160.7 L461.6 163.9 L481.2 167.0 L500.8 169.9 L520.4 172.7 L540.0 175.4" fill="none" stroke="currentColor" stroke-width="1.6" opacity="0.6"/>
  <path d="M50.0 20.0 L69.6 37.1 L89.2 49.3 L108.8 58.7 L128.4 66.4 L148.0 72.8 L167.6 78.3 L187.2 83.2 L206.8 87.4 L226.4 91.2 L246.0 94.7 L265.6 97.8 L285.2 100.7 L304.8 103.4 L324.4 105.9 L344.0 108.2 L363.6 110.4 L383.2 112.4 L402.8 114.3 L422.4 116.1 L442.0 117.9 L461.6 119.5 L481.2 121.1 L500.8 122.5 L520.4 124.0 L540.0 125.3" fill="none" stroke="currentColor" stroke-width="2.6"/>
  <text x="536" y="237.2" font-size="11" text-anchor="end" fill="currentColor">指数 0.9^(t/S)（v3 まで）</text>
  <text x="536" y="169.3" font-size="11" text-anchor="end" fill="currentColor">FSRS-4.5・5（DECAY −0.5）</text>
  <text x="536" y="119.3" font-size="11" text-anchor="end" fill="currentColor" font-weight="bold">FSRS-6（既定 w20 = 0.1542）</text>
  <text x="295" y="292" font-size="11" text-anchor="middle" fill="currentColor">前の復習からの日数 t（S = 10 日）</text>
</svg>

| t（S = 10 日） | 1 日 | 5 日 | 10 日 | 20 日 | 30 日 | 60 日 | 100 日 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 指数（v3 まで） | 99.0% | 94.9% | **90%** | 81.0% | 72.9% | 53.1% | 34.9% |
| FSRS-4.5・5 | 98.8% | 94.6% | **90%** | 82.5% | 76.6% | 64.5% | 54.7% |
| FSRS-6（既定） | 98.6% | 94.0% | **90%** | 84.6% | 80.9% | 74.3% | 69.3% |

- べき関数の曲線は、**はじめ（S まで）は速く下がり、そのあとはゆっくり下がる**。たくさんのカードの記憶をまとめると、1 枚 1 枚は指数関数で忘れても、全体ではこういう形になるため、と説明されている
- 数値は、wiki の式に既定値を入れて、このノートで計算した

## 間隔の決め方

**目標の正答率**（desired retention）r を決めると、忘却曲線を t について解いて、つぎの間隔 I が決まる。

$$
I(r,S)=\frac{S}{\mathit{factor}}\left(r^{-1/w_{20}}-1\right)
$$

- r = 0.9 なら I = S（安定度そのものが間隔になる）
- Anki の初期値は r = 0.9（90%）

| 目標の正答率 r（S = 10 日） | 95% | 90% | 85% | 80% | 70% |
| --- | --- | --- | --- | --- | --- |
| FSRS-4.5・5 の間隔 | 4.6 日 | **10 日** | 16.4 日 | 24.0 日 | 44.4 日 |
| FSRS-6（既定）の間隔 | 4.0 日 | **10 日** | 19.1 日 | 33.2 日 | 92.9 日 |

- 正答率を上げると、間隔が短くなり、**復習の回数が大きく増える**。下げると楽になるが、忘れる率が上がる。90% 前後が、手間と覚え具合のつりあいがよいとされる
- Anki には、復習の量をシミュレーションして正答率を選ぶ手伝いをする画面がある（26.05 で「FSRS Help Me Decide」の効率のグラフが作りなおされた）

## 安定度と難易度の更新

$w_0, w_1, \ldots$ が **パラメーター**（FSRS-6 は 21 個、FSRS-5 は 19 個、FSRS-4.5 は 17 個）。

### はじめての評価
- 初期の安定度：$S_0(G)=w_{G-1}$。FSRS-6 の既定値では、Again 0.21 日、Hard 1.29 日、**Good 2.31 日**、Easy 8.30 日
- 初期の難易度（FSRS-5 以降）：$D_0(G)=w_4-e^{w_5(G-1)}+1$

### 難易度
$$
\Delta D=-w_6\,(G-3),\qquad D'=D+\Delta D\cdot\frac{10-D}{9},\qquad D''=w_7\,D_0(4)+(1-w_7)\,D'
$$

- Again・Hard で上がり、Easy で下がる。**$\tfrac{10-D}{9}$ をかけて、10 に近づくほど上がりにくくする**（FSRS-5 からの「linear damping」）
- 最後に、少しだけ $D_0(4)$（はじめに Easy と答えたときの難易度）に引きもどす（**平均への回帰**）。SM-2 系の「易しさの地獄」（ease hell：一度 Again を押すと、ずっと間隔がのびなくなる）を防ぐ

### 思い出せたとき（Hard・Good・Easy）
$$
S'_r=S\left(e^{w_8}\,(11-D)\,S^{-w_9}\left(e^{w_{10}(1-R)}-1\right)\cdot w_{15}^{[G=2]}\cdot w_{16}^{[G=4]}+1\right)
$$

安定度の増え方 $S'_r/S$ について：
1. **難しい**（D が大きい）ほど増えにくい
2. **すでに安定している**（S が大きい）ほど増えにくい
3. **忘れかけていた**（R が小さい）ほど大きく増える（**分散効果**。ぎりぎりで思い出すと、よく定着する）
4. 思い出せたなら、安定度は必ず増える（1 以上）

- 復習が遅れた（R が下がった）ときも、3 の効果で安定度は増えるが、ある上限に近づく。SM-2 系のように、遅れた日数に比例してのびることはない

### 忘れたとき（Again）
$$
S'_f=w_{11}\,D^{-w_{12}}\left((S+1)^{w_{13}}-1\right)e^{w_{14}(1-R)}
$$

- 忘れても、前の安定度が大きかったカードほど、忘れたあとの安定度も大きい（一からやり直しにはならない）

### 同じ日の復習（FSRS-6）
$$
S'=S\cdot e^{w_{17}(G-3+w_{18})}\cdot S^{-w_{19}}
$$

- 学習中の同じ日の復習でも安定度を更新する。FSRS-6 では $S^{-w_{19}}$ が加わり、**S が小さいうちは速く、大きくなるとゆっくり** 増える

## パラメーターの最適化
- 自分の **復習の記録**（どのカードを、いつ、どのボタンで答えたか）から、上の $w$ を計算する。Anki の「最適化」ボタンで行う
- 記録が少ないうちは、既定値（多くの人の記録から決めた値）を使う
- 予測した R と、実際に思い出せたかどうかのずれ（対数損失）が小さくなるように $w$ を決める。Anki 25.07 で、学習の目安が対数損失に変わった
- **すべての端末を最新にして同期してから、最適化をやりなおす** のがよい（AnkiDroid 2.23 の案内）

## 版の移り変わり

| 版 | パラメーター | 主な変更 | Anki |
| --- | --- | --- | --- |
| v1〜v3 | 7〜14 | 指数関数の忘却曲線 | アドオン（FSRS4Anki）で使えた |
| **v4** | 17 | 忘却曲線をべき関数に（DECAY = −1） | 23.10 から標準（記憶による） |
| **4.5** | 17 | DECAY = −0.5、FACTOR = 19/81 | 23.12 から（記憶による） |
| **5** | 19 | 同じ日の復習の式、難易度の linear damping、回帰先を $D_0(4)$ に | 24.11 から（記憶による） |
| **6** | 21 | 忘却曲線の減り方 $w_{20}$ を学習、同じ日の復習に $S^{-w_{19}}$ | **25.07** から |

- 26.08 で、Anki の中の fsrs-rs が 6.6.1 になり、速くなった

## 押さえどころ
- FSRS は、記憶を **R（思い出せる確率）・S（安定度）・D（難易度）** で表すモデル
- 安定度 S は、**思い出せる確率が 90% に下がるまでの日数**
- **目標の正答率** を決めると、それに合う日に復習させる。初期値は 90%
- パラメーターは、**自分の復習の記録から最適化** する。FSRS-6 は 21 個
- 忘却曲線は **べき関数**。はじめ速く、あとゆっくり下がる
- 忘れかけたころ思い出すほど、安定度が大きく増える（分散効果）

## 出典
- [open-spaced-repetition：The Algorithm（awesome-fsrs の wiki）](https://github.com/open-spaced-repetition/awesome-fsrs/wiki/The-Algorithm)：記号の定義、FSRS-6・5・4.5・v4 などの式と既定のパラメーター、安定度の増え方の 4 つの性質、DHP モデルが起源であること
- [GitHub：ankitects/anki のリリース](https://github.com/ankitects/anki/releases)、[newreleases.io：Anki 25.07](https://newreleases.io/project/github/ankitects/anki/release/25.07)：25.07 の FSRS-6、対数損失、26.05 の Help Me Decide、26.08 の fsrs-rs 6.6.1（検索結果の要約をふくむ）
- [APKMirror：AnkiDroid 2.23.0](https://www.apkmirror.com/apk/ankidroid-open-source-team/ankidroid-flashcards/ankidroid-flashcards-2-23-0-release/)：同期してから最適化しなおす案内（検索結果の要約）
- 表の数値（忘却曲線と間隔）：上の式と既定値で、このノートで計算した
- 作った人と墨墨背单词、Anki 23.10・23.12・24.11 で入った版、べき関数になる理由、90% 前後がよいこと：一般的な知識（ウェブでの確認はしていない）

関連：[[FSRS ライブラリ]]、[[Anki]]
