# 分割法

※どうやら日本人でこの辺りに興味がある人は皆無のようだ。

## 用語の定義

実験を実施する根源事象の集合 $\Omega$ を **観測空間** *Observational space*, あるいは **実験空間** *Total Experimental Space* と呼ぶ。

観測値 $Y$ とは、$\Omega$ から実数値 $\mathbb{R}$ への可測関数、すなわち確率変数である。
$$
Y : \Omega \to \mathbb{R}
$$

### 因子、水準、処理、割付

これらの概念は、実験者が系に加える操作ないし介入の構造を定義する。

実験者が影響を評価したいと考え、意図的に操作する属性の次元を **因子** *Factor* という。
因子の総数を $K$ とすると、それらは $\{ \mathcal{F_k} \}_{k=1}^K$ と表記される。

- 例：$\mathcal{F}_1 = \text{温度}, \ \mathcal{F}_2 = \text{圧力}$

そして、ある因子がとりうる具体的な値を **水準** *level* という。
因子 $\mathcal{F}_k$ が $n_k$ 個の水準 $l_{k1}, l_{k2}, \dots, l_{k_{n_k}}$ を取るとき、それらをまとめた有限集合
$$
\mathcal{L}_k = \{ l_{k1}, l_{k2}, \dots, l_{kn_k} \}
$$
を因子 $\mathcal{F}_k$ の **水準集合** と呼ぶ。
- 例：
	- 温度因子 $\mathcal{F}_1$ の水準集合 $\mathcal{L}_1 = \{ 100 \,{}^\circ\mathrm{C}, \, 200 \, {}^\circ\text{C} \}$
	- 圧力因子 $\mathcal{F}_2$ の水準集合 $\mathcal{L}_2 = \{ 1 \, \mathrm{atm}, \, 2 \, \mathrm{atm} \}$

すべての因子の水準を 1 つずつ選んで組み合わせてできる具体的な実験条件を **処理** *Treatment* という。
すべての因子の水準集合 $\mathcal{L}_1, \mathcal{L}_2, \dots, \mathcal{L}_{K}$ の直積集合
$$
\mathcal{T} = \mathcal{L}_1 \times \mathcal{L}_2 \times \dots \times \mathcal{L}_K
$$
は **処理空間** *Treatment space* 、あるいは単に処理集合などと呼ばれ、その一つの元 $t \in \mathcal{L}$ を処理と定義する。

- 例：温度因子 $\mathcal{F}_1$ と圧力因子 $\mathcal{F}_2$ の例では、処理空間 $\mathcal{T}$ は
$$
\mathcal{T} = \mathcal{L}_1 \times \mathcal{L_2} 
= \{ (100 \, {}^\circ\mathrm{C}, 1 \, \mathrm{atm}), 
(100 \, {}^\circ\mathrm{C}, 2 \, \mathrm{atm}), 
(200 \, {}^\circ\mathrm{C}, 1 \, \mathrm{atm}),
(200 \, {}^\circ\mathrm{C}, 2 \, \mathrm{atm}) \}
$$
- $\mathcal{T}$ の元 
$(100 \, {}^\circ\mathrm{C}, 1 \, \mathrm{atm})$,
$(100 \, {}^\circ\mathrm{C}, 2 \, \mathrm{atm})$,
$(200 \, {}^\circ\mathrm{C}, 1 \, \mathrm{atm})$,
$(200 \, {}^\circ\mathrm{C}, 2 \, \mathrm{atm})$
が処理を表す。

そして、処理空間 $\mathcal{T}$ を実験空間 $\Omega$ に対応付けることを **割付** *Assignment* という。割付は写像
$$
\phi : \Omega \to \mathcal{T}
$$
で定義され、この写像 $\phi$ を **割付写像** *Assignment map* と呼ぶ。




## 参考


- 
- https://www.youtube.com/playlist?list=PLmM_3MA2HWpbhmpBvtdHxxVtMeNI6WERg