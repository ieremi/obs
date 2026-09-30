---
aliases:
  - TCP のシーケンス番号
  - sequence number
date: 2026-09-26
tags:
  - ネットワーク
  - ネットワーク/TCP
related:
  - "[[TCPウィンドウ]]"
  - "[[TCPとUDP]]"
---

# TCP のシーケンス番号

TCP はデータをバイト列として管理し、sequence number で位置を示す。

`ACK 1501` は基本的に「1500まで受信したので、次は1501から欲しい」という意味。

観察：

```bash
sudo tcpdump -nn -S tcp port 80
```

別端末：

```bash
curl http://example.com/
```

シーケンス番号により、順序の入れ替わりや消失があっても元のバイト列を復元できる。
