Section4 相位估计

[TOC]

相位估计(Phase Estimation)可以看成量子傅里叶变换的一个应用

## 目标

一个幺正算符 $U$ 的本征向量 $\left|\phi_{1}\right\rangle,\left|\phi_{2}\right\rangle, \ldots$, $\left|\phi_{d}\right\rangle$，这些 本征向量相互正交。本征方程
$$
U\left|\phi_{n}\right\rangle=e^{2 \pi i \theta_{n}}\left|\phi_{n}\right\rangle
$$
注意到，如果我们用算符 $U$ 对一个本征向量作用 $j$ 次
$$
U^{j}\left|\phi_{n}\right\rangle=U^{j-1}\left(e^{2 \pi i \theta_{n}}\left|\phi_{n}\right\rangle\right)=\left(e^{2 \pi i \theta_{n}}\right)^{j}\left|\phi_{n}\right\rangle=e^{2 \pi i \theta_{n} j}\left|\phi_{n}\right\rangle
$$
相位估计(Phase Estimation)想要解决的问题是: 

> 给一个幺正算符 $U$ 和对应的本征向量 $|\phi\rangle$ ，估算角度 $\theta$ ，这个角度和本征值 $e^{2 \pi i \theta_{n}}$ 有关。假设我们想知道相位角$\theta$到$m$位的精度。

给定初态
$$
\left|\psi_{i n}\right\rangle=|0\rangle^{\otimes m}|\phi\rangle
$$
其中 $|\phi\rangle$ 是我们已经知道的 $n$ 量子比特态的本征值 
$$
|\phi\rangle=\left|\phi_{n-1}, \phi_{n-2}, \ldots, \phi_{1}, \phi_{0}\right\rangle 
$$

## 算法过程

### 1 Hadamard 门

对 $|0\rangle$ 使用 Hadamard 门来生成叠加态
$$
\left|\psi^{\prime}\right\rangle=H^{\otimes m}\left|\psi_{i n}\right\rangle=\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)^{\otimes m}|\phi\rangle=\frac{1}{2^{m / 2}} \sum_{x=0}^{2^{m}-1}|x\rangle|\phi\rangle
$$

### 2 U 门

使用幺正算子如下
$$
\left|\psi^{\prime \prime}\right\rangle=\frac{1}{2^{m / 2}} \sum_{x=0}^{2^{m}-1}|x\rangle\left(U^{x}|\phi\rangle\right)=\frac{1}{2^{m / 2}} \sum_{x=0}^{2^{m}-1}|x\rangle\left(e^{2 \pi i \theta x}|\phi\rangle\right)
$$
因为 $e^{2 \pi i \theta x}$ 至少一个数字，我们可以随意移动它的位置。所以得到下式
$$
\left|\psi^{\prime \prime}\right\rangle=\frac{1}{2^{m / 2}} \sum_{x=0}^{2^{m}-1} e^{2 \pi i \theta x}|x\rangle|\phi\rangle=\left(\frac{1}{2^{m / 2}} \sum_{x=0}^{2^{m}-1} e^{2 \pi i \theta x}|x\rangle\right)|\phi\rangle
$$
我们可以丢掉后面 $n$ 个量子比特，留下我们在意的输出态
$$
\left|\psi_{\text {out }}\right\rangle=\frac{1}{2^{m / 2}} \sum_{x=0}^{2^{m}-1} e^{2 \pi i \theta x}|x\rangle
$$
以上的算法过程可以用一个线路图(phase kickback circuit)描述

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20210818041319171.png" style="zoom: 50%;" />

### 3 傅里叶逆变化

为了估算角度 $\theta$，我们使用 量子傅里叶逆变化(inverse quantum Fourier transform) $U_{F}^{\dagger}$ 作用到上一步的输出态
$$
U_{F}{ }^{\dagger}\left|\psi_{\text {out }}\right\rangle=\frac{1}{2^{m}} \sum_{x=0}^{2^{m}-1} \sum_{y=0}^{2^{m}-1} e^{\left(-2 \pi i x y / 2^{m}\right) / 2^{m}+2 \pi i \theta x}|y\rangle=\frac{1}{2^{m}} \sum_{x, y=0}^{2^{m}-1} e^{2 \pi i x\left(\theta-y / 2^{m}\right)}|y\rangle
$$
发现系统处于态 $|y\rangle$ 的概率
$$
\operatorname{Pr}(y)=\left|\frac{1}{2^{m}} \sum_{x=0}^{2^{m}-1} e^{2 \pi i x\left(\theta-y / 2^{m}\right)}\right|^{2}=\frac{1}{2^{2 m}}\left|\sum_{x=0}^{2^{m}-1} e^{2 \pi i x\left(\theta-y / 2^{m}\right)}\right|^{2}
$$
式子看起来有点复杂，我们可以用几何级数(geometric series)估算这个项

如果 $|r|<1$，级数求和得到 
$$
\sum_{n=0}^{\infty} a r^{n}=\frac{a}{1-r}
$$
这个求和是有限的 
$$
\sum_{n=0}^{m-1} a r^{n}=a \frac{r^{m}-1}{r-1}
$$
如果我们让 $a=1$ 和 $r=e^{2 \pi i x\left(\theta-y / 2^{m}\right)}$，那么这个几何级数就是上面的概率函数
$$
\sum_{n=0}^{m-1} a r^{n}\rightarrow \sum_{x=0}^{2^{m}-1} e^{2 \pi i x\left(\theta-y / 2^{m}\right)}
$$
所以根据几何级数的求和公式，我们可以计算出概率
$$
\operatorname{Pr}(y)=\frac{1}{2^{2 m}}\left|\frac{r^{2 m}-1}{r-1}\right|^{2}
$$

## 估计误差

> 我们希望估计这个概率的下限

把估算的相位写成
$$
\theta=2 \pi\left(\frac{c}{2^{m}}+\delta\right)
$$
其中 

- $c=c_{n-1} c_{n-2} \cdots c_{1} c_{0}$
- $2 \pi \frac{c}{2^{m}} $ 是 $\theta$ 的最佳 n 比特估计

概率
$$
\begin{aligned}
\operatorname{P}(j)&=\frac{1}{2^{2 m}}\left|\frac{r^{2 m}-1}{r-1}\right|^{2}
\end{aligned}
$$
对于任何 $z \in\left[0, \frac{1}{2}\right],$ 有 $2 z \leqslant \sin (\mathrm{T} z) \leqslant \pi z,$ 我们得到
$$
\begin{aligned}
\left|1-\mathrm{e}^{2 \pi \mathrm{i} \delta 2^{n}}\right| &=2\left|\sin \left(\pi \delta 2^{n}\right)\right| \geqslant 4|\delta| 2^{n} \\
|1-\mathrm{e}^{2 \pi \mathrm{i} \delta} | &=2|\sin (\pi \delta)| \leqslant 2 \pi|\delta|
\end{aligned}
$$
概率
$$
\begin{aligned}
\operatorname{P}(j)&=\frac{1}{2^{2 m}}\left|\frac{r^{2 m}-1}{r-1}\right|^{2}\\
&=\left|c_{a}\right|^{2} \geqslant \frac{4}{\pi^{2}} \approx 0.405
\end{aligned}
$$


