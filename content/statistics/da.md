# 判別分析

DA : Discriminant Analysis

データをいくつかのグループに分ける方法。

## フィッシャーの線形判別分析 (2群の場合)

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

## 参考
- https://www.youtube.com/watch?v=mw2V9rhJ0lE