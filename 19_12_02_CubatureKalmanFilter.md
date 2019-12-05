## CKF
* 解决高维积分计算困难问题（Gaussian weighted integrals）
* 如果使用Product Rules如Gaussian Hermite积分定理，会出现维数灾难
* 如果使用Non-Product Rules如random Monte Carlo，quasi-Monte Carlo，sparse grid等方法，一定程度上也存在维数灾难
* 使用三阶全对称容积准则（third-degree fully）
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