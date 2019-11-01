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