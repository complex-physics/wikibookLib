section-2 Deutsch-Josza算法



Deutsch-Josza算法是Deutsch算法的推广，

- Deutsch算法是解决输入一位的问题
- Deutsch-Josza算法是解决输入 $x$ 是一个由 0 和 1 组成的 $n$ 个字符串的问题。

也就是说Deutsch算法是 Deutsch-Josza算法$n=1$ 的特殊情况

在Deutsch-Josza算法下，平衡函数和常数函数

1. 如果 $f(x)$ 是常数函数，对于所有可能的输入，输出都一样
2. 如果 $f(x)$ 是平衡函数，对于一半的输入，输出 $f(x)=0$ ；对于一半的输入，输出 $f(x)=1$ ；  

Deutsch-Josza算法是全过程如下
$$
\left|\psi_{\text {out}}\right\rangle=(H^{\otimes n} \otimes I) U_{f}(H^{\otimes n} \otimes H)|0\rangle^{\otimes n}|1\rangle
$$

接下来详细讲解这个公式的过程

### 初始化

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200513095343202.png" alt="image-20200513095343202" style="zoom:50%;" />

我们输入 $n$ 个状态 $|0 \rangle$ 的量子比特态，和一个 $|1 \rangle$ 的量子比特态。

每个态都作用一个Hadamard门
$$
\begin{aligned}
\left|\psi^{\prime}\right\rangle=&\left(H^{\otimes n}\right)\left(|0\rangle^{\otimes n}\right) \otimes(H|1\rangle) \\
=&\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
\end{aligned}
$$

### U门

使用 $U_{f}$ 门
$$
U_{f}|x, y\rangle=|x, y \otimes f(x)\rangle
$$
最后一个量子比特态 $|1 \rangle$ 扮演着公式中 $y$ 的角色，经过 $U_{f}$ 门输出是
$$
\left|\psi^{\prime \prime}\right\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x}(-1)^{f(x)}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$

### Hadamard门

第三步是Hadamard门作用到前 $n$ 个态 $|x\rangle$ 上
$$
H^{\otimes n}|x\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{y}(-1)^{x \cdot y}|y\rangle
$$

最后输出是
$$
\left|\psi_{\text {out}}\right\rangle=\frac{1}{2^{n}} \sum_{y} \sum_{x}(-1)^{x \cdot y+f(x)}|y\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$

### 判断

测量输出，现在前 $n$ 个态是 $|y\rangle$ 

- 如果前 $n$ 个态 $|y\rangle$ 的测量结果全都是0，那么 $f(x)$ 是常数函数
- 如果前 $n$ 个态 $|y\rangle$ 的测量结果有至少一个1或者更多的1，那么 $f(x)$ 是常数函数



### 例子1

  考虑两比特的输入，函数是$f(x)=1 .$ 写出详细的过程展示Deutsch-Josza算法下线路输出量子态 $|y\rangle=|00\rangle$ 

------

**Solution**
初始态输入 $\left|\psi_{i n}\right\rangle=|0\rangle|0\rangle|1\rangle .$ 运用 Hadamard门作用到态上
$$
\begin{aligned}
\left|\psi^{\prime}\right\rangle=&H ^{\otimes 3}|0\rangle|0\rangle|1\rangle
\\=&\frac{1}{2 \sqrt{2}}(|000\rangle-|001\rangle+|010\rangle-|011\rangle+|100\rangle-|101\rangle+|110\rangle-|111\rangle)
\end{aligned}
$$

> $$
> \begin{aligned}
> \left|\psi^{\prime}\right\rangle=&\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\\
> =&\frac{1}{\sqrt{2^{2}}} \sum_{x \in\{0,1\}^{2}}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\\
> =&\frac{1}{2\sqrt{2}} \sum_{x \in\{0,1\}^{2}}|x\rangle\left(|0\rangle-|1\rangle\right)\\
> =&\frac{1}{2\sqrt{2}} \sum_{x \in\{0,1\}^{2}}|x\rangle\left(|0\rangle-|1\rangle\right)
> \end{aligned}
> $$
>
> 求和的 $x \in\{0,1\}^{2}$ 可能性包含
>
> - $|x\rangle=|00\rangle$ 
> - $|x\rangle=|01\rangle$ 
> - $|x\rangle=|10\rangle$ 
> - $|x\rangle=|11\rangle$ 

运用 $U_{f}$ 门作用到上面的态上
$$
\begin{aligned}
\left|\psi^{\prime \prime}\right\rangle=& U_{f}\left|\psi^{\prime}\right\rangle
\\=&\frac{1}{2 \sqrt{2}}U_{f}(|000\rangle-|001\rangle+|010\rangle-|011\rangle+|100\rangle-|101\rangle+|110\rangle-|111\rangle)
\\=&\frac{1}{2 \sqrt{2}}(|001\rangle-|000\rangle+|011\rangle-|010\rangle+|101\rangle-|100\rangle+|111\rangle-|110\rangle)
\end{aligned}
$$
其中第二步用到逻辑关系 $f(x)=1 .$ 

> 补充过程
> $$
> \left|\psi^{\prime \prime}\right\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x}(-1)^{f(x)}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
> $$
>
> $$
> \left|\psi^{\prime \prime}\right\rangle=\frac{1}{\sqrt{2^{2}}} \sum_{x}(-1)^{1}|00\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
> $$
>
> 求和的 $x \in\{0,1\}^{2}$ 可能性包含
>
> - $|x\rangle=|00\rangle$ 
> - $|x\rangle=|01\rangle$ 
> - $|x\rangle=|10\rangle$ 
> - $|x\rangle=|11\rangle$ 
>
> 如果不用通用公式，而是直接计算，结果是？
> $$
> \begin{aligned}
> U _{ f }|000\rangle &=|0,0 \oplus f (0),0\rangle+|0,0, \oplus f (0)\rangle \\
> &=|010\rangle+|001\rangle
> \end{aligned}
> $$
> 还是？
> $$
> \begin{aligned}
> U _{ f }|000\rangle &=|0,0 \oplus f (0),0 \oplus f (0)\rangle\\
> &=|011\rangle 
> \end{aligned}
> $$
> 经过验算，我认为是后者

最后一步是把 $H^{\otimes 2}$ 作用到前面两个量子比特上
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{2 \sqrt{2}}\left[\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle\right.\\
&+\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|0\rangle
\\&+\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle \\&+\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|0\rangle
\end{aligned}
$$
展开所有项得到
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle= \frac{1}{4 \sqrt{2}}&[(|00\rangle+|01\rangle+|10\rangle+|11\rangle)|1\rangle-(|00\rangle+|01\rangle+|10\rangle+|11\rangle)|0\rangle\\
&+(|00\rangle-|01\rangle+|10\rangle-|11\rangle)|1\rangle-(|00\rangle-|01\rangle+|10\rangle-|11\rangle)|0\rangle \\
&+(|00\rangle+|01\rangle-|10\rangle-|11\rangle)|1\rangle-(|00\rangle+|01\rangle-|10\rangle-|11\rangle)|0\rangle \\
&+(|00\rangle-|01\rangle-|10\rangle+|11\rangle)|1\rangle-(|00\rangle-|01\rangle-|10\rangle+|11\rangle)|0\rangle]
\end{aligned}
$$
把这些项的第三位提取公因式 $(|0\rangle-|1\rangle / \sqrt{2})$ 得到
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{4}\left[-(|00\rangle+|01\rangle+|10\rangle+|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\right.\\
&-(|00\rangle-|01\rangle+|10\rangle-|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&-(|00\rangle+|01\rangle-|10\rangle-|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&\left.-(|00\rangle-|01\rangle-|10\rangle+|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\right]
\\ =&-|00\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
\end{aligned}
$$
测量前两位量子比特得到 $00,$ 确认这是常数函数



### 例子2

> 假设 $f(00)=f(01)=0,$ $ f(10)=f(11)=1 .$ 使用 Deutsch-Josza 算法，证明最后的量子比特的前两位至少一个是1 

初态是 $\left|\psi_{\text {in}}\right\rangle=|0\rangle|0\rangle|1\rangle $ ，运用 Hadamard门作用到态上
$$
|\psi^{\prime}\rangle= \frac{1}{2 \sqrt{2}}(|000\rangle-|001\rangle+|010\rangle-|011\rangle+|100\rangle-|101\rangle+|110\rangle-|111\rangle)
$$
运用 $U_{f}$ 门作用到上面的态上
$$
\left|\psi^{\prime \prime}\right\rangle=\frac{1}{2 \sqrt{2}}(|000\rangle-|001\rangle+|010\rangle+|011\rangle+|101\rangle-|100\rangle+|111\rangle-|110\rangle)
$$
把 $H^{\otimes 2}$ 作用到前面两位量子比特上
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{4}\left[\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle-\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|1\rangle\right.\\
&+\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|0\rangle+\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|1\rangle \\
&+\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle \\
&+\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|0\rangle
\end{aligned}
$$
展开
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{4 \sqrt{2}}[(|00\rangle+|01\rangle-|10\rangle-|11\rangle)|1\rangle+(|00\rangle+|01\rangle+|10\rangle+|11\rangle)|0\rangle\\
&-(|00\rangle+|01\rangle+|10\rangle+|11\rangle)|1\rangle+(|00\rangle-|01\rangle+|10\rangle-|11\rangle)|0\rangle \\
&+(|00\rangle-|01\rangle+|10\rangle-|11\rangle)|1\rangle-(|00\rangle+|01\rangle-|10\rangle-|11\rangle)|0\rangle \\
&+(|00\rangle-|01\rangle-|10\rangle+|11\rangle)|1\rangle-(|00\rangle-|01\rangle-|10\rangle+|11\rangle)|0\rangle]
\end{aligned}
$$
重新整合
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{4}\left[(|00\rangle+|01\rangle+|10\rangle+|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\right.\\
&+(|00\rangle-|01\rangle+|10\rangle-|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&-(|00\rangle+|01\rangle-|10\rangle-|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&-(|00\rangle-|01\rangle-|10\rangle+|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\\
=&|10\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
\end{aligned}
$$
测量结果前两位是 10, 证明最后的量子比特的前两位至少一个是1 







