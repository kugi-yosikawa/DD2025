# MOAA GPV データのダウンロードと描画

## MOAA GPV データとは
[Argoフロート](https://www.jamstec.go.jp/argo/j/)のデータやその他利用可能な水温塩分データを、最適内挿法を用いて格子化したデータセット。[海洋研究開発機構（JAMSTEC）](https://www.jamstec.go.jp/j/)が作成・公開を行っている。英語名は Grid Point Value of the Monthly Objective Analysis using the Argo data。

MOAA GPV データの詳細は[ここ](https://www.jamstec.go.jp/argo_research/dataset/moaagpv/moaa_ja.html)を参照。2025年9月に ver2 が公開された。2025年10月現在、水温, 塩分が公開されている。本課題演習ではこの ver2 を解析に使用。
データセットは Argo フロートが展開された 2001 年からあるが、2005年ころまではフロート数が十分でない点に注意。

## MOAA GPV データのダウンロード
[ここ](https://pubargo.jamstec.go.jp/argo_product/catalog/moaagpv2/catalog.html)からダウンロード。データセットには速報性を重視した near real time （準リアルタイム）と正確性を重視した delayed mode （遅延モード）がある。課題演習では遅延モードを解析。  
ファイルは年毎に MOAAv2_OI_20XX_MON.tar.gz ファイルにまとめられている。 ファイル拡張子が tar のファイルは複数のファイルを tar コマンドでまとめたファイル、拡張子が gz のファイルはgzipコマンドで圧縮したファイルを示すのが慣例。
ファイル名をクリック、開いたサイトの Access の HTTPServer をクリックしてダウンロード。

ダウンロードしたファイルを以下の tar コマンドで解凍・展開する。

``` tar xvfz ***.tar.gz```

上記 tar のオプションの意味は以下。 
- x:extraction（ファイルを取り出す。まとめるときは c を指定）
- v:verbose（ファイル情報を端末に出力する）
- f:file（おまじないと思って良い）
- z:gzip（gzip で圧縮・解凍）
各月毎のファイルが展開される。

## MOAA GPV データの読み込み
MOAA GPV データは [NETCDF](https://www.unidata.ucar.edu/software/netcdf) ファイル形式で格納されている。簡単に言うと、数値データだけでなくそのフォーマットもファイル内に記述されているファイル形式。気象・海洋分野の世界的標準形式になっている。fortran や python で読み込める。  
含まれているデータを知るには、以下の ncdump コマンドが便利。

```ncdump -h NETCDFデータ```

以下は出力結果。

```
dimensions:
        LONGITUDE = 360 ;
        LATITUDE = 142 ;
        PRES = 66 ;
        STRING16 = 16 ;
variables:
        int PRES(PRES) ;
                PRES:name = "PRES" ;
        char CDATE0(STRING16) ;
                CDATE0:name = "CDATE0" ;
        char DATASET_TYPE(STRING16) ;
                DATASET_TYPE:name = "DATASET_TYPE" ;
                DATASET_TYPE:long_name = "Dataset type" ;
        float SOI_ERR(PRES, LATITUDE, LONGITUDE) ;
                SOI_ERR:name = "SOI_ERR" ;
                SOI_ERR:FillValue = -10000.f ;
        float TOI_ERR(PRES, LATITUDE, LONGITUDE) ;
                TOI_ERR:name = "TOI_ERR" ;
                TOI_ERR:FillValue = -10000.f ;
        float LATITUDE(LATITUDE) ;
                LATITUDE:name = "LATITUDE" ;
        float LONGITUDE(LONGITUDE) ;
                LONGITUDE:name = "LONGITUDE" ;
        float SOI(PRES, LATITUDE, LONGITUDE) ;
                SOI:name = "SOI" ;
                SOI:FillValue = -10000.f ;
        float S_CLIM(PRES, LATITUDE, LONGITUDE) ;
                S_CLIM:name = "S_CLIM" ;
                S_CLIM:FillValue = -10000.f ;
        float TOI(PRES, LATITUDE, LONGITUDE) ;
                TOI:name = "TOI" ;
                TOI:FillValue = -10000.f ;
        float T_CLIM(PRES, LATITUDE, LONGITUDE) ;
                T_CLIM:name = "T_CLIM" ;
                T_CLIM:FillValue = -10000.f ;
        float S_STDEV(PRES, LATITUDE, LONGITUDE) ;
                S_STDEV:name = "S_STDEV" ;
                S_STDEV:FillValue = -10000.f ;
        float T_STDEV(PRES, LATITUDE, LONGITUDE) ;
                T_STDEV:name = "T_STDEV" ;
                T_STDEV:FillValue = -10000.f ;
```


- dimensions：データの格子数（配列数）  
  LONGITUDE：経度方向格子数、LATITUDE：緯度方向格子数、PRES：深度（圧力）方向格子数  
  STRING16：文字数（１６文字の文字変数として定義されている）
- variables：データの種類  
  int PRES(PRES) ：整数変数で名前がPRES（圧力 dbar）の１次元配列、格子数もPRES  
  char CDATE0(STRING16) ：文字変数で名前がCDATE0（解析日時の中央値）、文字数がSTRING16  
  float SOI_ERR(PRES, LATITUDE, LONGITUDE) ：実数変数で名前がSOI_ERR（最適内挿時の塩分推定誤差、PSS-78、psu）の３次元（経度、緯度、深度）配列、不定値は -10000.0 が入っている  
  float TOI_ERR：水温推定誤差（ITS90、℃）  
  float LATITUDE(LATITUDE)：字数変数で名前がLATITUDE（緯度）の１次元配列  
  float LONGITUDE：経度  
  float SOI：塩分の最適内挿値（PSS-78、psu）  
  float S_CLIM：塩分の気候値（WOA13の平均値＝最適内挿法での初期値）  
  float TOI：水温の最適内挿値（ITS90、℃）  
  float T_CLIM：水温の気候値  
  float S_STDEV：塩分の格子内観測値の標準偏差  
  float T_STDEV：水温の格子内観測値の標準偏差  

  
