# MOAA GPV データのダウンロードと描画

## MOAA GPV データとは
[Argoフロート](https://www.jamstec.go.jp/argo/j/)のデータやその他利用可能な水温塩分データを、最適内挿法を用いて格子化したデータセット。[海洋研究開発機構（JAMSTEC）](https://www.jamstec.go.jp/j/)が作成・公開を行っている。英語名は Grid Point Value of the Monthly Objective Analysis using the Argo data。

MOAA GPV データの詳細は[ここ](https://www.jamstec.go.jp/argo_research/dataset/moaagpv/moaa_ja.html)を参照。ダウンロードサイトも同ページに記載。2025年9月に ver2 が公開された。2025年10月現在、水温, 塩分が公開されている。本課題演習ではこの ver2 を解析に使用。
データセットは Argo フロートが展開された 2001 年からあるが、2005年ころまではフロート数が十分でない点に注意。

## MOAA GPV データのダウンロードと読み込み
データセットには速報性を重視した near real time （準リアルタイム）と正確性を重視した delayed mode （遅延モード）がある。課題演習では遅延モードを解析。
ファイルは年毎に tar.gz ファイルにまとめられている。 tar は複数のファイルをまとめるコマンドで、そのようにしてまとめたファイルは ***.tar と名付けるのが慣例。gzip はファイル圧縮のコマンドで、そのようにして圧縮したファイルは ***.gz と名付けるのが慣例。

``` tar xvfz ***.tar.gz```
