

Grover算法可以描述为量子数据库搜索算法。这里给出的演示过于简单，没有太多实际用途。Grover的算法再次证明了量子计算机的威力，因为与经典计算机相比，该算法大大减少了解决问题所需的运算量。



有 $n$ 位比特的输入，$x \in\{0,1\}^{n}$，函数 $f(x)$ 的输出是一个比特，因此我们可以有

-  $f(x)=0$ 
- 或 $f(x)=1$.

用Grover算法解决的任务如下

> 我们将所有数据存在数据库中，假设我们有n个量子比特, 用来记录数据库中的每一个数据的索引，一共可以表示 $2^{n}$ 个数据，记为 $N$ 个。我们希望搜索得到的数据有M个。为了表示一个数据是否我我们搜索的结果。我们建立一个函数:
> $$
> f(x)=\left\{\begin{array}{ll}
> 0 & \left(x \neq x_{0}\right) \\
> 1 & \left(x=x_{0}\right)
> \end{array}\right.
> $$
> 其中 $x_{0}$ 为我们的搜索目标的索引值。也就是说, 
>
> - 当我们搜索到我们的目标时，我们的函 数值 $f ( x )$ 置为 1 , 
> - 如果搜索的结果不是我们的目标时， $f ( x )$ 置为  0。



用经典的方法求解这个问题，我们就用输入 $x$ 代入函数，观察输出是否是  $f(x)=1$。用这个方法，需要尝试的数量级  $2^{n}-1$ 。

用Grover算法，只需要 $\sqrt{2^{n}}$ 次的尝试。

例如，一个很短的输入 $n=5$，

- 经典算法需要的尝试次数  $2^{5}-1=31$ 
- Grover算法需要的尝试次数  $\sqrt{2^{5}} \approx 6$ 

可以看到Grover算法带来的明显改善，如果输入字符串的量子比特位 $n$ 越大，Grover算法带来的改善将会更加大。



把我们要找的目标输入记作 $\left|x^{\prime}\right\rangle$，那么
$$
f\left(x^{\prime}\right)=1
$$
所有其他 $x$ 在函数下是 $f(x)=0$ 

我们的任务是用 Grover算法找到 $\left|x^{\prime}\right\rangle$ 。

基本思路是产生一个叠加态，然后用Grover算子 $G$ 把叠加态旋转到 $\left|x^{\prime}\right\rangle$ 



流程：

1. 初始态：$n$个量子比特态 $|0\rangle^{\otimes n}$ 
2. 用 $H^{\otimes n}$ 作用到初始态 $|0\rangle^{\otimes n}$ 来产生叠加态

我们定义 $|\psi\rangle$ 是所有可能态 $|x\rangle$ 的叠加态 
$$
|\psi\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle
$$
这个叠加态包含了目标态 $\left|x^{\prime}\right\rangle$ ，所以可以内积得到
$$
\left\langle x^{\prime} \mid \psi\right\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}\left\langle x^{\prime} \mid x\right\rangle=\frac{1}{\sqrt{2^{n}}}
$$
从叠加态 $|\psi\rangle$ 中排除 $\left|x^{\prime}\right\rangle$，我们得到
$$
\left|\psi^{\prime}\right\rangle=\frac{1}{\sqrt{2^{n}-1}} \sum_{x \in\{0,1\}^{n}, x \neq x^{\prime}}|x\rangle
$$
其实 $\left|x^{\prime}\right\rangle$ 和 $\left|\psi^{\prime}\right\rangle$ 可以一起构成一组正交基(因为 $\left\langle x^{\prime} \mid \psi^{\prime}\right\rangle=0$)



现在定义两个算子

1. $U_{f} $ 算子
2. $W$ 算子

$$
U_{f}=\sum_{x \in\{0,1\}^{n}}(-1)^{f(x)}|x\rangle \langle x |=\sum_{x \in\{0,1\}^{n}}(-1)^{\delta_{x, x^{\prime}}} | x \rangle\langle x|
$$

其中
$$
\delta_{x, x^{\prime}}=\left\{\begin{array}{ll}
1 & x=x^{\prime} \\
0 & \text { otherwise }
\end{array}\right.
$$
是delta 函数(Kronecker delta function)  

利用 $|\psi\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle$ , 可以定义
$$
W=2|\psi\rangle\langle\psi|-I
$$
我们可以把量子态 $|\psi\rangle$ 分成两部分，目标态 $\left|x^{\prime}\right\rangle$ 和剩余的部分
$$
|\psi\rangle=\sqrt{\frac{2^{n}-1}{2^{n}}}\left|\psi^{\prime}\right\rangle+\frac{1}{\sqrt{2^{n}}}\left|x^{\prime}\right\rangle
$$
计算得到内积
$$
\begin{aligned}
\left\langle\psi \mid \psi^{\prime}\right\rangle=&(\sqrt{\frac{2^{n}-1}{2^{n}}}\langle \psi^{\prime}|+\frac{1}{\sqrt{2^{n}}}\langle x^{\prime}|)\left|\psi^{\prime}\right\rangle
\\
=&\sqrt{\frac{2^{n}-1}{2^{n}}}
\end{aligned}
$$
(其中利用了关系 $\left\langle x^{\prime} \mid \psi^{\prime}\right\rangle=0$)

把 $|\psi\rangle=\sqrt{\frac{2^{n}-1}{2^{n}}}\left|\psi^{\prime}\right\rangle+\frac{1}{\sqrt{2^{n}}}\left|x^{\prime}\right\rangle$ 用几步简单的代数化为 $\left|x^{\prime}\right\rangle=\sqrt{2^{n}}|\psi\rangle-\sqrt{2^{n}-1}\left|\psi^{\prime}\right\rangle$, 然后用算子作用在上面
$$
\begin{aligned}
W\left|x^{\prime}\right\rangle &=(2|\psi\rangle\langle\psi|-I)\left(\sqrt{2^{n}}|\psi\rangle-\sqrt{2^{n}-1}\left|\psi^{\prime}\right\rangle\right) \\
&=2 \sqrt{2^{n}}|\psi\rangle\langle\psi \mid \psi\rangle-\sqrt{2^{n}}|\psi\rangle-2 \sqrt{2^{n}-1}|\psi\rangle\left\langle\psi \mid \psi^{\prime}\right\rangle+\sqrt{2^{n}-1}\left|\psi^{\prime}\right\rangle \\
&=2 \sqrt{2^{n}}|\psi\rangle-\sqrt{2^{n}}|\psi\rangle-2 \sqrt{2^{n}-1} \sqrt{\frac{2^{n}-1}{2^{n}}}|\psi\rangle+\sqrt{2^{n}-1}\left|\psi^{\prime}\right\rangle
\end{aligned}
$$
用 $|\psi\rangle=\sqrt{\frac{2^{n}-1}{2^{n}}}\left|\psi^{\prime}\right\rangle+\frac{1}{\sqrt{2^{n}}}\left|x^{\prime}\right\rangle$ 代入上面公式
$$
W\left|x^{\prime}\right\rangle=\frac{2 \sqrt{2^{n}-1}}{2^{n}}\left|\psi^{\prime}\right\rangle+\left(\frac{2}{2^{n}}-1\right)\left|x^{\prime}\right\rangle
$$
用几步简单的代数化为
$$
W\left|\psi^{\prime}\right\rangle=-\left(\frac{2}{2^{n}}-1\right)\left|\psi^{\prime}\right\rangle+\frac{2 \sqrt{2^{n}-1}}{2^{n}}\left|x^{\prime}\right\rangle
$$
如果我们定义一个角 $\theta$ 为
$$
\sin \theta=\frac{2 \sqrt{2^{n}-1}}{2^{n}}
$$
那么上面两个方程可以化为
$$
\begin{array}{l}
W\left|x^{\prime}\right\rangle=-\cos \theta\left|x^{\prime}\right\rangle+\sin \theta\left|\psi^{\prime}\right\rangle \\
W\left|\psi^{\prime}\right\rangle=\sin \theta\left|x^{\prime}\right\rangle+\cos \theta\left|\psi^{\prime}\right\rangle
\end{array}
$$
如果我们用Grover算子 $G=W U_{f}$, 得到了这个形式就是大家熟悉的旋转
$$
\begin{aligned}
G\left|x^{\prime}\right\rangle &=\cos \theta\left|x^{\prime}\right\rangle-\sin \theta\left|\psi^{\prime}\right\rangle \\
G\left|\psi^{\prime}\right\rangle &=\sin \theta\left|x^{\prime}\right\rangle+\cos \theta\left|\psi^{\prime}\right\rangle
\end{aligned}
$$
基本思想是用Grover算子把 $\left|\psi^{\prime}\right\rangle$ 态旋转到我们要找的态 $\left|x^{\prime}\right\rangle$. 它一次只能转一点点角度，所以我们必须多次应用它，假设是 $m$ 次
$$
\begin{aligned}
G^{m}\left|x^{\prime}\right\rangle &=\cos m \theta\left|x^{\prime}\right\rangle-\sin m \theta\left|\psi^{\prime}\right\rangle \\
G^{m}\left|\psi^{\prime}\right\rangle &=\sin m \theta\left|x^{\prime}\right\rangle+\cos m \theta\left|\psi^{\prime}\right\rangle
\end{aligned}
$$

> 假设 $m \theta=\pi / 2$, 那么公式 $G^{m}\left|\psi^{\prime}\right\rangle=\sin m \theta\left|x^{\prime}\right\rangle+\cos m \theta\left|\psi^{\prime}\right\rangle$ 告诉我们算子 $G^{m}$ 把 $\left|\psi^{\prime}\right\rangle$ 变成 $\left|x^{\prime}\right\rangle$, 因为 $\sin \pi / 2=1, \cos \pi / 2=0$. 所以 $G^{m}\left|\psi^{\prime}\right\rangle=\left|x^{\prime}\right\rangle \quad(m \theta=\pi / 2)$.

根据定义 
$$
\sin \theta=\frac{2 \sqrt{2^{n}-1}}{2^{n}}
$$
用小角近似 (i.e., $\sin \theta \approx \theta$ ) 得到
$$
\theta \approx \frac{2 \sqrt{2^{n}-1}}{2^{n}}
$$
把这个角度公式代入 $m \theta=\pi / 2$ 得到t, we know that the condition that must be met in order to find $\left|x^{\prime}\right\rangle$ is
$$
\begin{array}{l}
m \theta=m \frac{2 \sqrt{2^{n}-1}}{2^{n}}=\frac{\pi}{2} \\
\Rightarrow m=\frac{\pi}{4} \frac{2^{n}}{\sqrt{2^{n}-1}} \approx \frac{\pi}{4} \sqrt{2^{n}}
\end{array}
$$
$m$ 的含义就是找到目标态 $\left|x^{\prime}\right\rangle$ 需要的运算次数。从结果来看，需要的次数是 $\sqrt{2^{n}}$ 级别的

