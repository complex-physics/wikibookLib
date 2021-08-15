# section1.3 二量子比特门

1. 二量子比特态和门的矩阵表示
   - 态的表示
   - 门的表示
2. 控制门
   - 控制非门
   - 控制Hadamard门
3. 门分解
   - 等价性证明



[TOC]





#### 二量子比特态的表示

用狄拉克标记符号，二量子比特态可以写成两个单量子比特态之间的张量积(tensor products)
$$
|a\rangle \otimes|b\rangle
$$
一般简写成

- $|a\rangle|b\rangle$ 
- 或者 $|a b\rangle$ 

二量子比特态总共有4种可能
$$
|00\rangle,|01\rangle,|10\rangle,|11\rangle
$$
如果用向量表示
$$
|01\rangle=\left(\begin{array}{l}
1 \\
0
\end{array}\right) \otimes\left(\begin{array}{l}
0 \\
1
\end{array}\right)=\left(\begin{array}{l}
0 \\
1 \\
0 \\
0
\end{array}\right)
$$

$$
|11\rangle=\left(\begin{array}{l}
0 \\
1
\end{array}\right) \otimes\left(\begin{array}{l}
0 \\
1
\end{array}\right)=\left(\begin{array}{l}
0 \\
0 \\
0 \\
1
\end{array}\right)
$$

另外两个态类似

#### 二量子比特门的表示

二量子比特门的矩阵表示
$$
U \doteq\left(\begin{array}{cccc}
\langle 00|U| 00\rangle & \langle 00|U| 01\rangle & \langle 00|U| 10\rangle & \langle 00|U| 11\rangle \\
\langle 01|U| 00\rangle & \langle 01|U| 01\rangle & \langle 01|U| 10\rangle & \langle 01|U| 11\rangle \\
\langle 10|U| 00\rangle & \langle 10|U| 01\rangle & \langle 10|U| 10\rangle & \langle 10|U| 11\rangle \\
\langle 11|U| 00\rangle & \langle 11|U| 01\rangle & \langle 11|U| 10\rangle & \langle 11|U| 11\rangle
\end{array}\right)
$$

只要你知道这个门对这些态 $|a b\rangle$ 的作用后果，那就可以计算出每个矩阵元素，从而得到整个矩阵。



例如

CNOT 门对量子态的作用后果是
$$
\begin{array}{l}
|00\rangle \mapsto|00\rangle \\
|01\rangle \mapsto|01\rangle \\
|10\rangle \mapsto|11\rangle \\
|11\rangle \mapsto|10\rangle
\end{array}
$$
那么CNOT 门的矩阵表示就是
$$
C N=\left(\begin{array}{llll}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0
\end{array}\right)
$$


### 控制门

对于二量子比特门，一般其中一个量子比特视为另一个操作的控制比特

- 控制门是作用是做 **如果-否则(if - else)** 的构造
- 判断是否对受控量子比特做门变换

控制比特记作 $C .$

- 如果 $C=0,$ 那么二量子比特门对量子态不做任何变换
- 如果$C=1,$ 那么二量子比特门对量子态做特定的变换

下面具体讲解 受控非门(CNOT 门)和 受控H门(CH 门)

### CNOT 门

我们介绍的第一个二量子比特门是受控非门(CNOT 门)

前面说到CNOT门对量子态的作用后果 
$$
\begin{array}{l}
|00\rangle \mapsto|00\rangle \\
|01\rangle \mapsto|01\rangle \\
|10\rangle \mapsto|11\rangle \\
|11\rangle \mapsto|10\rangle
\end{array}
$$
这些可以写成两个比特值的 异或操作
$$
|a, b\rangle \rightarrow|a, b \oplus a\rangle
$$

- 如果控制比特 $|a=0 \rangle $ ，那么目标量子比特不做任何变换 $|0, b \oplus 0\rangle=|0, b \rangle$
- 如果控制比特 $|a=1 \rangle $ ，那么目标量子比特做NOT变换，或者说 $X$ 泡利矩阵作用到目标量子比特 $|1, b \oplus 1\rangle=|1, \bar{b} \rangle$

描述好量子态在受控非门(CNOT gate)作用下的变化，我们来看看受控非门(CNOT gate)本身的几种表示方法

1. 矩阵表示

$$
C N=\left(\begin{array}{llll}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0
\end{array}\right)
$$

2. 受控非门(CNOT gate)可以写成外积形式(outer product)

$$
C N=|00\rangle\langle 00|+| 01\rangle\langle 01|+| 10\rangle\langle 11|+| 11\rangle\langle 10|
$$

3. 受控非门(CNOT gate)的线路表示

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200329130731859.png" alt="image-20200329130731859" style="zoom:50%;" />



##### 外积形式下CNOT门对态的变化

> 用狄拉克标记法下量子态，被外积形式下CNOT门的作用过程和结果

CNOT门作用到下面的态

1.  $|10\rangle $
2.  $|11\rangle $
3.  $\alpha|10\rangle+\beta|11\rangle$

这三个态的控制比特都是 $| 1\rangle$，所以后面的受控比特需要被作用
$$
\begin{aligned}
C N|10\rangle &=(|00\rangle\langle 00|+| 01\rangle\langle 01|+| 10\rangle\langle 11|+| 11\rangle\langle 10|)|10\rangle \\
&=|00\rangle\langle 00|| 10\rangle+|01\rangle\langle 01|| 10\rangle+|10\rangle\langle 11 ||10\rangle+|11\rangle\langle 10 ||10\rangle
\end{aligned}
$$
计算这些内积，需要利用态的正交关系
$$
\langle a b|c d\rangle=\langle a | c\rangle\langle b | d\rangle
$$
对应位置的比特分别内积，只要有任何一个位置是正交的，那么最后内积结果必然是 0
$$
\begin{aligned}
\langle 00 | 10\rangle &=\langle 0 | 1\rangle\langle 0 | 0\rangle=0 \\
\langle 01 | 10\rangle &=\langle 0 | 1\rangle\langle 1 | 0\rangle=0 \\
\langle 11 | 10\rangle &=\langle 1 | 1\rangle\langle 1 | 0\rangle=0 \\
\langle 10 | 10\rangle &=\langle 1 | 1\rangle\langle 0 | 0\rangle=1
\end{aligned}
$$
CNOT门作用到$|10\rangle $的结果
$$
\begin{aligned}
C N|10\rangle &=(|00\rangle\langle 00|+| 01\rangle\langle 01|+| 10\rangle\langle 11|+| 11\rangle\langle 10|)|10\rangle \\
&=|00\rangle\langle 00|| 10\rangle+|01\rangle\langle 01|| 10\rangle+|10\rangle\langle 11 ||10\rangle+|11\rangle\langle 10 ||10\rangle
\\&=|11\rangle
\end{aligned}
$$


CNOT门作用到$|11\rangle $的结果
$$
\begin{aligned}
C N|11\rangle &=(|00\rangle\langle 00|+| 01\rangle\langle 01|+| 10\rangle\langle 11|+| 11\rangle\langle 10|)|11\rangle \\
&=|00\rangle\langle 00||11\rangle+|01\rangle\langle 01|| 11\rangle+|10\rangle\langle 11|| 11\rangle+|11\rangle\langle 10|| 11\rangle \\
&=|10\rangle
\end{aligned}
$$


从这两个结果可以看出来，控制比特都是 $| 1\rangle$的时候，目标比特会被翻转。

第三个态其实就是前面两个态的线性叠加，根据线性关系，分别作用得到
$$
\begin{aligned}
CN(\alpha|10\rangle+\beta|11\rangle)&=\alpha C N|10\rangle+\beta C N|11\rangle
\\&=\alpha|11\rangle+\beta|10\rangle
\end{aligned}
$$

### CH门

#### 产生贝尔态

> 构建一个线路，这个线路可以产生贝尔态(Bell states)

我们先考虑CNOT门作用到一类态的结果，其中受控比特是叠加态 $|c\rangle=|0\rangle+|1\rangle$，目标比特是 $| 0\rangle$
$$
\begin{aligned}
C N(|00\rangle+|10\rangle)=&(|00\rangle\langle 00|+| 01\rangle\langle 01|+| 10\rangle\langle 11|+| 11\rangle\langle 10|)(|00\rangle+|10\rangle) \\
=&|00\rangle\langle ||00 00\rangle+|01\rangle\langle ||01 00\rangle+|10\rangle\langle ||11 00\rangle+|11\rangle\langle ||10 00\rangle \\
&+|00\rangle\langle ||00 10\rangle+|01\rangle\langle ||01 10\rangle+|10\rangle\langle ||11 10\rangle+|11\rangle\langle ||10 10\rangle \\
=&|00\rangle+|11\rangle
\end{aligned}
$$
贝尔态(Bell states)如下
$$
\begin{aligned}
&\left|\beta_{00}\right\rangle=\frac{|00\rangle+|11\rangle}{\sqrt{2}}\\
&\left|\beta_{01}\right\rangle=\frac{|01\rangle+|10\rangle}{\sqrt{2}}\\
&\left|\beta_{10}\right\rangle=\frac{|00\rangle-|11\rangle}{\sqrt{2}}\\
&\left|\beta_{11}\right\rangle=\frac{|01\rangle-|10\rangle}{\sqrt{2}}
\end{aligned}
$$
可以写成统一的式子
$$
\left|\beta_{a b}\right\rangle=\frac{|0, b\rangle+(-1)^{a}|1, \bar{a}\rangle}{\sqrt{2}}
$$
可以看出来，上面的作用结果就得到贝尔态$\left|\beta_{00}\right\rangle$ (忽略系数 $\frac{1}{\sqrt{2}}$)

类似的，受控比特是叠加态 $|c\rangle=|0\rangle+|1\rangle$，目标比特是 $| 1\rangle$，我们可以得到贝尔态 $\left|\beta_{01}\right\rangle$ 

我们观察一下CNOT门的矩阵
$$
C N=\left(\begin{array}{llll}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0
\end{array}\right)
$$
其中右下角的小矩阵
$$
\left(\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right)
$$
是做一个单比特翻转的矩阵，加上前面的受控比特是叠加态 $|c\rangle=|0\rangle+|1\rangle$，所以一个 $| 0\rangle$被翻转，一个 $| 0\rangle$不翻转，所以可以形成 $|0\rangle \mapsto|0\rangle+|1\rangle$ 的贝尔态。

另外两个态 $\left|\beta_{10}\right\rangle$ 和 $\left|\beta_{11}\right\rangle$ 的生成需要产生一个相位翻转，这使得我们回想到之前 Hadamard门的作用，
$$
H|1\rangle=\frac{|0\rangle-|1\rangle}{\sqrt{2}}
$$
加上控制门
$$
C H=\left(\begin{array}{cccc}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
0 & 0 & \frac{1}{\sqrt{2}} & \frac{-1}{\sqrt{2}}
\end{array}\right)
$$
我们得到了控制Hadamard门(CH gate)矩阵

用狄拉克外积形式写
$$
C H=|00\rangle\langle 00|+| 01\rangle \langle 01 |+\frac{1}{\sqrt{2}}(|10\rangle\langle 10|+| 10\rangle\langle 11|+| 11\rangle\langle 10|-| 11\rangle\langle 11|)  
$$

#### 控制Hadamard门

在矩阵表象下，控制Hadamard门对二量子比特态的作用效果
$$
\begin{aligned}
C H|01\rangle&=\left(\begin{array}{cccc}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
0 & 0 & \frac{1}{\sqrt{2}} & \frac{-1}{\sqrt{2}}
\end{array}\right)\left(\begin{array}{l}
0 \\
1 \\
0 \\
0
\end{array}\right)=\left(\begin{array}{l}
0 \\
1 \\
0 \\
0
\end{array}\right)
\\&=|01\rangle
\end{aligned}
$$

- 当控制比特 $|a=0\rangle $ ，那么目标量子比特不做任何变换 $CH|0, b \rangle=|0, b \rangle$

$$
\begin{aligned}
C H|11\rangle&=\left(\begin{array}{cccc}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
0 & 0 & \frac{1}{\sqrt{2}} & \frac{-1}{\sqrt{2}}
\end{array}\right)\left(\begin{array}{l}
0 \\
0 \\
0 \\
1
\end{array}\right)=\left(\begin{array}{c}
0 \\
0 \\
\frac{1}{\sqrt{2}} \\
\frac{-1}{\sqrt{2}}
\end{array}\right)
\\&=\frac{|10\rangle-|11\rangle}{\sqrt{2}}
\end{aligned}
$$

- 当控制比特 $|a=1 \rangle $ ，那么目标量子比特做Hadamard变换得到贝尔态(Bell states)

##### 练习

> 用外积形式(outer product)计算控制Hadamard门对二量子比特态的作用效果


$$
\begin{aligned}
C H|01\rangle=&\left[|00\rangle\langle 00|+| 01\rangle \langle 01 |+\frac{1}{\sqrt{2}}(|10\rangle\langle 10|+| 10\rangle\langle 11|+| 11\rangle\langle 10|-| 11\rangle\langle 11|)\right] | 01 \rangle \\
=&|00\rangle\langle ||00 01\rangle+|01\rangle\langle 01|| 01\rangle+\frac{1}{\sqrt{2}}(|10\rangle\langle 10 ||01\rangle+|10\rangle\langle 11|| 01\rangle\\
&+|11\rangle\langle 10|| 01\rangle-|11\rangle\langle ||11 01\rangle)\\
=&|01\rangle
\end{aligned}
$$

$$
\begin{aligned}
C H|11\rangle=&\left[|00\rangle\langle 00|+| 01\rangle \langle 01 |+\frac{1}{\sqrt{2}}(|10\rangle\langle 10|+| 10\rangle\langle 11|+| 11\rangle\langle 10|-| 11\rangle\langle 11|)\right] | 01 \rangle \\
=& |00\rangle\langle 00|| 11\rangle+|01\rangle\langle ||01 11\rangle+\frac{1}{\sqrt{2}}(|10\rangle\langle 10 ||11\rangle+|10\rangle\langle 11|| 11\rangle\\
&+|11\rangle\langle 10 ||01\rangle -|11\rangle\langle 11 ||11\rangle)
\\=&\frac{|10\rangle-|11\rangle}{\sqrt{2}}
\end{aligned}
$$

### 门分解

如果有个控制幺正算子 $U$ ，它的效果**等价**于几个单比特门与控制非门的组合。我们就说这个控制幺正算子 $U$ 可以**分解**。

> 门分解有很大的应用意义，在你设计线路的时候，一个效果可以用不同的线路来实现。可以规避一些难以操作或者使用的门。

#### 例子

> 证明：如下图，控制非门可以分解成两个Hadamard门和控制Z门。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200329181636576.png" alt="image-20200329181636576" style="zoom:50%;" />

左边的控制非门可以用投影算符写成
$$
P_{0} \otimes I+P_{1} \otimes X
$$
其中 $X$ 门和单位矩阵 $I$ 都可以分解成投影算符的组合

- $X=|0\rangle\langle 1|+| 1\rangle\langle 0|=P_{+}-P_{-}$
- $I=P_{+}+P_{-}$

所以左边的控制非门可以改写成
$$
\begin{aligned}
&P_{0} \otimes I+P_{1} \otimes X\\
=& P_{0} \otimes\left(P_{+}+P_{-}\right)+P_{1} \otimes\left(P_{+}-P_{-}\right)\\
=&\left(P_{0}+P_{1}\right) \otimes P_{+}+\left(P_{0}-P_{1}\right) \otimes P_{-}
\end{aligned}
$$
后面一步用了分配法

根据关系

- $I=P_{0}+P_{1}$ 
- $Z=P_{0}-P_{1}$

控制非门可以进一步改写成
$$
\begin{aligned}
&\left(P_{0}+P_{1}\right) \otimes P_{+}+\left(P_{0}-P_{1}\right) \otimes P_{-}\\
=&I \otimes P_{+}+Z \otimes P_{-}
\end{aligned}
$$




接下来处理右边的线路，把右边的线路等价变换成左边式子，就可以证明两个线路是等价的

首先Hadamard算子的狄拉克表记
$$
H=\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|)
$$
在投影算符 $P_{0}$ 的作用下
$$
\begin{aligned}
P_{0} H &=(|0\rangle\langle 0|) \frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|) \\
&=\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|)
\end{aligned}
$$
继续施加另一个Hadamard算子
$$
\begin{aligned}
H P_{0} H &=\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|) \frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|) \\
&=\frac{1}{2}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|+| 1\rangle\langle 1|) \\
&=P_{+}
\end{aligned}
$$
提取等号自由有 $H P_{0} H=P_{+}$，左右同时张量积一个单位算符
$$
\begin{aligned}
P_{+}=&H P_{0} H\\
I \otimes P_{+}=&I \otimes H P_{0} H
\\=&(I \otimes H)\left(I \otimes P_{0} H\right)
\\=&(I \otimes H)\left(I \otimes P_{0}\right)(I \otimes H)
\end{aligned}
$$
类似的，我们可以计算得到
$$
Z \otimes P_{-}=(I \otimes H)\left(Z \otimes P_{1}\right)(I \otimes H)
$$
两式相加
$$
\begin{aligned}
I \otimes P_{+}+Z \otimes P_{-} &=(I \otimes H)\left(I \otimes P_{0}\right)(I \otimes H)+(I \otimes H)\left(Z \otimes P_{1}\right)(I \otimes H) \\
&=(I \otimes H)\left(I \otimes P_{0}+Z \otimes P_{1}\right)(I \otimes H)
\end{aligned}
$$
我们注意到式子中的 $I \otimes P_{+}+Z \otimes P_{-}$ 就是控制非门的一种等价表示，说明左右两个线路是等价的

- 左边是控制非门
- 右边 $(I \otimes H)\left(I \otimes P_{0}+Z \otimes P_{1}\right)(I \otimes H)$ 表示一个控制Z门和两个Hadamard的组合



#### 补充材料-投影算符





