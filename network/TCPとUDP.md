---
aliases:
  - TCP と UDP
date: 2026-09-29
tags:
  - ネットワーク
  - ネットワーク/TCP
  - ネットワーク/UDP
related:
  - "[[TCPシーケンス番号]]"
---

# TCP と UDP

UDP 自体は到達確認、順序保証、再送を行わない。ヘッダも比較的単純。

DNS の UDP 通信を観察：

```bash
sudo tcpdump -n udp port 53
dig example.com
```

UDP 上でもアプリケーション層で信頼性を実装できる。QUIC が代表例。
