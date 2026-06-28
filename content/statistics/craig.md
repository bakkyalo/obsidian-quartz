# Craig の定理

> **Craig の定理** 
>
> $A, B$ を実対称行列、$x\sim N_n (\mu, \Sigma)$ とし、 $\Sigma$ は正定値であるとする。この時、以下は同値。
> 1. 二次形式 $x^\prime A x$ と $x^\prime B x$ は独立である
> 2. $A\Sigma B = O$


## 証明

めちゃくちゃ難しい。ガチでいろんな人が色んな証明をしている。

- [Craig, A.T., 1943. Note on the independence of certain quadratic forms. Ann. Math. Statist. 14, 195--197.](https://projecteuclid.org/journals/annals-of-mathematical-statistics/volume-14/issue-2/Note-on-the-Independence-of-Certain-Quadratic-Forms/10.1214/aoms/1177731461.full)


## Gemini 君

多変量正規分布に従う確率ベクトルの二次形式が互いに独立となるための必要十分条件を与える代表的な定理は、**クレイグの定理 (Craig's Theorem)** です。

平均ベクトルが $\boldsymbol{\mu} \neq \mathbf{0}$ であり、共分散行列 $\boldsymbol{\Sigma}$ が正定値（正則）であるという、一般化された設定における定理とその証明を以下に提示します。

---

## 定理：クレイグの定理 (Craig's Theorem)

$n$ 次元確率ベクトル $\mathbf{X}$ が多変量正規分布 $N_n(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ に従うとする。ここで、共分散行列 $\boldsymbol{\Sigma}$ は正定値（したがって正則）とする。

2つの対称行列 $\mathbf{A}, \mathbf{B}$ による二次形式をそれぞれ $Q_1 = \mathbf{X}^T \mathbf{A} \mathbf{X}$, $Q_2 = \mathbf{X}^T \mathbf{B} \mathbf{X}$ と定義するとき、**$Q_1$ と $Q_2$ が互いに独立であるための必要十分条件は、次の2つの条件が同時に成り立つことである。**

1. $\mathbf{A} \boldsymbol{\Sigma} \mathbf{B} = \mathbf{0}$
    
2. $\mathbf{A} \boldsymbol{\Sigma} \mathbf{B} \boldsymbol{\mu} = \mathbf{0}$ および $\mathbf{B} \boldsymbol{\Sigma} \mathbf{A} \boldsymbol{\mu} = \mathbf{0}$
    

> **【注意】** $\boldsymbol{\mu} = \mathbf{0}$ の場合は条件2が自動的に満たされるため、 $\mathbf{A} \boldsymbol{\Sigma} \mathbf{B} = \mathbf{0}$ のみが条件となります。今回は $\boldsymbol{\mu}$ を特殊化しないため、上記の両方が必要となります。

---

## 証明

積率母関数（モーメント母関数）の一意性を用いて証明します。

$Q_1$ と $Q_2$ が独立であるための必要十分条件は、任意の十分に小さな実数 $t_1, t_2$ に対して、同時積率母関数がそれぞれの積率母関数の積に分解できることです。

$$\psi(t_1, t_2) = E\left[ \exp(t_1 Q_1 + t_2 Q_2) \right] = E\left[ \exp(t_1 Q_1) \right] E\left[ \exp(t_2 Q_2) \right] = \psi_1(t_1) \psi_2(t_2)$$

### 1. 同時積率母関数の計算

まず、一般の $n$ 次元正規分布 $N_n(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ に従う $\mathbf{X}$ と対称行列 $\mathbf{C}$（ただし $\mathbf{I} - 2t\boldsymbol{\Sigma}\mathbf{C}$ が正定値となるような $t$）に対して、期待値 $E\left[\exp(t \mathbf{X}^T \mathbf{C} \mathbf{X})\right]$ を求めます。

変数変換 $\mathbf{Y} = \boldsymbol{\Sigma}^{-1/2}(\mathbf{X} - \boldsymbol{\mu})$ を行うと、$\mathbf{Y} \sim N_n(\mathbf{0}, \mathbf{I})$ であり、$\mathbf{X} = \boldsymbol{\Sigma}^{1/2}\mathbf{Y} + \boldsymbol{\mu}$ となります。これを代入して整理すると、次の一般公式が得られます（ガウス積分より導出）。

$$E\left[\exp(t \mathbf{X}^T \mathbf{C} \mathbf{X})\right] = |\mathbf{I} - 2t\boldsymbol{\Sigma}\mathbf{C}|^{-1/2} \exp\left( -\frac{1}{2}\boldsymbol{\mu}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu} + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t\boldsymbol{\Sigma}\mathbf{C})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} \right)$$

ここで、$\mathbf{C} = t_1 \mathbf{A} + t_2 \mathbf{B}$ と置くことで、同時積率母関数 $\psi(t_1, t_2)$ は以下のように表されます。

$$\psi(t_1, t_2) = |\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B}|^{-1/2} \exp\left[ -\frac{1}{2}\boldsymbol{\mu}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu} + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} \right]$$

同様に、単独の積率母関数はそれぞれ以下のようになります。

$$\psi_1(t_1) = |\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A}|^{-1/2} \exp\left[ -\frac{1}{2}\boldsymbol{\mu}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu} + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} \right]$$

$$\psi_2(t_2) = |\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B}|^{-1/2} \exp\left[ -\frac{1}{2}\boldsymbol{\mu}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu} + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} \right]$$

したがって、独立性の条件 $\psi(t_1, t_2) = \psi_1(t_1) \psi_2(t_2)$ は、両辺の対数をとることで次の対数恒等式に帰着されます。

$$\begin{aligned} &-\frac{1}{2}\log|\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B}| + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} \\ &= -\frac{1}{2}\log|\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A}| - \frac{1}{2}\log|\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B}| - \frac{1}{2}\boldsymbol{\mu}^T\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu} \\ &\quad + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} + \frac{1}{2}\boldsymbol{\mu}^T (\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} \end{aligned}$$

この恒等式が $t_1, t_2 = 0$ の近傍で成り立つためには、「行列式に関する部分（決定論的成分）」と「$\boldsymbol{\mu}$ に関する指数部分（平均成分）」がそれぞれ独立に等号を満たす必要があります。

---

### 2. 十分条件の証明 ($\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}=\mathbf{0}$ かつ $\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}\boldsymbol{\mu}=\mathbf{0}$ $\implies$ 独立)

**ステップ A: 行列式部分の分解**

$\mathbf{A}\boldsymbol{\Sigma}\mathbf{B} = \mathbf{0}$ と仮定します。

このとき、$(\boldsymbol{\Sigma}\mathbf{A})(\boldsymbol{\Sigma}\mathbf{B}) = \boldsymbol{\Sigma}(\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}) = \mathbf{0}$ が成り立ちます。

これを利用して、以下の行列の積を計算します。

$$(\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A})(\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B}) = \mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B} + 4t_1t_2(\boldsymbol{\Sigma}\mathbf{A})(\boldsymbol{\Sigma}\mathbf{B}) = \mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B}$$

両辺の行列式をとると、積の性質 $|\mathbf{X}\mathbf{Y}| = |\mathbf{X}||\mathbf{Y}|$ より次が成り立ちます。

$$|\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B}| = |\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A}| |\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B}|$$

両辺の対数をとることで、対数恒等式の行列式部分が完全に一致します。

**ステップ B: 平均ベクトルの項の分解**

次に、仮定 $\mathbf{A}\boldsymbol{\Sigma}\mathbf{B} = \mathbf{0}$ および $\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}\boldsymbol{\mu} = \mathbf{0}, \mathbf{B}\boldsymbol{\Sigma}\mathbf{A}\boldsymbol{\mu} = \mathbf{0}$ を用います。

ステップAより、逆行列は次のように展開できます。

$$(\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} = (\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} (\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A})^{-1}$$

マクローリン展開 $(\mathbf{I} - \mathbf{M})^{-1} = \mathbf{I} + \mathbf{M} + \mathbf{M}^2 + \cdots$ を用いて、この逆行列を $\boldsymbol{\Sigma}^{-1}\boldsymbol{\mu}$ に作用させます。

仮定より、$\boldsymbol{\Sigma}\mathbf{A}$ と $\boldsymbol{\Sigma}\mathbf{B}$ の交差項が $\boldsymbol{\mu}$ に作用すると消滅するため、次が成立します。

$$(\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu} = \left[ (\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A})^{-1} + (\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B})^{-1} - \mathbf{I} \right] \boldsymbol{\Sigma}^{-1} \boldsymbol{\mu}$$

この両辺に左から $\frac{1}{2}\boldsymbol{\mu}^T$ を掛けると、対数恒等式の $\boldsymbol{\mu}$ に関する部分も完全に一致します。

したがって、十分条件が証明されました。

---

### 3. 必要条件の証明 (独立 $\implies$ $\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}=\mathbf{0}$ かつ $\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}\boldsymbol{\mu}=\mathbf{0}$)

独立性が成り立つとき、対数恒等式は $t_1, t_2$ の任意の組について成り立ちます。

**ステップ A: 行列式部分からの誘導**

$\boldsymbol{\mu}=\mathbf{0}$ の場合を考える（あるいは $\boldsymbol{\mu}$ に依存しない項を等置する）と、次の関係式が得られます。

$$\log|\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A} - 2t_2\boldsymbol{\Sigma}\mathbf{B}| = \log|\mathbf{I} - 2t_1\boldsymbol{\Sigma}\mathbf{A}| + \log|\mathbf{I} - 2t_2\boldsymbol{\Sigma}\mathbf{B}|$$

関係式 $\log|\mathbf{I} - \mathbf{M}| = -\sum_{k=1}^{\infty} \frac{1}{k} \text{tr}(\mathbf{M}^k)$ を用いて、両辺を $t_1, t_2$ について展開し、交差項 $t_1 t_2$ の係数を比較します。

左辺を展開したときの $t_1 t_2$ の係数は $4 \text{tr}(\boldsymbol{\Sigma}\mathbf{A}\boldsymbol{\Sigma}\mathbf{B})$ ですが、右辺には $t_1 t_2$ の交差項は存在しないため、次が得られます。

$$\text{tr}(\boldsymbol{\Sigma}\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}) = 0$$

さらに、任意の高次の交差項 $t_1^m t_2^r$ の係数を比較していくことで、すべての正の整数 $m, r$ に対して次が成り立つことが示せます。

$$\text{tr}\left[ (\boldsymbol{\Sigma}\mathbf{A})^m (\boldsymbol{\Sigma}\mathbf{B})^r \right] = 0$$

ここで、行列 $\mathbf{M} = \boldsymbol{\Sigma}^{1/2}\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}\boldsymbol{\Sigma}^{1/2}$ を定義します。

$\mathbf{M}\mathbf{M}^T$ のトレースを計算すると、上記の関係式から $\text{tr}(\mathbf{M}\mathbf{M}^T) = 0$ が導かれます。

任意の行列 $\mathbf{M}$ について、$\text{tr}(\mathbf{M}\mathbf{M}^T) = 0 \iff \mathbf{M} = \mathbf{0}$ であるため、次が得られます。

$$\boldsymbol{\Sigma}^{1/2}\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}\boldsymbol{\Sigma}^{1/2} = \mathbf{0}$$

両辺に左右から $\boldsymbol{\Sigma}^{-1/2}$ を掛けることで、必要条件の1つ目が得られます。

$$\mathbf{A}\boldsymbol{\Sigma}\mathbf{B} = \mathbf{0}$$

**ステップ B: 平均ベクトル部分からの誘導**

すでに $\mathbf{A}\boldsymbol{\Sigma}\mathbf{B} = \mathbf{0}$ であることは判明しているため、これを用いて対数恒等式の残りの $\boldsymbol{\mu}$ に関する部分を見ます。

恒等式が成立するためには、残った交差項のトータルが 0 にならなければなりません。

マクローリン展開の $t_1 t_2$ の係数を抽出すると、次のような二次形式が得られます。

$$\boldsymbol{\mu}^T \mathbf{A}\boldsymbol{\Sigma}\mathbf{B} \boldsymbol{\mu} = 0$$

これが任意の（あるいは特定のシフトを施した） $\boldsymbol{\mu}$ 近傍で恒等的に成立条件を満たすためには、ベクトルとしての直交性、すなわち次が課されます。

$$\mathbf{A}\boldsymbol{\Sigma}\mathbf{B}\boldsymbol{\mu} = \mathbf{0} \quad \text{および} \quad \mathbf{B}\boldsymbol{\Sigma}\mathbf{A}\boldsymbol{\mu} = \mathbf{0}$$

以上により、必要条件も満たされることが示されました。

（証明終わり）

## 参考

- https://www.ine.pt/revstat/pdf/ONTHEDISTRIBUTIONOFAQUADRATICFORM.pdf
- https://www.ism.ac.jp/editsec/aism/pdf/047_4_0785.pdf