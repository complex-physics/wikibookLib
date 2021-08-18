## section-1 Deutsch算法

Deutsch算法其实很简单，但它展示了量子计算机的强大威力。

[TOC]

#### 常数函数&平衡函数

Deutsch算法解决如下问题

> 给定输入和输出，如何快捷地判断 $f ( x )$ 是属于常数函数，或是平衡函数。

输入 $x$ 是一可能是0或者1

然后解释什么是常数函数和平衡函数

1. 常数函数(constant function)
   - 不论输入是0还是1，输出都是 $f(x)=0$
   - 不论输入是0还是1，输出都是 $f(x)=1$
2. 平衡函数(balanced function)有两种情况
   - 恒等函数(identity function)：输入是0，输出是 $f(0)=0$，输入是1，输出是 $f(1)=1$  
   - 翻转函数(bit flip function)：输入是0，输出是 $f(0)=1$，输入是1，输出是 $f(1)=0$  

常数函数和平衡函数的一个区别特征是

- 平衡函数(balanced function)对于不同的输入，输出0和1是各一半
- 常数函数(constant function)对于不同的输入，输出的都一样

#### 经典算法的步骤

> 在经典算法中我们是如何判断未知函数 $f ( x )$ 是常数函数，或是平衡函数?

判断步骤如下

1. 给出输入 $x=0$，根据 $f(0)=0$ 或 $f(0)=1$ 分成两种分支
2. 再给输入 $x=1$，根据前面分类的判据给出结果 

![](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20210817140552593.png)

#### 一个线路图例子

> 在量子算法Deutsch算法中我们是如何判断未知函数 $f ( x )$ 是常数函数，或是平衡函数?

我们先介绍一个作用于两个量子位的幺正运算$U_{f}$
$$
U_{f}|x, y\rangle=|x, y \otimes f(x)\rangle
$$
这个门的作用是

- 第一位的量子比特保持不变
- 第二位量子比特 $y $ 和函数产生新的输出 $y \otimes f(x)$



<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200513083111541.png" alt="image-20200513083111541" style="zoom:50%;" />

对于这个线路图，过程如下

1. 对第一位的初始态 $|0\rangle$ 作用一个Hadamard门。输出 $\frac{|0\rangle+|1\rangle}{\sqrt{2}}$
2. 第一位输出的$\frac{|0\rangle+|1\rangle}{\sqrt{2}}$ 和第二位的初始态 $|0\rangle$  一起被 一个作用于两个量子位的幺正运算输出 $U_{f}|x, y\rangle=|x, y \otimes f(x)\rangle$

假如 $f(x)$ 是恒等函数，过程计算如下
$$
\begin{aligned}
U_{f}\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle
&=\frac{1}{\sqrt{2}}\left(U_{f}|00\rangle+U_{f}|10\rangle\right)
\\&=\frac{|0,0 \oplus f(0)\rangle+|1,0 \oplus f(1)\rangle}{\sqrt{2}}
\\&=\frac{|00\rangle+|11\rangle}{\sqrt{2}}
\end{aligned}
$$
其中

- $0 \oplus 0=1 \oplus 1=0$ 
- $0 \oplus 1=1 \oplus 0=1$ 

更一般的输出如下
$$
U_{f}\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle=\frac{|0, f(0)\rangle+|1, f(1)\rangle}{\sqrt{2}}
$$


### Deutsch's算法的一般流程

根据我们目前对Deutsch's算法的介绍，

系统处于叠加状态 $\sum | x\rangle | f(x)\rangle$以获取有关函数**全局属性**的信息，所谓的全局属性信息是指函数是常数函数 $f(0)=f(1)$ 还是平衡函数 $f(0) \neq f(1) .$ 
$$
\left|\psi_{\text {out}}\right\rangle=(H \otimes I) U_{f}(H \otimes H)|0\rangle|1\rangle
$$
接下来我们详细分析这个公式的计算过程

#### 步骤1：叠加态

二量子比特态在二Hadamard门下产生叠加态
$$
\begin{aligned}
(H \otimes H)|0\rangle|1\rangle &=\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&=\frac{1}{2}(|00\rangle-|01\rangle+|10\rangle-|11\rangle)
\end{aligned}
$$


#### 步骤2：U门

把 $U_{f}$ 作用到 $(H \otimes H)|0\rangle|1\rangle$ 的每一个项上

##### 第一项

$$
\begin{aligned}
U_{f}|00\rangle&=|0,0 \oplus f(0)\rangle
\\&=(1-f(0))| 00\rangle+f(0)|01\rangle
\end{aligned}
$$

接下来的步骤就取决于函数是是常数函数，还是平衡函数?

1. 如果 $f(0)=0,$ 那么 $0 \oplus f(0)=0 \oplus 0=0$ 所以
   $$
   \begin{aligned}
   |0,0 \oplus f(0)\rangle&=(1-f(0))|00\rangle+f(0)|01\rangle
   \\&=|00\rangle+(0)|01\rangle
   \\&=|00\rangle
   \end{aligned}
   $$

2. 如果 $f(0)=1,$ then $0 \oplus f(0)=0 \oplus 1=1$ and
   $$
   \begin{aligned}
   |0,0 \oplus f(0)\rangle&=(1-f(0))|00\rangle+f(0)|01\rangle
   \\&=(0)|00\rangle+(1)|01\rangle
   \\&=|01\rangle
   \end{aligned}
   $$

##### 其他项

和第一项类似的，其他项可以得到
$$
\begin{aligned} 
U_{f}|01\rangle&=|0,1 \oplus f(0)\rangle=f(0)|00\rangle+(1-f(0))|01\rangle \\
U_{f}|10\rangle&=|0,1 \oplus f(0)\rangle=(1-f(1))|00\rangle+f(1)|01\rangle \\
U_{f}|11\rangle&=|0,1 \oplus f(1)\rangle=f(1)|10\rangle+(1-f(1))|11\rangle
 \end{aligned}
$$
所以在 $U_{f}$ 作用下
$$
\begin{aligned}
\left|\psi^{\prime}\right\rangle=& U_{f}(H \otimes H)|0\rangle|1\rangle \\
=&(1-f(0))|00\rangle+f(0)|01\rangle+f(0)|00\rangle+(1-f(0))|01\rangle \\
&+(1-f(1))|00\rangle+f(1)|01\rangle+f(1)|10\rangle+(1-f(1))|11\rangle
\end{aligned}
$$

#### 步骤3：输出

把 $H \otimes I$ 作用到 $\left|\psi^{\prime}\right\rangle$ 上，也就是把Hadamard门作用到第一位的量子比特上，第二位量子比特保持不变

对于前半部分
$$
\begin{array}{l}
(H \otimes I)[(1-f(0))|00\rangle+f(0)|01\rangle] \\
\quad=(1-f(0))(H|0\rangle) \otimes|0\rangle+f(0)(H|0\rangle) \otimes|1\rangle \\
\quad=(1-f(0))\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right) \otimes|0\rangle+f(0)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right) \otimes|1\rangle \\
\quad=(1-f |(0))\left(\frac{|00\rangle+|10\rangle}{\sqrt{2}}\right)+f(0)\left(\frac{|01\rangle+|11\rangle}{\sqrt{2}}\right)
\end{array}
$$
类似的，对于所有项
$$
\left|\psi_{o u t}\right\rangle=(1-f(0)-f(1))|0\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)+(f(1)-f(0))|1\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$
根据这个输出，我们可以判断函数 $f(x)$ 是常数函数，还是平衡函数?

1. 如果 $f(x)$ 是常数函数 $(f(0)=f(1))$

$$
\left|\psi_{\text {out}}\right\rangle=-|0\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$

所以如果输入是这个结果，我们可以反推出 $f(x)$ 是常数函数

2. 如果 $f(x)$ 是平衡函数，那么  $f(0) \neq f(1),$ 也就是 $f(0)=0, f(1)=1,$ 或 $f(0)=1, f(1)=0$ 

$$
\left|\psi_{\text {out }}\right\rangle=\pm|1\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$



### 小结























































