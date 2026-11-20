---
aliases:
  - Gemini でプログラミングするには
  - Geminiでコーディング
  - ジェミニでプログラミング
tags:
  - AI
  - programming
---

# Geminiでプログラミングする方法

確認日：**2026年11月20日**。個人利用を中心にまとめる。ツールの提供状況・料金・上限は変更される。

**小さなアプリをブラウザで作るならGeminiのCanvas、手元のプロジェクトを読み書きして開発するならGoogle Antigravity**が選択肢になる。自作アプリにGeminiの応答機能を組み込む場合は、Google AI Studio／Gemini APIを使う。

## 用途による使い分け

| やりたいこと | 使うもの | 作業の進め方 |
| --- | --- | --- |
| コードの説明・エラーの相談・短いスクリプトの作成 | Geminiのチャット | コードやエラーを渡し、自分の環境で実行する |
| Webアプリや画面の試作 | Gemini Canvas | 指示して生成し、プレビューを見ながら直す |
| 既存のリポジトリの修正・テスト | AntigravityのIDE拡張／専用IDE／CLI | プロジェクトを開き、エージェントに作業を指示する |
| 自作アプリからGeminiを呼び出す | Google AI Studio／Gemini API | モデルを試し、APIをプログラムに組み込む |

出典：[Canvas公式ヘルプ](https://support.google.com/gemini/answer/16047321)、[Antigravity導入ガイド](https://antigravity.google/docs/getting-started)、[Google公式・開発者向けプラン案内](https://gemini.google/subscriptions/)。

## 1. まずブラウザで試す：Canvas

1. [Gemini](https://gemini.google.com/)にログインする。
2. 入力欄付近のメニューで **Canvas** を選ぶ。表示位置は画面や端末によって異なる。
3. 作りたいもの、使用言語、必要な機能を伝える。
4. プレビューを操作し、変更したい部分を追加で指示する。コードの直接編集やコンソールでのエラー確認もできる。

依頼例：

> HTML・CSS・JavaScriptで、読書記録を管理するアプリを作って。書名・著者・読了日を登録し、一覧から編集・削除できるようにして。データはブラウザのlocalStorageに保存し、スマートフォンでも操作しやすくして。

Canvasは画面の試作に向いている。Pythonなどのコードを生成しても、その実行環境までCanvas内に用意されるとは限らないため、ローカル環境で動かす場合は実行方法も説明させる。

出典：[Canvasでドキュメントやアプリなどを作成する](https://support.google.com/gemini/answer/16047321)。

## 2. 手元のコードを開発する：Antigravity

既存プロジェクトの調査・修正・テストまで依頼したい場合の選択肢。VS Codeなどのエディタに導入する方法と、専用IDEやターミナルで使う方法がある。

### VS Codeで始める

1. VS Codeの拡張機能画面を開く。Macでは `Cmd + Shift + X`。
2. **Google Antigravity** を検索し、公式の拡張機能をインストールする。
3. 個人のGoogleアカウントでログインする。
4. 開発したいプロジェクトのフォルダを開き、エージェントのパネルから依頼する。

最初の依頼例：

> このリポジトリの構成と起動方法を調べて説明して。まずファイルは変更しないで。

構成が分かったら、具体的な変更を頼む。

> 読書記録に「評価1〜5」を追加して。既存の書き方に合わせ、必要な画面・保存処理を修正し、関連するテストを実行して。最後に変更点とテスト結果を説明して。

CLIを使いたい場合は[公式導入ガイド](https://antigravity.google/docs/getting-started?tab=cli)に従ってAntigravity CLIをインストールする。現在のコマンド名は `agy`。専用IDEは[公式ダウンロードページ](https://antigravity.google/download)から入手できる。

出典：[Antigravity Get started](https://antigravity.google/docs/getting-started)。

### 古いGemini CLI／Code Assistの記事に注意

公式案内では、**2026年6月18日から、個人向け・Google AI Pro・UltraでのGemini Code Assist IDE拡張とGemini CLIの提供が終了**し、それらでの「Login with Google」は利用できなくなった。移行先としてAntigravityが案内されている。これは個人向けの認証・提供枠に関する説明で、Gemini API全体の終了を意味しない。

出典：[Gemini Code Assist consumer accountsの提供終了案内](https://developers.google.com/gemini-code-assist/docs/deprecations/code-assist-individuals)。

## 3. 料金プランはどう関係するか

- **最初から有料契約は必須ではない。** Antigravityは無料枠があり、アプリ・CLI・IDE拡張などで使える。
- **Google AI Pro／Ultra** はAntigravityのモデルや利用上限を拡張する。無料枠で試し、不足したら検討するとよい。
- **Geminiアプリの利用枠とAntigravityの利用枠は区別する。** [[Geminiの料金プラン]]にあるGeminiアプリの倍率を、そのまま開発ツールの利用回数とは考えない。
- **APIの課金も確認する。** Gemini APIはプロジェクトに紐づく無料枠・有料枠で管理される。Google AI Proの月額料金だけでAPIを無制限に呼べるわけではない。

出典：[Antigravity料金・利用枠](https://antigravity.google/pricing)、[Gemini APIの課金](https://aistudio.google.com/docs/billing)。日本の個人向け月額料金は [[Geminiの料金プラン]] を参照。

## 4. 自作アプリにGeminiを組み込む場合

[Google AI Studio](https://aistudio.google.com/)でモデルの応答を試し、Gemini APIを利用する。これは「Geminiに開発を手伝わせる」ことに加えて、「完成したアプリの機能としてGeminiを呼ぶ」用途。

例えば、読書記録アプリに「感想を要約する」機能を付ける場合に使う。導入時には利用モデル、APIキー、プロジェクトの課金設定と使用量を確認する。

出典：[Google公式・開発者向け案内](https://gemini.google/subscriptions/)、[Gemini APIの課金](https://aistudio.google.com/docs/billing)。

## 依頼をうまく進めるコツ

以下は実作業の進め方の目安。

- **目的と完了条件を示す。** 「検索を付ける」より、「書名の部分一致で絞り込み、空欄なら全件表示する」と伝える。
- **環境を示す。** 言語・フレームワーク・バージョン、起動コマンド、エラー全文を添える。
- **小さい変更で確認する。** 一度に多くの機能を頼まず、動いたことを確かめて次に進む。
- **差分と実行結果を確認する。** 生成されたコードの見た目だけで判断せず、起動・操作・関連テストで確かめる。

## 関連

- [[Geminiの料金プラン]]
