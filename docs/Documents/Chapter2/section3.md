# s2.3 量子傅里叶

1. 二量子比特态和门的矩阵表示
   - 态的表示
   - 



[TOC]





### 离散傅里叶vs量子傅里叶

#### 离散傅里叶

一个向量 $\{f(0), f(1), \ldots, f(N-1)\}$ 元素是复数，通过离散傅里叶变换可以转换成一个新的复向量  $\{\tilde{f}(0), \tilde{f}(1), \ldots, \tilde{f}(N-1) $\}
$$
\tilde{f}(k)=\frac{1}{\sqrt{N}} \sum_{x=0}^{N-1} e^{2 \pi i \frac{x k}{N}} f(x)
$$

####  量子傅里叶

对于一个 $n$ 量子比特的量子寄存器(对应 $N=2^{n}$ 个元素的向量)，一个幺正算子 $F$ 作用到这个向量态上
$$
F(|x\rangle)=\frac{1}{\sqrt{2^{n}}} \sum_{k=0}^{2^{n}-1} e^{2 \pi i \frac{x k}{2^{n}}}|k\rangle
$$
作用的结果是，一个任意态  $|\psi\rangle=\sum_{x} f(x)|x\rangle$ 被转换到
$$
\begin{aligned}
|\tilde{\psi}\rangle=&F|\psi\rangle
\\=&F\sum_{x} f(x)|x\rangle 
\\=&\sum_{x} f(x)F|x\rangle
\\=&\sum_{x} f(x)\frac{1}{\sqrt{2^{n}}} \sum_{k=0}^{2^{n}-1} e^{2 \pi i \frac{x k}{2^{n}}}|k\rangle
\\=&\sum_{k=0}^{2^{n}-1} \tilde{f}(k)|k\rangle
\end{aligned}
$$
其中

- 系数  $\{\tilde{f}(k)\}$ 就是系数 $\{f(x)\}$ 的离散傅里叶变换 
- 而算子 $F$ 就是量子傅里叶算符，把 $|\psi\rangle$ 转换到 $|\tilde{\psi}\rangle$

### QFT的线路图

下图就是QFT的线路图，我们详细分析每一步过程

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200513132430129.png" style="zoom:90%;" />



#### 输入

初态
$$
|x\rangle=\left|x_{n-1} x_{n-2} \ldots x_{0}\right\rangle
$$
表示一个 $n$ 位的量子比特态，

#### 第一位比特的操作

第一个Hadamard门作用到第一位比特
$$
\begin{aligned}
&H\left|x_{1} x_{2} \ldots x_{n}\right\rangle
\\=&H\left|x_{1}\right\rangle\left|x_{2} \ldots x_{n}\right\rangle
\\=&\frac{1}{\sqrt{2}}\left(|0\rangle+e^{i2 \pi   x_{1}}|1\rangle\right)\left|x_{2} \ldots x_{n}\right\rangle
\end{aligned}
$$
其中

- 如果 $x_{1}=0$ 那么 $H\left|x_{1}\right\rangle=\frac{|0\rangle+|1\rangle}{\sqrt{2}}$
- 如果 $x_{1}=1$ 那么 $H\left|x_{1}\right\rangle=\frac{|0\rangle-|1\rangle}{\sqrt{2}}$

#### 相位门

我们先介绍一下接下来遇到的门(phase gate)相位门的矩阵
$$
R_{k}=\left[\begin{array}{cc}
1 & 0 \\
0 &  e^{\left(\frac{2 \pi i}{2^{k}}\right)}
\end{array}\right]
$$
这个门对标准基底的作用

- $R_{k}|0\rangle=|0\rangle$
- $ R_{k}|1\rangle=e^{\left(\frac{2 \pi i}{2^{k}}\right)}|1\rangle$



第一位量子比特接下来作为控制比特，和第二位量子比特一起遇到 控制 $R_{2}$ 门

- 如果控制比特是 $|0\rangle$，那么 $R_{2}$ 门不起作用
- 如果控制比特是 $|1\rangle$，那么 $R_{2}$ 门对第二位量子比特作用如下

$$
\begin{aligned}
R_{2}|0\rangle=&|0\rangle
\\
R_{2}|1\rangle=&e^{\left(\frac{2 \pi i}{2^{2}}\right)}|1\rangle
\end{aligned}
$$

所以
$$
\begin{aligned}
&CR_{2}\frac{1}{\sqrt{2}}\left(|0\rangle+e^{i2 \pi   x_{1}}|1\rangle\right)\left|x_{2} \ldots x_{n}\right\rangle
\\=& \frac{1}{\sqrt{2}}\left(|0\rangle+e^{i2 \pi   x_{1}}|1\rangle R_{2}\left|x_{2} \right\rangle\right)\left|x_{3} \ldots x_{n}\right\rangle
\\=& \frac{1}{\sqrt{2}}\left(|0\rangle+e^{i2 \pi   x_{1}}e^{\left(x_{2}\frac{2 \pi i}{2^{2}}\right)}|1\rangle \left|x_{2} \right\rangle\right)\left|x_{3} \ldots x_{n}\right\rangle
\end{aligned}
$$


#### 通用公式

仅看第一条线路，第一个量子比特还会陆续受到控制 $R_{3}, R_{4}$ 直到 $R_{n}$ ，第一个比特最后会是
$$
\begin{aligned}
&R_{3}, R_{4}\dots R_{n}\frac{1}{\sqrt{2}}\left(|0\rangle+e^{i2 \pi   x_{1}}e^{\left(x_{2}\frac{2 \pi i}{2^{2}}\right)}|1\rangle  \right)\left|x_{2} \ldots x_{n}\right\rangle
\\=& \frac{1}{\sqrt{2}}\left(|0\rangle+e^{i2 \pi   x_{1}}e^{\left(x_{2}\frac{2 \pi i}{2^{2}}\right)}e^{\left(x_{3}\frac{2 \pi i}{2^{3}}\right)}\dots e^{\left(x_{n}\frac{2 \pi i}{2^{n}}\right)}|1\rangle  \right)\left|x_{2} \ldots x_{n}\right\rangle
\\=& \frac{1}{\sqrt{2}}\left(|0\rangle+ e^{i2\pi\left(x_{1}+x_{2}\frac{1}{2^{2}}+x_{3}\frac{1}{2^{3}}\dots+x_{n}\frac{1}{2^{n}} \right)}  |1\rangle \right)\left|x_{2} \ldots x_{n}\right\rangle
\end{aligned}
$$
我们看到指数上有一个数列
$$
x_{1}+x_{2} \frac{1}{2^{2}}+x_{3} \frac{1}{2^{3}} \cdots+x_{n} \frac{1}{2^{n}}
$$
为了方便书写，我们给数列一个新的标记符号
$$
0 . x_{l} x_{l+1} \ldots x_{m}=\frac{1}{2} x_{l}+\frac{1}{4} x_{l+1}+\cdots+\frac{1}{2^{m-l+1}} x_{m}
$$

所以第一个比特最后会是
$$
\begin{aligned}
& \frac{1}{\sqrt{2}}\left(|0\rangle+ e^{i2\pi\left(x_{1}+x_{2}\frac{1}{2^{2}}+x_{3}\frac{1}{2^{3}}\dots+x_{n}\frac{1}{2^{n}} \right)}  |1\rangle \right)\left|x_{2} \ldots x_{n}\right\rangle
\\=& \frac{1}{\sqrt{2}}\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{2} \dots x_{n}}|1\rangle\right)\left|x_{2} \dots x_{n}\right\rangle
\end{aligned}
$$




#### 第2位比特的操作

第2个Hadamard门作用到第2位比特
$$
\begin{aligned}
& H\frac{1}{\sqrt{2}}\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{2} \dots x_{n}}|1\rangle \left|x_{2} \right\rangle\right)\left|x_{3} \ldots x_{n}\right\rangle
\\=&\frac{1}{\sqrt{2}}\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{2} \dots x_{n}}|1\rangle H \left|x_{2} \right\rangle\right)\left|x_{3} \ldots x_{n}\right\rangle
\\=&\frac{1}{2}\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{2} \dots x_{n}}|1\rangle  \right)\left(|0\rangle+e^{2 \pi i 0 \cdot x_{2}}|1\rangle\right)\left|x_{3} \ldots x_{n}\right\rangle
\end{aligned}
$$
控制- $R_{2}$ 到控制 $R_{n-1}$ 陆续作用到第2位比特，得到
$$
\frac{1}{2^{2 / 2}}\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{2} \ldots x_{n}}|1\rangle\right)\left(|0\rangle+e^{2 \pi i 0 . x_{2} \ldots x_{n}}|1\rangle\right)\left|x_{3} \ldots x_{n}\right\rangle
$$


#### 第n位比特的操作

通过上面的操作，我们可以得到这个线路的最后输出
$$
\frac{1}{2^{n / 2}}\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{2} \ldots x_{n}}|1\rangle\right)\left(|0\rangle+e^{2 \pi i 0 . x_{2} \ldots x_{n}}|1\rangle\right) \ldots\left(|0\rangle+e^{2 \pi i 0 . x_{n}}|1\rangle\right)
$$




### QFT的表示

量子傅里叶变换
$$
|\tilde{\psi}\rangle=F|\psi\rangle
$$
把一个量子态 $|\psi\rangle$ 映射到 另一个态 $|\tilde{\psi}\rangle$，我们可以从两个角度来理解这种变换

- 基底
- 系数





#### 乘积态表示

乘积态方式(product representation)表示量子傅里叶变换的过程
$$
\begin{aligned}
F(|x\rangle) &=\frac{1}{\sqrt{2^{n}}} \sum_{k=0}^{2^{n}-1} \exp \left(\frac{2 \pi i x k}{2^{n}}\right)|k\rangle \\
&=\frac{1}{\sqrt{2^{n}}} \sum_{k_{n}-1=0}^{1} \ldots \sum_{k_{0}=0}^{1} \exp \left(2 \pi i x \sum_{l=1}^{n} \frac{k_{n-l}}{2^{l}}\right)\left|k_{n-1} \ldots k_{0}\right\rangle \\
&=\frac{1}{\sqrt{2^{n}}} \sum_{k_{n-1}=0}^{1} \ldots \sum_{k_{0}=0}^{1} \otimes_{l=1}^{n} \exp \left(2 \pi i x \frac{k_{n-l}}{2^{l}}\right)\left|k_{n-l}\right\rangle \\
&=\frac{1}{\sqrt{2^{n}}} \otimes_{l=1}^{n}\left[\sum_{k_{n-l}=0}^{1} \exp \left(2 \pi i x \frac{k_{n-l}}{2^{l}}\right)\left|k_{n-l}\right\rangle\right] \\
&=\frac{1}{\sqrt{2^{n}}} \otimes_{l=1}^{n}\left[|0\rangle+\exp \left(2 \pi i x \frac{1}{2^{l}}\right)|1\rangle\right] \\
&=\frac{1}{\sqrt{2^{n}}}\left(|0\rangle+e^{2 \pi i 0 . x_{0}}|1\rangle\right)\left(|0\rangle+e^{2 \pi i 0 . x_{1} x_{0}}|1\rangle\right) \cdots
\\&\cdots\left(|0\rangle+e^{2 \pi i 0 . x_{n}-1 x_{n-2} \dots x_{0}}|1\rangle\right)
\end{aligned}
$$
也就是算子 $F$ 把基底 $|x\rangle$ 转变到基底 $|k\rangle$
$$
F(|x\rangle)=\frac{1}{\sqrt{2^{n}}} \sum_{k=0}^{2^{n}-1} e^{2 \pi i \frac{x k}{2^{n}}}|k\rangle
$$

#### 矩阵表示

当 $n=1$
$$
\begin{aligned}
F_{1}=&\frac{1}{\sqrt{2}}\left(\begin{array}{cc}
1 & 1 \\
1 & e^{2 \pi i / 2}
\end{array}\right)
\\=&\frac{1}{\sqrt{2}}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right)
\end{aligned}
$$
当 $n=2$
$$
\begin{aligned}
F_{2}=&\frac{1}{\sqrt{2^{2}}}\left(\begin{array}{cccc}
1 & 1 & 1 & 1 \\
1 & \omega_{2}^{-1} & \omega_{2}^{-2} & \omega_{2}^{-3} \\
1 & \omega_{2}^{-2} & \omega_{2}^{-4} & \omega_{2}^{-6} \\
1 & \omega_{2}^{-3} & \omega_{2}^{-6} & \omega_{2}^{-9}
\end{array}\right)
\\=&\frac{1}{\sqrt{2^{2}}}\left(\begin{array}{cccc}
1 & 1 & 1 & 1 \\
1 & -i & -1 & i \\
1 & -1 & 1 & -1 \\
1 & i & -1 & -i
\end{array}\right) .
\end{aligned}
$$
当 $n=3$
$$
F_{3}=\frac{1}{\sqrt{2^{3}}}\left[\begin{array}{cccccccc}
1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
1 & \omega & \omega^{2} & \omega^{3} & \omega^{4} & \omega^{5} & \omega^{6} & \omega^{7} \\
1 & \omega^{2} & \omega^{4} & \omega^{6} & 1 & \omega^{2} & \omega^{4} & \omega^{6} \\
1 & \omega^{3} & \omega^{6} & \omega^{1} & \omega^{4} & \omega^{7} & \omega^{2} & \omega^{5} \\
1 & \omega^{4} & 1 & \omega^{4} & 1 & \omega^{4} & 1 & \omega^{4} \\
1 & \omega^{5} & \omega^{2} & \omega^{7} & \omega^{4} & \omega^{1} & \omega^{6} & \omega^{3} \\
1 & \omega^{6} & \omega^{4} & \omega^{2} & 1 & \omega^{6} & \omega^{4} & \omega^{2} \\
1 & \omega^{7} & \omega^{6} & \omega^{5} & \omega^{4} & \omega^{3} & \omega^{2} & \omega^{1}
\end{array}\right]
$$
其中

- 傅里叶变换矩阵 $F_{n}$ 是 $N \times N$ 的矩阵，其中 $N \equiv 2^{n}$ 
- $\omega_{n}=e^{2 \pi i / N}$







