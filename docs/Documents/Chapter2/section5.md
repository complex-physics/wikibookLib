Section5 相位估计

[TOC]





## 加密

对于一个可分解的正奇数 $N$, 很容易验证一个给定的数是否是分解因子，但是求它的素数因子很难。

>  例子
>
> - **简单**：验证104322269是否是208497011393549533的素数因子 
>
> $$
> \frac{208497011393549533}{104322269}=1998585857
> $$
>
> - **困难**：求一个数208497011393549533的素数因子
>
> $$
> 208497011393549533=104322269 \times 1998585857
> $$



所以根据这个原理，设计出很多被广泛应用的密码系统(如RSA)。

Shor算法就是用来分解素数的量子算法，Shor算法体现了量子计算的强大和重要性。这意味着如果有一台实用的量子计算机被建造出来，它可以用来破解加密代码。不用说，这个算法得到了很多人的关注。

## Shor算法

Shor算法包含两个部分：

1. 用经典计算机的简化算法，将因数分解简化成求阶问题(order finding)。
2. 用量子算法，解决求阶问题。



## 求阶order finding

#### 问题是什么

设 $x$ 和 $N$ 是正整数，以及 $x<N$. 数 $x$ 的(order)阶 $r$ 是使得下面公式成立的最小的正整数
$$
x^{r}=1 \bmod N
$$


#### 例子

> 对于 $x=5$ 和 $N=44$，求解 $x$ 的(order)阶 $r$ 
> $$
> x^{r}=a \bmod N
> $$

先计算

- $5^{1}=5$
- $5^{2}=25$
- $5^{3}=125$

我们注意到44在$5^{2}$和$5^{3}$之间，根据

- $44 \times 2=88$
- $125-88=37$  

所以
$$
5^{3}=37(\bmod 44)
$$
接着 

-  $5^{4}=625$ 
-  $(14\times 44)=616$ 
- $625-616=9$  

$$
5^{4}=9(\bmod 44)
$$

最后

-  $5^{5}=3125$ 
-  $71 \times 44=3124$  

$$
5^{5}=1(\bmod 44)
$$

所以  $x=5$ 的阶(order)是 5。



通过这个例子的计算，了解到计算  $x^{r}=1(\bmod N)$  是非常花费时间的。对于大数 $N$，最好的计算机也需要 $\log N$ 的时间来计算。

#### 相位估计

使用基于相位估计的量子算法可以更有效地解决这个问题。为了计算求阶问题(problem of order finding)，考虑幺正算符
$$
U_{x}|y\rangle=\left\{\begin{array}{ll}
|x y \bmod N\rangle & 0 \leq y \leq N-1 \\
|y\rangle & N \leq y \leq 2^{L}-1
\end{array}\right.
$$
其中 $L=\lceil\log N\rceil$. 

算符 $U_{x}$ 的本征态 
$$
\left|u_{t}\right\rangle=\frac{1}{\sqrt{r}} \sum_{k=0}^{r-1} \exp \left(-\frac{2 \pi i k t}{r}\right) \mid x^{k} \bmod \rangle
$$
本征值由下面的本征方程给出
$$
U_{x}\left|u_{t}\right\rangle=e^{2 \pi i(t / r)}\left|u_{t}\right\rangle
$$
我们注意到对这些状态可以应用相位估计算法来估计相位  $t / r$，以此得到阶(order)的估计。求阶算法(The order-finding algorithm)就是从这些本征态的叠加开始。

因为 $\sum_{k=0}^{r-1} \exp (-(2 \pi i k t) / r)=r \delta_{k, 0}$ 所以本征态的求和等于 $|1\rangle$，过程如下
$$
\begin{aligned}
& \frac{1}{\sqrt{r}} \sum_{t=0}^{r-1}\left|u_{t}\right\rangle
\\=& \frac{1}{\sqrt{r}} \sum_{t=0}^{r-1} \frac{1}{\sqrt{r}} \sum_{k=0}^{r-1} \exp \left(-\frac{2 \pi i k t}{r}\right)\left|x^{k} \bmod N\right\rangle
\\=& |1\rangle
\end{aligned}
$$
所以输入态为
$$
\left|\psi_{i n}\right\rangle=|1\rangle=\frac{1}{\sqrt{r}} \sum_{t=0}^{r-1}\left|u_{t}\right\rangle
$$
我们可以用量子并行计算 
$$
x^{k} \bmod N
$$
相位估计过程会给出周期 $r / t$ 从而找到阶 $r$。如果我们其实态 $|0\rangle^{\otimes n}|1\rangle$，于是 
$$
\frac{1}{\sqrt{r}} \sum_{t=0}^{r-1}\left(\frac{1}{\sqrt{2^{s}}} \sum_{k=0}^{2^{s}-1} \exp \left(-\frac{2 \pi i k t}{r}\right)|k\rangle\right)\left|u_{t}\right\rangle=\frac{1}{\sqrt{r}} \sum_{t=0}^{r-1}|t / r\rangle\left|u_{t}\right\rangle
$$
其中我们定义了
$$
|t / r\rangle=\frac{1}{\sqrt{2^{s}}} \sum_{k=0}^{2^{s}-1} \exp \left(-\frac{2 \pi i k t}{r}\right)|k\rangle
$$
测量会给出 $t / r$ 的估算，其中 $t$ 的范围 $0 \leq t \leq r-1 $。如果要获得准确的值，需要使用连分数。

求阶算法(The order-finding algorithm)只是Shor算法中的量子部分，其他部分涉及的是经典计算。





## 补充知识

1. Mod 运算符

### Mod 运算

Mod 运算符称为求模运算符（就是求余运算），求一个整数 $a$  除以另一个整数 $b$ 的余数 $c$，记作
$$
a \bmod b=c
$$
模运算的性质
$$
a b \bmod N=[(a \bmod N) \times(b \bmod N)] \bmod N
$$

> 例子：求解 $5^{3} \bmod 11$

$$
\begin{aligned}
& 5^{3} \bmod 11\\
=&5^{2} \times 5 \bmod 11 \\
=&25 \times 5 \bmod 11 \\
=&3 \times 5 \bmod 11 \\
=&15 \bmod 11\\
=&4
\end{aligned}
$$

更一般的我们可以写成
$$
f(r)=a^{r} \bmod N
$$


### 对称加密&非对称加密





































































