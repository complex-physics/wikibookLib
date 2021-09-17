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