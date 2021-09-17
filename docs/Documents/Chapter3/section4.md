## Quantum Euclidean Distance Calculation

和点积很像，欧几里得距离是一些机器学习算法的核心，比如k-均值算法。用向量表示的经典数据，可以编码到量子态内
$$
|a\rangle=\frac{\vec{a}}{\|\vec{a}\|}=\|\vec{a}\|^{-1} \sum_{i=0}^{N-1} a_{i}|i\rangle
$$
在机器学习中，我们兴趣的向量间的欧几里得距离一般不是单位向量。

把两个向量 $\vec{a}$ 和 $\vec{b}$  归一化得到两个量子态向量 $|a\rangle$ 和 $|b\rangle$ 。用 $|a\rangle$ 和 $|b\rangle$ 和另一个量子比特，我们可以制造两个新的态 $|\psi\rangle$ 和 $|\phi\rangle$  
$$
\begin{array}{l}
|\psi\rangle=\frac{1}{\sqrt{2}}(|0\rangle \otimes|a\rangle+|1\rangle \otimes|b\rangle) \\
\left.|\phi\rangle=\frac{1}{\sqrt{Z}}(\|\vec{a}\| |0\rangle-\|\vec{b}\||1\rangle\right)
\end{array}
$$
其中

- $ Z$ 是 $\vec{a}$ 和 $\vec{b}$ 的平方和, $Z=\|\vec{a}\|^{2}+\|\vec{b}\|^{2} .$

对 $|\psi\rangle$ 和 $|\phi\rangle$  进行交换测试，测量ancilla量子比特处于 $|0\rangle$ 的概率，可以得到点积 $\langle\psi \mid \phi\rangle$ 如下式
$$
P(|0\rangle)=\frac{1}{2}+\frac{1}{2}\langle\psi \mid \phi\rangle^{2}
$$
现在点积 $\langle\psi \mid \phi\rangle$ 可以如下化简
$$
\begin{aligned}
\langle\psi \mid \phi\rangle=&\frac{1}{\sqrt{2}} (\langle a|\langle 0|+ \langle b|\langle 1|) \frac{1}{\sqrt{Z}}(\|\vec{a}|\| 0\rangle-\| \vec{b}|||1\rangle)  \\
=&\frac{1}{\sqrt{2 Z}}(\|\vec{a}\|\langle a|\langle 0 \mid 0\rangle-\|\vec{b}\|\langle a|\langle 0 \mid 1\rangle+\|\vec{a}\|\langle b|\langle 1 \mid 0\rangle-\| \vec{b}||| b\rangle\langle 1 \mid 1\rangle \\
=&\frac{1}{\sqrt{2 Z}}(\|\vec{a}\|\langle a|-\|\vec{b}\|\langle b|)\\
=&\frac{1}{\sqrt{2 Z}}(\vec{a}-\vec{b})^{T}
\end{aligned}
$$
把这个表达式 $\langle\psi \mid \phi\rangle$ 代入测量概率
$$
\begin{aligned}
P(|0\rangle)&=\frac{1}{2}+\frac{1}{2} \| \frac{1}{\sqrt{2} Z}(\vec{a}-\vec{b}) \mid \\
&=\frac{1}{2}+\frac{1}{4} \frac{1}{Z}\|(\vec{a}-\vec{b})\|^{2}
\end{aligned}
$$
反过来，要得到欧几里得距离的平方，可以从范数和测量概率中得到
$$
\|(\vec{a}-\vec{b})\|^{2}=4 Z(P(|0\rangle)-0.5)
$$

### Creating the Initial States Without QRAM 

用QRAM很容易制造出初态 $|\psi\rangle=\frac{1}{\sqrt{2}}(|0\rangle \otimes|a\rangle+|1\rangle \otimes|b\rangle)$ 。但是我们没有QRAM，所以要找一个替代方案来制造初态。下图的线路可以用来制造初态 $|\psi\rangle$. 

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20210822015333582.png" style="zoom:80%;" />

> Fig5-2 Initial state creation circuit for Euclidean distance computation

起始是四比特寄存器（ $\left|q_{0}\right\rangle_{A},\left|q_{1}\right\rangle_{W},\left|q_{2}\right\rangle_{I N P_{1}}$, $\left|q_{3}\right\rangle_{I N P_{2}} $ ）

- 第一个寄存器是 $\left|q_{0}\right\rangle_{A}$ ，其中后缀 $A$ 表示这是一个ancilla量子比特
- 第二个寄存器 $\left|q_{1}\right\rangle_{W}$ 是工作寄存器(work) 
- ancilla寄存器和工作寄存器的张量积 $\left|q_{0}\right\rangle_{A} \otimes\left|q_{1}\right\rangle_{W}$ 在线路最后的输出是 $\frac{1}{\sqrt{2}}(|0\rangle \otimes|a\rangle+|1\rangle \otimes|b\rangle)$ 
- 一旦要求的态 $\frac{1}{\sqrt{2}}(|0\rangle \otimes|a\rangle+|1\rangle \otimes|b\rangle)$ 被造出来了，我们需要让 $q_{2}$ 和 $q_{3}$ 的态不要计算，保持输入态 $|a\rangle$ 和 $|b\rangle$ 为初始态 $|0\rangle$ 所以他们不会和前面两个寄存器纠缠 

#### Quantum Euclidean Distance Gompute Routine Implementation

用交换测试方法来实现量子欧几里得距离

1. 构造两个态
   - $|\psi\rangle=\frac{1}{\sqrt{2}}(|0\rangle \otimes|a\rangle+|1\rangle \otimes|b\rangle)$ 
   - $|\phi\rangle=\frac{1}{\sqrt{Z}}(\|\vec{a}\||0\rangle-\|\vec{b}\||1\rangle)$  
2. 用交换测试法计算出 $\langle\psi \mid \phi\rangle$.  
3. 距离平方可以根据 $\|(\vec{a}-\vec{b})\|^{2}=4 Z(P(|0\rangle)-0.5)$ 