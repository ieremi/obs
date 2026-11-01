---
tags: [プログラミング, セキュリティ, パスワード, ソフトウェア]
aliases: [1Password, ワンパスワード, 1password, op, 1Password CLI, AgileBits, パスワードマネージャー]
date: 2026-11-01
---
# 1Password

**カナダの 1Password 社（旧名 AgileBits）が作る、有料のパスワードマネージャー。** パスワード・パスキー・クレジットカード・メモ・SSH の鍵などを暗号化して保存し、どの端末からでも使えるように同期する。

| 項目 | 内容 |
| --- | --- |
| 会社 | 1Password（カナダ、トロント）。2006 年に AgileBits として始まった |
| 対応 | Windows・macOS・**Linux**・iOS・Android、ブラウザーの拡張機能（Chrome・Firefox・Safari・Edge など） |
| 料金 | **サブスクリプションだけ**（無料の版はない。14 日の試用あり） |
| 保存のしかた | 1Password のサーバーに **暗号化したまま** 置く（クラウド型） |
| 競合 | Bitwarden（オープンソース、無料の版あり）、KeePass 系（ファイルを自分で持つ）、Apple の「パスワード」、Google パスワードマネージャー、Dashlane など |

## 料金（個人向け）
2026 年 3 月 27 日以降の更新から値上げした。

| プラン | 値上げ前 | 値上げ後 |
| --- | --- | --- |
| **Individual**（1 人） | 年 35.88 ドル（月 2.99 ドル） | **年 47.88 ドル（月 3.99 ドル）** |
| **Families**（5 人まで） | 年 59.88 ドル（月 4.99 ドル） | **年 71.88 ドル（月 5.99 ドル）** |

- 会社向けに Teams・Business・Enterprise がある
- 日本円の値段は、アプリやストアによってちがう

## しくみの言葉

| 言葉 | 意味 |
| --- | --- |
| **アカウントパスワード**（旧名 マスターパスワード） | 自分で決めて、自分だけが覚えるパスワード |
| **Secret Key**（シークレットキー。旧名 Account Key） | アカウントを作るとき **端末の中で作られる** 鍵。`A3-ASWWYB-798JRYLJVD4-23DC2-86TVM-H43EB` のような形で、ランダムな 26 文字（約 128 ビット）。1Password 社には送られない |
| **Emergency Kit**（緊急キット） | Secret Key などを書いた PDF。**印刷して保管する**。Secret Key とすべての端末をなくすと、だれにも開けなくなる |
| **保管庫**（vault） | アイテムを入れる箱。家族や同僚と **保管庫ごと共有** できる |
| **アイテム** | 1 つのログイン情報、カード、メモ、SSH の鍵など |
| **Watchtower** | 漏れたパスワード、使い回し、弱いパスワード、2 要素認証が使えるのに使っていないサイトなどを知らせる |
| **トラベルモード** | 国境を越えるときなどに、指定した保管庫だけを残して、ほかを端末から消しておく |

## 安全のしくみ（2 つの秘密）
1Password の特徴は、**アカウントパスワードと Secret Key の 2 つを組み合わせて鍵を作る** こと（Two-Secret Key Derivation、2SKD）。

1. アカウントパスワードを **PBKDF2-HMAC-SHA256（65 万回）** でゆっくりハッシュする
2. それと Secret Key（HKDF にかけたもの）を XOR して、**Account Unlock Key（AUK）** を作る
3. AUK で自分の **秘密鍵** を開き、秘密鍵で **保管庫の鍵**（vault key）を開き、保管庫の鍵で **アイテム** を開く

- 暗号：アイテムなどは **AES-256-GCM**、公開鍵は **RSA-OAEP（2048 ビット）**
- サインインには **SRP**（Secure Remote Password）を使う。パスワードそのものも、パスワードから作った値も、**サーバーに送らずに** 「知っていること」を証明する
- そのため、**サーバーのデータがまるごと盗まれても**、Secret Key がない攻撃者は、アカウントパスワードを総当たりで当てることができない。弱いパスワードでも守られる、というのが 1Password の説明
- 逆に、**Secret Key とアカウントパスワードを両方なくしたら、1Password 社にも戻せない**（家族プランや会社のプランでは、管理者が「回復」できる）
- いまは、パスキーや SSO（会社のアカウント）でロックを解く方法もある

## 開発者向けの機能

### 1Password CLI（`op`）
Linux なら APT・DNF などで `1password-cli` を入れる。デスクトップアプリの「設定 → 開発者 → 1Password CLI と連携」をオンにすると、指紋やシステムの認証で `op` が使える（Linux では PolKit が要る）。

```sh
sudo apt install 1password-cli
op --version
op vault list                       # はじめて使うと認証を求められる
op signin                           # アカウントが複数あるとき
```

秘密は **シークレット参照**（`op://保管庫/アイテム/[セクション/]フィールド`）で指す。

```sh
# 1 つ読む
op read op://development/GitHub/credentials/personal_token

# .env に平文を書かず、参照を書いておく
cat node.env
# DB_USER="op://app-dev/db/user"
# DB_PASSWORD="op://app-dev/db/password"
op run --env-file="./node.env" -- node app.js   # 実行のあいだだけ環境変数に入る

# 設定ファイルのテンプレートの参照を、本当の値に置きかえる
op inject --in-file config.yml.tpl --out-file config.yml
```

- `op run` は、子プロセスの出力に秘密が出てくると、隠して表示する
- **シークレット参照なら、`.env` や設定ファイルを git に入れても秘密は漏れない**

### SSH エージェント
- 1Password に **SSH の鍵** を入れておき、1Password を ssh-agent として使える。秘密鍵は 1Password から出ず、使うたびに確認が出る
- ~/.ssh/config に、1Password のエージェントのソケットを書く：

  ```text
  Host *
    IdentityAgent ~/.1password/agent.sock
  ```

- 同じ鍵で **git のコミットに署名** できる（git 2.34 以上。アプリの鍵の画面の「Configure」で、`~/.gitconfig` に書く内容が出る）。GitHub で「Verified」になる
- Linux では PolKit が要り、**Snap 版ではエージェントが動かない**

### そのほか
- **Service Account**：CI など人のいない所から使うためのアカウント（トークンで `op` を動かす）
- **Connect サーバー**：自分のサーバーに置く、REST API の中継。Kubernetes・Terraform などから使う

## Bitwarden とのちがい（よく比べられる）

| | 1Password | Bitwarden |
| --- | --- | --- |
| 料金 | 有料のみ | 無料の版あり。有料も安い |
| ソースコード | 公開していない | **オープンソース**。サーバーを自分で立てられる（Vaultwarden など） |
| 鍵 | アカウントパスワード＋**Secret Key** | マスターパスワードだけ（＋2 要素認証） |
| 使いやすさ | アプリの出来がよいと評判 | 機能は十分、見た目はやや素朴 |

## 押さえどころ
- 1Password は、カナダの会社の **有料（サブスクリプション）** のパスワードマネージャー。Linux にも公式アプリがある
- **アカウントパスワード＋Secret Key** の 2 つから鍵を作り、**サーバーには暗号化したデータしかない**。Emergency Kit は印刷して保管する
- 2026 年 3 月から値上げ：個人 月 3.99 ドル、家族 月 5.99 ドル（年払い）
- 開発では、`op`（シークレット参照 `op://…`、`op run`・`op inject`）と **SSH エージェント**（git の署名も）が便利

## 出典
- [1Password Security Design White Paper（Release 0.5.3、2026 年 10 月 28 日）](https://agilebits.github.io/security-design/1Password_Security_Design.pdf)：Secret Key の形と長さ、旧名 Account Key、Emergency Kit、PBKDF2-HMAC-SHA256 65 万回と HKDF の XOR、SRP、AES-256-GCM と RSA-OAEP 2048 ビット、保管庫の鍵のしくみ、パスキー・SSO での解錠、Connect と Service Account
- [1Password CLI：Get started](https://www.1password.dev/cli/get-started/)：Linux での入れ方、アプリとの連携、PolKit、`op vault list`・`op signin`
- [1Password CLI：Secret references](https://www.1password.dev/cli/secret-references)：`op://` の書き方、`op read`・`op run`・`op inject` の例
- [MacRumors（2026 年 2 月 24 日）](https://www.macrumors.com/2026/02/24/1password-march-price-increase/)：値上げの前とあとの値段、3 月 27 日から
- [1Password ブログ：Git commit signing](https://1password.com/blog/git-commit-signing)、[コミュニティの回答](https://1password.community/discussion/134747/ssh-agent-on-linux-sign-and-send-pubkey-agent-refused-operation)：git 2.34 以上、Configure、Linux で PolKit が要り Snap 版では動かないこと（検索結果の要約による）
- 会社の歴史（トロント、2006 年、AgileBits）、Watchtower、トラベルモード、`agent.sock` のパス、`op run` が出力を隠すこと、Bitwarden との比べ：一般的な知識（ウェブでの確認はしていない）

関連：[[個人情報を自社のDBに持たない設計]]、[[Synology]]
