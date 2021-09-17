## Quantum K-Means Glustering

量子k-均值算法，可以用欧几里得距离和Grover搜索算法来实现。

#### Initialize 

可以类似于经典版本的k-均值算法，随机选择 $k$ 个数据点。在本次量子版本中，初始化 $k$ 簇质心 $\mu_{1}, \mu_{2} \ldots \mu_{k} \in R ^{n}$ 

#### Until Convergence 

步骤

1. 对于每个数据点 $x_{i} \in R ^{n}$ 

   - 幅度 $\left\|\overrightarrow{x_{i}}\right\|_{2}$ 可以用经典存储
   - 单位范数的 $\left|x_{i}\right\rangle$ 可以存储为量子态

   对于每个 $k$ 簇质心，计算得到量子欧几里得距离

$$
d(i, j)=\left\|\left(x_{i}-u_{j}\right)\right\|^{2}=4 Z(P(|0\rangle)-0.5) \quad j \in\{1,2, . . k\}
$$

2. 用 Grover's 搜索算法赋予每个数据点 $x_{i}$ 归属于 $k$ 个族簇的其中一个。Grover搜索算法的oracle需要能给出距离 $d(i, j)$ 和正确的簇分配 $c_{i}$  

$$
c_{i}=\underbrace{\operatorname{argmin}}_{j}\left\|\left(x_{i}-u_{j}\right)\right\|^{2} \quad c_{i} \in\{1,2, . . k\}
$$

3. 一旦每个数据点 $x_{i}$ 都被分配给各自的簇 $c_{i} \in\{1,2, \ldots k\}$ ，每个簇的平均或者说中心可以如下计算获得
   $$
   u_{j}=\frac{1}{N_{j}} \sum_{c=j} x_{i}
   $$
   其中 $N_{j}$ 表示第 $j$ 个簇的所有数据点数量

$$
u_{j}=\frac{1}{N_{j}} \sum_{c=j} x_{i}
$$

算法收敛

后续的迭代下，数据点不再改变各自的族簇，这种情况下可以说算法收敛了。



复杂度：经典k-均值算法的每一次迭代的复杂度是 $O(M N k)$ 

1. 计算每个数据点与簇的距离的计算复杂度是 $O(N)$ ，其中 $N$ 是数据点的特征数量
2. 因为有 $k$ 个簇，所以每个数据点到所有簇的距离，计算复杂度就是 $O(N k)$.
3. 因为数据点有 $M$ 个，所以每一次迭代的复杂度是 $O(M N k)$ 

我们在量子k-均值算法中得分项其实是第一步

1. 计算每个数据点到簇的量子欧几里得距离d 算法复杂度是 $O(\log N)$  
2. 后续的步骤和经典的一样，所以最后的复杂度是 $\operatorname{Mlog}(N) k$. 

这里我们并没有考虑给每个数据点分配到各自的簇的过程，如果运用Grover搜索算法在这个分配过程，那么可以提供很多的加速。



### Quantum K-Means Clustering Using Cosine Distance

这一节中，我们把cosin距离看成距离矩阵，用来完成量子k-均值算法。

余弦相似度，就是计算两个向量( $\vec{x}$ 和 $\vec{y}$ )间的夹角的余弦值。 
$$
\text { similarity }=\cos (\theta)=\frac{\vec{x} \cdot \vec{y}}{\|x\| \cdot\|y\|}
$$
余弦距离就是用1减去这个获得的余弦相似度
$$
\text { cosine distance }=1-\text { similarity }=1-\cos (\theta)
$$
既然 $\vec{x}$ 和 $\vec{y}$ 是单位范数，那么他们可以直接映射到量子态。单位向量 $|x\rangle$ 和 $|y\rangle$ 的欧几里得距离的平方是
$$
\begin{aligned}
|||x\rangle-|y\rangle \|^{2}=&\langle x \mid x\rangle+\langle y \mid y\rangle-2\langle x \mid y\rangle
\\=& 2-2\langle x \mid y\rangle
\\=& 2(1-\langle x \mid y\rangle)
\end{aligned}
$$
回忆交换测试，我们知道测量0的概率如果是是 $\frac{1}{2}+\frac{1}{2}\langle x \mid y\rangle^{2}$, 那么测量态1的概率是
$$
\begin{aligned}
P (1)=&\frac{1}{2}-\frac{1}{2}\langle x \mid y\rangle^{2}
\\=&\frac{1}{2}\left(1-\langle x \mid y\rangle^{2}\right)
\\=& \frac{1}{2}(1-\langle x \mid y\rangle)(1+\langle x \mid y\rangle)
\end{aligned}
$$
 