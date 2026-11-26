---
aliases:
  - heic
  - HEIF
  - heif
  - High Efficiency Image File Format
  - 高効率画像フォーマット
tags:
  - 画像
  - ファイル形式
  - 圧縮
  - iPhone
確認日: 2026-11-26
---
# HEIC

**iPhone のカメラが標準で保存する写真の形式。** 正確には、画像の入れ物である **HEIF**（High Efficiency Image File Format、ISO/IEC 23008-12）に、**HEVC（H.265）** で圧縮した画像を入れたもので、拡張子が `.heic` になる。iOS 11（2017年）から iPhone 7 以降で使われている。[Apple：Using HEIF or HEVC media on Apple devices](https://support.apple.com/en-us/116944)、[Library of Congress：HEIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000525.shtml)

## HEIF と HEIC の違い

| 名前 | 役割 |
| --- | --- |
| HEIF | 画像を格納する入れ物（コンテナ）の規格。MPEG が定め、2017年に ISO 規格として初めて発行された。 |
| HEVC（H.265） | 画像を圧縮する方式（コーデック）。もとは動画用。 |
| HEIC | HEVC で圧縮した画像を HEIF に入れたもの。iPhone の写真はこれ。 |
| AVIF | AV1 で圧縮した画像を HEIF に入れたもの。HEIF の仲間。 |

HEIF 自体が画像を圧縮するのではなく、中に入れるコーデックが画質と容量を決める。[Library of Congress：HEIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000525.shtml)

## メリット

### 1. 同じ画質で容量が小さい

- Apple は、HEIF は JPEG と同じ見た目の画質を保ちながら、端末と iCloud 写真の容量を少なくできると説明している。[Apple：Using HEIF or HEVC media on Apple devices](https://support.apple.com/en-us/116944)
- 導入時の WWDC 2017 の発表では、圧縮効率は JPEG の **最大2倍** とされた。つまり同じ画質なら、ファイルの大きさが最大でおよそ半分になる。写真によって差は変わり、いつも半分になるわけではない。[Apple WWDC 2017 Session 503：Introducing HEIF and HEVC（スライド PDF）](https://devstreaming-cdn.apple.com/videos/wwdc/2017/503i6plfvfi7o3222/503/503_introducing_heif_and_hevc.pdf)
- 写真を何千枚も撮る iPhone では、この差がストレージと iCloud の容量にそのまま効く。これが Apple が標準にした一番の理由である。

### 2. JPEG より表現できる幅が広い

- HEIF は、JPEG の 8 ビットより高いビット深度、広い色域、HDR のメタデータ、ICC プロファイルに対応している。[Library of Congress：HEIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000525.shtml)
- そのため、明暗の差が大きい場面や鮮やかな色を、JPEG より階調を保って残せる。

### 3. 1つのファイルに複数の画像や付属データを入れられる

- 1つのファイルに、いくつでも画像を入れられる。連写、ステレオ写真（左右2枚）、画像の連続（アニメーション）にも使える。[Library of Congress：HEIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000525.shtml)
- 本体の画像に、**深度マップ**（ポートレートモードのぼかしに使う奥行きの情報）や**透明度（アルファ）**を補助画像として付けられる。Exif・XMP のメタデータやサムネイルも入る。[Library of Congress：HEIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000525.shtml)
- JPEG にはこうした仕組みがない。iPhone で撮った後にポートレートのぼかしを変えられるのは、奥行きの情報が写真と一緒に残っているからである。

## デメリット：困るのは互換性

| 場面 | 状況 |
| --- | --- |
| Windows | 標準では開けないことがある。Microsoft Store の「HEIF 画像拡張機能」に加えて「HEVC ビデオ拡張機能」を入れる必要がある。HEVC のほうは有料（0.99ドル）という報告が多い。[Microsoft Store：HEIF Image Extension](https://apps.microsoft.com/detail/9pmmsr1cgpwg) |
| Web ブラウザ | 表示できるのは Safari 17 以降だけ。Chrome、Edge、Firefox は対応していない。[Can I use：HEIF/HEIC](https://caniuse.com/heif) |
| Web サービス・アプリ | アップロードできない、または黙って JPEG に変換されることがある。 |
| Mac・iPhone・iPad | macOS High Sierra・iOS 11 以降はそのまま扱える。[Apple：Using HEIF or HEVC media on Apple devices](https://support.apple.com/en-us/116944) |

対応が広がらない大きな理由は、中で使う HEVC の **特許とライセンス** である。HEVC には特許があり、ライセンスのまとめ役（パテントプール）に入っていない特許の持ち主もいるため、扱いが複雑で費用もかかる。Can I use は、ブラウザが HEIC に対応しにくいのは複雑でライセンスの費用が高いからだと説明し、無料で使える後継として AVIF と JPEG XL を挙げている。[Library of Congress：HEIF](https://www.loc.gov/preservation/digital/formats/fdd/fdd000525.shtml)、[Can I use：HEIF/HEIC](https://caniuse.com/heif)

## HEIC で困るときの対処

確認日：**2026-11-26**。設定の場所は iOS のバージョンによって変わることがある。

### 1. これから撮る写真を JPEG にする

1. 「設定」→「カメラ」→「フォーマット」を開く。
2. 「**互換性優先**」を選ぶ。

これで、新しく撮る写真は JPEG、動画は H.264 で保存される。元に戻すときは「高効率」を選ぶ。[Apple：Using HEIF or HEVC media on Apple devices](https://support.apple.com/en-us/116944)

- すでに撮った写真は HEIC のまま変わらない。
- 写真1枚あたりの容量は増える。容量を節約するという HEIC のメリットは失われる。

### 2. HEIC のまま撮り、渡すときだけ JPEG にする

容量の節約を残したいなら、こちらのほうがよい。iPhone には、相手が HEIC に対応していないときに自動で変換する仕組みがある。[Apple：Using HEIF or HEVC media on Apple devices](https://support.apple.com/en-us/116944)

- **USB で PC に取り込むとき**：JPEG・H.264 に変換されることがある。変換させたくないときだけ、「設定」→「アプリ」→「写真」で「元のフォーマットのまま」を選ぶ。PC で困るなら、この設定を「自動」のままにしておく。
- **AirDrop・メッセージ・メール**：受け取る側が HEIF に対応していないと、JPEG・H.264 に変換されることがある。
- **iCloud 写真**：元の形式のまま保存される。

### 3. 手元の HEIC ファイルを JPEG に変える

- **Mac**：「プレビュー」で開き、「ファイル」→「書き出す」でフォーマットを JPEG にする。たくさんあるときは、ターミナルで macOS 標準の `sips` を使う。

```sh
sips -s format jpeg IMG_0001.heic --out IMG_0001.jpg
```

- **Windows**：上の拡張機能を入れると、「フォト」で表示できるようになる。ただし拡張機能は表示用で、JPEG への一括変換はできないという報告がある。[Microsoft Q&A：How do I convert HEIC to JPG for free on Windows 11?](https://learn.microsoft.com/en-us/answers/questions/5569451/how-do-i-convert-heic-to-jpg-for-free-on-windows-1)

## どちらを選ぶか

| 使い方 | おすすめ |
| --- | --- |
| 写真は主に iPhone・Mac・iCloud で見る | 「高効率」（HEIC）のまま。 |
| ときどき Windows や Web に渡す | 「高効率」のまま撮り、渡すときの自動変換に任せる。 |
| いつも Windows・Web サービス・古い機器で使う | 「互換性優先」（JPEG）に切り替える。 |

## 関連

- [[Ogg]]：同じく「入れ物」と「圧縮方式」を分けて考えるファイル形式。
