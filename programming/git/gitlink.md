---
aliases:
  - gitlink
  - Git の gitlink
date: 2026-10-09
tags:
  - プログラミング
  - プログラミング/Git
related:
  - "[[Gitのサブモジュール]]"
---

# gitlink

gitlink は、Git の tree の中で**別リポジトリのコミット**を指すエントリ。サブモジュールの実体はこれ。

普通のファイルは blob、ディレクトリは tree を指すが、gitlink はモード `160000`、種類 `commit` で、サブモジュール側のコミットハッシュだけを記録する。

$$
\boxed{\text{gitlink}=\text{パス}+\text{コミットハッシュ}\ (\text{mode } 160000)}
$$

親リポジトリ（superproject）はサブモジュールの中身を持たない。「このパスには、あのリポジトリのこのコミットを置く」という指定だけを持つ。

観察：

```bash
git init sub && git -C sub commit --allow-empty -m init
git init super && cd super
git -c protocol.file.allow=always submodule add ../sub sub
git ls-files -s
```

（ローカルパスからの追加は、最近の Git では `protocol.file.allow=always` がないと拒否される。）

出力（ハッシュは例）：

```text
100644 1a2b3c... 0	.gitmodules
160000 9f8e7d... 0	sub
```

コミット後は `git ls-tree HEAD` でも同じように見える：

```text
160000 commit 9f8e7d...	sub
```

| 役割 | 置き場所 |
| --- | --- |
| どのコミットか | gitlink（tree のエントリ） |
| どこから取得するか（URL） | `.gitmodules` |
| ローカルの設定 | `.git/config` |

サブモジュール側で別のコミットに移ると、親の `git diff` には gitlink の差分として出る：

```text
-Subproject commit 9f8e7d...
+Subproject commit 4c5d6e...
```

親で `git add sub` してコミットすると、gitlink の指すハッシュが更新される。

注意：別のリポジトリが入ったディレクトリを `git add` すると、`.gitmodules` なしの gitlink だけができる（`adding embedded git repository` という警告が出る）。この状態では clone した側が中身を取得できない。
