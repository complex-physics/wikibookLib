Quantum Linear Regression



在任何回归问题，给定输入特征 $x^{(1)}, x^{(2)} \ldots x^{(N)}$ ，算出预测 $y_{i} \in R$。其中输入可以看成 $N$-维度的输入向量 $x \in R ^{N}$。在线性回归中，我们把输出看成输入的一个线性组合
$$
\begin{aligned}
y_{i}&=\theta_{1} x^{(1)}+\theta_{2} x^{(2)}+\ldots \theta_{N} x^{(N)}+b+e_{i} \\
&=\sum_{i=1}^{N} \theta_{i} x^{(i)}+b+e_{i}
\end{aligned}
$$
其中

- $e_{i}$ 是无法消除的误差，不可学习的参数
-  $\theta_{i}$ 对应每个特征，学习的参数
-  $b$ 是偏置，学习的参数

把参数 $\theta_{i} ; i \in\{1,2, . . N\}$ 用一个向量 $\theta \in R ^{N}$ 来表示，上面的线性方程可以写成
$$
y_{i} / x_{i}=\theta^{T} x_{i}+b+e_{i}
$$
其中

-  $y_{i} / x_{i}$ 表示： $y_{i}$ 的值取决于 $x_{i}$ 的条件。
- 误差 $e_{i}$ 需要符合征态分布，平均值的中心在0，标准差是 $\sigma$ :

$$
e_{i} \sim N\left(0, \sigma^{2}\right)
$$

给定 $x_{i}$ 后，项 $\theta^{T} x_{i}+b$ 是常数。
$$
\begin{array}{l}
\theta^{T} x_{i}+b+e_{i} \sim N\left(\theta^{T} x_{i}+b, \sigma^{2}\right) \\
\quad \rightarrow y_{i} / x_{i} \sim N\left(\theta^{T} x_{i}+b, \sigma^{2}\right)
\end{array}
$$
所以，目标标记 $y _{i}$ 也是一个征态分布，平均值在 $\theta^{T} x_{i}+b$ 
$$
\hat{y}_{i}= E \left[y_{i} / x_{i}\right]=\theta^{T} x_{i}+b
$$
误差的平分求和得到损失函数，对损失函数求最小值，可以确定模型参数 $\theta$ 和 $b$。

有了模型参数 $\theta$ 和 $b$ 之后，可以预测
$$
\hat{y}_{i}=\theta^{T} x_{i}
$$
对于有 $M$ 个数据点的系统，写成矩阵形式：
$$
\left[\begin{array}{c}
x_{1}^{T} \rightarrow \\
x_{2}^{T} \rightarrow \\
x_{i}^{T} \rightarrow \\
\cdot \cdot \\
x_{M \rightarrow}^{T}
\end{array}\right] \theta=\left[\begin{array}{c}
y_{1} \\
\hat{y}_{2} \\
\ddot{y}_{i} \\
\ddot{y}_{M}
\end{array}\right]
$$
把输入特征向量组成一个矩阵 $X \in R ^{M \times(N+1)}$ ，预测值构成一个向量 $\hat{Y}_{i} \in R ^{M}$, 预测方程可以写成
$$
X \theta=\hat{Y}
$$
真实目标值 $y_{i}$ 组成向量 $Y \in R ^{M}$, 那么误差向量 $e \in R ^{M}$ 可以写成
$$
e=Y-\hat{Y}=Y-X \theta
$$
损失函数写成：误差平方求和，再求平均
$$
L(\theta)=\frac{1}{M} \sum_{i=1}^{M} e_{i}^{2}
$$
这个式子也可以表达成误差向量 $e \in R ^{M}$ 与自己的点积，所以损失函数可以写成矩阵形式
$$
\begin{aligned}
L(\theta)&=\frac{1}{M} \sum_{i=1}^{M} e_{i}^{2} \\
&=\frac{1}{M} e ^{T} e \\
&=\frac{1}{M}(Y-X \theta)^{T}(Y-X \theta)
\end{aligned}
$$
最小化 $L(\theta)$ 来确定参数 $\theta$，最小化的需要求损失函数 $L(\theta)$ 相应参数  $\theta$ 的梯度
$$
\begin{aligned}
\nabla_{\theta} &=-\frac{2}{M} X^{T}(Y-X \theta)=0 \\
& \rightarrow\left(X^{T} X\right) \theta=X^{T} Y
\end{aligned}
$$
矩阵 $\left(X^{T} X\right)$ 是厄密的，所以可以当作量子系统的哈密顿量。

## Quantum Swap Test Subroutine

量子交换测试（The quantum swap test）是一个等效子程序，用测量Ancilla态 $|0\rangle$ 的概率来 计算两个量子状态的点乘积。计算点积是所有机器学习算法都需要的，所以交换测试子程序将是执行量子机器学习的核心。如图 $5-1$ 里的两个单位规范向量 $|a\rangle$ 和 $|b\rangle$ ，我们可以用线路计算出两个之间的点积。向量 $|a\rangle$ 和 $|b\rangle$ 可以用 $\log _{2} n$ 个量子比特，其实 $n$ 是这些态向量的维度。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20210822014703553.png" style="zoom:50%;" />

> Figure 5-1. Swap test to compute dot product

We will look at the combined state of the qubits at each stage of the swap test subroutine to understand the series of transformations involved in computing the dot product.

#### Initial State

初始态:
$$
\left|\psi_{o}\right\rangle=|0\rangle \otimes|a\rangle \otimes|b\rangle
$$

#### Hadamard Gate on the Ancilla Qubit

使用Hadamard门作用到ancilla量子比特上，系统的态变成
$$
\left|\psi_{1}\right\rangle=\frac{1}{\sqrt{2}}(|0\rangle+|1\rangle) \otimes|a\rangle \otimes|b\rangle
$$

#### Controlled Swap Operation

在这步中，根据ancilla量子比特态的情况，决定两个态要不要交换I 

- 如果ancilla量子比特态是 $|0\rangle$, 态向量 $|a\rangle$ 和 $|b\rangle$ 保持不变
- 如果ancilla量子比特态是 $|1\rangle$, 态向量 $|a\rangle$ 和 $|b\rangle$ 相互交换

所以经过控制交换操作（controlled SWAP），系统态是
$$
\left|\psi_{2}\right\rangle=\frac{1}{\sqrt{2}}(|0\rangle \otimes|a\rangle \otimes|b\rangle+|1\rangle \otimes|b\rangle \otimes|a\rangle)
$$

#### Hadamard Gate on the Control Qubit

然后对控制比特位加一个Hadamard门
$$
\begin{aligned}
\left|\psi_{3}\right\rangle &=H\left|\psi_{2}\right\rangle
\\&=\frac{1}{2}(|0\rangle+|1\rangle) \otimes|a\rangle \otimes|b\rangle+\frac{1}{2}(|0\rangle-|1\rangle) \otimes|b\rangle \otimes|a\rangle \\
&=\frac{1}{2}|0\rangle(|a\rangle \otimes|b\rangle+|b\rangle \otimes|a\rangle)+\frac{1}{2}|1\rangle(|a\rangle \otimes|b\rangle-|b\rangle \otimes|a\rangle)
\end{aligned}
$$
在态 $\left|\psi_{3}\right\rangle$ 中，ancilla量子比特处于 $|0\rangle$ 的概率可以通过态 $\left|\phi_{0}\right\rangle=\frac{1}{2}(|a\rangle \otimes|b\rangle+|b\rangle \otimes|a\rangle)$ 的平方
$$
\begin{aligned}
P(|0\rangle)=&\left\langle\phi_{0} \mid \phi_{0}\right\rangle \\
=&\frac{1}{4}(\langle b|\otimes\langle a|+\langle a|\otimes\langle b|)(|a\rangle \otimes|b\rangle+|b\rangle \otimes|a\rangle) \\
=&\frac{1}{4}(\langle b|\langle a \mid a\rangle| b\rangle+\langle b|\langle a \mid b\rangle| a\rangle+\langle a|\langle b \mid a\rangle| b\rangle+\langle a|\langle b \mid b\rangle| a\rangle) \\
=&\frac{1}{4}\left(1+2\langle a \mid b\rangle^{2}+1\right)\\
=&\frac{1}{2}+\frac{1}{2}\langle a \mid b\rangle^{2}
\end{aligned}
$$

- 如果测量ancilla量子比特处于 $|0\rangle$ 的概率是0.5，那么 $\langle a \mid b\rangle=0$，也就是态向量 $|a\rangle$ 和 $|b\rangle$ 正交。
- 如果态向量 $|a\rangle$ 和 $|b\rangle$ 相等，那么$\langle a \mid b\rangle=1$，所以ancilla量子比特处于 $|1\rangle$ 的概率是1

对比经典方法，计算点产品的量子交换测试方法的好处是时间复杂度，不会随着每个状态所需的Qubit数量而缩放。