# リー代数の表現論

## 表現

> **定義 (表現)**
> $\mathfrak{g}$ をリー代数、$V$ を $\mathbb{C}$ 上ベクトル空間とする。
> $(\pi, V)$ が $\mathfrak{g}$ の **表現** であるとは、線形写像 $\pi : \mathfrak{g} \to \mathfrak{gl} (V)$  が括弧積について準同型であることをいう。
> $$\forall X, Y \in \mathfrak{g} \text{に対して} \,
> \pi ([X, Y]) = [\pi(X), \pi(Y)]
> $$
> このとき、$V$ を **表現空間** という。


## ワイルの指標公式

> **ワイルの指標公式 (Weyl Character Formula)**
>
> 最高ウェイト $\lambda$ の既約表現 $V$ の指標 $\chi_\lambda$ は
> $$
> \chi_\lambda = \frac{\sum_{w \in W} \mathrm{sgn} (w) e^{w (\lambda + \rho)}}
> {\sum_{w \in W} \mathrm{sgn} (w) e^{w (\rho)}}
> $$
> - $W$ : ワイル群
> - $\rho = \displaystyle\frac{1}{2} \sum_{\alpha \in \Delta^{+}} \alpha$ : ワイルベクトル
>   + $\Delta^{+}$ : 正のルート

### 例 : $\mathfrak{su} (2)$

2 次の特殊ユニタリ群 $SU(2)$ は行列式 1 の 2 次ユニタリ行列全体の集合である。

$$SU (2) = \{ g \in GL(2, \mathbb{C}) \mid g^\dagger g = I_2, \
\det g = 1\}$$

公式 $\det e^A = e^{\mathrm{Tr} (A)}$ により、 リー群 $SU (2)$ に付随するリー代数 $\mathfrak{su} (2)$ は、トレースがゼロの $2 \times 2$ 歪エルミート行列全体の集合となる。

$$\mathfrak{su} (2) = \{ X \in \mathfrak{gl}(2, \mathbb{C}) \mid
\mathrm{Tr} (X) = 0 ,
X^\dagger + X = 0 \}$$

一般に、トレースがゼロの $2\times 2$ の歪対称エルミート行列 $X \in \mathfrak{su} (2)$ は $a, b, c \in \mathbb{R}$ を任意の **実数** として
$$
X = \frac{i}{2} \begin{pmatrix}
a & b + ci\\
b - ci & -a
\end{pmatrix}
$$
と書けるため、

$$
E_1 = \frac{1}{2} \begin{pmatrix}
i & 0\\
0 & -i
\end{pmatrix}, \quad
E_2 = \frac{1}{2} \begin{pmatrix}
0 & i\\
i & 0
\end{pmatrix}, \quad
E_3 = \frac{1}{2} \begin{pmatrix}
0 & -1\\
1 & 0
\end{pmatrix}
$$
は $\mathfrak{su} (2)$ の基底となり $(X = aE_1 + b E_2 + c E_3, \ a, b, c\in\mathbb{R})$、以下の交換関係を満たす。

$$
[E_1, E_2] = E_3, \quad
[E_2, E_3] = E_1, \quad
[E_3, E_1] = E_2
$$

なお、ふつうは展開係数 $a, b, c$ を複素数 $\mathbb{C}$ まで許してできる $\mathfrak{sl} (2, \mathbb{C})$ を考える (これを $\mathfrak{su} (2)$ の **複素化 (complexification)** という)。

#### 1. ワイル・カルタン基底を決める

- ワイル群 $W$ は $W = \{ +1, -1 \}$

