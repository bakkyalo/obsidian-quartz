# リー代数の表現論

## リー代数と表現

> **定義 (リー代数)**
>
> $\mathfrak{g}$ が有限次元リー代数であるとは、$\mathfrak{g}$ がある $\underline{\text{体} \, K}$ 上の有限次元ベクトル空間であって、以下を満たす二項演算 $[\cdot, \cdot] : \mathfrak{g} \times \mathfrak{g} \to \mathfrak{g}$ が定義されていることをいう。
>
> 1. **双線形性 (bilinear)**
> 任意の $\underline{a, b \in K}$ と $X, Y, Z \in \mathfrak{g}$ に対して
> $$
> [aX + bY, Z] = a [X, Z] + b[Y, Z]
> $$
>
> $$
> [Z, aX + bY] = a [Z, X] + b[Z, Y]
> $$
> 2. **歪対称性 (skew symmetric)**
>任意の $X, Y \in \mathfrak{g}$ に対して
>$$
> [X, Y] = -[Y, X]
> $$
>
> 3. **ヤコビ恒等式 (Jacobi identity)**
>任意の $X, Y, Z \in \mathfrak{g}$ に対して
>
> $$
> [X, [Y, Z]] + [Y, [Z, X]] + [Z, [X, Y]] = 0
> $$

- $[\cdot, \cdot]$ を **括弧積**、**リーブラケット** などと呼ぶ事もある。
- 歪対称性から $[X, X] = 0 \quad (\forall X \in \mathfrak{g})$ も分かる。
- 係数体 $K$ が実数体 $\mathbb{R}$ であるときは **実リー代数**、複素数体 $\mathbb{C}$ であるときは **複素リー代数** と呼ぶ。
- 物理でよく出てくる $[X, Y] = XY- YX$ は、$\mathfrak{g}$ の元に別途 "ふつうの積" が定義された **普遍包絡代数** *(universal enveloping algebra)* での話。今回はそこでの話はしない。

> **定義 (表現)**
> $\mathfrak{g}$ をリー代数、$V$ を $\mathbb{C}$ 上ベクトル空間とする。
> $(\pi, V)$ が $\mathfrak{g}$ の **表現** であるとは、線形写像 $\pi : \mathfrak{g} \to \mathfrak{gl} (V)$  が括弧積について準同型であることをいう。
> $$
> \forall X, Y \in \mathfrak{g} \text{に対して} \,
> \pi ([X, Y]) = [\pi(X), \pi(Y)]
> $$
> このとき、$V$ を **表現空間** という。

### 複素化

$\mathfrak{su} (N)$ など、実数体 $\mathbb{R}$ 上のリー代数で重要なものはたくさんあるが、数学では複素リー代数を議論する方がより強力な示唆を得ることができる。
そこで、以下に示す所定の手続きにより係数体を複素数に拡張することがよく (あるいは暗黙のうちに) 行われる。

> **複素化 (complexification)**
>
> $\mathfrak{g}$ を実リー代数とすると
> $$
> \mathfrak{g}_{\mathbb{C}} \coloneqq \mathfrak{g} \otimes_{\mathbb{R}} \mathbb{C} = \mathfrak{g} \oplus i \mathfrak{g}
> $$
> は $\mathbb{C}$ 上ベクトル空間となり、括弧積 $[\cdot, \cdot]$ を適当に定義することにより複素リー代数になる。
> この $\mathfrak{g}_\mathbb{C}$ を $\mathfrak{g}$ の **複素化** *(complexification)* といい、逆に $\mathfrak{g}$ を $\mathfrak{g}_\mathbb{C}$ の **実形** *(real form)* という。

- 言い換えると、$X, Y \in \mathfrak{g}$ に対して $X + iY \in \mathfrak{g}_\mathbb{C}$ を対応させるということ。
- 「適当」 の意味は括弧積 $[\cdot, \cdot]$ が普通の複素数の計算に従う $\mathbb{C}$-双線形形式になってくれるよう要請するという意味であって、式で書くと以下のように定義するということ。
$$
[X_1 + i Y_1, X_2 + i Y_2]
\coloneqq ([X_1, X_2] - [Y_1, Y_2] ) + i ([X_1, X_2] + [Y_1, X_2])
\quad \text{for all} \, X_1, X_2, Y_1, Y_2 \in \mathfrak{g}
$$

#### 例1: 一般線形リー代数 $\mathfrak{gl} (n, \mathbb{R})$

一般線形リー代数 $\mathfrak{gl} (n, \mathbb{R})$ の複素化は、$\mathfrak{gl} (n, \mathbb{C})$ と同型である。
$$
\mathfrak{gl} (n, \mathbb{R})_{\mathbb{C}} \cong \mathfrak{gl(n, \mathbb{C})}
$$

#### 例2: 特殊直交リー代数 $\mathfrak{so} (n)$

<u>実</u> 歪対称行列の集まりである特殊直交リー代数 $\mathfrak{so} (n)$ の複素化は、<u>複素</u> 歪対称行列の集まりである $\mathfrak{so} (n, \mathbb{C})$ と同型である。
$$
\mathfrak{so} (n)_{\mathbb{C}} \cong \mathfrak{so}(n, \mathbb{C})
$$

#### 例3: 特殊ユニタリリー代数 $\mathfrak{su} (n)$

トレースゼロの歪エルミート行列の集まりである特殊ユニタリリー代数 $\mathfrak{su} (n)$ の複素化は、トレースゼロの任意の複素行列の集まりである $\mathfrak{sl} (n, \mathbb{C})$ と同型である。
$$
\mathfrak{su} (n)_{\mathbb{C}} \cong \mathfrak{sl}(n, \mathbb{C})
$$

#### 例4: 特殊線形リー代数 $\mathfrak{sl} (n, \mathbb{R})$

トレースゼロの任意の実行列の集まりである特殊線形リー代数 $\mathfrak{sl} (n, \mathbb{R})$ の複素化は、先ほどの $\mathfrak{sl} (n, \mathbb{C})$ と同型である。
$$
\mathfrak{sl} (n, \mathbb{R})_{\mathbb{C}} \cong \mathfrak{sl}(n, \mathbb{C})
$$

例3, 4 で見たように、異なるリー代数 $\mathfrak{su} (n), \mathfrak{sl} (n, \mathbb{R})$ の複素化が、同じリー代数 $\mathfrak{sl} (n, \mathbb{C})$ と同型になることもある。

すなわち、 $\mathfrak{su} (n)$ と $\mathfrak{sl} (n, \mathbb{R})$ はともに $\mathfrak{sl} (n, \mathbb{C})$ の実形である。


## ルート系

ここでは特定のリー代数についての議論からいったん離れ、「ルート系」と呼ばれるある特別なベクトル空間の一般論について議論する。
後に、複素半単純リー代数から「ルート系」を構成していく様を述べていくが、その前に先に「ルート系」の特徴を探っておこうという訳である。

> **定義 (ルート系)**
>
>  $V$ を内積 $(\cdot, \cdot)$ が定義された <u>有限次元実</u>ベクトル空間とする。
> $V$ の<u>有限</u>部分集合 $\Phi$  が以下の条件をすべて満たす時、$(V, \Phi)$  は **ルート系** *(root system)* であるという。
>
> 0. (非零)：$\Phi$ は $0$ ベクトルを含まない。
> 1. $\Phi$ は $V$ を張る。
> 2. (スカラー倍の制限)：$\alpha \in \Phi$ であるならば、$\alpha$ の定数倍で $\Phi$ に含まれるのは $\alpha$ と $-\alpha$ のみである。
> 3. (鏡映閉包性)：任意の $\alpha \in \Phi$ に直交する超平面に関する鏡映 $s_\alpha$
> $$
> s_\alpha (x) = x - 2 \frac{(x, \alpha)}{(\alpha, \alpha)} \alpha
> \quad (x \in V)
> $$
> は、$\Phi$ 全体を $\Phi$ 自身に写す。
> 4. (結晶基底条件)：任意の $\alpha, \beta \in \Phi$ について
> $$
> \langle \beta, \alpha \rangle \coloneqq 2 \frac{(\beta, \alpha)}{(\alpha, \alpha)}
> $$
> は整数である。

- 単に $\Phi$ をルート系と呼ぶ事もある。当たり前だが $\Phi$ は単なる $V$ の部分集合であって、部分空間 (ベクトル空間) ではない。
- $\Phi$ の元を **ルート** *(roots)* と呼ぶ。

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

$$
SU (2) = \{ g \in GL(2, \mathbb{C}) \mid g^\dagger g = I_2, \
\det g = 1\}
$$

公式 $\det e^A = e^{\mathrm{Tr} (A)}$ により、 リー群 $SU (2)$ に付随するリー代数 $\mathfrak{su} (2)$ は、トレースがゼロの $2 \times 2$ 歪エルミート行列全体の集合となる。

$$
\mathfrak{su} (2) = \{ X \in \mathfrak{gl}(2, \mathbb{C}) \mid
\mathrm{Tr} (X) = 0 ,
X^\dagger + X = 0 \}
$$

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

