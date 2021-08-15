# section2单量子门

1. 量子非门(quantum NOT gate)
   - 矩阵表示
   - 外积形式(outer product form)
2. Hadamard门
3. 相位移动门(phase shift)
   - 相位翻转门(phase flip)
   - $Z$ 门
   - $S$ 门
4. 通用单量子门
5. 单量子门的线路表示



[TOC]



由于量子门必须是**幺正算符**(unitary)，我们经常会在“门”和“算符”这两个词之间来回应用——所以请记住，在本文中，它们的意思是**相同的**。
$$
\text { 门 } =\text { 算符 }
$$
量子算符可以用矩阵表示。那么具有$n$输入和输出的量子门可以由度为$2^{n}$的矩阵表示。

例如

- 对比1个量子比特，要求对应作用的矩阵的自由度是$2^{1}=2 $，所以作用到1个量子比特的量子门是一个 $2 \times 2$ 的幺正矩阵 
- 对比2个量子比特，要求对应作用的矩阵的自由度是$2^{2}=4 $，所以作用到2个量子比特的量子门是一个 $4 \times 4$ 的幺正矩阵 

### 量子非门

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

#### 习题

> 我们已经介绍了量子非门(quantum NOT gate)作用到标准基底 $|0\rangle,|1\rangle$ 的结果。如果量子非门(quantum NOT gate)作用到下面的基底会有什么结果？
> $$
> |+\rangle=\frac{1}{\sqrt{2}}\left(\begin{array}{l}
> 1 \\
> 1
> \end{array}\right), \quad|-\rangle=\frac{1}{\sqrt{2}}\left(\begin{array}{c}
> 1 \\
> -1
> \end{array}\right)
> $$
>
> 要求用量子非门(quantum NOT gate)的外积形式(outer product form)。

**解答**

1. 我们先求出量子非门(quantum NOT gate)在标准基底下的矩阵
2. 然后求出标准基底与新基底的转换矩阵
3. 准基底下的$X$ 矩阵在 转换矩阵 的作用下会变成新基底下的$X$ 矩阵

##### 步骤1-标准基底矩阵

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

所以
$$
\begin{aligned}
X&=\left(\begin{array}{cc}
\langle 0|X| 0\rangle & \langle 0|X| 1\rangle \\
\langle 1|X| 0\rangle & \langle 1|X| 1\rangle
\end{array}\right)
\\&=\left(\begin{array}{cc}
\langle 0| 1\rangle & \langle 0|0\rangle \\
\langle 1|1\rangle & \langle 1|0\rangle
\end{array}\right)
\\&=\left(\begin{array}{cc}
0 & 1 \\
1 & 0
\end{array}\right)
\end{aligned}
$$

##### 步骤2-转换矩阵

> 要写出量子非门(quantum NOT gate)在新基底 $|+\rangle,|-\rangle$ 的矩阵形式，我们需要写出两个基底之间的转换矩阵 $U_{\text {trans }}$

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

##### 步骤3-基底变换

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

这就是新基底下量子非门(quantum NOT gate)的矩阵

### Hadamard矩阵

Hadamard是很重要的量子门，后面我们会专门一节来讲解。现在先讲解单比特Hadamard矩阵的基本性质。

前面我们从转换基底过程得到Hadamard矩阵
$$
H=\frac{1}{\sqrt{2}}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right)
$$
Hadamard矩阵写成外积的形式
$$
H=\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|)
$$
这里探究一下Hadamard矩阵对量子态 $|0\rangle$ 的作用
$$
\begin{aligned}
H|0\rangle &=\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|)|0\rangle \\
&=\frac{1}{\sqrt{2}}(|0\rangle\langle 0 | 0\rangle+|0\rangle\langle 1 | 0\rangle+|1\rangle\langle 0 | 0\rangle-|1\rangle\langle 1 | 0\rangle) \\
&=\frac{|0\rangle+|1\rangle}{\sqrt{2}}
\end{aligned}
$$
类似的
$$
H|1\rangle=\frac{|0\rangle-|1\rangle}{\sqrt{2}}
$$
Hadamard矩阵作用到标准基底得到两个叠加态
$$
\left\{\frac{|0\rangle+|1\rangle}{\sqrt{2}}, \frac{|0\rangle-|1\rangle}{\sqrt{2}}\right\}
$$


### 相位移动门(phase shift)

我们先介绍一个特殊的相位移动门(phase shift)——相位翻转门(phase flip)

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

#### 特殊情况

相位移动门(phase shift gate)
$$
P=\left(\begin{array}{cc}
1 & 0 \\
0 & e^{i \theta}
\end{array}\right)
$$
当 $\theta$ 等于一些特殊值的时候对应一些专有名称的门

- $\theta=\pi$

这种情况对应的就是前面说的 $Z$ 门

- $\theta=\pi / 2 $

根据欧拉公式 $e^{i \pi / 2}=\cos (\pi / 2)+i \sin (\pi / 2)=i$ 所以对应的矩阵是
$$
S=\left(\begin{array}{ll}
1 & 0 \\
0 & i
\end{array}\right)
$$

这个矩阵叫做 $S$ 门

-  $\theta=\pi / 4 .$ 

根据欧拉公式 
$$
T=\left(\begin{array}{cc}
1 & 0 \\
0 & e^{i \pi / 4}
\end{array}\right)=e^{i \pi / 8}\left(\begin{array}{cc}
e^{-i \pi / 8} & 0 \\
0 & e^{i \pi / 8}
\end{array}\right)
$$
这个矩阵叫做 $T$ 门



### 通用单量子门

#### 旋转矩阵

一个旋转了角度 $\gamma$ 的旋转矩阵
$$
R(\gamma)=\left(\begin{array}{cc}
\cos \gamma & -\sin \gamma \\
\sin \gamma & \cos \gamma
\end{array}\right)
$$
描述当这个矩阵作用到一个量子比特
$$
|\psi\rangle=\cos \theta|0\rangle+\sin \theta|1\rangle
$$
上的效果

**Solution**

旋转矩阵作用到态上的过程如下:
$$
\begin{aligned}
R(\gamma)|\psi\rangle=&\left(\begin{array}{cc}
\cos \gamma & -\sin \gamma \\
\sin \gamma & \cos \gamma
\end{array}\right)\left(\begin{array}{c}
\cos \theta \\
\sin \theta
\end{array}\right)
\\=&\left(\begin{array}{c}
\cos \gamma \cos \theta-\sin \gamma \sin \theta \\
\sin \gamma \cos \theta+\cos \gamma \sin \theta
\end{array}\right)
\end{aligned}
$$
根据三角恒等式
$$
\begin{array}{l}
\cos (\alpha+\beta)=\cos \alpha \cos \beta-\sin \alpha \sin \beta \\
\sin (\alpha+\beta)=\sin \alpha \cos \beta+\cos \alpha \sin \beta
\end{array}
$$
旋转后的态可以写成
$$
\begin{aligned}
\left|\psi^{\prime}\right\rangle=&R(\gamma)|\psi\rangle
\\=&\left(\begin{array}{c}
\cos \gamma \cos \theta-\sin \gamma \sin \theta \\
\sin \gamma \cos \theta+\cos \gamma \sin \theta
\end{array}\right)
\\=&\left(\begin{array}{c}
\cos (\gamma+\theta) \\
\sin (\gamma+\theta)
\end{array}\right)
\\=&\cos (\gamma+\theta)|0\rangle+\sin (\gamma+\theta)|1\rangle
\end{aligned}
$$
结果的解读

> 从布洛赫球的图像观察，量子态 $|\psi\rangle$ 被旋转矩阵 $R(\gamma)$ 沿着 $z$ 轴旋转了 $\gamma$ 角度。
>
> - 初始态测量到 $|0\rangle$ 的概率是 $\cos ^{2} \theta$ 
> - 旋转之后的态测量到 $|0\rangle$ 的概率是 $\cos ^{2}(\gamma+\theta)$ 
>
> 相对的变化是
> $$
> \begin{aligned}
> \cos ^{2} \theta \mapsto \cos ^{2}(\gamma+\theta) \\
> \sin ^{2} \theta \mapsto \sin ^{2}(\gamma+\theta)
> \end{aligned}
> $$
>
> 

#### 定理证明

一个矩阵 $U$ 如果是幺正的，而且厄米的，那么下面的等式成立
$$
\exp (-i \theta U)=\cos \theta I-i \sin \theta U
$$
**证明**

一个算子 $U$ 如果是幺正的，那么
$$
U U^{\dagger}=U^{\dagger} U=I
$$
一个算子 $U$ 如果是厄米的，联合两个性质，会得到
$$
U^{2}=U U=U U^{\dagger}=I
$$
矩阵函数的泰勒展开得到
$$
\exp (-i \theta U)=I-i \theta U+(-i)^{2} \frac{\theta^{2}}{2 !} U^{2}+(-i)^{3} \frac{\theta^{3}}{3 !} U^{3}+(-i)^{4} \frac{\theta^{4}}{4 !} U^{4}+(-i)^{5} \frac{\theta^{5}}{5 !} U^{5}+\cdots
$$
因为 $U^{2}=I$ 和 $i^{2}=-1,$ 后面多次幂的 $U^{n}$ 可以化简为

- 当 $n$ 是偶数，那么 $U^{n}=1$ 
- 当 $n$ 是奇数，那么 $U^{n}=U$ 

所以泰勒展开式可以化简为
$$
\begin{aligned}
\exp (-i \theta U) &=\left(I-\frac{\theta^{2}}{2 !} I+\frac{\theta^{4}}{4 !} I-\cdots\right)-i \theta U+i \frac{\theta^{3}}{3 !} U-i \frac{\theta^{5}}{5 !} U+\cdots \\
&=\left(1-\frac{\theta^{2}}{2 !}+\frac{\theta^{4}}{4 !}-\cdots\right) I-i\left(\theta-\frac{\theta^{3}}{3 !}+\frac{\theta^{5}}{5 !}+\cdots\right) U \\
&=\cos \theta I-\sin \theta U
\end{aligned}
$$


#### 指数形式

> 给定一个矩阵，写出对应的指数形式

我们可以把任何旋转矩阵分解成布洛赫球上沿着 $x, y,$ $z$ 轴旋转的泡利矩阵
$$
\begin{array}{l}
R_{x}(\gamma)=e^{-i \gamma X / 2}=\left(\begin{array}{cc}
\cos \left(\frac{\gamma}{2}\right) & -i \sin \left(\frac{\gamma}{2}\right) \\
-i \sin \left(\frac{\gamma}{2}\right) & \cos \left(\frac{\gamma}{2}\right)
\end{array}\right) \\
R_{y}(\gamma)=e^{-i \gamma Y / 2}=\left(\begin{array}{cc}
\cos \left(\frac{\gamma}{2}\right) & -\sin \left(\frac{\gamma}{2}\right) \\
\sin \left(\frac{\gamma}{2}\right) & \cos \left(\frac{\gamma}{2}\right)
\end{array}\right) \\
R_{z}(\gamma)=e^{-i \gamma Z / 2}=\left(\begin{array}{cc}
e^{-i \gamma / 2} & 0 \\
0 & e^{i \gamma / 2}
\end{array}\right)
\end{array}
$$
也就是说给定一个单量子比特算子 $U,$ 我们可以找到四个实数 $a, b, c, d$ 使得算子可以被下面的形式分解
$$
U=e^{i a} R_{z}(b) R_{y}(c) R_{z}(d)
$$

这种分解被称为 Z–Y 分解

##### 例子

对 $T$ 门进行Z–Y分解，并且写成指数形式
$$
T=e^{i \pi / 8}\left(\begin{array}{cc}
e^{-i \pi / 8} & 0 \\
0 & e^{i \pi / 8}
\end{array}\right)
$$
**解答**

根据扫描的公式
$$
R_{z}(\gamma)=e^{-i \gamma Z / 2}=\left(\begin{array}{cc}
e^{-i \gamma / 2} & 0 \\
0 & e^{i \gamma / 2}
\end{array}\right)
$$
 $T$ 门可以写成
$$
\begin{aligned}
T=&e^{i \pi / 8}\left(\begin{array}{cc}
e^{-i \pi / 8} & 0 \\
0 & e^{i \pi / 8}
\end{array}\right)
\\=& e^{i \pi / 8} e^{-i \pi Z / 8}
\\=& e^{i \pi / 8} R_{z}\left(\frac{\pi}{4}\right)
\end{aligned}
$$
也就是

- 指数形式 $T=e^{i \pi / 8} e^{-i \pi Z / 8}$
- Z–Y 分解得到 $T$ 门的作用是使得量子态沿着 $z$ 轴旋转了 $\frac{\pi}{4}$ 角度。

### 单量子门的线路表示

- 左边的符号表示输入量子比特态
- 右边的符号表示输出量子比特态
- 中间表示量子门

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200329114737249.png" alt="image-20200329114737249" style="zoom:50%;" />

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200329114914978.png" alt="image-20200329114914978" style="zoom:50%;" />

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200329114914978.png" alt="image-20200329114914978" style="zoom:50%;" />

后面用PPT重新画图