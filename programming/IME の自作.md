---
tags: [プログラミング, 日本語入力, IME, Linux]
aliases: [IME 自作, IME を作る, 日本語入力システムの自作, かな漢字変換の自作, インプットメソッドの自作, fcitx5 のアドオン, ビタビ, Viterbi]
date: 2026-11-01
---
# IME の自作

**IME**（Input Method Editor、インプットメソッド）は、キーボードの入力を、そのままでは打てない文字（日本語なら、かな・漢字）に変える仕組み。自作するには、大きく 2 つの部分を作る。

| 部分 | すること | 難しさ |
| --- | --- | --- |
| **変換エンジン** | ローマ字 → かな、かな → 漢字 | **ここがいちばん難しい**。辞書と、文の区切り方・候補の順番を決める仕組みが要る |
| **OS とのつなぎ** | キーを受け取り、入力中の文字（下線つき）と候補の窓を出し、確定した文字をアプリに渡す | OS ごとに仕組みが違う。Linux なら **fcitx5** か **IBus** の部品として作る |

## IME の中で起きていること

```text
キー入力  k a n j i
   ↓  ローマ字 → かな
入力中（プリエディット）  かんじ        ← 下線つきで表示。まだアプリには渡していない
   ↓  スペース：かな漢字変換
候補  漢字 / 感じ / 幹事 / 監事 …      ← 候補の窓（ルックアップテーブル）
   ↓  Enter：確定
アプリに渡す（コミット）  漢字
```

| 用語 | 意味 |
| --- | --- |
| **プリエディット**（preedit、未確定文字列） | 変換中で、まだアプリに渡していない文字。アプリの中に下線つきで出す |
| **コミット**（commit、確定） | 文字をアプリに渡すこと |
| **候補の窓**（lookup table、candidate list） | 変換の候補を並べる窓 |
| **文節** | 変換の区切り。「わたしの／なまえは」 |
| **インプットメソッドフレームワーク** | アプリと IME の間を取りもつ仕組み。Linux の fcitx5・IBus、Windows の TSF、macOS の InputMethodKit |

## 作り方の段階

難しさの順に、3 つの段階がある。

| 段階 | 作るもの | 量 |
| --- | --- | --- |
| 1. **表で引くだけの IME** | 「キーの並び → 文字」の表。fcitx5 の **table** 入力メソッドに渡すだけ | プログラムなしで、すぐできる |
| 2. **SKK 方式** | 変換の始まりを、人が大文字で指定する。「KanJi」→「漢字」。区切りを機械が決めなくてよい | 小さい。辞書を引くだけ |
| 3. **ふつうの IME**（Mozc・ATOK・MS-IME の方式） | 文全体を入れて、区切りと漢字を自動で決める | 大きい。辞書・品詞・接続コスト・学習が要る |

### 1. 表で引くだけ（fcitx5 の table）

fcitx5 には、「キーの並び → 文字」の表で入力する **table** 入力メソッドがある（中国語の倉頡や五筆に使われている）。表を自分で作れば、それだけで自分の入力メソッドになる。略語の入力、記号の入力、独自の配列などに向く。

表の元のファイル（`my.txt`）：

```text
KeyCode=abcdefghijklmnopqrstuvwxyz
Length=4
[Data]
nk 日本
nkg 日本語
kj 漢字
```

- `KeyCode`：使うキー、`Length`：いちばん長いキーの並び、`[Data]` の下に「キーの並び 文字」

辞書の形に変える：

```sh
libime_tabledict my.txt my.main.dict        # 作る
libime_tabledict -d my.main.dict /dev/stdout  # 中身を確かめる
```

入力メソッドの設定（`~/.local/share/fcitx5/inputmethod/my.conf`）：

```ini
[InputMethod]
Name=My Table
Label=私
LangCode=ja
Addon=table

[Table]
File=table/my.main.dict
PageSize=9
```

辞書を `~/.local/share/fcitx5/table/my.main.dict` に置き、fcitx5 を再起動して（`fcitx5 -r`）、fcitx5 の設定で入力メソッドに加える。

- 書式は、fcitx5 に入っている倉頡の設定（`/usr/share/fcitx5/inputmethod/cangjie5.conf`）に合わせた。辞書を作るところまでは、このパソコンで動くことを確かめた。fcitx5 に読みこませるところは、まだ試していない

### すでにある倉頡の表に、自分の定義を足す

fcitx5 の倉頡（`cangjie5`）は、上の table 入力メソッドで動いている。もとの辞書（`/usr/share/fcitx5/table/cangjie5.main.dict`、68,602 項目）は書きかえず、**追加の辞書** を重ねるのがよい。

| 方法 | 置き場所 | 向いている場面 |
| --- | --- | --- |
| **1. 追加の辞書**（おすすめ） | `~/.local/share/fcitx5/table/cangjie5.dict.d/` に `.txt` か `.dict` | 自分のコードと字を足す。もとの辞書はそのまま |
| 2. 辞書を丸ごと写して直す | `~/.local/share/fcitx5/table/cangjie5.main.dict` | もとの項目を消したり変えたりしたいとき |
| 3. QuickPhrase | `~/.local/share/fcitx5/data/quickphrase.d/*.mb` | 倉頡に限らず、どの入力メソッドでも使う略語や記号 |

#### 1. 追加の辞書
fcitx5 の table は、`table/<入力メソッドの名前>.dict.d` というフォルダの中の、**`.txt`（文字のまま）と `.dict`（変換したもの）を全部読む**。倉頡なら `cangjie5.dict.d`。ユーザーのフォルダ（`~/.local/share/fcitx5/`）にも置ける。

`~/.local/share/fcitx5/table/cangjie5.dict.d/my.txt`：

```text
zzkj 漢字
zzrb 壇嗇
```

- **フォルダの名前は変えられない**。`<名前>` は、入力メソッドの設定ファイルの名前（`inputmethod/cangjie5.conf` の `cangjie5`）で決まる。fcitx5 は、その名前から `table/cangjie5.dict.d` を作って探すので、ほかの名前のフォルダは読まれない（ソースの `TableIME::requestDict(name)` で、`inputmethod/<name>.conf` と `table/<name>.dict.d` に同じ `name` を使っている）
- **フォルダの中のファイルの名前は自由**。終わりが `.txt` か `.dict` であればよい（`my.txt`、`kanji.dict` など）。いくつ置いてもよい
- 別の名前のフォルダにしたいなら、入力メソッドそのものを別の名前で作る。たとえば `~/.local/share/fcitx5/inputmethod/mycangjie.conf` に、`cangjie5.conf` を写して `Name` を変え、`File=table/cangjie5.main.dict` はそのままにする。すると `table/mycangjie.dict.d` が読まれる。もとの倉頡とは別の入力メソッドとして、設定画面に出る（ユーザー辞書や設定の上書きも `mycangjie` の名前で別になる）
- 1 行に「コード 字（または語）」。ヘッダー（`KeyCode=` など）は要らない
- もとの辞書と同じコードにすると、候補の窓にいっしょに並ぶ。かぶらないコードにすると、その字だけがすぐ出る
- `.txt` はそのまま読まれる。項目が多いときは、変換して `.dict` にすると読みこみが速い：

  ```sh
  libime_tabledict -e -m /usr/share/fcitx5/table/cangjie5.main.dict my.txt my.dict
  ```

  `-e` は追加の辞書、`-m` はもとの辞書。中身は `libime_tabledict -d -e -m （もとの辞書） my.dict /dev/stdout` で確かめられる
- 置いたら、fcitx5 を再起動する（`fcitx5 -r -d`、またはトレイのアイコンから「再起動」）

#### 2. 辞書を丸ごと写して直す
fcitx5 は、同じ名前のファイルがあれば、**ユーザーのフォルダのほうを先に読む**。

```sh
libime_tabledict -d /usr/share/fcitx5/table/cangjie5.main.dict cj5.txt   # 文字にする
# cj5.txt を直す（[Data] の下が「コード 字」の行）
libime_tabledict cj5.txt ~/.local/share/fcitx5/table/cangjie5.main.dict  # 変換して置く
```

- パッケージが新しくなっても、写したほうが使われ続ける。もとの辞書の更新を取りこむには、写しなおす

#### 3. QuickPhrase
- fcitx5 の「クイックフレーズ」は、決まったキー（設定による）を押してから略語を打つと、登録した語が出る機能。入力メソッドに関係なく使える
- `~/.local/share/fcitx5/data/quickphrase.d/` に `.mb` のファイルを置き、1 行に「略語 語」と書く

#### そのほか
- 倉頡の入力メソッドの設定（候補の数、自動確定など）は、`~/.config/fcitx5/table/cangjie5.conf` で上書きできる（fcitx5 の設定画面からも変えられる）
- 打ったことのある語は、自動で `~/.local/share/fcitx5/table/cangjie5.user.dict`（ユーザー辞書）に記録される。中身は `libime_tabledict -d -u （ファイル） /dev/stdout` で見られる
- もとの辞書で、壇は `gywm`、嗇は `gowr`。[[壇]]・[[嗇]] のノートに書いた倉頡のコードと同じだった

#### 確かめたこと
- `.dict.d` のフォルダを読むことと、その中の `.txt`・`.dict` の扱いは、fcitx5-chinese-addons 5.1.3 のソース（`im/table/ime.cpp`）で確かめた
- 追加の辞書を `libime_tabledict -e` で作れること、ヘッダーなしの行だけでよいことは、このパソコンで確かめた
- 実際に `~/.local/share/fcitx5/` に置いて、fcitx5 で入力できるかは、まだ試していない

### 2・3. かな漢字変換を作る

#### ローマ字 → かな
- 表で引く。「ka → か」「shi → し」など
- 気をつけるところ：
  - **同じ子音が 2 つ** 続いたら「っ」（「kk」→「っk」）。ただし「nn」は「ん」
  - **「n」** は、あとに母音か y が来なければ「ん」（「kanji」→「かんじ」）。**最後の n は、つぎのキーが来るまで決められない**（「kan」は「かん」か「かな…」の途中か分からない）
  - 「k」だけのように、まだ途中の文字は、そのまま残しておく

#### かな → 漢字（ふつうの IME の方式）

文を区切る方法が何通りもあるので、**すべての区切り方と候補を、1 つの図（ラティス）にして、いちばんよい道を探す**。

```text
読み：  き   しゃ   が
       [木]  [社]  [が]      ← 1 文字目から：き → 木・気・来
       [気]  [車]            ← 2 文字目から：しゃ → 社・車
       [ 記者  ]             ← 1 文字目から：きしゃ → 記者・汽車・貴社
       [ 汽車  ]
道の例：記者＋が、気＋社＋が、木＋車＋が …
```

- 辞書の単語ごとに **コスト**（よく使う語ほど小さい）をつける
- となりあう 2 つの語の **つながりやすさ**（品詞どうしの **接続コスト**）もつける。「名詞のあとに助詞」は小さく、「助詞のあとに助詞」は大きい、など
- コストの合計がいちばん小さい道を、**ビタビ（Viterbi）アルゴリズム**（動的計画法）で探す。文の長さに比例する手間ですむ
- 2 番目、3 番目によい道（**N-best**）が、ほかの候補になる
- いまの IME は、これに **言語モデル**（よく続く単語の組み合わせの統計）や、**ユーザーの学習**（前に選んだ候補を上にする）を加えている

#### おもちゃの例（Python）

下は、考え方を見るための小さな例。辞書はほんの数語で、接続コストはない。このパソコンで動くことを確かめた。

```python
# ローマ字 → かな（一部だけ）
TABLE = {
    "a": "あ", "i": "い", "u": "う", "e": "え", "o": "お",
    "ka": "か", "ki": "き", "ku": "く", "ke": "け", "ko": "こ",
    "sa": "さ", "shi": "し", "su": "す", "ta": "た", "chi": "ち", "te": "て", "to": "と",
    "na": "な", "ni": "に", "ha": "は", "ga": "が", "ji": "じ", "de": "で",
    "pa": "ぱ", "po": "ぽ", "sha": "しゃ", "nn": "ん",
}
VOWELS = "aiueo"

def romaji_to_kana(s):
    """変換できた部分と、まだ残っているローマ字を返す。"""
    out, i = "", 0
    while i < len(s):
        if i + 1 < len(s) and s[i] == s[i + 1] and s[i] not in VOWELS + "n":
            out += "っ"; i += 1; continue          # kk → っk
        if s[i] == "n" and i + 1 < len(s) and s[i + 1] not in VOWELS + "ny":
            out += "ん"; i += 1; continue          # 子音の前の n → ん
        for L in (3, 2, 1):
            if s[i:i + L] in TABLE:
                out += TABLE[s[i:i + L]]; i += L; break
        else:
            return out, s[i:]                      # まだ途中（"k" など）
    return out, ""

# かな → 漢字：読み → [(表記, コスト)]
DICT = {
    "きしゃ": [("記者", 3000), ("汽車", 3500), ("貴社", 3600)],
    "しゃ": [("社", 4500), ("車", 4600)],
    "き": [("木", 4000), ("気", 3800), ("来", 3900)],
    "きた": [("来た", 3000), ("北", 3200)],
    "が": [("が", 1000)], "で": [("で", 1000)], "た": [("た", 2000)],
}
UNKNOWN = 10000   # 辞書にない 1 文字のコスト

def convert(kana):
    n = len(kana)
    best = [(0, [])] + [(float("inf"), None)] * n   # best[i]：i 文字目までの最小コストと単語列
    for i in range(n):
        cost, path = best[i]
        if path is None:
            continue
        for j in range(i + 1, n + 1):
            yomi = kana[i:j]
            cands = DICT.get(yomi) or ([(yomi, UNKNOWN)] if j == i + 1 else [])
            for word, c in cands:
                if cost + c < best[j][0]:
                    best[j] = (cost + c, path + [word])
    return "".join(best[n][1])

for r in ["kishaga", "kishadekita", "nippon", "kanji"]:
    kana, rest = romaji_to_kana(r)
    print(r, "→", kana + rest, "→", convert(kana) + rest)
```

結果：

```text
kishaga → きしゃが → 記者が
kishadekita → きしゃできた → 記者で来た
nippon → にっぽn → にっぽn       ← 最後の n はまだ決められない
kanji → かんじ → かんじ          ← 辞書に「かんじ」がないので、そのまま
```

- 「きしゃ」を 1 語（記者 3000）で取るほうが、「き」＋「しゃ」（気 3800 ＋ 社 4500）より安いので、「記者」が選ばれる
- 本物の IME では、辞書が数十万〜数百万語、接続コストが品詞の数 × 品詞の数（Mozc で数千 × 数千）の表になる

## 辞書とデータ

| 名前 | 中身 | 使いどころ |
| --- | --- | --- |
| **SKK 辞書**（SKK-JISYO.L など） | 「よみ /漢字1/漢字2/」の形。単純で扱いやすい | SKK 方式。手始めにちょうどよい |
| **Mozc の辞書**（`dictionary_oss`） | 単語・品詞 ID・コストと、品詞どうしの **接続コストの表**（connection） | ふつうの IME の方式をそのまま試せる |
| **IPAdic・UniDic**（形態素解析 MeCab の辞書） | 単語・品詞・コスト・接続表 | 形態素解析と同じ仕組みなので流用できる |
| Wikipedia などの大量の文章 | 単語の組み合わせの数え上げ（n-gram） | 自分で言語モデルを作るとき |

- ライセンスを確かめること（SKK-JISYO.L は GPL、Mozc は BSD 系、UniDic・IPAdic はそれぞれの条件）
- かな漢字変換は、**形態素解析の逆**（形態素解析は「漢字かな交じり文 → 単語と読み」、IME は「読み → 単語」）とみなせる。MeCab と同じラティスとビタビの仕組みが使える

## OS とのつなぎ

| OS | 仕組み | 作り方 |
| --- | --- | --- |
| **Linux** | **fcitx5**（このパソコンで使っているもの）、**IBus** | fcitx5：C++ の **アドオン**（共有ライブラリ）。IBus：エンジンを別のプログラムとして作り、D-Bus でつなぐ。Python（PyGObject）でも書ける |
| Windows | **TSF**（Text Services Framework） | COM の部品（DLL）を C++ で作る。古い IMM32 もある |
| macOS | **InputMethodKit** | `IMKInputController` を継承したアプリを作り、`~/Library/Input Methods` に置く |
| Android | `InputMethodService` | 画面のキーボードごと作る |
| iOS | キーボード拡張（Custom Keyboard Extension） | 画面のキーボードごと作る。できることに制限が多い |
| Emacs | `quail`、`register-input-method` | Emacs Lisp で書く。Emacs の中だけで使える（SKK の **ddskk** が有名） |
| ブラウザー | `compositionstart` などのイベント | IME そのものは作れない。Web ページの中で IME の入力を扱うときの話 |

- Wayland でも、アプリとの通信は fcitx5・IBus が引き受けるので、エンジンを作る側はあまり気にしなくてよい

### fcitx5 のアドオンの骨組み（C++）

**以下は、fcitx5 の API の形を示すための下書き。このパソコンには開発用のヘッダー（`libfcitx5core-dev`）が入っておらず、コンパイルして試していない。** 実際に作るときは、fcitx5 の公式のアドオン（fcitx5-mozc、fcitx5-anthy など）のソースと見比べること。

```cpp
// myime.cpp
#include <fcitx/addonfactory.h>
#include <fcitx/addonmanager.h>
#include <fcitx/inputcontext.h>
#include <fcitx/inputmethodengine.h>
#include <fcitx/inputpanel.h>
#include <fcitx/instance.h>
#include <fcitx/text.h>

class MyIME : public fcitx::InputMethodEngineV2 {
public:
    explicit MyIME(fcitx::Instance *instance) : instance_(instance) {}

    void keyEvent(const fcitx::InputMethodEntry &, fcitx::KeyEvent &event) override {
        if (event.isRelease()) return;
        auto *ic = event.inputContext();
        const auto &key = event.key();

        if (key.check(FcitxKey_Return) && !buffer_.empty()) {
            ic->commitString(buffer_);          // 確定してアプリに渡す
            buffer_.clear();
        } else if (key.check(FcitxKey_BackSpace) && !buffer_.empty()) {
            buffer_.pop_back();                 // 本当は UTF-8 の 1 文字分を消す
        } else if (key.isSimple()) {
            buffer_ += fcitx::Key::keySymToUTF8(key.sym());  // ここでローマ字 → かな
        } else {
            return;                             // 扱わないキーはアプリに渡す
        }
        updatePreedit(ic);
        event.filterAndAccept();                // このキーは IME が使った
    }

    void reset(const fcitx::InputMethodEntry &, fcitx::InputContextEvent &event) override {
        buffer_.clear();
        updatePreedit(event.inputContext());
    }

private:
    void updatePreedit(fcitx::InputContext *ic) {
        ic->inputPanel().reset();
        if (!buffer_.empty()) {
            fcitx::Text preedit(buffer_, fcitx::TextFormatFlag::Underline);
            ic->inputPanel().setClientPreedit(preedit);   // アプリの中に下線つきで出す
        }
        ic->updatePreedit();
        ic->updateUserInterface(fcitx::UserInterfaceComponent::InputPanel);
    }

    fcitx::Instance *instance_;
    std::string buffer_;
};

class MyIMEFactory : public fcitx::AddonFactory {
    fcitx::AddonInstance *create(fcitx::AddonManager *manager) override {
        return new MyIME(manager->instance());
    }
};

FCITX_ADDON_FACTORY(MyIMEFactory);
```

```cmake
# CMakeLists.txt
cmake_minimum_required(VERSION 3.16)
project(myime CXX)
find_package(Fcitx5Core REQUIRED)
add_library(myime SHARED myime.cpp)
target_link_libraries(myime Fcitx5::Core)
set_target_properties(myime PROPERTIES PREFIX "")
```

設定ファイルを 2 つ置く。形は、このパソコンの fcitx5-mozc の設定（`/usr/share/fcitx5/addon/mozc.conf`、`/usr/share/fcitx5/inputmethod/mozc.conf`）に合わせた。

```ini
# addon/myime.conf
[Addon]
Name=MyIME
Category=InputMethod
Library=myime
Type=SharedLibrary
OnDemand=True
```

```ini
# inputmethod/myime.conf
[InputMethod]
Name=MyIME
Label=自
LangCode=ja
Addon=myime
```

- 共有ライブラリは、fcitx5 のアドオンの置き場（このパソコンでは `/usr/lib/x86_64-linux-gnu/fcitx5/`）に置く
- 候補の窓は、`fcitx::CommonCandidateList` を作って `ic->inputPanel().setCandidateList(...)` で出す
- 変換エンジン（上の Python の例の部分）を C++ で書くか、別のプロセス（サーバー）にして通信する。**Mozc** は、変換エンジンを `mozc_server` という別のプロセスにして、fcitx5・IBus・Windows・macOS のつなぎの部分から呼んでいる

### IBus なら Python で書ける
- IBus では、エンジンが **別のプログラム** なので、Python（`gi.repository.IBus`）で書ける。`IBus.Engine` を継承して、`do_process_key_event` でキーを受け、`update_preedit_text`・`update_lookup_table`・`commit_text` で表示と確定をする
- 試すのは手軽だが、このパソコンは fcitx5 を使っていて、IBus の Python 用の部品（`gir1.2-ibus-1.0`）も入っていない

## 参考になるオープンソースの IME

| 名前 | 方式 | 特徴 |
| --- | --- | --- |
| **Mozc** | ふつうの IME（統計的なかな漢字変換） | Google 日本語入力のオープンソース版。C++。エンジンとつなぎの部分の分け方、辞書、接続表まで、全部が見られる。このパソコンにも入っている |
| **SKK**（ddskk、libskk、AquaSKK など） | SKK 方式 | 仕組みが単純で、自作の手本にしやすい |
| Anthy | ふつうの IME | 古くからある Linux の IME。いまは Anthy-unicode などが引き継ぐ |
| libkkc | ふつうの IME | n-gram の言語モデルを使う |
| AZIK・ACT | ローマ字の打ち方の工夫 | 変換ではなく、キーの打ち方（ローマ字の表）を変える。表を変えるだけで試せる |

## 押さえどころ
- IME は、**変換エンジン** と **OS とのつなぎ** の 2 つに分けて考える
- いちばん手軽なのは、**fcitx5 の table** に自分の表を渡すこと。プログラムが要らない
- かな漢字変換は、**辞書 ＋ 接続コスト ＋ ビタビ** で、いちばんコストの小さい区切り方と漢字を選ぶ。形態素解析の逆
- 区切りを自動で決めたくなければ、**SKK 方式** が小さく作れる
- Linux なら、fcitx5（C++ のアドオン）か IBus（Python でも書ける）。Mozc のソースが、全体の手本になる

## 出典
- fcitx5 の設定ファイルの形、table の辞書の作り方：このパソコンの fcitx5 5.1.7 の設定ファイルと `libime_tabledict` で確かめた
- 追加の辞書（`.dict.d`）の読みこみ：[fcitx5-chinese-addons 5.1.3 の im/table/ime.cpp](https://github.com/fcitx/fcitx5-chinese-addons/blob/5.1.3/im/table/ime.cpp)
- Python の例：このパソコンで動かして確かめた
- fcitx5 の C++ API、IBus の API、ほかの OS の仕組み、辞書のライセンス、参考の IME：一般的な知識（ウェブでの確認はしていない）
