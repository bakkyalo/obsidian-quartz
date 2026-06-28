# 判別分析

DA : Discriminant Analysis

データをいくつかのグループに分ける方法。

## フィッシャーの線形判別分析 (2群の場合)

線形判別分析 (LDA : linear discriminant analysis) は
- データが独立である
- <u>等分散である</u> (共分散行列が共通である, 平均は異なっても良い)

時に適用できる。[^1]

[^1]: 正規性はとりあえず必須ではないが、LDA は 2 次モーメントまでのみでデータを評価しているので、極端な分布の場合は期待した結果にならないことがある。

### 0. 目標

データ $x$ を $w$ 方向に射影した判別スコア $z$ を定義する。

$$
z = w^\prime x
$$

フィッシャーの線形判別分析は以下を要求する。

1. グループ間の平均はできるだけ離れること
2. 各グループの分散はできるだけ小さくなること

データを 2 つのグループ $C_1, C_2$ に分類できたとし、それぞれのグループ内平均を $\mu_1, \mu_2$ とする。

### 1. 平均を離す

射影後の平均を $m_1, m_2$ とすると
$$
m_1 = w^\prime \mu_1, \quad
m_2 = w^\prime \mu_2
$$

射影後の平均の差の二乗は
$$
(m_1-m_2)^2
= \{ w^\prime(\mu_1-\mu_2)\}^2
= w^\prime (\mu_1 - \mu_2) (\mu_1 - \mu_2)^\prime w
\eqqcolon w^\prime S_B \, w
$$

ここで $S_B \coloneqq (\mu_1-\mu_2) (\mu_1-\mu_2)^\prime$ は群間共分散行列 (Between-class scatter matrix)。

### 2. 分散を小さくする

グループ $C_1$ の射影後の平方和 $s_1^2$ は
$$
s_1^2 = \sum_{i \in C_1} (z_i - m_1)^2
= \sum_{i\in C_1} (w^\prime x_i - w^\prime \mu_1)^2
= w^\prime \left[ \sum_{i \in C_1} (x_i - \mu_1)(x_i - \mu_1)^\prime \right] w
\eqqcolon w^\prime S_1 \, w
$$

ここで $S_1 \coloneqq \sum_{i \in C_1} (x_i - \mu_1) (x_i - \mu_1)^\prime$ はグループ $C_1$ の射影後の群内平方和。

グループ $C_2$ の射影後の平方和 $s_2^2$ も同様に、$S_2 \coloneqq \sum_{i \in C_2} (x_i - \mu_2) (x_i - \mu_2)^\prime$ として $w^\prime S_2 \, w$ となる。

よって全データの射影後の群内平方和は
$$
s_1^2 + s_2^2 = w^\prime (S_1 + S_2) w 
\eqqcolon w^\prime S_W \, w
$$

$S_W \coloneqq S_1 + S_2$ は群内共分散行列 (Within-class scatter matrix)。

※データが等分散的でない (共分散行列が共通でない) 場合はこのような単純な足し算ができないため、ここで論理が破綻する。
二次判別分析 (QDA) などを検討する。

### 問題設定

以上から
- $w^\prime S_B \, w$ を大きく
- $w^\prime S_W \, w$ を小さく

するような射影 $w$ を求めろ、という問題になる。フィッシャーの定式化は以下の通り。

> **フィッシャーの線形判別分析** (Fisher's linear discriminant)
> $$
> \text{maximize} \qquad
> J(w) = \frac{w^\prime S_B \, w}{w^\prime S_W \, w}
> $$

このように設定すると、$w$ の定数倍の依存性が消えてなくなるのと、下で述べるように一般化固有値問題などのようなアルゴリズムのよく知られた問題に書き換えられるので都合が良い。

$J(w)$ は **フィッシャーの線形判別関数** *(Fisher's linear discriminant)* などといい、
右辺の分数は **レイリー商** *(Rayleigh quotient)* と呼ばれる。

### 一般化固有値問題

$J(w)$ の $w$ による微分が $0$ になるという式を立てる。
行列の微分公式 $\frac{\partial}{\partial x} x^\prime A x = (A+A^\prime) x$ と商の微分公式から
$$
S_B \,w (w^\prime S_W w) - (w^\prime S_B \, w) S_W w = 0
$$
$w^\prime S_W w$ も $w^\prime S_B \, w$ もスカラーなので、$\lambda \coloneqq \frac{w^\prime S_B \, w}{w^\prime S_W \, w}$ とすると

$$
S_B \, w = \lambda S_W \, w
$$
という一般化固有値問題 (generalized eigenvalue problem) になる。

#### Sw が正則の場合
特に $S_W$ が正則である場合は普通の固有値問題になる。

$$
S_W^{-1} S_B \, w = \lambda w
$$


$S_B = (\mu_1 - \mu_2) (\mu_1 - \mu_2)^\prime$ だったので、これを代入してみる。

さらに <u>2 クラス分類の場合</u> 、
左辺に現れる $(\mu_1 - \mu_2)^\prime w$ はスカラーになるのでこれを $k$ とすると
$$
w = \frac{k}{\lambda} \cdot S_W^{-1} (\mu_1 -\mu_2)
$$

LDA では射影 $w$ の定数倍はどうでもよいので、改めて

> $$
> w \propto S_W^{-1} (\mu_1-\mu_2)
> $$

と書ける。

この式が示唆することは結構深く、
- 固有値問題を解かずとも $S_W$ の逆行列さえわかれば LDA ができる。
- 射影ベクトル $w$ は $(\mu_1 - \mu_2)$ に比例しており、 2 群の重心を結ぶ方へ向かせようとしている。
- ただし群内の共分散の逆行列 $S_W^{-1}$ が掛けられており、散らばりが大きい方向の影響が弱まるように回転させている。

## 正準判別分析 (3群以上の場合)

CDA : Canonical Discriminant Analysis

分けたいグループ数 $K$ が 3 以上の場合も同様に議論出来、正準判別分析などと呼ばれる。[^2]

[^2]: 「正準」 (Canonical) という言葉はキリスト教の <u>聖書正典</u> (Canon)  や <u>教会法</u> (Canon law) などが語源であるとされ、「規範的」といった意味がある。
多変量分析には <u>正準相関分析</u> (CCA : Canonical Correlation Analysis) という方法があり、数学的には CDA は CCA の一種である。

差し当って、3 群以上に分類するフィッシャーの線形判別分析 (LDA) のことだと思っておけばよい。

### 設定と問題

$D$ 次元の $N$ 個のデータ $x_1, x_2, \dots, x_N \in \mathbb{R}^D$ を $K$ 個のクラス $C_1, C_2, \dots, C_K$ に分類したい。

射影先を $H$ 次元 ($H<D$) とすると、射影変換は行列 $W \in \mathbb{R}^{D\times H}$ で表され、判別関数も行列式で表される。

> **正準判別分析** (CDA : Canonical Discriminant Analysis)
> $$
> \text{maximize} \qquad
> J(W) = \frac{\det (W^\prime S_B \, W)}{\det (W^\prime S_W \, W)}
> $$
> - クラス間共分散行列 (Between-class scatter matrix) $S_B \in \mathbb{R}^{D\times D}$
> $$
> S_B= \sum_{k=1}^K N_k (\mu_k - \mu) (\mu_k - \mu)^\prime
> $$
> - クラス内共分散行列 (Within-class scatter matrix) $S_W \in \mathbb{R}^{D\times D}$
> $$
> S_W = \sum_{k=1}^K \sum_{i \in C_k} (x_i - \mu_k) (x_i - \mu_k)^\prime
> $$

- $N_k$ はクラス $C_k$ のデータ数、$\mu_k = \frac{1}{N_k} \sum_{i\in C_k} x_i$ はクラス $k$ の平均ベクトル、$\mu = \frac{1}{N} \sum_{k=1}^K N_k \mu_k$ は全体平均ベクトル。
- $S_W$ が well-defined であるためにはデータの独立性かつ等分散性が必須。
- $\text{rank} (S_B) \leq \min (D, K-1)$
- $\text{rank} (S_W) \leq \min (D, N-K)$
- よって、データの数があまりにも少ない場合 ($N-K<D$ くらい)、 $S_W \in \mathbb{R}^{D\times D}$ がフルランクでなくなって $S_W^{-1}$ が存在しないなどヤバいことが起きる。SSS  (Small Sample Size) problem などと呼ばれる


### 固有値問題

2クラス分類の場合と同様に $W$ で微分して $0$ とすると一般化固有値問題が得られる。

> $$S_B w_j = \lambda_j  S_W w_j$$

特に $S_W$ が正則である場合、ふつうの固有値問題になる。

$$
S_W^{-1} S_B w_j = \lambda_j w_j
$$

固有値 $\lambda_j$ が大きい順に固有ベクトルを並べたものが最適な射影行列 $W$ である。ただし、ランクを上回る本数は取れない。


## 2次判別分析 (QDA)

QDA : Quadratic Discriminant Analysis

QDA はフィッシャーの LDA のようにレイリー商最大化として定式化できないため、ベイズの定理に基づいて最尤推定することを考える。よって <u>正規性の仮定が必須になる</u> が、その代わりに等分散性の仮定が不要になる。(等分散を仮定すると LDA になる)

- データが独立である
- 必ずしも等分散でなくてよい (等分散だと LDA に帰着する)
- 多変量正規分布に従う


## 参考


- [PRML](https://www.microsoft.com/en-us/research/wp-content/uploads/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf)  (とりあえず載ってなくはないくらい)
- [Qu, L.; Pei, Y. A Comprehensive Review on Discriminant Analysis for Addressing Challenges of Class-Level Limitations, Small Sample Size, and Robustness. _Processes_ **2024**, _12_, 1382. https://doi.org/10.3390/pr12071382](https://www.mdpi.com/2227-9717/12/7/1382)　(適当にググったらでてきたやつ)
- [Linear discriminant analysis for the small sample size problem: an overview](https://link.springer.com/article/10.1007/s13042-013-0226-9)　(SSS 周辺が分かりやすい)
- https://www.youtube.com/watch?v=mw2V9rhJ0lE

