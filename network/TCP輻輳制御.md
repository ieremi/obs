---
aliases:
  - TCP の輻輳制御
  - congestion control
  - cwnd
date: 2026-09-28
tags:
  - ネットワーク
  - ネットワーク/TCP
related:
  - "[[TCPウィンドウ]]"
---

# TCP の輻輳制御

flow control は受信側を守る。congestion control はネットワークの混雑を抑える。

送信側は congestion window（cwnd）を持ち、ACK が順調なら増やし、損失などから混雑を推定すれば減らす。

実際に一度に送れる量は概ね、

$$
\boxed{\min(rwnd,cwnd)}
$$

```bash
ss -ti
```
