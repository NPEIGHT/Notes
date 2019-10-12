# Chapter 1 Numerical Basics
## 1. Numerical Integration of Differential Equations
* ### Euler integration
$$
\dot{x}=f(x,t)\\
\dot{x}=f(x,t)=\frac{x(t+h)-x(t)}{h}=\frac{x_k-k_{k-1}}{h}\\
x_k=x_{k-1}+hf(x,t)
$$
* ### Second order Runge-Kutta numerical integration
$$
\dot{x}=f(x,t)\\
x_k=x_{k-1}+0.5h[f(x,t)+f(x,t+h)]
$$
## 2. State-Space Notation
$$
\boldsymbol{\dot{x}=Fx+Gu+w}
$$
$\boldsymbol{x}$ is system *state vector*, $\boldsymbol{F}$ is systems *dynamics matrix*, $\boldsymbol{u}$ is a deterministic input called *control vector*, $\boldsymbol{w}$ is a radom forcing function called *process noise*
## 3. Fundamental Matrix
$$
\boldsymbol{\dot{x}=Fx}
$$
If the systems dynamics matrix $\boldsymbol{F}$ is **time invariant**, there is a transition or *fundamental matrix* $\Phi$ can be used to propagate the state forward from any time $t_o$ to time $t$:
$$
\boldsymbol{x(t)} = \Phi(t-t_o)\boldsymbol{x}(t_0)
$$
Laplace transforms and Taylor-series expansion can be used to find $\Phi$
$$
\Phi (\boldsymbol{t})=\mathscr{L}^{-1}[(\boldsymbol{sI-F})^{-1}]\\
\Phi(t)=e^{\boldsymbol{F}t}=\boldsymbol{I}+\boldsymbol{F}t+\frac{(\boldsymbol{F}t)^2}{2!}+...+\frac{(\boldsymbol{F}t)^n}{n!}+...
$$

# Chapter 2 Method of Least Squares
## 1. Zeroth-Order or One-State Filter
>Least-squares filtering/estimation  

We desire to minimize
$$
R=\sum_{k=1}^n(\hat{x}_k-x^*_k)^2=\sum_{k=1}^n(a_0-x_k^*)^2
$$
where $x_k^*$ is the measurement at time $k$, $\hat{x}_k$ is the estimate.   
In the zeroth-order system the estimate will be a constant
$$
\hat{x}_k=a_0
$$
so it is also called a one-state system.  
To minimize $R$, set $R'$ to zero and make sure $R''$ is positive
$$
\frac{\partial R}{\partial a_0}=0=2(a_0-x_1^*)+2(a_0-x_2^*)+...+2(a_0-x_n^*)\\
\frac{\partial^2R}{\partial a_0^2}=2+2+...+2=2n>0\\
a_0=\frac{\sum_{k=1}^nx_k^*}{n}
$$
The best constant in the *least-squares sense* is average value of the measurements.
## 2. First-Order of Two-State Filter
To fit the measurement data with the best straight line
$$
\hat{x}=a_0+a_1t\\
\hat{\dot{x}}=a1
$$
or in descrete notataion
$$
\hat{x}_k=a_0+a_1(k-1)T_s\\
\hat{\dot{x}}_k=a1
$$
$$
\frac{\partial R}{\partial a_0}=0=2(a_0-x_1^*)+2(a_0+a_1T_s-x_2^*)+...+2(a_0+a_1(n-1)T_s-x_n^*)\\
\frac{\partial R}{\partial a_1}=0=2(a_0+a_1Ts-x_2^*)T_s+...+2(n-1)T_s(a_0+a_1(n-1)T_s-x_n^*)\\
$$
and
$$
na_0+a_1\sum_{k=1}^n(k-1)T_s=\sum_{k=1}nx_k^*\\
a_0\sum_{k=1}^n(k-1)T_s+a_1\sum_{k=1}^n[(k-1)T_s]^2=\sum_{k=1}^n(k-1)T_sx_k^*
$$
## 3. Second-Order or Three-State Least-Squares Filter
$$
\hat{x}=a_0+a_1t+a_2t^2\\
\hat{x}_k=a_0+a_1(k-1)T_s+a_2[(k-1)T_s]^2
$$
---
>### The best least-squares polynomial will always go through all of the data when the order of the system is one less than the number of measurements. High order polynomials may fit the measurement noise and result in error.

# Chapter 3 Recursive Least-Squares Filtering
>Making batch-processing recursive
## 1. Recursive Zeroth-Order Least-Squares Filter
$$
\hat{x}_k=a_0=\frac{\sum_{i=1}^kx_i^*}{k}\\
\hat{x}_k=\hat{x}_{k-1}+\frac{1}{k}(x_k^*-\hat{x}_{k-1})
$$
The new estimate depends on the old estimate plus a gain (for zeroth-order filter is $\frac{1}{k}$) times a residual (current measurement minus preceding estimate)
$$
\hat{x}_k=\hat{x}_{k-1}+K_{1_k}{Res}_k
$$