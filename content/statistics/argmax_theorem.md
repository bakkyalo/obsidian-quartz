# M 推定量の一致性

確率変数の列がある確率変数に **一様収束** する時、各関数列を最大化する点 (argmax) の列も収束先の確率変数を最大化する点 (argmax) に収束する。

標語的に書くと、確率変数列が $L_n (\theta) \to L(\theta) \ (n\to\infty)$ のように収束するとき、以下のように $\lim$ と $\arg\max$ を交換できるということである。

$$
\lim_{n\to \infty} {\arg\max}_{\theta \in \Theta_0} L_n (\theta) =
{\arg\max}_{\theta\in\Theta_0} L (\theta)
$$

さらに直感的には、「山頂は山頂に収束する」とも言えよう。

この定理は **最尤推定量の一致性** がある条件の下成立することを示す際のクライマックスで暗躍する。


## 定理の主張
状況としては、母数空間 $\Theta$、 真の値 $\theta_0$ を持つ確率密度関数 $f(x; \theta_0)$ から独立同一に $n$ 個のデータ $X_1, X_2, \dots, X_n$ を取得し、それらから確率変数 $L_n(\theta)$ が仕立て上げられていることを考えている。

> **M推定量の一致性**
>
> 以下の 4 条件を仮定する。
> 1. **コンパクト性**： 母数空間 $\Theta$ はコンパクト (有界閉集合) な距離空間である。
> 2. **連続性**： 関数 $M(\theta)$ は $\theta \in \Theta$ 上で連続である。
> 3. **最大値の一意性 (識別可能性)** ：
> 関数 $M(\theta)$ は、<u>ただ一つの点</u> $\theta_0 \in \Theta$ で最大値をとる。
> すなわち、任意の $\theta \neq \theta_0$ に対し、$M(\theta) < M(\theta_0)$
> 
> 4. **一様収束**：確率変数列 $L_n (\theta)$ は $M(\theta)$ に <u>一様に</u> 概収束する。すなわち
> $$
> \mathrm{P} \left( \lim_{n\to\infty} \sup_{\theta\in\Theta}
> \left\vert L_n (\theta) - M (\theta) \right\vert = 0
> \right) = 1
> $$
>
> この時、$L_n (\theta)$ を最大化する推定量 $\hat{\theta}_n = {\arg\max}_{\theta\in\Theta} L_n(\theta)$ は、真のパラメータ $\theta_0$ に概収束する。
> $$
> \hat{\theta}_n \xrightarrow{a.s.} \theta_0 \quad (n\to\infty)
> $$

- $L_n (\theta)$ を「1個のデータ当たりの対数尤度」、$M (\theta)$ を「期待対数尤度」とすれば、これは最尤推定量の一致性を表すことになる。詳細はそちらで...
- 母数空間は必ずしも距離空間である必要はなく、可分で第一可算でありさえすればよい。ただ、実用性などを鑑みてここでは距離空間を仮定することにする。
- 一様収束の仮定を「確率収束」に置き換えれば、結論をそのまま「確率収束」に置き換えたものが成立する。


## 証明

概収束性の証明は、確率 1 の標本空間 $\Omega_0$ の任意の元 $\omega$ を固定して、確率変数列の収束の問題を通常の関数列の問題に置き換えるのが常套手段である。

あとは $\epsilon-\delta$ 論法の練習問題になる。

### 初期設定

$L_n (\theta)$ が $M (\theta)$ に一様収束するような標本の集合 (事象) を $\Omega_0$ とする。
$$
\Omega_0 \coloneqq \biggl\{
\omega \biggm| \lim_{n\to\infty} \sup_{\theta\in\Theta} 
\vert L_n (\theta) - M(\theta) \vert = 0
\biggr\}
$$

仮定より、この事象は確率 1 で起こる ($P(\Omega_0) = 1$)。

示すべきことは、任意の $\omega\in\Omega_0$ に対して、推定量 $\hat{\theta}_n (\omega)$ が $\theta_0$ に収束することである。

以下、$\omega \in \Omega_0$ を 1 つ固定して考える。

### 背理法の仮定

背理法の仮定として、「ある $\omega \in \Omega_0$ において、推定量 $\hat{\theta}_n (\omega)$ が $\theta_0$ に収束しない」と仮定する。

真の値 $\theta_0$ から距離が $\epsilon$ 以上離れているパラメータの空間 $K$ を
$$
K \coloneqq \left\{
\theta \in \Theta \mid \|\theta-\theta_0 \| \geq \epsilon
\right\}
$$
のように定義すると、
背理法の仮定は 「ある $\epsilon > 0$ が存在し、任意の自然数 $N \in \mathbb{N}$ に対し、$\hat{\theta}_n (\omega) \in K$ となる $n >N$ が存在する」と言い換えられる。


### 領域 $K$ の性質

仮定より、母数空間 $\Theta$ はコンパクトであり、かつ今の定義から $K$ はその部分閉集合であるため、$K$ もコンパクトである。
さらに仮定より、関数 $M (\theta)$ は連続関数であるため、コンパクト集合 $K$ 上で最大値を持つ。

しかし、$M (\theta)$ は $\theta_0$ において <u>一意に</u> 最大値を持つため、$\theta_0$ を含まない $K$ においては、最大値は $M (\theta_0)$ よりも真に小さい。
この差を $\delta > 0$ とする。

言い換えると、ある正の実数 $\delta > 0$ が存在して、
$$
\begin{equation}
\sup_{\theta\in K} M(\theta) \leq M (\theta_0) - \delta 
\end{equation}
$$
となることが言える。

<!--
特に、背理法の仮定を満たす $n = n_0$ については以下が言える。
$$
\delta \leq M (\theta_0) - M(\hat{\theta}_{n_0} (\omega))
$$
-->

### 一様収束の定義の利用

一方、今固定している標本 $\omega$ は一様収束を満たす集合 $\Omega_0$ の元であるから、ある自然数 $\tilde{N}$ が存在して、 $n > \tilde{N}$ を満たす任意の $n$ に対して
$$
\sup_{\theta\in\Theta} \vert L_n (\theta; \omega) - M (\theta) \vert < \frac{\delta}{2}
$$

とできる (任意の正の実数として $\frac{\delta}{2}$ を採用した)。

### 矛盾の証明

仮定より、推定量 $\hat{\theta}_n$ は $L_n (\theta)$ を最大化するため、
$$
L_n (\theta_0) \leq L_n (\hat{\theta}_n)
$$

これを用いて以下のような評価ができる。

$$
\begin{align}
 M (\theta_0) - M (\hat{\theta}_n) 
 &= \left[M(\theta_0) - L_n (\theta_0) \right]
     + [ L_n (\theta_0) - L_n (\hat{\theta}_n) ]
     + [ L_n (\hat{\theta}_n)- M(\hat{\theta}_n) ]\\
 &\leq \left[M(\theta_0) - L_n (\theta_0) \right]
     + 0
     + [ L_n (\hat{\theta}_n)- M(\hat{\theta}_n) ]\\
 &\leq \vert L_n (\theta_0) - M (\theta_0) \vert
     + \vert L_n(\hat{\theta}_n ) - M (\hat{\theta}_n) \vert\\
 &\leq 2 \sup_{\theta\in\Theta} \vert L_n (\theta) - M(\theta) \vert
\end{align}
$$

ここで背理法の仮定における任意の自然数 $N$ として $\tilde{N}$ をとると、$\hat{\theta}_{n_0} (\omega) \in K$ となるような $n_0 > \tilde{N}$ が存在することがいえる。
「領域 $K$ の性質」により、この $n = n_0$ においては今の不等式の最左辺を下から $\delta$ で抑えることができるので

$$
\frac{\delta}{2} \leq \sup_{\theta\in\Theta} \vert L_{n_0} (\theta; \omega) - M(\theta) \vert
$$

これと同時に、一様収束の定義における任意の $n$ として $n_0$ をとると

$$
\sup_{\theta\in\Theta} \vert L_{n_0} (\theta; \omega) - M (\theta) \vert < \frac{\delta}{2}
$$

でもあり、矛盾。

以上から、「任意の $\omega \in \Omega_0$ に対して、推定量 $\hat{\theta}_n (\omega)$ が $\theta_0$ に収束する」と結論付けられ、概収束の定義から

$$
\hat{\theta}_n \xrightarrow{a.s.} \theta_0 \quad (n\to\infty)
$$

Q.E.D.


## 注意点
1. 各点収束ではダメである。通常の大数の法則は各点収束に関する定理であるため、**一様大数の法則** というより強い前提条件を要する定理を用いることになる。
2. 下でも述べるが、ここで言う「収束」とは「確率収束」と「概収束」どちらでも成立する。定理の証明に 大数の弱法則/強法則 どちらを使用するかの違いであり、ほとんど同じように証明が可能である。
