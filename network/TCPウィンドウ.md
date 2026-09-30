---
aliases:
  - TCP のウィンドウ
  - フロー制御
  - flow control
date: 2026-09-27
tags:
  - ネットワーク
  - ネットワーク/TCP
related:
  - "[[TCP輻輳制御]]"
  - "[[TCPシーケンス番号]]"
---

# TCP のウィンドウ

受信側は window により、あと何 byte 受け取れるかを送信側へ知らせる。受信バッファが満杯なら window は 0 になり、送信側はいったん送信を止める。

これは flow control（受信側を守る仕組み）。

congestion control（ネットワークの混雑を抑える仕組み）とは別。

```bash
ss -tin
```
