---
tags: [プログラミング, 学習, アルゴリズム, ライブラリ, Python, TypeScript]
aliases: [FSRS ライブラリ, FSRS の実装, py-fsrs, ts-fsrs, fsrs-rs, rs-fsrs, fsrs-optimizer, go-fsrs, awesome-fsrs]
date: 2026-11-01
---
# FSRS ライブラリ

[[FSRS]] のアルゴリズムを、自分のアプリで使うためのライブラリ。多くは GitHub の **open-spaced-repetition** が出している。一覧は **awesome-fsrs** にまとまっている。

ライブラリは、大きく 2 つの役わりに分かれる。

| 役わり | すること |
| --- | --- |
| **スケジューラー**（Scheduler） | カードの状態（S・D）と答え（Again〜Easy）から、**つぎの復習の日** と新しい状態を計算する。軽い |
| **オプティマイザー**（Optimizer） | 復習の記録から、**パラメーター $w$ を最適化** する。機械学習のライブラリ（PyTorch や Burn）を使うので重い |

## 主なライブラリ

| 言語 | ライブラリ | 版 | 役わり | 備考 |
| --- | --- | --- | --- | --- |
| **Python** | **py-fsrs**（PyPI：`fsrs`） | FSRS-6 | スケジューラー＋オプティマイザー | オプティマイザーは `pip install "fsrs[optimizer]"` |
| Python | fsrs-optimizer | FSRS-6 | オプティマイザー | |
| Python | fsrs-rs-python | FSRS-6 | オプティマイザー | fsrs-rs を Python から使う |
| Python | rs-fsrs-python | FSRS-5 | スケジューラー | rs-fsrs を Python から使う |
| **Rust** | **fsrs-rs** | FSRS-6 | スケジューラー＋オプティマイザー | **Anki の中で使われているもの**。ブラウザーで動かす fsrs-browser もある |
| Rust | rs-fsrs | FSRS-5 | スケジューラー | Java・C・Node.js・Python 版の土台 |
| **TypeScript** | **ts-fsrs**（npm：`ts-fsrs`） | FSRS-6 | スケジューラー | ウェブのアプリでいちばんよく使われている |
| Go | go-fsrs | FSRS-5 | スケジューラー | |
| Kotlin | FSRS-Kotlin | FSRS-6 | スケジューラー | |
| Swift | swift-fsrs | FSRS-5 | スケジューラー | |
| Dart | dart-fsrs | FSRS-4.5 | スケジューラー | Flutter のアプリ向け |
| Java・C・Node.js | rs-fsrs-java・rs-fsrs-c・rs-fsrs-nodejs | FSRS-5 | スケジューラー | rs-fsrs を各言語から使う |
| そのほか | Scala（fsrs4s）、Lisp、Ruby、Elixir、Clojure、OCaml、Haskell など | v4〜v7 | スケジューラー | 一部は個人の作 |

- 「版」は awesome-fsrs の一覧に書かれた、対応する FSRS の版（2026 年 11 月に見たもの）。古い版のままのライブラリもある

## py-fsrs（Python）

```sh
pip install fsrs                 # スケジューラーだけ
pip install "fsrs[optimizer]"    # オプティマイザーも（PyTorch が入る）
```

```python
from datetime import datetime, timedelta, timezone
from fsrs import Scheduler, Card, Rating

scheduler = Scheduler(enable_fuzzing=False)  # 既定は desired_retention=0.9、fuzz あり
card = Card()
now = datetime(2026, 11, 1, 9, 0, tzinfo=timezone.utc)

for rating in [Rating.Good, Rating.Good, Rating.Good, Rating.Again, Rating.Good]:
    card, log = scheduler.review_card(card, rating, review_datetime=now)
    print(f"{now:%m-%d %H:%M} {rating.name:5} → 次 {card.due:%m-%d %H:%M}  "
          f"S={card.stability:.2f} D={card.difficulty:.2f} state={card.state.name}")
    now = card.due

r = scheduler.get_card_retrievability(card, current_datetime=card.due + timedelta(days=10))
print("10日遅れたときの R:", round(r, 3))
```

結果（このパソコンで py-fsrs 6.3.2 を動かした）：

```text
11-01 09:00 Good  → 次 11-01 09:10  S=2.31 D=2.12 state=Learning
11-01 09:10 Good  → 次 11-03 09:10  S=2.31 D=2.11 state=Review
11-03 09:10 Good  → 次 11-14 09:10  S=10.97 D=2.10 state=Review
11-14 09:10 Again → 次 11-14 09:20  S=1.54 D=7.39 state=Relearning
11-14 09:20 Good  → 次 11-16 09:20  S=1.57 D=7.38 state=Review
10日遅れたときの R: 0.719
```

- 1 回目の Good：はじめの **学習ステップ**（1 分 → 10 分）の 2 つ目へ進み、10 分後
- 2 回目の Good：学習を終えて **復習** になり、2 日後。安定度は、はじめの Good の既定値 2.31 日のまま
- 3 回目の Good：2 日あけて思い出せたので、安定度が **10.97 日** に増え、11 日後
- Again：**再学習**（10 分後）。安定度は 1.54 日に下がり、難易度は 2.10 → 7.39 に上がる

`Scheduler` の主な設定：

| 設定 | 既定 | 意味 |
| --- | --- | --- |
| `parameters` | 21 個の既定値 | FSRS-6 の $w$。オプティマイザーで求めた値に変える |
| `desired_retention` | `0.9` | 目標の正答率 |
| `learning_steps` | 1 分、10 分 | 新しいカードの学習ステップ。`()` でなくせる |
| `relearning_steps` | 10 分 | 忘れたカードの再学習ステップ |
| `maximum_interval` | `36500`（日） | 間隔の上限 |
| `enable_fuzzing` | `True` | 間隔を少しだけばらつかせる（同じ日に作ったカードが、ずっと同じ日に集まらないように） |

- 日時は **タイムゾーンつき（UTC）** で渡す
- `Card`・`ReviewLog`・`Scheduler` は `to_dict()`／`from_dict()`（JSON）で保存して読みもどせる

オプティマイザー：

```python
from fsrs import Optimizer, Scheduler

optimizer = Optimizer(review_logs)                      # ReviewLog のリスト
optimal_parameters = optimizer.compute_optimal_parameters()
scheduler = Scheduler(optimal_parameters)
optimal_retention = optimizer.compute_optimal_retention(optimal_parameters)  # 手間が少なくなる正答率
```

- オプティマイザーの部分は試していない（PyTorch を入れていない）。書き方は py-fsrs の README による

## ts-fsrs（TypeScript・JavaScript）

```sh
npm install ts-fsrs
```

```js
import { fsrs, generatorParameters, createEmptyCard, Rating, State } from 'ts-fsrs';

const name = (obj, v) => Object.keys(obj).find((k) => obj[k] === v);
const f = fsrs(generatorParameters({ request_retention: 0.9, enable_fuzz: false }));

let card = createEmptyCard(new Date('2026-11-01T09:00:00Z'));
let now = card.due;
for (const r of [Rating.Good, Rating.Good, Rating.Good, Rating.Again, Rating.Good]) {
  const { card: next } = f.next(card, now, r);
  console.log(now.toISOString().slice(5, 16), name(Rating, r).padEnd(5), '→',
    next.due.toISOString().slice(5, 16), 'S=' + next.stability.toFixed(2),
    'D=' + next.difficulty.toFixed(2), name(State, next.state));
  card = next;
  now = next.due;
}

// 4 つのボタンを押したときの次の日を、まとめて見る
const preview = f.repeat(card, now);
for (const r of [Rating.Again, Rating.Hard, Rating.Good, Rating.Easy])
  console.log(name(Rating, r).padEnd(5), preview[r].card.due.toISOString().slice(0, 10));
```

結果（このパソコンで ts-fsrs 6.0.0 を動かした）：

```text
11-01T09:00 Good  → 11-01T09:10 S=2.31 D=2.12 Learning
11-01T09:10 Good  → 11-03T09:10 S=2.31 D=2.11 Review
11-03T09:10 Good  → 11-14T09:10 S=10.97 D=2.10 Review
11-14T09:10 Again → 11-14T09:20 S=1.54 D=7.39 Relearning
11-14T09:20 Good  → 11-16T09:20 S=1.57 D=7.38 Review
Again 2026-11-16
Hard  2026-11-20
Good  2026-11-21
Easy  2026-11-24
```

- **py-fsrs と同じ答え方をさせると、日程も S・D も同じ** になった。どちらも同じ FSRS-6 の既定値を使っているため
- `Rating` と `State` は、名前 → 数のふつうのオブジェクト（`{ Manual: 0, Again: 1, Hard: 2, Good: 3, Easy: 4 }`）。数 → 名前の逆引きはできないので、上の `name` のような関数を使う（TypeScript の `enum` のつもりで `Rating[r]` と書くと `undefined` になった）
- `repeat` を使うと、ボタンを押す前に「それぞれ押したら次はいつか」を出せる。Anki のボタンの上に出る日数と同じもの
- `generatorParameters` の主な設定：`request_retention`（目標の正答率）、`maximum_interval`、`enable_fuzz`、`enable_short_term`（同じ日の短い間隔を使うか）、`w`（パラメーター）

## fsrs-rs（Rust）
- Anki の中で、スケジュールの計算と **パラメーターの最適化** に使われている。機械学習のライブラリ **Burn** を使う
- Anki 26.08 で 6.6.1 になった（→ [[Anki]]）

## アプリで使われている例
awesome-fsrs には、FSRS を使うアプリが多く載っている。

| アプリ | 使っているもの |
| --- | --- |
| [[Anki]] | fsrs-rs |
| Obsidian のプラグイン（obsidian-spaced-repetition-recall、True Recall、LearnKit、HiNote） | FSRS-6。True Recall は ts-fsrs |
| Mochi Cards、Rember、Etude ほか多数 | ts-fsrs など |
| Org-srs（Emacs） | 独自の実装 |
| Markji | MMX（FSRS の作者が作った変形版）。墨墨背单词の会社のアプリ |

- 自分の Obsidian のボールトのノートを間隔反復で覚えたいなら、Obsidian のプラグインか、[[AnkiConnect]] で Anki に送るかを選べる

## 自分で使うときの注意
- **日時はタイムゾーンをそろえる**（UTC にする）。日をまたぐ計算がずれる
- **復習の記録（ReviewLog）を必ず残す**。あとでオプティマイザーにかけられる
- **fuzz** を有効にすると、結果が毎回少し変わる。テストでは切る
- ライブラリによって、対応する FSRS の版がちがう。**Anki などとパラメーターをやりとりするときは、版（パラメーターの数：FSRS-6 は 21、FSRS-5 は 19、FSRS-4.5 は 17）をそろえる**

## 押さえどころ
- FSRS のライブラリは、**スケジューラー**（つぎの日を計算）と **オプティマイザー**（パラメーターを学習）に分かれる
- Python は **py-fsrs**（`pip install fsrs`）、JavaScript は **ts-fsrs**（`npm install ts-fsrs`）、Rust は **fsrs-rs**（Anki の中身）
- どれも、カードの状態と答えを渡すと、新しい状態とつぎの日が返ってくる
- 同じ版・同じパラメーターなら、言語がちがっても同じ結果になる

## 出典
- [awesome-fsrs（README）](https://github.com/open-spaced-repetition/awesome-fsrs)：ライブラリの一覧と対応する版、FSRS を使うアプリ（Obsidian のプラグイン、Markji ほか）
- [py-fsrs（README）](https://github.com/open-spaced-repetition/py-fsrs)：インストール、`Scheduler` の設定と既定値、オプティマイザーの使い方
- py-fsrs 6.3.2 と ts-fsrs 6.0.0：このパソコンの作業用フォルダに入れて、上の例を動かした
- fsrs-rs が Burn を使うこと、rs-fsrs が各言語版の土台であること：一般的な知識（ウェブでの確認はしていない）
