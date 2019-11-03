## Chapter 1 What are Bayesian filtering and smoothing
* ### Bayesian filtering: the Bayesian way of formulating optimal filtering (i.e estimating the state of a time-varying system which is indirectly observed through noisy measurements), only compute estimates of the current state.
* ### Bayesian smoothing: a class of methods within the field of Bayesian filtering, can be used to reconstruct states that happened before the current time.
* ### The purpose of the statistical inversion at hand is to estimate the hidden states from the observed measurements
    $$
    p(x_{0:T}|y_{1:T})=\frac{p(y_{1:T}|x_{0_T})p(x_{0_T})}{p(y_{1:T})} \tag{1}
    $$
    ### but it is intractable to compute the full posterior estimates.
## Chapter 2 Bayesian inference 贝叶斯推断
* 贝叶斯推断的核心问题：对测量结果的似然估计——$p(x|D)$
  $$
  p(x|D)=\int p(x,\theta|D)d\theta=\int p(x|\theta,D)p(\theta|D)d\theta=\int p(x|\theta)p(\theta|D)d\theta
  $$
  >x和D独立  

  由参数的后验分布估计——$p(\theta|D)$
  $$
  p(\theta|D)=\frac{p(D|\theta)p(\theta)}{p(D)}=\frac{p(D|\theta)p(\theta)}{\int p(D|\theta)p(\theta)d\theta}\\
  p(D|\theta)=\Pi_{k=1}^Np(x_k|\theta)
  $$
  >测量之间i.i.d.

## Chapter 3 Batch & recursive Bayesian estimation

$$
p\left(\boldsymbol{\theta} | \mathbf{y}_{1: T}\right)=\frac{1}{Z} p(\boldsymbol{\theta}) \prod_{k=1}^{T} p\left(\mathbf{y}_{k} | \boldsymbol{\theta}\right)
$$

$$
Z=\int p(\boldsymbol{\theta}) \prod_{k=1}^{T} p\left(\mathbf{y}_{k} | \boldsymbol{\theta}\right) \mathrm{d} \boldsymbol{\theta}
$$

## Chapter 4 Bayesian filtering equations

* ### 概率状态空间模型
  马尔可夫模型的重要性质：
  * $p\left(\mathbf{x}_{k} | \mathbf{x}_{1: k-1}, \mathbf{y}_{1: k-1}\right)=p\left(\mathbf{x}_{k} | \mathbf{x}_{k-1}\right)$ 已知k-1时刻状态，则k时刻状态与k-1时刻之前的状态和量测都独立
  * $p\left(\mathbf{x}_{k-1} | \mathbf{x}_{k: T}, \mathbf{y}_{k: T}\right)=p\left(\mathbf{x}_{k-1} | \mathbf{x}_{k}\right)$ 相应的，已知当前状态，过去的状态与将来的状态和量测独立
  * $p\left(\mathbf{y}_{k} | \mathbf{x}_{1: k}, \mathbf{y}_{1: k-1}\right)=p\left(\mathbf{y}_{k} | \mathbf{x}_{k}\right)$ 已知当前状态，当前量测量和此前所有的状态和量测独立
* ### 贝叶斯滤波方程
  递归计算预测分布$p\left(\mathbf{x}_{k} | \mathbf{y}_{1: k-1}\right)$和滤波分布$p\left(\mathbf{x}_{k} | \mathbf{y}_{1: k}\right)$
  1. 初始化：先验分布$p(x_0)$
  2. 预测：C-K方程计算k时刻状态的分布 $p\left(\mathbf{x}_{k} | \mathbf{y}_{1: k-1}\right)=\int p\left(\mathbf{x}_{k} | \mathbf{x}_{k-1}\right) p\left(\mathbf{x}_{k-1} | \mathbf{y}_{1: k-1}\right) \mathrm{d} \mathbf{x}_{k-1}$
  3. 更新：已知量测量，状态的后验分布 
        $$
        p\left(\mathbf{x}_{k} | \mathbf{y}_{1: k}\right)=\frac{1}{Z_{k}} p\left(\mathbf{y}_{k} | \mathbf{x}_{k}\right) p\left(\mathbf{x}_{k} | \mathbf{y}_{1: k-1}\right)
        $$
        其中Z是归一化常数
        $$
        Z_{k}=\int p\left(\mathbf{y}_{k} | \mathbf{x}_{k}\right) p\left(\mathbf{x}_{k} | \mathbf{y}_{1: k-1}\right) \mathrm{d} \mathbf{x}_{k}
        $$