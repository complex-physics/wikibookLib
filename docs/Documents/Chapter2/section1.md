# Chapter01

从量子比特到量子门，到量子线路

1. 经典逻辑门
2. 单量子门
3. 双量子门
4. 门分解



[TOC]



### 经典逻辑门

量子门是构建量子计算的基本构件，在进入量子门讲解之前，我们先来回顾一下经典计算机的逻辑门是什么样的。

1. 非门(NOT gate)
2. 或门(OR gate)
3. 与门(AND gate)
4. 异或门(XOR gate)

非门操作的对象是单个逻辑比特
$$
\begin{array}{|c|c|}
\hline \begin{array}{c}
\text { 输入 } \\
A
\end{array} & \begin{array}{c}
\text { 输出 } \\
NOT A
\end{array} \\
\hline 0 & 1 \\
\hline 1 & 0 \\
\hline
\end{array}
$$
对于输入的逻辑比特，输出相反的值。

另外三个逻辑门是需要两个输入比特。
$$
\begin{array}{|l|l|c|}
\hline  {\text { 输入A }} & {\text { 输入B }} &\text { 输出(A+B) } \\
\hline 0 & 0 & 0 \\
\hline 0 & 1 & 1 \\
\hline 1 & 0 & 1 \\
\hline 1 & 1 & 1 \\
\hline
\end{array}
$$

- 只要两个输入中至少有一个为（1），则输出为（1）；
- 若两个输入均为（0），输出才为（0）。
- 换句话说，或门的功能是得到两个二进制数的最大值

而与门的功能是得到两个二进制数的最小值。
$$
\begin{array}{|l|l|c|}
\hline {\text { 输入 }} & \text { 输出 }& \text { 输出 } \\
\hline A & B & A \text { AND B } \\
\hline 0 & 0 & 0 \\
\hline 0 & 1 & 0 \\
\hline 1 & 0 & 0 \\
\hline 1 & 1 & 1 \\
\hline
\end{array}
$$
对于**异或门(XOR gate)**，若两个输入的电平不同，则输出为（1）；若两个输入的电平相同，则输出为（0）。

### 单量子门

由于量子门必须是**幺正算符**(unitary)，我们经常会在“门”和“算符”这两个词之间来回应用——所以请记住，在本文中，它们的意思是**相同的**。
$$
门=算符
$$
量子算符可以用矩阵表示。那么具有$n$输入和输出的量子门可以由度为$2^{n}$的矩阵表示。

例如

- 对比1个量子比特，要求对应作用的矩阵的自由度是$2^{1}=2 $，所以作用到1个量子比特的量子门是一个 $2 \times 2$ 的幺正矩阵 
- 对比2个量子比特，要求对应作用的矩阵的自由度是$2^{2}=4 $，所以作用到2个量子比特的量子门是一个 $4 \times 4$ 的幺正矩阵 

#### 量子非门

从最简单的量子非门(quantum NOT gate)开始讨论，其实我们见过量子非门，那就是 $X$ 泡利矩阵。
$$
X=U_{N O T}=\left(\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right)
$$
把量子非门$U_{N O T}$作用到标准基底
$$
|0\rangle=\left(\begin{array}{l}
1 \\
0
\end{array}\right), \quad|1\rangle=\left(\begin{array}{l}
0 \\
1
\end{array}\right)
$$
作用过程和结果就是矩阵与向量的乘积
$$
\begin{array}{l}
U_{N O T}|0\rangle=\left(\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right)\left(\begin{array}{l}
1 \\
0
\end{array}\right)=\left(\begin{array}{l}
0 \\
1
\end{array}\right)=|1\rangle \\
U_{N O T}|1\rangle=\left(\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right)\left(\begin{array}{l}
0 \\
1
\end{array}\right)=\left(\begin{array}{l}
1 \\
0
\end{array}\right)=|0\rangle
\end{array}
$$

#### 新表示

我们用了最直观的矩阵表示了量子门，以及量子门对量子比特的作用。现在介绍新的表示方法
$$
X|j\rangle=|j \oplus 1\rangle
$$
其中

- $|j\rangle$ 是量子比特的狄拉克标记(Dirac notation)
- $\oplus$ 是异或算符(XOR)

总共有两种可能

1. 如果 $j=0,$ 那么 $X|0\rangle=|0 \oplus 1\rangle=|1\rangle .$ 
2. 如果 $j=1,$ 那么 $X|1\rangle=|1 \oplus 1\rangle=|0\rangle$

##### 习题

我们已经介绍了量子非门(quantum NOT gate)作用到标准基底 $|0\rangle,|1\rangle$ 的结果。如果量子非门(quantum NOT gate)作用到下面的基底会有什么结果？
$$
|+\rangle=\frac{1}{\sqrt{2}}\left(\begin{array}{l}
1 \\
1
\end{array}\right), \quad|-\rangle=\frac{1}{\sqrt{2}}\left(\begin{array}{c}
1 \\
-1
\end{array}\right)
$$

要求用量子非门(quantum NOT gate)的外积形式(outer product form)。

**解答**

在标准基底下，量子非门(quantum NOT gate)的矩阵可以写作
$$
X=\left(\begin{array}{cc}
\langle 0|X| 0\rangle & \langle 0|X| 1\rangle \\
\langle 1|X| 0\rangle & \langle 1|X| 1\rangle
\end{array}\right)
$$
你可以验证一下，这个矩阵可以写成外积形式(outer product form)
$$
X=|0\rangle\langle 1|+| 1\rangle\langle 0|
$$
所以量子非门(quantum NOT gate)作用到标准基底 $|0\rangle,|1\rangle$ 的过程可以用外积形式(outer product form)写成
$$
\begin{aligned}
X|0\rangle &=(|0\rangle\langle 1|+| 1\rangle\langle 0|)|0\rangle \\
&=|0\rangle\langle 1 | 0\rangle+|1\rangle\langle 0 | 0\rangle \\
&=|1\rangle
\end{aligned}
$$
和
$$
\begin{aligned}
X|1\rangle &=(|0\rangle\langle 1|+| 1\rangle\langle 0|)|1\rangle \\
&=|0\rangle\langle 1 | 1\rangle+|1\rangle\langle 0 | 1\rangle \\
&=|0\rangle
\end{aligned}
$$
其中我们用了基底的正交性

- $\langle 1 \mid 1\rangle=0$
- $\langle 0 \mid 0\rangle=0$

要写出量子非门(quantum NOT gate)的矩阵形式，我们需要写出两个基底之间的转换矩阵
$$
U_{\text {trans}}=\left(\begin{array}{cc}
\langle+| 0\rangle & \langle+| 1\rangle \\
\langle-| 0\rangle & \langle-| 1\rangle
\end{array}\right)
$$
的具体元素。

其中 $\{|+\rangle,|-\rangle\}$ 态在标准基底下的形式是
$$
|+\rangle=\frac{1}{\sqrt{2}}\left(\begin{array}{l}
1 \\
1
\end{array}\right), \quad|-\rangle=\frac{1}{\sqrt{2}}\left(\begin{array}{c}
1 \\
-1
\end{array}\right)
$$
所以计算矩阵元素的过程就是简单的内积计算:
$$
\begin{array}{l}
\langle+| 0\rangle=\frac{1}{\sqrt{2}}(1 \quad 1)\left(\begin{array}{l}
1 \\
0
\end{array}\right)=\frac{1}{\sqrt{2}} \\
\langle+| 1\rangle=\frac{1}{\sqrt{2}}(1 \quad 1)\left(\begin{array}{l}
0 \\
1
\end{array}\right)=\frac{1}{\sqrt{2}} \\
\langle-| 0\rangle=\frac{1}{\sqrt{2}}(1 \quad-1)\left(\begin{array}{l}
1 \\
0
\end{array}\right)=\frac{1}{\sqrt{2}} \\
\langle-| 1\rangle=\frac{1}{\sqrt{2}}(1 \quad-1)\left(\begin{array}{l}
1 \\
0
\end{array}\right)=-\frac{1}{\sqrt{2}}
\end{array}
$$
所以最后我们得到了转换矩阵
$$
U_{\text {trans}}=\frac{1}{\sqrt{2}}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right)=H
$$

我们最后给这个转换矩阵用了一个符号$H$，因为这个矩阵有专门的名称——Hadamard矩阵。



#### Hadamard矩阵

标准基底经过Hadamard矩阵变换得到的新基底称为Hadamard基底
$$
\begin{aligned}
U_{N O T}^{H} &=H U_{N O T} H\\
&=\frac{1}{2}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right)\left(\begin{array}{cc}
0 & 1 \\
1 & 0
\end{array}\right)\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right) \\
&=\frac{1}{2}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right)\left(\begin{array}{cc}
1 & -1 \\
1 & 1
\end{array}\right) \\
&=\left(\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right)
\end{aligned}
$$


#### 相位翻转门(phase flip)

我们前面说到量子非门(quantum NOT gate)就是 $X$ 泡利矩阵。其他泡利矩阵也是单量子比特门。

 $Z$-泡利矩阵被称为相位翻转门(phase flip)因为它把量子比特$|\psi\rangle=\alpha|0\rangle+\beta|1\rangle$ 转换为 $\left|\psi^{\prime}\right\rangle=\alpha|0\rangle-\beta|1\rangle .$ 

这个过程可以写成矩阵表示:
$$
Z|\psi\rangle=\left(\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right)\left(\begin{array}{l}
\alpha \\
\beta
\end{array}\right)=\left(\begin{array}{c}
\alpha \\
-\beta
\end{array}\right)
$$
这个过程也可以写成外积形式(outer product form)表示:
$$
\begin{aligned}
Z|\psi\rangle &=(|0\rangle\langle 0|-| 1\rangle\langle 1|)(\alpha|0\rangle+\beta|1\rangle) \\
&=\alpha|0\rangle\langle 0 | 0\rangle+\beta|0\rangle\langle 0 | 1\rangle-\alpha|1\rangle\langle 1 | 0\rangle-\beta|1\rangle\langle 1 | 1\rangle \\
&=\alpha|0\rangle-\beta|1\rangle
\end{aligned}
$$
其中 $Z$-泡利矩阵的外积形式
$$
Z=|0\rangle\langle 0|-| 1\rangle\langle 1|
$$
很容易看出，通常我们可以表示 $Z$-泡利矩阵的作用
$$
Z|j\rangle=(-1)^{j}|j\rangle
$$

#### 相位移动门(phase shift)

 $Z$-泡利矩阵把相位做了一个$180^{o}$翻转，更一般的，我们希望这种相位移动可以是任意角度 $\theta$，实现这种功能的量子门叫做相位移动门(phase shift gate)
$$
P=\left(\begin{array}{cc}
1 & 0 \\
0 & e^{i \theta}
\end{array}\right)
$$
对于任意态
$$
P|\psi\rangle=\left(\begin{array}{cc}
1 & 0 \\
0 & e^{i \theta}
\end{array}\right)\left(\begin{array}{l}
\alpha \\
\beta
\end{array}\right)=\left(\begin{array}{c}
\alpha \\
e^{i \theta} \beta
\end{array}\right)
$$

##### 例子

描述布洛赫球表现下，相位移动门(phase shift)对量子比特的作用。

解答

任意单量子比特
$$
|\psi\rangle=\cos \theta|0\rangle+e^{i \phi} \sin \theta|1\rangle
$$
相位移动门(phase shift gate)的外积形式
$$
P=|0\rangle\left\langle 0\left|+e^{i \gamma}\right| 1\right\rangle\langle 1|
$$
所以
$$
\begin{aligned}
P|\psi\rangle &=\left(|0\rangle\left\langle 0\left|+e^{i \gamma}\right| 1\right\rangle\langle 1|\right)\left(\cos \theta|0\rangle+e^{i \phi} \sin \theta|1\rangle\right) \\
&=\cos \theta|0\rangle+e^{i(\gamma+\phi)} \sin \theta|1\rangle
\end{aligned}
$$
作用前后量子比特的相位变化 $\phi \rightarrow \phi+\gamma$

##### 特殊情况



1. Hadamard Gates 
2. The Phase Gates 

