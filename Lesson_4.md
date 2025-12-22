# 主成分分析（Principal Component Analysis）／経験直交関数（Empirical Orthogonal Function）展開

## 主成分分析とは

自然現象に含まれる様々な変動を成分に分け（分解し）、そのうち主要な（卓越する）成分を抽出する統計手法。大気海洋分野では経験直行関数展開とも呼ばれる。

## 考え方の基本

+ 空間構造パターン（モード）をもとに成分に分解
  + 異なる空間構造を持つ成分（モード）に分解
  + 分解された各成分（モード）は空間構造を保ったまま振幅が時間変化
+ 観測データは成分（モード）の重ね合わせ（線型結合）
+ 観測される変動強度（分散）への寄与率（モードの変動強度／全体の変動強度）に基づいてモードを順番づけして抽出
+ 変動の力学などは考慮しない

## 応用

+ 複雑な変動から主要な変動を抽出
  + それが物理・力学過程の抽出になる場合もある
+ 将来の予測

## 準備
時刻 $n$ 、地点 $l$ で観測される変数を $x_{nl}$ （ $n=1-N$ 、 $l=1-L$ ）とする。ある地点 $l$ における観測データ $x_{nl}$ の時間に関する平均、分散、標準偏差、規格化を以下のように表記する。

平均：
```math
\begin{align}
& \overline{x}^{n}_l \equiv \frac{1}{N}\Sigma_n x_{nl}
\end{align}
```

分散（変動強度を表す指標）：
```math
\begin{align}
& s^{2}_l \equiv \frac{1}{N}\Sigma_n (x_{nl}- \overline{x}^n_l)^2
\end{align}
```

標準偏差（変動強度を表す指標）：
```math
\begin{align}
& s_l \equiv \sqrt{ \frac{1}{N}\Sigma_n (x_{nl}- \overline{x}^n_l)^2 }
\end{align}
```

規格化変数：
```math
\begin{align}
& x_{nl}^{norm} \equiv \frac{x_{nl}-\overline{x}^n_l}{s_l}
\end{align}
```

共分散（共変強度を表す指標）：
```math
\begin{align}
& c_{12} \equiv \frac{1}{N}\Sigma_n (x_{n1}-\overline{x}^n_1)(x_{n2}-\overline{x}^n_2)   \\  
& c_{11} = s^2_1
\end{align}
```

相関係数（共変強度を表す指標）：
```math
\begin{align}
r_{12} & \equiv \frac{c_{12}}{s_1s_2} \\
& = \frac{1}{N}\Sigma_n \frac{x_{n1}-\overline{x}^n_1}{s_1}\frac{x_{n2}-\overline{x}^n_2}{s_2}\\
& =\frac{1}{N}\Sigma_n x_{n1}^{norm} x_{n2}^{norm}
\end{align}
```

下の図は、左から、正の共変関係のある、ほとんど共変関係の無い、負の共変関係のある、２つのデータの組。それぞれの分散値はグラフの上に記してある。

<img src="https://github.com/kugi-yosikawa/DD2025/blob/main/scatter.jpg">

このように、分散は変動の強度指標、共分散は共変動の強度指標、である。

## 主成分分析：２地点データの場合の例

<img src="https://github.com/kugi-yosikawa/DD2025/blob/main/obsdat_sct.png">

例えば京都と東京の気温の時系列。横軸に京都の気温、縦軸に東京の気温を取ると、上の図のように（多分）なる。図からは、主要な特徴として

+ 京都の気温が高いときは東京の気温も高い時が多い
+ 京都の気温変化の方が、東京の気温変化よりも大きい（２倍くらい）

が読み取れる。ただし、主要な特徴からのズレも存在する（例えば第３象限に位置するデータ）。

これを言い換えると、観測される変動のうち、”主要な”変動は右上向きの赤線（傾きはおよそ1/2）軸（主軸）に沿う方向の変動、”ズレの”変動は左上向きの赤線軸（副軸）に沿う方向の変動、となる。これを変動強度（分散）を用いて定量的に表現する。

<img src="https://github.com/kugi-yosikawa/DD2025/blob/main/PCA_image.png">

+ 時刻 $n$ での変動 $(x_{n1},x_{n2})$ を、主軸と副軸の成分を用いて、$(y_{n1},y_{n2})$ で表現することを試みる。この際、時刻 $n$ での全変動強度を変えないように $y_{nl}$ を定義する。
  ```math
  x_{n1}^2+x_{n2}^2=y_{n1}^2+y_{n2}^2
  ```
  なお全変動強度も不変（ $\Sigma_n \Sigma_l x_{nl}^2 = \Sigma_n \Sigma_l y_{nl}^2$ ）に注意する。
+ 主軸を $\Sigma_n y_{n1}^2が最大となる軸とする。
+ 副軸を それに直交する軸とする。

## 主成分分析の定義と導出：一般化

### 準備

観測値：
```math
x_{nl}, n=1-N（観測時刻数）, l=1-L（観測地点数）
```  
ただし各地点での時間平均値 $\overline{x}^n_l$ は予め差し引いておく。

ある時刻 $n$ での観測値：
```math
\begin{align}
& \vec{x}_n=\left( x_{n1}, x_{n2}, \cdots, x_{nL} \right)
\end{align}
```

ある地点 $l$ での観測値：
```math
\begin{align}
& \vec{x}_l = \left( \begin{array}{c}
  x_{1l}\\
  x_{2l}\\
  \vdots\\
  x_{Nl}\\
  \end{array} \right)
\end{align}
```

主軸（第一モード）の空間構造：
```math
\begin{align}
& \vec{y}=\left( \begin{array}{c}
y_1\\
y_2\\
\vdots\\
y_L
\end{array}\right)
\\  
& \vec{y}^T\vec{y}=1
\end{align}
```

時刻 $n$ での観測値 $x_{nl}$ との内積値（主軸への射影成分）：
```math
\begin{align}
\vec{x}_n^T\vec{y} & =x_{n1}y_1+x_{n2}y_2+\cdots+x_{nL}y_L \\
& \equiv a_n \\
\end{align}
```

主軸（第一モード）で評価した時刻 $n$ での分散：
```math
\begin{align}
& a_n^2
\end{align}
```

### 主軸（第一モード）の定義

$\vec{y}^T\vec{y}=1$ の条件で $\Sigma_n a_n^2$ を最大とする $\vec{y}$ 

観測行列：
```math
\begin{align}
& \X \equiv (\vec{x}_1,\vec{x}_2,\cdots,\vec{x}_L)=\left(\begin{array}{c}
x_{11} & x_{12} & \cdots & x_{1L} \\
x_{21} & x_{22} & \cdots & x_{2L} \\
\vdots & \vdots & \ddots & \vdots \\
x_{N1} & x_{N2} & \cdots & x_{NL} \\
\end{array}\right)
\end{align}
```

内積ベクトル：
```math
\begin{align}
\vec{a} & \equiv \left( \begin{array}{c}
a_1 \\
a_2 \\
\vdots \\
a_N
\end{array} \right) = \left( \begin{array}{c}
x_11 y_1+x_12y_2+ \cdots +x_{1L}y_L \\
x_21 y_1+x_22y_2+ \cdots +x_{2L}y_L \\
\vdots \\
x_N1 y_1+x_N2y_2+ \cdots +x_{NL}y_L
\end{array} \right) \\
& = \left( \begin{array}{cccc}
x_{11} & x_{12} & \cdots & x_{1L} \\
x_{21} & x_{22} & \cdots & x_{2L} \\
\vdots & \vdots & \ddots & \vdots \\
x_{N1} & x_{N2} & \cdots & x_{NL} \\
\end{array}\right) \left(\begin{array}{c}
y_1\\
y_2\\
\vdots \\
y_L\\
\end{array}\right)=X\vec{y}
\end{align}
```

内積２乗和：
```math
\begin{align}
& \vec{a}^T\vec{a}=(X\vec{y})^TX\vec{y}=\vec{y}^TX^TX\vec{y}
\end{align}
```

共分散行列（正値対称行列）：
```math
\begin{align}
& C=X^TX=\left(\begin{array}{c}
x_{11} & x_{21} & \cdots & x_{N1} \\
x_{12} & x_{22} & \cdots & x_{N2} \\
\vdots & \vdots & \ddots & \vdots \\
x_{1L} & x_{2L} & \cdots & x_{NL} \\
\end{array}\right)\left(\begin{array}{c}
x_{11} & x_{12} & \cdots & x_{1L} \\
x_{21} & x_{22} & \cdots & x_{2L} \\
\vdots & \vdots & \ddots & \vdots \\
x_{N1} & x_{N2} & \cdots & x_{NL} \\
\end{array}\right)=\left(\begin{array}{cccc}
c_{11} & c_{12} & \cdots & c_{1L} \\
c_{21} & c_{22} & \cdots & c_{2L} \\
\vdots & \vdots & \ddots & \vdots \\
c_{L1} & c_{L2} & \cdots & c_{LL} \\
\end{array} \right)
\end{align}
```

第一モードの定義の数学的表現： $\vec{y}^T\vec{y}=1$ の条件のもと $\vec{a}^T\vec{a}=\vec{y}^TC\vec{y}$ が最大となる $\vec{y}$ 


### 第一モード（主軸）の導出
