## Quantum Advantages

Before coming to the design of quantum machine learning algorithms, this chapter is an interlude to discuss how quantum computing can actually assist machine learning. Although quantum computing researchers often focus on asymptotic computational speedups, there is more than one measure of merit when it comes to machine learning. We will discuss three dimensions here, namely the computational complexity, the sample complexity and the model complexity. 1 While the section on computational complexity allows us to establish the terminology already used in previous chapters with more care, the section on sample complexity ventures briefly into quantum extensions of statistical learning theory. The last section on model complexity provides arguments towards what has been called the exploratory approach to quantum machine learning, in which quantum physics is used as a resource to build new types of models altogether.

### 2 BCS Hamiltonian and Mean Field

#### BCS Hamiltonian

The most general form of Hamiltonian for interacting electrons is
$$
H=\sum_{m n} H_{m n} c_{n}^{\dagger} c_{m}+\frac{1}{2} \sum_{k l m n} V_{k l m n} c_{k}^{\dagger} c_{m}^{\dagger} c_{n} c_{l}
$$
Let's included the phonon effect in the effective interaction, the income electrons $\left( k , k^{\prime}\right)$ exchange phonon q, outcome as $\left( k - q , k^{\prime}+q\right)$. The Hamiltonian become
$$
H=\sum_{k} \xi_{k} c_{k}^{\dagger} c_{k}+\frac{1}{2 N} \sum_{k, k^{\prime}, q} V_{k, k^{\prime}}^{e f f} c_{k+q}^{\dagger} c_{k^{\prime}-q}^{\dagger} c_{k^{\prime}} c_{k}
$$
where $\xi_{k}=\varepsilon_{k}-\mu$ and $V_{k, k^{\prime}}=V_{0}$ if the magnitude of $\xi_{k}=\varepsilon_{k}-\mu$ is smaller than a cutoff energy $\hbar \omega_{D}$

![](http://jptanjing.oss-cn-beijing.aliyuncs.com/img/feynman.jpeg)

only the states near the fermi surface can be scattered.

![fermisphere](http://jptanjing.oss-cn-beijing.aliyuncs.com/img/fermisphere.png)

For simplify, we consider $q=0$ and only keep the singlet-pair terms,ignore triplet-pair terms and the rest of the terms
$$
H=\sum_{k} \xi_{k} c_{k}^{\dagger} c_{k}+\frac{1}{N} \sum_{k, k^{\prime}, q} V_{k, k^{\prime}} c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger} c_{-k} c_{k}
$$
The second term describes the destruction of a Cooper pair two electrons with opposite momenta and spin, and the subsequent creation of another Cooper pair

### Mean-Field of BCS Hamiltonian

We are going to mean-field decoupling of the quartic term $c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger} c_{-k} c_{k}$

#### Mean-Field 

First we define
$$
\begin{aligned}
\delta^{\prime} &=\left\langle c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger}\right\rangle \\
\delta &=\left\langle c_{-k} c_{k}\right\rangle
\end{aligned}
$$
Thus we have
$$
\begin{aligned}
c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger} &=\delta^{\prime}-\delta^{\prime}+c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger}=\delta^{\prime}+\left(c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger}-\delta^{\prime}\right) \\
c_{-k} c_{k} &=\delta-\delta+c_{-k} c_{k}=\delta+\left(c_{-k} c_{k}-\delta\right)
\end{aligned}
$$
Then, the quartic term express by
$$
\begin{aligned}
c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger} c_{-k} c_{k} &=\left[\delta^{\prime}+\left(c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger}-\delta^{\prime}\right)\right]\left[\delta+\left(c_{-k} c_{k}-\delta\right)\right] \\
&=\delta^{\prime} \delta+\delta\left(c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger}-\delta^{\prime}\right)+\delta^{\prime}\left(c_{-k} c_{k}-\delta\right)+(\ldots) \\
&=\delta^{\prime} \delta+\delta c_{k^{\prime}}^{\dagger} c_{-k^{\prime}}^{\dagger}+\delta^{\prime} c_{-k} c_{k}+(\ldots)
\end{aligned}
$$
the small part $(\ldots)$ can be neglected









### Computational Complexity of Learning

The concept of runtime complexity and speedups has already been used in the previous sections and is the most common figure of merit when accessing potential contributions of quantum computing to machine learning. Quantum machine learning inherited this focus on runtime speedups from quantum computing, where- - for lack of practical experiments-researchers mostly resort to proving theoretical runtime bounds to advertise the power of their algorithms. Let us briefly introduce the basics of asymptotic computational complexity.

The runtime of an algorithm on a computer is the time it takes to execute the algorithm, in other words, the number of elementary operations multiplied by their respective execution times. In conventional computers, the number of elementary operations could in theory still be established by choosing the fastest implementations for every subroutine and count the logic gates. However, with fast technological advancements in the IT industry it becomes obvious that a device-dependent runtime is not a suitable theoretical tool to measure the general speed of an algorithm. This is why computational complexity theory looks at the asymptotic complexity or the rate of growth of the runtime with the size n of the input. "Asymptotic" thereby refers to the fact that one is interested in laws for sufficiently large inputs only. If the resources needed to execute an algorithm or the number of elementary operations grow polynomially (that is, not more than a factor nc for a constant c ) with the size of the input n, it is tractable and the problem in theory efficiently solvable. Of course, if c is large, even polynomial runtime algorithms can take too long to make them feasible for certain applications. The argument is that if we just wait a reasonable amount of time, our technology could in principle master the task. Exponential growth makes an algorithm intractable and the problem hard because for large enough problem sizes, it quickly becomes impossible to solve the problem.