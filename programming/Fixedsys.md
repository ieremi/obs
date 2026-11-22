# Fixedsys

**Fixedsys** は、初期の Microsoft Windows に付属した等幅のビットマップフォント。ピクセル単位で描かれた角張った字形と、横幅の揃った文字が特徴で、古い Windows のテキスト画面を連想させる。[Windows screen fonts](https://www.atarimagazines.com/compute/issue151/56_Windows_screen_fonts.php)

## 特徴と用途

- **等幅**：英数字の文字幅が揃うため、ソースコードや表などの位置合わせに向く。
- **ビットマップフォント**：特定のサイズ・解像度に合わせた点の集まりで字形を表す。TrueType のようなアウトラインフォントと違い、任意の大きさに滑らかに拡大できるわけではない。
- Windows 95・98・Me のメモ帳の標準フォントとしても知られる。[Fixedsys Excelsior プロジェクト](https://github.com/MARTYR-X-LTD/fixedsys-excelsior)

旧 Windows のシステム用等幅フォントとの互換性は、Win32 の `SYSTEM_FIXED_FONT` にも残っている。ただし、API が選択する実際のフォントや描画は環境に依存する。[Microsoft Learn: Using a Stock Font to Draw Text](https://learn.microsoft.com/en-us/windows/win32/gdi/using-a-stock-font-to-draw-text)

## Fixedsys Excelsior

**Fixedsys Excelsior** は、Fixedsys をもとにした非公式の TrueType 版で、対応文字を拡張したもの。元の Windows 付属フォントとは別物であり、Unicode のすべての文字を収録しているわけではない。日本語などの表示や配布・改変条件は、入手する版ごとに確認する。[Fixedsys Excelsior](https://github.com/MARTYR-X-LTD/fixedsys-excelsior)

## 関連

- [[IBM Plex Sans]] — IBM Plex ファミリーには等幅の IBM Plex Mono もある。
