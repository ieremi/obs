---
tags: [プログラミング, 学習, API, Anki]
aliases: [AnkiConnect, Anki-Connect, Anki Connect, アンキコネクト, 2055492159]
date: 2026-11-01
---
# AnkiConnect

**AnkiConnect**（Anki-Connect）は、[[Anki]] の **アドオン**。動いている Anki の中に **ローカルの HTTP サーバー** を立て、ほかのアプリやスクリプトから、ノートの追加・検索・更新、カードの操作などをできるようにする。

- 作者：**FooSoft**（Alex Yatskov）。ソースは **SourceHut**（`git.sr.ht/~foosoft/anki-connect`）。GitHub の `FooSoft/anki-connect` は移転の案内だけになっている
- アドオンのコード：**`2055492159`**
- **Anki Desktop 26.08 以降** が必要（26.08 と 26.09.3 で試験されている）
- 使い道：辞書の拡張機能（Yomitan など）から単語カードを作る、Obsidian などのノートから Anki のカードを作る、自分のスクリプトでまとめてカードを作る、など

## 入れ方
1. Anki で「**ツール → アドオン → アドオンを取得**」
2. コード **`2055492159`** を入れる
3. Anki を再起動し、使いたいプロファイルを開く

- 使っている間、**Anki を起動したままにする**。リクエストは、開いているプロファイルのコレクションに対して行われる
- macOS では、HTTP サーバーが動き出すと、自動で **App Nap**（裏に回したアプリを休ませる機能）を止める。前のように `defaults write` で止める必要はない
- Windows では、聞かれたらファイアウォールで Anki を許可する

## 2 つの API

| | **API v1**（新しい） | **legacy API**（これまでの） |
| --- | --- | --- |
| 宛先 | `POST http://127.0.0.1:8765/api/v1` | `POST http://127.0.0.1:8765/` |
| 形式 | **JSON-RPC 2.0**（`method` と名前つきの `params`） | `{"action": …, "version": 6, "params": …}` |
| 数 | 94 のメソッド | 122 のアクション |
| ID | 文字列（`"1700000000000"`） | 数値 |
| 答え | `{"jsonrpc":"2.0","id":1,"result":…}` か `error` | `{"result":…,"error":null}` |
| 長い処理 | **操作のハンドル** を返す。`operations.get` で終わったかを問い合わせる | 終わるまで待つ |
| すすめ | **新しく作るならこちら** | 前からあるアプリはこのままでよい（移行しなくてよい） |

- どちらも同じコレクションを操作する
- `api.describe` で、いま動いている Anki で使えるメソッドと制限を調べられる

## 設定
「ツール → アドオン → AnkiConnect → 設定」で変える。サーバーの設定を変えたら Anki を再起動する。

| 設定 | 初期値 | 意味 |
| --- | --- | --- |
| `webBindAddress` | `127.0.0.1` | 待ち受けるアドレス。初期値は **自分のパソコンからだけ** |
| `webBindPort` | `8765` | ポート |
| `apiKey` | `null` | 認証のかぎ。`null` なら認証なし |
| `webCorsOriginList` | `["http://localhost"]` | ブラウザーから使ってよいオリジン |
| `ignoreOriginList` | `[]` | 許可を聞く画面を出さないオリジン |
| `apiLogPath` | `null` | API のログの置き場 |

- `apiKey` を決めたら、v1 は `Authorization: Bearer <かぎ>` のヘッダー、legacy は JSON の `key` に入れる
- ブラウザー（拡張機能やウェブページ）からは、かぎとは別に **オリジンの許可** が要る。`access.requestPermission`（legacy は `requestPermission`）で許可をもらう
- `webBindAddress` を `0.0.0.0` にするとほかのパソコンからも使えてしまう。そうするなら `apiKey` を必ず決める

## はじめてのリクエスト

v1：

```sh
curl --request POST http://127.0.0.1:8765/api/v1 \
  --header 'Content-Type: application/json' \
  --data '{"jsonrpc":"2.0","id":1,"method":"decks.list","params":{}}'
```

```json
{"jsonrpc":"2.0","id":1,"result":[{"id":"1","name":"Default","kind":"normal","presetId":"1"}]}
```

legacy：

```sh
curl --request POST http://127.0.0.1:8765/ \
  --header 'Content-Type: application/json' \
  --data '{"action":"deckNames","version":6,"params":{}}'
```

```json
{"result":["Default"],"error":null}
```

- legacy で `version` を省くと、**version 4** として扱われ、答えの形が変わる（`result` の包みがない）。**いつも `"version": 6` を書く**

## ノートを追加する

v1 の `notes.create`：

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "notes.create",
  "params": {
    "noteType": {"name": "Basic"},
    "deck": {"name": "Default"},
    "fields": {"Front": "cat", "Back": "猫"},
    "tags": ["vocabulary"]
  }
}
```

- `duplicates` で、重複をどう扱うかを決められる。初期値は **重複を許さない**（`allow: false`、コレクション全体で判定）
- 中身の空いた問題（表が空のカード）は、初期値で拒否される（`rejectEmptyQuestions: true`）
- まとめて作るなら `notes.createMany`。`atomic: true` にすると、1 つでも失敗したら全部取り消す

legacy の `addNote`（音声もつける例）：

```json
{
  "action": "addNote",
  "version": 6,
  "params": {
    "note": {
      "deckName": "Default",
      "modelName": "Basic",
      "fields": {"Front": "cat"},
      "audio": [{"filename": "cat.mp3", "data": "eHl6", "fields": ["Back"]}],
      "tags": ["vocabulary"]
    }
  }
}
```

- 答えはノートの ID（数値）。`Back` に `[sound:cat.mp3]` が入る（`data` は base64 の音声。例の値はダミー）
- legacy では、ノートタイプを `modelName` とよぶ（Anki の古い名前「model」のなごり）

## v1 のメソッドの種類

| 種類 | 主なメソッド |
| --- | --- |
| 調べる・まとめて実行 | `api.describe`、`api.execute` |
| アクセス・プロファイル | `access.requestPermission`、`profiles.list`・`getActive`・`switch` |
| コレクション | `collection.get`・`sync`（AnkiWeb と同期）・`refresh`・`checkIntegrity`・`undo` |
| **ノート** | `notes.get`・`getMany`・**`search`**・`validate`・**`create`**・**`createMany`**・**`update`**・`delete`・`convert`・`findEmpty` |
| タグ | `tags.list`・`add`・`remove`・`replace`・`deleteUnused` |
| カード | `cards.get`・`search`・`render`・`move`・`setSuspended`・`setFlags` |
| スケジュール | `scheduling.get`・`getQueue`・`predict`・`getDue`・`answer`・`repositionNewCards`・`reset`・`setDueDate` |
| デッキ・プリセット | `decks.list`・`get`・`create`・`update`・`delete`・`getCounts`、`deckPresets.*` |
| ノートタイプ | `noteTypes.list`・`get`・`create`・`update`・`editStructure` ほか |
| メディア | `media.store`・`get`・`list`・`delete`・`getDirectory` |
| 復習の記録・統計 | `reviews.list`、`statistics.getToday`・`getSummary` ほか |
| パッケージ | `packages.import`・`export`（.apkg） |
| 画面の操作 | `browser.open`・`select`、`editors.openNote`・`openAdd`、`reviewer.showAnswer`・`answer` ほか |
| 長い処理 | `operations.get`・`cancel` |

- 検索の `query` は、Anki の検索の書き方そのまま（`deck:英単語 tag:動詞 is:due` など）。`notes.search` は 1 回に最大 1,000 件で、続きは `cursor` で取る

## エラー
- v1 は、結果もエラーも **HTTP 200** で返す（JSON-RPC の決まり）。ただし、かぎがちがえば **401**、オリジンが許されなければ **403**、POST でなければ **405**、大きすぎれば **413**（本文は空）
- エラーは、文の中身ではなく `error.code` か `error.data.type` で見分ける

| コード | 種類 | 意味 |
| --- | --- | --- |
| 1001 | `notFound` | 指定したものがない |
| 1002 | `validationFailed` | 中身の検査に通らない（重複など） |
| 1003 | `editorConflict` | 開いている編集画面がじゃまをしている。閉じてからやり直す |
| 1004 | `collectionUnavailable` | コレクションが開いていない |
| 1013 | `invalidSearch` | 検索の書き方がまちがっている |

- **書きこみの答えが返ってこなかったとき、自動でやり直さない**（すでに書きこまれているかもしれない。リクエストの ID は二重実行を防がない）

## 例：このボールトの漢字ノートから、Anki のカードを作る

[[壇]]・[[嗇]] などの漢字ノート（`japanese/漢字/`）の frontmatter から、「表：字、裏：読み・倉頡」のカードを作るスクリプト。v1 の `call` 関数は、AnkiConnect の資料の Python の例のとおり。

```python
import itertools, json, pathlib, urllib.request
import yaml  # PyYAML

ENDPOINT = "http://127.0.0.1:8765/api/v1"
ids = itertools.count(1)

def call(method, **params):
    rid = next(ids)
    body = {"jsonrpc": "2.0", "id": rid, "method": method, "params": params}
    req = urllib.request.Request(ENDPOINT, json.dumps(body).encode(),
                                 headers={"Content-Type": "application/json"}, method="POST")
    with urllib.request.urlopen(req) as res:
        reply = json.load(res)
    if "error" in reply:
        raise RuntimeError(reply["error"])
    return reply["result"]

def frontmatter(path):
    text = path.read_text(encoding="utf-8")
    return yaml.safe_load(text.split("---")[1]) if text.startswith("---") else {}

notes = []
for p in sorted(pathlib.Path("japanese/漢字").glob("*.md")):
    fm = frontmatter(p)
    back = "<br>".join([
        "音：" + "・".join(fm.get("音読み") or []),
        "訓：" + "・".join(fm.get("訓読み") or []),
        f"倉頡：{fm.get('倉頡', '')}（{fm.get('倉頡コード', '')}）",
    ])
    notes.append({"noteType": {"name": "Basic"}, "deck": {"name": "漢字"},
                  "fields": {"Front": fm["字"], "Back": back}, "tags": ["obsidian"]})

call("decks.create", name="漢字")          # デッキがすでにあるときの動きは未確認
print(call("notes.createMany", notes=notes))  # 重複は初期値でエラーになる
```

- **このスクリプトは、Anki を動かして試していない**（このパソコンに Anki が入っていない）。frontmatter を読む部分だけは、ボールトのファイルで動くことを確かめた（「嗇 音：ショク 訓：おしむ・やぶさか 倉頡：土人田口（GOWR）」などが出る）
- `decks.create` の引数が `name` だけであることは、資料で確かめた。`notes.createMany` の `notes` の 1 つ 1 つは、`notes.create` と同じ形（NoteInput）

## Obsidian から使う
- Obsidian のプラグイン（「Obsidian_to_Anki」など）は、AnkiConnect を通してノートからカードを作る
- そのときは、`webCorsOriginList` に Obsidian のオリジン（`app://obsidian.md`）を足す必要がある、とプラグインの説明にある（記憶による。プラグインの説明で確かめること）

## 押さえどころ
- AnkiConnect は、Anki の中に **ローカルの HTTP API**（`127.0.0.1:8765`）を立てるアドオン。コードは **`2055492159`**
- いまは **API v1**（JSON-RPC 2.0、`/api/v1`）と **legacy API**（`action` と `version: 6`）の 2 つ。新しく作るなら v1
- **Anki 26.08 以降** が必要。使う間は Anki を起動したままにする
- ノートの追加は v1 の `notes.create`／`createMany`、legacy の `addNote`／`addNotes`
- ほかのパソコンから使えるようにするなら、`apiKey` を決める

## 出典
- [AnkiConnect の README（SourceHut）](https://git.sr.ht/~foosoft/anki-connect/blob/master/README.md)：必要な Anki の版、入れ方、App Nap、設定と初期値、はじめてのリクエスト、v1 と legacy の違い、メソッドの数
- [API_V1.md](https://git.sr.ht/~foosoft/anki-connect/blob/master/API_V1.md)：JSON-RPC の形式、認証、HTTP の状態コード、エラーコード、`notes.create`・`notes.createMany`・`notes.search`・`media.store`、重複の扱い、Python の例、メソッドの一覧
- [API_LEGACY.md](https://git.sr.ht/~foosoft/anki-connect/blob/master/API_LEGACY.md)：`addNote` の例、`version` を省いたときの扱い、認証の `key`
- [plugin/config.json](https://git.sr.ht/~foosoft/anki-connect/blob/master/plugin/config.json)：`apiLogPath` をふくむ設定の初期値
- [GitHub：FooSoft/anki-connect](https://github.com/FooSoft/anki-connect)：SourceHut へ移転した旨
- 作者名（Alex Yatskov）、Yomitan・Obsidian_to_Anki での使われ方、`app://obsidian.md`：一般的な知識（ウェブでの確認はしていない）
