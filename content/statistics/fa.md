# 因子分析 (FA)

FA : Factor Analysis

目に見える観測データ (観測変数) の背後に、それらを支配する共通の見えない潜在因子が少数あると仮定し、その影響の大きさを逆問題として推定する方法である。

壮大なたとえ話をすると、物体の動きという目に見えるものを観測して、その運動を引き起こす 4つの力 (重力・電磁気力・強い力・弱い力) を見出し、それらの強さ (結合定数) を推定しようとするようなものである。[^1]

[^1]: そんなので説明できるほど宇宙は単純ではないので安心してください。

## 問題設定

$D$ 次元の $N$ 個の観測データ $x \in \mathbb{R}^{D\times N}$ が、<u>少数</u> の潜在因子 (**共通因子** : *common factor*) $f \in \mathbb{R}^M \ (M \ll D)$ とノイズ (**独自因子** : *unique factor*) $\varepsilon\in \mathbb{R}^D$ によって線形に生成されているというモデルを仮定する。

> [!info] **因子分析** *(FA : Factor Analysis)*
> $$
> x = \Lambda f + \varepsilon
> $$
> ただし以下を課す。
> - 共通因子 $f$ と独自因子 $\varepsilon$ は独立： $\mathbb{E} [fe^\prime] = 0$
> - $\mathbb{E} [ f ] = 0, \ \mathbb{E}[ff^\prime] = \Phi$ (正定値行列)
> - $\mathbb{E}[\varepsilon] = 0, \ \mathbb{E} [\varepsilon \varepsilon^\prime] = \Psi$ (対角要素が非負の対角行列; 独自因子間は無相関)

$\Lambda \in \mathbb{R}^{D\times M}$ を **因子負荷量** *(factor loading)* という。

これにさらに制約を加えて、色々なモデルが定義される。

- 共通因子 $f$ 間も無相関 ($\Phi = I_M$) → 直交モデル
- 共通因子 $f$ 間の相関を許す ($\Phi \neq I_M$) → 斜交モデル
- $\Lambda$ の一部を人為的に固定できる → **確証的因子分析** *(CFA : Confirmatory Factor Analysis)*

CFA に対して、$\Lambda$ のすべてを未知数として解くモデルを **探索的因子分析** *(EFA : Exploratory Factor Analysis)* という。[^2]

[^2]: このページで単に因子分析と言ったらそれは EFA のことである。
一方、この先の 共分散構造分析 (SEM) で主役になる因子分析は CFA の方 (新ページを作ります)。

### ヘイウッド・ケース

分散がマイナスになったり、相関係数が 1 を上回る結果になる場合を **ヘイウッド・ケース** *(Heywood case)* と呼ぶ。
主な原因は
- データが少なすぎる
- 因子が多すぎる
- 観測変数間に多重共線性 (マルチコ) がある


### 理論共分散行列

理論的な共分散行列を $\Sigma \coloneqq \mathbb{E} [xx^\prime]$ とすると、
$f$ と $\varepsilon$ の独立性の仮定などから
$$
\begin{align*}
\Sigma 
  &= \mathbb[(\Lambda f+\varepsilon)(\Lambda f + \varepsilon)^\prime]\\
  &= \Lambda \,\mathbb{E} [ff^\prime] \Lambda^\prime 
	  + \mathbb{E}[\varepsilon\varepsilon^\prime]\\
  &= \Lambda \Phi \Lambda^\prime + \Psi
\end{align*}
$$

### 回転の不定性

rotational indeterminacy

因子分析モデル
$$
x = \Lambda f + \varepsilon
$$
は、$\Lambda, f$ が一意に定まらない。
例えば、$M$ 次直交行列 $T \in O(M)$ を任意にとって[^arb]、
新たな因子負荷量 $\Lambda^*$ と共通因子 $f^*$ を
$\Lambda^* \coloneqq \Lambda T, \, f^* \coloneqq T^\prime f$ と定義すると、
モデル式は

[^arb]: 実は、 $T$ は正則行列 $T \in GL(M, \mathbb{R})$ でさえあればこの後の議論をある程度続けられるが、
後に説明する varimax および promax では結局直交行列であることが要求されるので、
$T$ は最初から 直交行列であるとしている。

$$
\begin{align*}
x &= \Lambda f + \varepsilon\\
  &= (\Lambda^* T^\prime) (T f^*) + \varepsilon\\
  &= \Lambda^* f^* + \varepsilon
\end{align*}
$$
のように同じ形の式に従う。
共通因子 $f^*$ の期待値は $\mathbb{E} [f^*] = 0$ のままであり、
共分散行列 $\Phi^* \coloneqq \mathbb{E} [f^* (f^*)^\prime]$ は
$$
\Phi^*
  = \mathbb{E} [T^\prime f (T^\prime f)^\prime]
  = T^\prime \mathbb{E} [ff^\prime] T
  = T^\prime \Phi T
$$
のように変換される。しかし、理論共分散行列 $\Sigma$ はこの変換によって
$$
\begin{align*}
\Sigma^*
	&\coloneqq \Lambda^* \Phi^*(\Lambda^*)^\prime + \Psi \\
	&= (\Lambda T) (T^\prime \Phi T) (\Lambda T)^\prime + \Psi \\
	&= \Lambda \Phi T^\prime + \Psi\\
	&= \Sigma
\end{align*}
$$
となり、変換 $T$ によってデータの平均および共分散構造が保たれる。

すなわち、因子分解モデルは直交行列 $T$ だけの任意性を持っており、
これを **回転の不定性** *(rotational indeterminacy)* と呼ぶ。

逆にいうと、我々は計算結果として出てくる共通因子 $f$ が分かりやすくなるように
直交行列 $T \in O(M)$ を好きに選べるということである。

とはいうものの、歴史的・伝統的に良いとされる直交変換が知られており、
それが以下の「直交因子モデル」 節で説明する varimax 回転である。

### 直交因子モデル

直交モデルは、共通因子 $f$ が無相関かつ標準化されているという仮定を新たに課す。

> - $
> \mathbb{E} [f] = 0, \,
> \mathbb{E} [ff^\prime] = I_M
> $



### 斜交因子モデル

## R の例

### `factanal()`

https://stat.ethz.ch/R-manual/R-patched/library/stats/html/factanal.html

標準に `factanal` がある。
最尤法。

### `psych::fa()`

https://cran.r-project.org/web/packages/psych/index.html

`psych` パッケージに `fa()` がある。
オプションの分量がエグい。

```r
library(psych)

result <- fa(
	r = data,
	nfactors = 3,
	rotate = "promax"	# 斜交モデル
	fm = ""				# factor method
)
```


