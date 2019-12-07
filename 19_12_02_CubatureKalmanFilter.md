## CKF
* 解决高维积分计算困难问题（Gaussian weighted integrals）
* 如果使用Product Rules如Gaussian Hermite积分定理，会出现维数灾难
* 如果使用Non-Product Rules如random Monte Carlo，quasi-Monte Carlo，sparse grid等方法，一定程度上也存在维数灾难问题
* 利用容积准则计算积分：
$$
\int_{\mathcal{D}} \mathcal{P}(\mathbf{x}) w(\mathbf{x}) d \mathbf{x}=\sum_{i=1}^{m} \omega_{i} \mathcal{P}\left(\mathbf{x}_{i}\right)
$$
* 利用不变量理论减少等式数量
* 容积点和权值与被积函数无关，可以预先算好保存
* Spherical-Radial Transformation
    $$
    \begin{aligned} I(g ; p) &=\int \cdots \int_{R^{d}} g(\mathbf{t}) p(\mathbf{t}) d \mathbf{t} \\ &=\int \cdots \int_{R^{d}} g^{*}(\mathbf{x}) p^{*}(\mathbf{x}) d \mathbf{x} \\ &=\int_{0}^{\infty} \int_{U_{d}} g^{*}(r \mathbf{z}) p^{*}(r \mathbf{z}) d \mathbf{z} r^{d-1} d r \end{aligned}
    $$ 
    关键在于单位球面上点$z\in R^{n-1}$，所以Jacobian为
    $$
    \begin{vmatrix}
    r\\
    &r\\
    &&\ddots \\
    &&&r\\
    &&&&1 
    \end{vmatrix}
    $$
    即为$r^{d-1}$

* 进行Transform之后，将球面径向积分分解成一个球面积分和一个径向积分，分别用容积准则和高斯积分准则计算

$$
S(r)=\int_{U_{n}} \mathbf{f}(r \mathbf{y}) d \sigma(\mathbf{y})
$$
$$
I=\int_{0}^{\infty} S(r) r^{n-1} \exp \left(-r^{2}\right) d r
$$

### 1. 球面容积准则
$$
\int_{U_{n}} \mathbf{f}(\mathbf{y}) d \sigma(\mathbf{y}) \approx \omega \sum_{i=1}^{2 n} \mathbf{f}[u]_{i}
$$

* 容积点应属于一个全对称集，对于排列和符号变化是不变的（invariant），可以设特值来推算容积点位置
    $$
    \mathbf{f}(\mathbf{y})=1: \quad 2 n \omega=\int_{U_{n}} d \sigma(\mathbf{y})=A_{n}
    $$
    $$
    \mathbf{f}(\mathbf{y})=y_{1}^{2}: \quad 2 \omega u^{2}=\int_{U_{n}} y_{1}^{2} d \sigma(\mathbf{y})=\frac{A_{n}}{n}
    $$
    $A_n$是单位球表面积$A_{n}=2 \sqrt{\pi^{n}} / \Gamma(n / 2)$，$\Gamma(n)=\int_{0}^{\infty} x^{n-1} \exp (-x) d x$，所以$\omega=A_{n} / 2 n$，$u^{2}=1$  
    所以容积点在单位球和坐标轴的交点上

### 2. 径向准则
$$
\int_{a}^{b} f(x) w(x) d x \approx \sum_{i=1}^{m} \omega_{i} f\left(x_{i}\right)
$$
* 用高斯积分定理计算径向积分（令$t=x^2$）
$$
\int_{0}^{\infty} f(x) x^{n-1} \exp \left(-x^{2}\right) d x=\frac{1}{2} \int_{0}^{\infty} \tilde{f}(t) t^{\left(\frac{n}{2}-1\right)} \exp (-t) d t
$$
* 为使准则对所有三阶多项式都是精确的，使用一阶高斯勒让德求积
    $$
    \int_{0}^{\infty} f(x) x^{n-1} \exp \left(-x^{2}\right) d x \approx \omega_{1} f\left(x_{1}\right)
    $$
    $$
    \omega_{1}=\Gamma(n / 2) / 2, \text { and } x_{1}=\sqrt{n / 2}
    $$

### 3. 球面径向准则
* $m_r$点高斯求积计算径向积分
$$
\int_{0}^{\infty} f(r) r^{n-1} \exp \left(-r^{2}\right) d r=\sum_{i=1}^{m_{r}} a_{i} f\left(r_{i}\right)
$$

* $m_s$点容积准则计算球面积分
$$
\int_{U_{n}} \mathbf{f}(r \mathbf{s}) d \sigma(\mathbf{s})=\sum_{j=1}^{m_{s}} b_{j} \mathbf{f}\left(r \mathbf{s}_{j}\right)
$$

* $m_s\times m_r$点球面径向准则
$$
\int_{\mathbb{R}^{n}} \mathbf{f}(\mathbf{x}) \exp \left(-\mathbf{x}^{T} \mathbf{x}\right) d \mathbf{x} \approx \sum_{j=1}^{m_{s}} \sum_{i=1}^{m_{r}} a_{i} b_{j} \mathbf{f}\left(r_{i} \mathbf{s}_{j}\right)
$$
* 令$w_{1}(\mathbf{x})=\exp \left(-\mathbf{x}^{T} \mathbf{x}\right)$，$w_{2}(\mathbf{x})=\mathcal{N}(\mathbf{x} ; \mu, \Sigma)$，$\sqrt{\Sigma} \sqrt{\Sigma}^{T}=\Sigma$
$$
\int_{\mathbb{R}^{n}} \mathbf{f}(\mathbf{x}) w_{2}(\mathbf{x}) d \mathbf{x}=\frac{1}{\sqrt{\pi^{n}}} \int_{\mathbb{R}^{n}} \mathbf{f}(\sqrt{2 \Sigma} \mathbf{x}+\mu) w_{1}(\mathbf{x}) d \mathbf{x}
$$
* 对于三阶球面径向容积准则，$m_r=1,m_s=2n$，则共有2n个容积点，根据以上推论，可以计算高斯加权积分
$$
I_{\mathcal{N}}(\mathbf{f})=\int_{\mathbf{R}^{n}} \mathbf{f}(\mathbf{x}) \mathcal{N}(\mathbf{x} ; \mathbf{0}, \mathbf{I}) d \mathbf{x} \approx \sum_{i=1}^{m} \omega_{i} \mathbf{f}\left(\xi_{i}\right)
$$
$$
\begin{aligned} \xi_{i} &=\sqrt{\frac{m}{2}}[1]_{i} \\ \omega_{i} &=\frac{1}{m}, \quad i=1,2, \ldots m=2 n \end{aligned}
$$

### SCKF
* 在每个update cycle中，误差协方差矩阵应始终保持对称和正定，可以提高滤波器数值稳定性。实际应用中由于矩阵开方、求逆和舍入误差，往往导致对称性和正定性被破坏。还有一些特殊状况下的非线性滤波问题可能引发该现象，导致不稳定和滤波发散。
* 平方根CKF传递预测和先验误差协方差的平方根系数，保持了协方差矩阵的对称性和（半）正定性，同时提供二阶精度