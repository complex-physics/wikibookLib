# Section4 H门与量子干涉

1. 先介绍量子门之间的两种关系
   - 并行
   - 顺序
2. 探索了Hadamard门的一些并行和顺序计算的性质
3. Hadamard门产生量子干涉



[TOC]

## 顺序计算和并行计算

<img src="C:\Users\JPZhuang\AppData\Roaming\Typora\typora-user-images\image-20200512193644394.png" alt="image-20200512193644394" style="zoom: 50%;" />

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20210816110424038.png" style="zoom: 50%;" />

### 顺序计算和并行计算的矩阵表示

从线路图看，两个量子门

- 同一个线上的前后顺序
- 同一个时间上的并行排列

对于前后顺序的两个量子门，可以先后作用到量子比特态上。作用效果也可以先把两个门反序相乘，再作用到量子比特态上。矩阵表示如下
$$
\begin{aligned}
H  H &=\frac{1}{\sqrt{2}}\left(\begin{array}{rr}
1 & 1 \\
1 & -1
\end{array}\right)\frac{1}{\sqrt{2}}\left(\begin{array}{rr}
1 & 1 \\
1 & -1
\end{array}\right)\\
&=\left(\begin{array}{ll}
1 & 0 \\
0 & 1
\end{array}\right)
\end{aligned}
$$
同一个时间上的并行排列的两个量子门，矩阵表示是两个门的张量积(tensor product)
$$
\begin{aligned}
H \otimes H &=\frac{1}{\sqrt{2}}\left(\begin{array}{rr}
H & H \\
H & -H
\end{array}\right)\\
&=\frac{1}{2}\left(\begin{array}{rrrr}
1 & 1 & 1 & 1 \\
1 & -1 & 1 & -1 \\
1 & 1 & -1 & -1 \\
1 & -1 & -1 & 1
\end{array}\right)
\end{aligned}
$$
注意：在前后顺序的量子门，矩阵相乘的顺序要相反，例如下面这个线路图

<img src="C:\Users\JPZhuang\AppData\Roaming\Typora\typora-user-images\image-20200512203558716.png" alt="image-20200512203558716" style="zoom:50%;" />

1. $P(\theta)$ 先作用到态上 $|\psi_{1}\rangle=P(\theta)|\psi_{0}\rangle$ 
2. 然后是 $H$ 作用到前面的结果 $|\psi_{2}\rangle=H|\psi_{1}\rangle=HP(\theta)|\psi_{0}\rangle$ 
3. 然后是 $H$ 作用到前面的结果 

$$
|\psi_{3}\rangle=Z|\psi_{2}\rangle=ZH|\psi_{1}\rangle=ZHP(\theta)|\psi_{0}\rangle
$$

4. 最后看效果，是 $Z H P(\theta)$ 作用到输入的初态上，和线路图上的左右顺序是相反的

$$
\begin{aligned}
Z H P(\theta) &=\left(\begin{array}{rr}
1 & 0 \\
0 & -1
\end{array}\right) \frac{1}{\sqrt{2}}\left(\begin{array}{rr}
1 & 1 \\
1 & -1
\end{array}\right)\left(\begin{array}{cc}
1 & 0 \\
0 & e^{i \theta}
\end{array}\right)
\\&=\frac{1}{\sqrt{2}}\left(\begin{array}{rr}
1 & e^{i \theta} \\
-1 & e^{i \theta}
\end{array}\right)
\end{aligned}
$$





## Hadamard 门 

1. Hadamard 作用到任意态 $ | \psi\rangle=\alpha|0\rangle+\beta|1\rangle .$  
2. 如果Hadamard连续作用到一个态上两次，它会回到原来的态
3. 前面是对单量子比特态的操作，如果对多个量子比特态的并行操作
   - 两个态并行
   - 三个态并行
   - 任意 $n$ 个态的简易缩写



#### 作用到任意态

Hadamard 作用到任意态 $ | \psi\rangle=\alpha|0\rangle+\beta|1\rangle .$  
$$
\begin{aligned}
H|\psi\rangle &=\alpha H|0\rangle+\beta H|1\rangle\\
&=\alpha\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)+\beta\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\left(\frac{\alpha+\beta}{\sqrt{2}}\right)|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)|1\rangle
\end{aligned}
$$

#### 顺序：两次回到原来

<img src="C:\Users\JPZhuang\AppData\Roaming\Typora\typora-user-images\image-20200512193644394.png" alt="image-20200512193644394" style="zoom: 50%;" />

如果Hadamard连续作用到一个态上两次，它会回到原来的态
$$
\begin{aligned}
&\quad H\left[\left(\frac{\alpha+\beta}{\sqrt{2}}\right)|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)|1\rangle\right] \\&=\left(\frac{\alpha+\beta}{\sqrt{2}}\right) H|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right) H|1\rangle \\
&=\left(\frac{\alpha+\beta}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\left(\frac{\alpha+\alpha+\beta-\beta}{2}\right)|0\rangle+\left(\frac{\alpha-\alpha+\beta+\beta}{2}\right)|1\rangle \\
&=\alpha|0\rangle+\beta|1\rangle=|\psi\rangle
\end{aligned}
$$


#### 两个并行

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20210816110424038.png" style="zoom: 50%;" />

对于二量子比特态 $|1\rangle|1\rangle$，使用两个Hadamard门 $H \otimes H$ 同时作用
$$
\begin{aligned}
(H \otimes H)|1\rangle|1\rangle &=(H|1\rangle)(H|1\rangle)\\
&=\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\frac{1}{2}(|00\rangle-|01\rangle-|10\rangle+|11\rangle)
\end{aligned}
$$
对于二量子比特态 $|0\rangle|0\rangle$，使用两个Hadamard门 $H \otimes H$ 同时作用  
$$
\begin{aligned}
(H \otimes H)|0\rangle|0\rangle &=(H|0\rangle)(H|0\rangle)\\
&=\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right) \\
&=\frac{1}{2}(|00\rangle+|01\rangle+|10\rangle+|11\rangle)
\end{aligned}
$$
对于乘积态 $|0\rangle|1\rangle$，使用两个Hadamard门 $H \otimes H$ 同时作用 
$$
\begin{aligned}
(H \otimes H)|0\rangle|1\rangle &=\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\frac{1}{2}(|00\rangle-|01\rangle+|10\rangle-|11\rangle)
\end{aligned}
$$




#### 三个并行

同时作用三个Hadamard门 
$$
\begin{aligned}
&(H \otimes H \otimes H)|0\rangle|0\rangle|0\rangle
\\=&(H|0\rangle)(H|0\rangle)(H|0\rangle) \\
=&\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right) \\
=& \frac{1}{\sqrt{2^{3}}}(|000\rangle+|001\rangle+|010\rangle+|100\rangle+|101\rangle\\
&+|110\rangle+|111\rangle)
\end{aligned}
$$

#### n个并行 & 简标

当 $n$ 个Hadamard门并行作用到 $n$ 个量子比特上，这个过程可以称之为 (Hadamard transform) **Hadamard 变换**。如果都按照上面的方式书写，那会非常庞杂，所以我们可以使用一种简写符号来表示 $n$ 个并行的Hadamard门：
$$
H^{\otimes n}
$$
用这种符号表示的话

- 两个Hadamard门可以写成  $H^{\otimes 2} .$
- 三个 Hadamard门作用到态上可以写成 $H^{\otimes 3}|0\rangle|0\rangle|0\rangle$

从上面的例子我们知道
$$
\begin{aligned}
H^{\otimes 2} |0\rangle|0\rangle =\frac{1}{2}(|00\rangle+|01\rangle+|10\rangle+|11\rangle)
\end{aligned}
$$
从这个公式看出，如果多个量子比特态，结果会更加庞杂。所以除了算子需要简洁的表示方法，态也需要简洁表示方法。

- 用 $|x\rangle$ 表示普遍态。如果是二量子比特态，$x \in\{0,1\}^{2} $表示 $x$ 可以在集合中任选两个元素(可重复), 所以 $|x\rangle$ 会是 $|00\rangle,|01\rangle,|10\rangle,|11\rangle .$ 中的一个。 
- 如果是三量子比特态 $x \in\{0,1\}^{3},$ 那么 $|x\rangle$ 表示这些三量子态 $|000\rangle,|001\rangle,$ $|010\rangle,|100\rangle,$ $|101\rangle,|110\rangle,|111\rangle .$ 中的一个
- 总结一下上面 $|x\rangle $ 的写法，我们可以用简洁的符号重新写 两个Hadamard门 $H \otimes H$ 同时作用的过程

$$
(H \otimes H)|0\rangle|0\rangle=H^{\otimes 2}|0\rangle^{\otimes 2}=\frac{1}{\sqrt{2^{2}}} \sum_{x \in[0,1]^{2}}|x\rangle
$$

更普遍的，$n$ 个Hadamard门 $H^{\otimes n}$ 并行作用到 $n$ 个 $$|0\rangle$$ 的量子态上
$$
H^{\otimes n}\left(|0\rangle^{\otimes n}\right)=\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle
$$

#### 例子

为了更清楚理解 $n$ 个Hadamard门并行作用的公式，我们写几个例子
$$
(H \otimes H)|0\rangle|0\rangle=\frac{1}{\sqrt{2^{2}}} \sum_{x \in\{0,1\}^{2}}|x\rangle
\\
(H \otimes H)|0\rangle|1\rangle=\frac{1}{2} \sum_{x \in\{0,1\}}(-1)^{x}|x\rangle
\\
(H \otimes H)|1\rangle|1\rangle =\frac{1}{2} \sum_{x \in\{0,1\}^{2}}(-1)^{x_{0} \oplus x_{1}}|x\rangle
$$

#### example arbitrary qubit

对下面的量子态应用 Hadamard 变换
$$
|\psi\rangle=\frac{|0\rangle+(-1)^{x}|1\rangle}{\sqrt{2}}
$$
其中 $x \in\{0,1\}$

------

**解答**

首先计算 Hadamard 门对一般量子态的作用
$$
\begin{aligned}
H  | \psi\rangle &=\alpha H|0\rangle+\beta H|1\rangle \\
&=\alpha\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)+\beta\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\left(\frac{\alpha+\beta}{\sqrt{2}}\right)|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)|1\rangle
\end{aligned}
$$
在本题中，可以对应

- $\alpha=1$
- $\beta=(-1)^{x}$

所以
$$
H|\psi\rangle=\left(\frac{1+(-1)^{x}}{2}\right)|0\rangle+\left(\frac{1-(-1)^{x}}{2}\right)|1\rangle
$$

-  如果 $x=0,$ 结果是

$$
H\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)=|0\rangle
$$

-  如果 $x=1,$ 结果是

$$
H\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)=|1\rangle
$$

#### 结果小总结

量子算符中很重要的一步是生成叠加态，这个可以用 Hadamard gates
$$
H|0\rangle=\frac{|0\rangle+|1\rangle}{\sqrt{2}}
\\
 H|1\rangle=\frac{|0\rangle-|1\rangle}{\sqrt{2}}
$$

1. Hadamard 作用到任意态 $ | \psi\rangle=\alpha|0\rangle+\beta|1\rangle .$  

$$
\begin{aligned}
H|\psi\rangle =\left(\frac{\alpha+\beta}{\sqrt{2}}\right)|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)|1\rangle
\end{aligned}
$$

2. 如果Hadamard连续作用到一个态上两次，它会回到原来的态

$$
HH|\psi\rangle=H\left[\left(\frac{\alpha+\beta}{\sqrt{2}}\right)|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)|1\rangle\right]=|\psi\rangle
$$

3. 前面是对单量子比特态的操作，如果对多个量子比特态的并行操作

- 三个态并行

$$
\begin{aligned}
&(H \otimes H \otimes H)|0\rangle|0\rangle|0\rangle
\\=&(H|0\rangle)(H|0\rangle)(H|0\rangle) \\
=&\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right) \\
=& \frac{1}{\sqrt{2^{3}}}(|000\rangle+|001\rangle+|010\rangle+|100\rangle+|101\rangle\\
&+|110\rangle+|111\rangle)
\end{aligned}
$$

Hadamard分别作用到各自的态上，再分配叠加  

- 任意 $n$ 个态的简易缩写

$$
H^{\otimes n}\left(|0\rangle^{\otimes n}\right)=\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle
$$



## 量子干涉Quantum interference

Hadamard 门对量子比特的作用是量子干涉的一个例子。

回顾前面Hadamard 作用到任意态 $ | \psi\rangle=\alpha|0\rangle+\beta|1\rangle .$  
$$
\begin{aligned}
H|\psi\rangle &=\alpha H|0\rangle+\beta H|1\rangle\\
&=\alpha\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)+\beta\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\left(\frac{\alpha+\beta}{\sqrt{2}}\right)|0\rangle+\left(\frac{\alpha-\beta}{\sqrt{2}}\right)|1\rangle
\end{aligned}
$$

测量到 $|0\rangle$ 的概率发生了如下变化
$$
\alpha \rightarrow \frac{\alpha+\beta}{\sqrt{2}}
$$
测量到 $|1\rangle$ 的概率发生了如下变化
$$
\beta \rightarrow \frac{\alpha-\beta}{\sqrt{2}}
$$


我们看到Hadamard 门对态做了转换  
$$
|\psi\rangle=\frac{|0\rangle+|1\rangle}{\sqrt{2}} \rightarrow|0\rangle
$$
这是量子干涉在数学上的表现，这意味着概率振幅的增加。

量子干涉有两种

- 正干涉，增加概率幅
- 负干涉，减小概率幅

具体到这个例子
$$
|\psi\rangle=\frac{|0\rangle+|1\rangle}{\sqrt{2}} \rightarrow|0\rangle
$$


- 对于基底 $|0\rangle $ 是正干涉，两个幅度叠加，测量 发现0的概率增加。  
- 对于基底 $|1\rangle $ 是负干涉，两个幅度叠加，测量 发现0的概率降低。  

量子干涉在量子算法的发展中起着重要作用：

> 量子干涉允许我们获得关于函数 $f(x)$ 的信息，该信息依赖于在 $x $ 的许多值处评估函数。也就是说，干涉允许我们推导出函数的某些全局属性。

