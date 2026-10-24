---
aliases:
  - ogg
  - OGG
  - Ogg Vorbis
tags:
  - 音声
  - ファイル形式
  - 圧縮
---
# Ogg

**音声・映像などのデータを格納する、オープンなコンテナ形式。** Xiph.Org Foundationが開発している。音楽ファイルの文脈で「ogg」と言う場合、Vorbisで圧縮した音声をOggに格納した **Ogg Vorbis** を指すことが多い。[Xiph.Org：Ogg](https://www.xiph.org/ogg/)、[Vorbis公式FAQ](https://www.xiph.org/vorbis/faq/)

## OggとVorbisの違い

| 名前 | 役割 |
| --- | --- |
| Ogg | 音声・映像などを格納し、ストリームとして扱うための入れ物（コンテナ） |
| Vorbis | 音声を圧縮・復号する方式（コーデック） |
| Ogg Vorbis | Vorbis音声をOggコンテナに格納したもの |
| Opus | Vorbisとは別の音声コーデック。Oggにも格納できる |

**Ogg自体が音声を非可逆圧縮するのではなく、中に格納するコーデックが圧縮方式を決める。** [Vorbis公式FAQ](https://www.xiph.org/vorbis/faq/)、[Xiph.Org：Ogg Opus](https://wiki.xiph.org/OggOpus)

## 拡張子

| 拡張子 | 主な用途・推奨される使い分け |
| --- | --- |
| `.ogg` | Ogg Vorbis音声 |
| `.opus` | Oggに格納したOpus音声 |
| `.oga` | その他のOgg音声 |
| `.ogv` | Ogg映像 |
| `.ogx` | 多重化されたOggなど |

過去のファイルではこの区分に沿わない場合もある。**拡張子だけで中のコーデックを断定できない。** [Xiph.Org：MIME Types and File Extensions](https://wiki.xiph.org/MIME_Types_and_File_Extensions)

## Ogg Vorbisの特徴

Vorbisは、音楽などを小さく保存するための**非可逆圧縮**方式。復号しても元の音声データを完全には再現できない。音質と容量は、エンコード時の品質設定や音源によって変わる。[Vorbis公式仕様・紹介](https://www.xiph.org/vorbis/)

MP3と同じく、圧縮した音楽を持ち運ぶ用途で比較されてきた。ただし「同じ容量なら常にこちらが高音質」とは言い切れず、コーデックの実装・設定・音源・評価方法に左右される。元のデータを完全に保つ必要がある場合は、FLACなどの可逆圧縮と区別する。[Vorbis公式FAQ](https://www.xiph.org/vorbis/faq/)

## 携帯音楽プレーヤーとの関係

[[iRiver]]や[[Rio Player]]のような専用プレーヤーを選ぶ際には、MP3以外の形式に対応しているかも比較点になる。ただし、ブランド全体が一律にOgg Vorbisへ対応しているとは限らない。**機種・ファームウェア・対応コーデック**を個別に確認する。

古い機器の説明にある「Ogg対応」は、Ogg Vorbisへの対応を指す場合がある。Ogg Opusなど、同じコンテナに入る別の音声まで再生できるとは限らない。

## 拡張子の変更と変換

`.mp3` を `.ogg` に改名しても、形式は変わらない。音声形式を変えるには、復号して別のコーデックで再圧縮するなどの処理が必要になる。

MP3からVorbisのように非可逆圧縮同士で変換しても、最初の圧縮で失われた情報は戻らず、再圧縮による劣化も生じうる。形式を変えて保存するなら、元の無圧縮・可逆圧縮音源から作成する方が、非可逆圧縮の繰り返しを避けられる。[Vorbis公式FAQ](https://www.xiph.org/vorbis/faq/)

## 関連

- [[iRiver]]
- [[Rio Player]]
