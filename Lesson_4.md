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
\overline{x}^{n}_l \equiv \frac{1}{N}\Sigma_n x_{nl}
```

分散（変動強度を表す指標）：
```math
s^{2}_l \equiv \frac{1}{N}\Sigma_n (x_{nl}- \overline{x}^n_l)^2
```

標準偏差（変動強度を表す指標）：
```math
s_l \equiv \sqrt{ \frac{1}{N}\Sigma_n (x_{nl}- \overline{x}^n_l)^2 }
```

規格化変数：
```math
x_{nl}^{norm} \equiv \frac{x_{nl}-\overline{x}^n_l}{s_l}
```

共分散（共変強度を表す指標）：
```math
c_{12} \equiv \frac{1}{N}\Sigma_n (x_{n1}-\overline{x}^n_1)(x_{n2}-\overline{x}^n_2)   \\  
c_{11} = s^2_l
```

相関係数（共変強度を表す指標）：
```math
r_{12} \equiv \frac{c_{12}}{s_1s_2} = \frac{1}{N}\Sigma_n \frac{x_{n1}-\overline{x}^n_1}{s_1}\frac{x_{n2}-\overline{x}^n_2}{s_2}=\frac{1}{N}\Sigma_n x_{n1}^{norm} x_{n2}^{norm}
```



!## 簡単な例

!### その１

![サンプル１](https://github.com/kugi-yosikawa/DD2025/blob/main/PCAsample1.gif)

!第１モード、第２モード

!### その２


\psfrag{title}[][]{第１モード}
\psfrag{xtitle}[][]{観測地点}
\psfrag{ytitle}[][]{観測値}
\includegraphics[width=0.32\textwidth]{../Idl/Eps/EofTwo/Sample2/modstr1.eps}
\psfrag{title}[][]{第２モード}
\psfrag{xtitle}[][]{観測地点}
\psfrag{ytitle}[][]{観測値}
\includegraphics[width=0.32\textwidth]{../Idl/Eps/EofTwo/Sample2/modstr2.eps}
\psfrag{title}[][]{主成分得点}
\psfrag{xtitle}[][]{観測時刻}
\psfrag{ytitle}[][]{モード振幅}
\includegraphics[width=0.32\textwidth]{../Idl/Eps/EofTwo/Sample2/scrtim.eps}


\vspace{1cm}
%\begin{center}
\begin{tabular}{l|ll}
モード番号 & 寄与率  & 累積寄与率 \\\hline
１         & 79.9 \% & 79.9 \%    \\
２         & 20.0 \% & 99.9 \%    \\\hline
\end{tabular}
%\end{center}




\psfrag{title}[][]{観測値}
\psfrag{xtitle}[][]{観測地点}
\psfrag{ytitle}[][]{観測値}
\href{../Idl/Eps/EofOne/Sample1/obsdat.gif}{%
\hspace{0.25\textwidth}\includegraphics[width=0.5\textwidth]{../Idl/Eps/EofOne/Sample1/obsdat63.eps}}


%動画２の例では、二つの観測点でのデータの変動を示している。この場合に卓越
%するモードは、左側の地点での振幅が右側のそれの約２倍の変動であろうと考え
%ることができる。実際EOFを用いて解析した結果得られた卓越モード（図）およ
%びその時間変化（図）は、そのような変動をうまく取り出せている。



\psfrag{title}[][]{第１モード}
\psfrag{xtitle}[][]{観測地点}
\psfrag{ytitle}[][]{観測値}
\includegraphics[scale=0.2]{../Idl/Eps/EofOne/Sample1/modstr1.eps}
\psfrag{title}[][]{第２モード}
\psfrag{xtitle}[][]{観測地点}
\psfrag{ytitle}[][]{観測値}
\includegraphics[scale=0.2]{../Idl/Eps/EofOne/Sample1/modstr2.eps}
\psfrag{title}[][]{主成分得点}
\psfrag{xtitle}[][]{観測時刻}
\psfrag{ytitle}[][]{モード振幅}
\includegraphics[scale=0.2]{../Idl/Eps/EofOne/Sample1/scrtim.eps}

\vspace{1cm}
%\begin{center}
\begin{tabular}{l|ll}
モード番号 & 寄与率 & 累積寄与率 \\\hline
１         & 99.4\% & 99.4\%     \\
２         &  0.6\% & 100 \%     \\\hline
\end{tabular}
%\end{center}


\end{slide}
