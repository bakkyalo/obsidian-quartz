# 因子分析 (FA)

FA : Factor Analysis

目に見える観測データ (観測変数) の背後に、それらを支配する共通の見えない潜在因子が少数あると仮定し、その影響の大きさを逆問題として推定する方法である。

壮大なたとえ話をすると、物体の動きという目に見えるものを観測して、その運動を引き起こす 4つの力 (重力・電磁気力・強い力・弱い力) を見出し、それらの強さ (結合定数) を推定しようとするようなものである。[^1]

[^1]: そんなので説明できるほど宇宙は単純ではないので安心してください。

## 問題設定

$D$ 次元の $N$ 個の観測データ $x \in \mathbb{R}^{D\times N}$ が、<u>少数</u> の潜在因子 (**共通因子** : *common factor*) $f \in \mathbb{R}^M \ (M \ll D)$ とノイズ (**独自因子** : *unique factor*) $\varepsilon\in \mathbb{R}^D$ によって線形に生成されているというモデルを仮定する。

> **因子分析** *(FA : Factor Analysis)*
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

### 直交モデル

### 斜交モデル

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


