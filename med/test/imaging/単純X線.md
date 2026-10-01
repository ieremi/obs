---
name: 単純X線
name_en: plain radiography
aliases:
  - 単純 X 線
  - 単純X線撮影
  - X 線写真
  - レントゲン
  - plain radiograph
  - X-ray
date: 2026-10-01
tags:
  - test
  - test/imaging
---

# 単純 X 線撮影

## 概要
- 造影剤を使わずに、体に X 線を当て、**通り抜けた X 線** を検出器で受けて画像にする検査
- 体の厚み方向の情報が **1 枚の平面に重なった投影像** になる
- 速く、安く、どこでも撮れる。胸部・腹部・骨の検査の第一歩

## 原理：X 線の減衰

厚さ $dx$ の物質を通ると、X 線の強さ $I$ は、そのときの強さと厚さに比例して減る。比例定数を **線減弱係数** $\mu$ とすると、

$$
dI=-\mu I\,dx
\quad\Longrightarrow\quad
\boxed{I=I_0\,e^{-\mu x}}
$$

いくつかの組織を順に通るときは、指数の部分が足し合わされる。

$$
I=I_0\exp\left(-\sum_i\mu_ix_i\right)
$$

$\mu$ は物質の密度 $\rho$ と、質量減弱係数 $\mu/\rho$ の積である。強さが半分になる厚さ（半価層）は、$e^{-\mu x}=1/2$ より、

$$
x_{1/2}=\frac{\log2}{\mu}
$$

最後に、約 60 keV の X 線で、水（$\mu/\rho=0.206$ cm²/g、$\rho=1.00$）と皮質骨（$\mu/\rho=0.315$、$\rho=1.92$）の値を代入すると、

$$
\mu_\text{水}\approx0.21\ /\text{cm},\quad x_{1/2}\approx3.4\ \text{cm};\qquad
\mu_\text{骨}\approx0.60\ /\text{cm},\quad x_{1/2}\approx1.1\ \text{cm}
$$

<svg viewBox="0 0 560 260" width="560" role="img" aria-label="X 線の透過率 I/I₀ = exp(−μx) と厚さ x の関係（約 60 keV）。μ は肺（含気）約 0.05、脂肪約 0.19、水・軟部組織約 0.21、皮質骨約 0.60 /cm。骨は数 cm で X 線をほとんど通さない" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <g stroke="currentColor" stroke-width="1" opacity="0.18">
    <path d="M70 162.5 H530"/>
    <path d="M70 115.0 H530"/>
    <path d="M70 67.5 H530"/>
    <path d="M70 20.0 H530"/>
  </g>
  <path d="M70 210.0 H530 M70 20 V210" stroke="currentColor" stroke-width="1" opacity="0.5" fill="none"/>
  <g fill="currentColor" font-size="12" opacity="0.75">
    <text x="62" y="214.0" text-anchor="end">0</text>
    <text x="62" y="166.5" text-anchor="end">0.25</text>
    <text x="62" y="119.0" text-anchor="end">0.5</text>
    <text x="62" y="71.5" text-anchor="end">0.75</text>
    <text x="62" y="24.0" text-anchor="end">1</text>
    <text x="70.0" y="226" text-anchor="middle">0</text>
    <text x="162.0" y="226" text-anchor="middle">2</text>
    <text x="254.0" y="226" text-anchor="middle">4</text>
    <text x="346.0" y="226" text-anchor="middle">6</text>
    <text x="438.0" y="226" text-anchor="middle">8</text>
    <text x="530.0" y="226" text-anchor="middle">10</text>
    <text x="300" y="244" text-anchor="middle">厚さ x（cm）</text>
    <text x="16" y="115" text-anchor="middle" transform="rotate(-90 16 115)">透過率 I/I₀</text>
  </g>
  <polyline points="70.0,20.0 73.8,20.8 77.7,21.7 81.5,22.5 85.3,23.3 89.2,24.1 93.0,25.0 96.8,25.8 100.7,26.6 104.5,27.4 108.3,28.2 112.2,29.0 116.0,29.8 119.8,30.6 123.7,31.4 127.5,32.2 131.3,33.0 135.2,33.7 139.0,34.5 142.8,35.3 146.7,36.1 150.5,36.8 154.3,37.6 158.2,38.4 162.0,39.1 165.8,39.9 169.7,40.6 173.5,41.4 177.3,42.1 181.2,42.8 185.0,43.6 188.8,44.3 192.7,45.0 196.5,45.8 200.3,46.5 204.2,47.2 208.0,47.9 211.8,48.6 215.7,49.4 219.5,50.1 223.3,50.8 227.2,51.5 231.0,52.2 234.8,52.9 238.7,53.6 242.5,54.2 246.3,54.9 250.2,55.6 254.0,56.3 257.8,57.0 261.7,57.6 265.5,58.3 269.3,59.0 273.2,59.7 277.0,60.3 280.8,61.0 284.7,61.6 288.5,62.3 292.3,62.9 296.2,63.6 300.0,64.2 303.8,64.9 307.7,65.5 311.5,66.1 315.3,66.8 319.2,67.4 323.0,68.0 326.8,68.7 330.7,69.3 334.5,69.9 338.3,70.5 342.2,71.1 346.0,71.8 349.8,72.4 353.7,73.0 357.5,73.6 361.3,74.2 365.2,74.8 369.0,75.4 372.8,76.0 376.7,76.6 380.5,77.1 384.3,77.7 388.2,78.3 392.0,78.9 395.8,79.5 399.7,80.0 403.5,80.6 407.3,81.2 411.2,81.8 415.0,82.3 418.8,82.9 422.7,83.4 426.5,84.0 430.3,84.6 434.2,85.1 438.0,85.7 441.8,86.2 445.7,86.8 449.5,87.3 453.3,87.8 457.2,88.4 461.0,88.9 464.8,89.4 468.7,90.0 472.5,90.5 476.3,91.0 480.2,91.6 484.0,92.1 487.8,92.6 491.7,93.1 495.5,93.6 499.3,94.1 503.2,94.7 507.0,95.2 510.8,95.7 514.7,96.2 518.5,96.7 522.3,97.2 526.2,97.7 530.0,98.2" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round" stroke-dasharray="3 2"><title>肺（含気）：μ ≈ 0.053 /cm</title></polyline>
  <polyline points="70.0,20.0 73.8,23.0 77.7,25.9 81.5,28.8 85.3,31.7 89.2,34.5 93.0,37.2 96.8,39.9 100.7,42.6 104.5,45.2 108.3,47.8 112.2,50.4 116.0,52.9 119.8,55.3 123.7,57.8 127.5,60.2 131.3,62.5 135.2,64.8 139.0,67.1 142.8,69.4 146.7,71.6 150.5,73.7 154.3,75.9 158.2,78.0 162.0,80.1 165.8,82.1 169.7,84.1 173.5,86.1 177.3,88.0 181.2,90.0 185.0,91.8 188.8,93.7 192.7,95.5 196.5,97.3 200.3,99.1 204.2,100.8 208.0,102.6 211.8,104.2 215.7,105.9 219.5,107.5 223.3,109.1 227.2,110.7 231.0,112.3 234.8,113.8 238.7,115.3 242.5,116.8 246.3,118.3 250.2,119.7 254.0,121.1 257.8,122.5 261.7,123.9 265.5,125.3 269.3,126.6 273.2,127.9 277.0,129.2 280.8,130.5 284.7,131.7 288.5,132.9 292.3,134.2 296.2,135.3 300.0,136.5 303.8,137.7 307.7,138.8 311.5,139.9 315.3,141.0 319.2,142.1 323.0,143.2 326.8,144.2 330.7,145.3 334.5,146.3 338.3,147.3 342.2,148.3 346.0,149.2 349.8,150.2 353.7,151.1 357.5,152.1 361.3,153.0 365.2,153.9 369.0,154.7 372.8,155.6 376.7,156.5 380.5,157.3 384.3,158.1 388.2,158.9 392.0,159.7 395.8,160.5 399.7,161.3 403.5,162.1 407.3,162.8 411.2,163.6 415.0,164.3 418.8,165.0 422.7,165.7 426.5,166.4 430.3,167.1 434.2,167.8 438.0,168.4 441.8,169.1 445.7,169.7 449.5,170.4 453.3,171.0 457.2,171.6 461.0,172.2 464.8,172.8 468.7,173.4 472.5,174.0 476.3,174.5 480.2,175.1 484.0,175.6 487.8,176.2 491.7,176.7 495.5,177.2 499.3,177.7 503.2,178.3 507.0,178.7 510.8,179.2 514.7,179.7 518.5,180.2 522.3,180.7 526.2,181.1 530.0,181.6" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round" stroke-dasharray="8 4"><title>脂肪：μ ≈ 0.19 /cm</title></polyline>
  <polyline points="70.0,20.0 73.8,23.3 77.7,26.5 81.5,29.7 85.3,32.8 89.2,35.9 93.0,38.9 96.8,41.9 100.7,44.8 104.5,47.7 108.3,50.5 112.2,53.3 116.0,56.0 119.8,58.7 123.7,61.3 127.5,63.9 131.3,66.4 135.2,68.9 139.0,71.3 142.8,73.7 146.7,76.1 150.5,78.4 154.3,80.7 158.2,83.0 162.0,85.2 165.8,87.3 169.7,89.5 173.5,91.5 177.3,93.6 181.2,95.6 185.0,97.6 188.8,99.6 192.7,101.5 196.5,103.4 200.3,105.2 204.2,107.0 208.0,108.8 211.8,110.6 215.7,112.3 219.5,114.0 223.3,115.6 227.2,117.3 231.0,118.9 234.8,120.5 238.7,122.0 242.5,123.6 246.3,125.1 250.2,126.5 254.0,128.0 257.8,129.4 261.7,130.8 265.5,132.2 269.3,133.5 273.2,134.8 277.0,136.2 280.8,137.4 284.7,138.7 288.5,139.9 292.3,141.1 296.2,142.3 300.0,143.5 303.8,144.7 307.7,145.8 311.5,146.9 315.3,148.0 319.2,149.1 323.0,150.1 326.8,151.2 330.7,152.2 334.5,153.2 338.3,154.2 342.2,155.2 346.0,156.1 349.8,157.0 353.7,158.0 357.5,158.9 361.3,159.7 365.2,160.6 369.0,161.5 372.8,162.3 376.7,163.1 380.5,164.0 384.3,164.8 388.2,165.5 392.0,166.3 395.8,167.1 399.7,167.8 403.5,168.5 407.3,169.3 411.2,170.0 415.0,170.7 418.8,171.4 422.7,172.0 426.5,172.7 430.3,173.3 434.2,174.0 438.0,174.6 441.8,175.2 445.7,175.8 449.5,176.4 453.3,177.0 457.2,177.6 461.0,178.1 464.8,178.7 468.7,179.2 472.5,179.7 476.3,180.3 480.2,180.8 484.0,181.3 487.8,181.8 491.7,182.3 495.5,182.8 499.3,183.2 503.2,183.7 507.0,184.2 510.8,184.6 514.7,185.0 518.5,185.5 522.3,185.9 526.2,186.3 530.0,186.7" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"><title>水・軟部組織：μ ≈ 0.21 /cm</title></polyline>
  <polyline points="70.0,20.0 73.8,29.3 77.7,38.1 81.5,46.5 85.3,54.4 89.2,62.0 93.0,69.2 96.8,76.1 100.7,82.6 104.5,88.9 108.3,94.8 112.2,100.4 116.0,105.7 119.8,110.8 123.7,115.6 127.5,120.3 131.3,124.6 135.2,128.8 139.0,132.8 142.8,136.5 146.7,140.1 150.5,143.5 154.3,146.8 158.2,149.8 162.0,152.8 165.8,155.6 169.7,158.2 173.5,160.7 177.3,163.1 181.2,165.4 185.0,167.6 188.8,169.7 192.7,171.6 196.5,173.5 200.3,175.3 204.2,177.0 208.0,178.6 211.8,180.1 215.7,181.6 219.5,183.0 223.3,184.3 227.2,185.5 231.0,186.7 234.8,187.9 238.7,188.9 242.5,190.0 246.3,191.0 250.2,191.9 254.0,192.8 257.8,193.6 261.7,194.4 265.5,195.2 269.3,195.9 273.2,196.6 277.0,197.2 280.8,197.9 284.7,198.4 288.5,199.0 292.3,199.5 296.2,200.1 300.0,200.5 303.8,201.0 307.7,201.4 311.5,201.9 315.3,202.3 319.2,202.6 323.0,203.0 326.8,203.3 330.7,203.7 334.5,204.0 338.3,204.3 342.2,204.5 346.0,204.8 349.8,205.1 353.7,205.3 357.5,205.5 361.3,205.7 365.2,206.0 369.0,206.2 372.8,206.3 376.7,206.5 380.5,206.7 384.3,206.9 388.2,207.0 392.0,207.2 395.8,207.3 399.7,207.4 403.5,207.5 407.3,207.7 411.2,207.8 415.0,207.9 418.8,208.0 422.7,208.1 426.5,208.2 430.3,208.3 434.2,208.4 438.0,208.4 441.8,208.5 445.7,208.6 449.5,208.7 453.3,208.7 457.2,208.8 461.0,208.8 464.8,208.9 468.7,209.0 472.5,209.0 476.3,209.1 480.2,209.1 484.0,209.1 487.8,209.2 491.7,209.2 495.5,209.3 499.3,209.3 503.2,209.3 507.0,209.4 510.8,209.4 514.7,209.4 518.5,209.5 522.3,209.5 526.2,209.5 530.0,209.5" fill="none" stroke="currentColor" stroke-width="3" stroke-linejoin="round"><title>骨（皮質骨）：μ ≈ 0.6 /cm</title></polyline>
  <text x="530.0" y="90.2" fill="currentColor" font-size="13" text-anchor="end" opacity="1">肺（含気）</text>
  <text x="530.0" y="173.6" fill="currentColor" font-size="13" text-anchor="end" opacity="1">脂肪</text>
  <text x="520.8" y="199.6" fill="currentColor" font-size="13" text-anchor="end" opacity="1">水・軟部組織</text>
  <text x="186.4" y="153.0" fill="currentColor" font-size="13" text-anchor="start" opacity="1">骨（皮質骨）</text>
</svg>

骨は水の約 3 倍 X 線を止めるので白く写り、空気をふくむ肺はほとんど止めないので黒く写る。

## 5 つの基本濃度

<svg viewBox="0 0 580 165" width="580" role="img" aria-label="単純 X 線写真の 5 つの基本濃度。X 線を通しやすい順に、空気（黒）、脂肪（濃い灰色）、軟部組織・水（灰色）、骨・石灰化（白に近い）、金属（真っ白）" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <g><title>空気：肺・腸管ガス</title><rect x="20" y="20" width="104" height="56" rx="4" fill="#050505" stroke="currentColor" stroke-opacity="0.5"/></g>
  <text x="72.0" y="96" fill="currentColor" font-size="13" text-anchor="middle">空気</text>
  <text x="72.0" y="113" fill="currentColor" font-size="11" text-anchor="middle" opacity="0.75">肺・腸管ガス</text>
  <g><title>脂肪：皮下脂肪</title><rect x="132" y="20" width="104" height="56" rx="4" fill="#4a4a4a" stroke="currentColor" stroke-opacity="0.5"/></g>
  <text x="184.0" y="96" fill="currentColor" font-size="13" text-anchor="middle">脂肪</text>
  <text x="184.0" y="113" fill="currentColor" font-size="11" text-anchor="middle" opacity="0.75">皮下脂肪</text>
  <g><title>軟部組織・水：心臓・筋肉・血液</title><rect x="244" y="20" width="104" height="56" rx="4" fill="#8c8c8c" stroke="currentColor" stroke-opacity="0.5"/></g>
  <text x="296.0" y="96" fill="currentColor" font-size="13" text-anchor="middle">軟部組織・水</text>
  <text x="296.0" y="113" fill="currentColor" font-size="11" text-anchor="middle" opacity="0.75">心臓・筋肉・血液</text>
  <g><title>骨・石灰化：肋骨・椎体</title><rect x="356" y="20" width="104" height="56" rx="4" fill="#d9d9d9" stroke="currentColor" stroke-opacity="0.5"/></g>
  <text x="408.0" y="96" fill="currentColor" font-size="13" text-anchor="middle">骨・石灰化</text>
  <text x="408.0" y="113" fill="currentColor" font-size="11" text-anchor="middle" opacity="0.75">肋骨・椎体</text>
  <g><title>金属：人工物・造影剤</title><rect x="468" y="20" width="104" height="56" rx="4" fill="#ffffff" stroke="currentColor" stroke-opacity="0.5"/></g>
  <text x="520.0" y="96" fill="currentColor" font-size="13" text-anchor="middle">金属</text>
  <text x="520.0" y="113" fill="currentColor" font-size="11" text-anchor="middle" opacity="0.75">人工物・造影剤</text>
  <path d="M30 146 H550" stroke="currentColor" stroke-width="1.2"/><path d="M550 146 L540 141 L540 151 Z" fill="currentColor"/>
  <text x="290" y="138" fill="currentColor" font-size="11" text-anchor="middle" opacity="0.8">右ほど X 線を吸収しやすい（白く写る）</text>
</svg>

- X 線をよく通す（黒く写る）ことを **透過性亢進**、通しにくい（白く写る）ことを **透過性低下** という
- 単純 X 線で区別できるのは、おおまかにこの 5 段階だけ。**軟部組織と水（血液・胸水）は区別できない**

## シルエットサイン

同じ濃度のものどうしが **接している** と、その境目は見えなくなる。逆に、境目が見えれば、両者は接していない（前後にずれている）。

<svg viewBox="0 0 600 330" width="600" role="img" aria-label="シルエットサインの模式図。左：心臓の右縁に接する右中葉の病変では、病変と心臓が同じ濃度で接するので右心縁が見えなくなる（陽性）。右：心臓より後ろの右下葉の病変では、心臓と接していないので右心縁が見える（陰性）" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <rect x="0" y="0" width="285.0" height="275.5" fill="#1a1a1a"/>
  <path d="M19.0 275.5 L23.8 57.0 Q38.0 19.0 104.5 17.1 L180.5 17.1 Q247.0 19.0 261.2 57.0 L266.0 275.5 Z" fill="#6e6e6e"/>
  <path d="M121.6 47.5 Q76.0 42.8 52.2 85.5 Q38.0 152.0 39.9 237.5 Q80.8 213.8 121.6 228.0 Z" fill="#262626"/>
  <path d="M163.4 47.5 Q209.0 42.8 232.8 85.5 Q247.0 152.0 245.1 242.2 Q204.2 220.4 163.4 228.0 Z" fill="#262626"/>
  <path d="M125.4 66.5 Q66.5 57.0 45.6 87.4" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M159.6 66.5 Q218.5 57.0 239.4 87.4" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M125.4 98.8 Q66.5 89.3 45.6 119.7" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M159.6 98.8 Q218.5 89.3 239.4 119.7" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M125.4 131.1 Q66.5 121.6 45.6 152.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M159.6 131.1 Q218.5 121.6 239.4 152.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M125.4 163.4 Q66.5 153.9 45.6 184.3" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M159.6 163.4 Q218.5 153.9 239.4 184.3" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M125.4 195.7 Q66.5 186.2 45.6 216.6" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M159.6 195.7 Q218.5 186.2 239.4 216.6" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M125.4 19.0 L159.6 19.0 L163.4 142.5 L121.6 142.5 Z" fill="#b0b0b0"/>
  <path d="M115.9 142.5 Q106.4 190.0 117.8 226.1 Q161.5 237.5 210.9 224.2 Q224.2 190.0 190.0 152.0 Q166.2 133.0 142.5 137.8 Z" fill="#c4c4c4"/>
  <ellipse cx="102.6" cy="194.8" rx="24.7" ry="28.5" fill="#c4c4c4"/>
  <path d="M39.9 237.5 Q80.8 210.9 121.6 228.0 M163.4 228.0 Q204.2 220.4 245.1 242.2" fill="none" stroke="#9e9e9e" stroke-width="1.9"/>
  <rect x="310" y="0" width="285.0" height="275.5" fill="#1a1a1a"/>
  <path d="M329.0 275.5 L333.8 57.0 Q348.0 19.0 414.5 17.1 L490.5 17.1 Q557.0 19.0 571.2 57.0 L576.0 275.5 Z" fill="#6e6e6e"/>
  <path d="M431.6 47.5 Q386.0 42.8 362.2 85.5 Q348.0 152.0 349.9 237.5 Q390.8 213.8 431.6 228.0 Z" fill="#262626"/>
  <path d="M473.4 47.5 Q519.0 42.8 542.8 85.5 Q557.0 152.0 555.1 242.2 Q514.2 220.4 473.4 228.0 Z" fill="#262626"/>
  <path d="M435.4 66.5 Q376.5 57.0 355.6 87.4" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M469.6 66.5 Q528.5 57.0 549.4 87.4" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M435.4 98.8 Q376.5 89.3 355.6 119.7" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M469.6 98.8 Q528.5 89.3 549.4 119.7" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M435.4 131.1 Q376.5 121.6 355.6 152.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M469.6 131.1 Q528.5 121.6 549.4 152.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M435.4 163.4 Q376.5 153.9 355.6 184.3" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M469.6 163.4 Q528.5 153.9 549.4 184.3" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M435.4 195.7 Q376.5 186.2 355.6 216.6" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M469.6 195.7 Q528.5 186.2 549.4 216.6" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="2.8"/>
  <path d="M435.4 19.0 L469.6 19.0 L473.4 142.5 L431.6 142.5 Z" fill="#b0b0b0"/>
  <ellipse cx="405.0" cy="210.9" rx="32.3" ry="22.8" fill="#8a8a8a" fill-opacity="0.75"/>
  <path d="M425.9 142.5 Q416.4 190.0 427.8 226.1 Q471.5 237.5 520.9 224.2 Q534.2 190.0 500.0 152.0 Q476.2 133.0 452.5 137.8 Z" fill="#c4c4c4"/>
  <path d="M425.9 142.5 Q416.4 190.0 427.8 226.1 Q471.5 237.5 520.9 224.2 Q534.2 190.0 500.0 152.0 Q476.2 133.0 452.5 137.8 Z" fill="none" stroke="#e6e6e6" stroke-width="1.1"/>
  <path d="M349.9 237.5 Q390.8 210.9 431.6 228.0 M473.4 228.0 Q514.2 220.4 555.1 242.2" fill="none" stroke="#9e9e9e" stroke-width="1.9"/>
  <text x="142" y="298" fill="currentColor" font-size="13" text-anchor="middle">右中葉の病変（心臓に接する）</text>
  <text x="142" y="318" fill="currentColor" font-size="13" text-anchor="middle" font-weight="bold">→ 右心縁が消える：陽性</text>
  <text x="452" y="298" fill="currentColor" font-size="13" text-anchor="middle">右下葉の病変（心臓より後ろ）</text>
  <text x="452" y="318" fill="currentColor" font-size="13" text-anchor="middle" font-weight="bold">→ 右心縁が見える：陰性</text>
</svg>

- 右心縁が見えない → 病変は心臓に接する **右中葉**
- 左心縁が見えない → **左舌区**
- 横隔膜が見えない → **下葉**

1 枚の正面像から、病変の **前後の位置** を推定できる。

## 撮影方向と拡大

X 線は点状の線源から広がるので、**検出器から離れたものほど大きく写る**。線源から検出器までの距離を $\mathrm{SID}$、線源から物体までの距離を $\mathrm{SOD}$ とすると、相似な三角形から、

$$
\frac{W}{w}=\frac{\mathrm{SID}}{\mathrm{SOD}}
$$

（$w$：物体の実際の幅、$W$：検出器上の像の幅）。

<svg viewBox="0 0 600 300" width="600" role="img" aria-label="X 線写真の拡大。点状の X 線源から広がる X 線で、検出器から離れた物体ほど大きく写る。拡大率は 線源–検出器距離 ÷ 線源–物体距離。PA 像では心臓が検出器に近く拡大は小さい。AP 像では心臓が検出器から遠く、線源も近いので拡大が大きい" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <text x="165" y="20" fill="currentColor" font-size="14" text-anchor="middle" font-weight="bold">PA（立位・後→前）</text>
  <circle cx="165" cy="40" r="5" fill="currentColor"/>
  <text x="175" y="44" fill="currentColor" font-size="11">線源</text>
  <path d="M165 40 L137.5 260 M165 40 L192.5 260" stroke="currentColor" stroke-width="1" stroke-dasharray="4 3" opacity="0.7"/>
  <rect x="140.0" y="232" width="50" height="16" rx="6" fill="currentColor" fill-opacity="0.5"/>
  <text x="198.0" y="244" fill="currentColor" font-size="11">心臓（幅 w）</text>
  <path d="M55 260 H275" stroke="currentColor" stroke-width="3"/>
  <path d="M137.5 268 H192.5" stroke="currentColor" stroke-width="5" opacity="0.6"/>
  <text x="165" y="286" fill="currentColor" font-size="11" text-anchor="middle">検出器上の像（幅 W = 1.10 w）</text>
  <path d="M40 40 V260 M36 40 H44 M36 260 H44" stroke="currentColor" opacity="0.7"/>
  <text x="34" y="150.0" fill="currentColor" font-size="11" text-anchor="end">SID</text>
  <path d="M65 40 V240 M61 240 H69" stroke="currentColor" opacity="0.7"/>
  <text x="71" y="152.0" fill="currentColor" font-size="11">SOD</text>
  <text x="465" y="20" fill="currentColor" font-size="14" text-anchor="middle" font-weight="bold">AP（臥位・前→後）</text>
  <circle cx="465" cy="40" r="5" fill="currentColor"/>
  <text x="475" y="44" fill="currentColor" font-size="11">線源</text>
  <path d="M465 40 L431.7 200 M465 40 L498.3 200" stroke="currentColor" stroke-width="1" stroke-dasharray="4 3" opacity="0.7"/>
  <rect x="440.0" y="152" width="50" height="16" rx="6" fill="currentColor" fill-opacity="0.5"/>
  <text x="498.0" y="164" fill="currentColor" font-size="11">心臓（幅 w）</text>
  <path d="M355 200 H575" stroke="currentColor" stroke-width="3"/>
  <path d="M431.7 208 H498.3" stroke="currentColor" stroke-width="5" opacity="0.6"/>
  <text x="465" y="226" fill="currentColor" font-size="11" text-anchor="middle">検出器上の像（幅 W = 1.33 w）</text>
  <path d="M340 40 V200 M336 40 H344 M336 200 H344" stroke="currentColor" opacity="0.7"/>
  <text x="334" y="120.0" fill="currentColor" font-size="11" text-anchor="end">SID</text>
  <path d="M365 40 V160 M361 160 H369" stroke="currentColor" opacity="0.7"/>
  <text x="371" y="112.0" fill="currentColor" font-size="11">SOD</text>
  <text x="590" y="294" fill="currentColor" font-size="10" text-anchor="end" opacity="0.6">模式図。距離の比は例</text>
</svg>

- **PA 像**（立位で背中から前へ）：心臓が前胸部側、つまり検出器の近くにあり、SID も長いので **拡大が小さい**。胸部正面の標準
- **AP 像**（臥位・ポータブルで前から後ろへ）：心臓が検出器から遠く、SID も短いので **心臓が大きく写る**

最後に、例として PA（$\mathrm{SID}=180$ cm、心臓が検出器から約 12 cm で $\mathrm{SOD}=168$ cm）と AP（$\mathrm{SID}=100$ cm、心臓が検出器から約 15 cm で $\mathrm{SOD}=85$ cm）を代入すると、

$$
\text{PA}：\frac{180}{168}\approx1.07,\qquad
\text{AP}：\frac{100}{85}\approx1.18
$$

（図は差がわかるように誇張している）

## 心胸郭比（CTR）

<svg viewBox="0 0 560 320" width="560" role="img" aria-label="胸部 X 線写真（PA）の模式図と心胸郭比の測り方。正中線から心臓の右縁までの最大距離 a、左縁までの最大距離 b、胸郭の内側の最大横径 c を測り、CTR = (a + b) / c" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto">
  <rect x="10" y="10" width="300.0" height="290.0" fill="#1a1a1a"/>
  <path d="M30.0 300.0 L35.0 70.0 Q50.0 30.0 120.0 28.0 L200.0 28.0 Q270.0 30.0 285.0 70.0 L290.0 300.0 Z" fill="#6e6e6e"/>
  <path d="M138.0 60.0 Q90.0 55.0 65.0 100.0 Q50.0 170.0 52.0 260.0 Q95.0 235.0 138.0 250.0 Z" fill="#262626"/>
  <path d="M182.0 60.0 Q230.0 55.0 255.0 100.0 Q270.0 170.0 268.0 265.0 Q225.0 242.0 182.0 250.0 Z" fill="#262626"/>
  <path d="M142.0 80.0 Q80.0 70.0 58.0 102.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M178.0 80.0 Q240.0 70.0 262.0 102.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M142.0 114.0 Q80.0 104.0 58.0 136.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M178.0 114.0 Q240.0 104.0 262.0 136.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M142.0 148.0 Q80.0 138.0 58.0 170.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M178.0 148.0 Q240.0 138.0 262.0 170.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M142.0 182.0 Q80.0 172.0 58.0 204.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M178.0 182.0 Q240.0 172.0 262.0 204.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M142.0 216.0 Q80.0 206.0 58.0 238.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M178.0 216.0 Q240.0 206.0 262.0 238.0" fill="none" stroke="#bdbdbd" stroke-opacity="0.35" stroke-width="3.0"/>
  <path d="M142.0 30.0 L178.0 30.0 L182.0 160.0 L138.0 160.0 Z" fill="#b0b0b0"/>
  <path d="M132.0 160.0 Q122.0 210.0 134.0 248.0 Q180.0 260.0 232.0 246.0 Q246.0 210.0 210.0 170.0 Q185.0 150.0 160.0 155.0 Z" fill="#c4c4c4"/>
  <path d="M132.0 160.0 Q122.0 210.0 134.0 248.0 Q180.0 260.0 232.0 246.0 Q246.0 210.0 210.0 170.0 Q185.0 150.0 160.0 155.0 Z" fill="none" stroke="#e6e6e6" stroke-width="1.2"/>
  <path d="M52.0 260.0 Q95.0 232.0 138.0 250.0 M182.0 250.0 Q225.0 242.0 268.0 265.0" fill="none" stroke="#9e9e9e" stroke-width="2.0"/>
  <path d="M160.0 40.0 V290.0" stroke="#ffffff" stroke-dasharray="4 3" stroke-width="1"/>
  <path d="M124.0 215.0 H160.0" stroke="#ffffff" stroke-width="2"/>
  <path d="M160.0 230.0 H238.0" stroke="#ffffff" stroke-width="2"/>
  <path d="M50.0 272.0 H272.0" stroke="#ffffff" stroke-width="2"/>
  <text x="142.0" y="210.0" fill="#ffffff" font-size="14" font-style="italic" text-anchor="middle">a</text>
  <text x="199.0" y="225.0" fill="#ffffff" font-size="14" font-style="italic" text-anchor="middle">b</text>
  <text x="215.0" y="267.0" fill="#ffffff" font-size="14" font-style="italic" text-anchor="middle">c</text>
  <text x="330" y="50" fill="currentColor" font-size="13">a：正中線から心臓の右縁まで</text>
  <text x="330" y="74" fill="currentColor" font-size="13">b：正中線から心臓の左縁まで</text>
  <text x="330" y="98" fill="currentColor" font-size="13">c：胸郭の内側の最大横径</text>
  <text x="330" y="140" fill="currentColor" font-size="13" font-weight="bold">CTR = (a + b) / c</text>
  <text x="330" y="164" fill="currentColor" font-size="13">成人の PA 像で 50% 以下が目安</text>
  <text x="330" y="230" fill="currentColor" font-size="13">写真の左側が患者の右</text>
  <text x="330" y="250" fill="currentColor" font-size="13">（患者と向き合って見る）</text>
  <text x="16" y="28" fill="#ffffff" font-size="12">R</text><text x="296" y="28" fill="#ffffff" font-size="12" text-anchor="end">L</text>
</svg>

$$
\boxed{\mathrm{CTR}=\frac{a+b}{c}}
$$

- 成人の PA 像で **50% 以下** が目安。超えると心拡大を疑う
- AP 像では心臓が大きく写るので、CTR は大きめに出る
- 吸気が浅い（横隔膜が高い）と、心臓が横に寝て大きく見える

最後に、例として $a=4.5$ cm、$b=9.0$ cm、$c=28$ cm を代入すると、

$$
\mathrm{CTR}=\frac{4.5+9.0}{28}=\frac{13.5}{28}\approx0.48
$$

## 読む前の確認
- 患者名・日付・**PA か AP か**・立位か臥位か
- **吸気** は十分か（右横隔膜の上に後部肋骨が 10 本ほど見える）
- **回転** していないか（左右の鎖骨の内側の端が、棘突起から等しい距離にあるか）
- 線量は適切か（心臓の裏の椎体がうっすら見える程度）

## 被ばく
- 胸部正面 1 回の実効線量は、およそ 0.02〜0.1 mSv 程度とされる
- 自然放射線による被ばく（世界平均で年 約 2.4 mSv）の数十分の 1 以下

## 出典
- 質量減弱係数：[NIST X-Ray Mass Attenuation Coefficients](https://physics.nist.gov/PhysRefData/XrayMassCoef/)（水、皮質骨、脂肪組織。密度は ICRU-44）
- そのほかは一般的な知識
