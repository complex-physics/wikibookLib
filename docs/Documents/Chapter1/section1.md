# Section1经典逻辑门

从量子比特到量子门，到量子线路

1. 经典逻辑门
2. 单量子门
3. 双量子门
4. 门分解



[TOC]





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

