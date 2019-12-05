## 基本概念
* 方阵$A$的特征值$\lambda$，特征向量$\upsilon$
$$
A v=\lambda v
$$


## Hermitian矩阵
* 共轭对称方阵，每一个第i行第j列的元素都是第j行第i列的元素的复共轭
* 主对角线上元素都是实数，特征值为实数
* A,B为H矩阵，A+B为H矩阵，AB=BA时，AB为H矩阵

## 正定矩阵
* 正定矩阵是H矩阵的一种，对于任意非零复向量$z$，都有$z^*Mz>0$，$z^*$表示共轭转置，则称$M$正定
* 若为实对称矩阵，则对于任意非零向量$z$，都有$z^TMz>0$，称$M$正定
* 正定矩阵行列式恒为正
* A>0, B>0, A+B>0
* M正定，M的所有特征值都为正
* M正定，则存在唯一的下三角矩阵L，使得$M=LL^*$，称为Cholesky分解，其中$L$的所有对角元素大于零


## Kronecker积
* 两个任意大小的矩阵间的运算，表示为$\otimes$
* 如果A是一个 m × n 的矩阵，而B是一个 p × q 的矩阵，克罗内克积$A\otimes B$则是一个 mp × nq 的分块矩阵
    $$
    A \otimes B=\left[\begin{array}{ccc}{a_{11} B} & {\cdots} & {a_{1 n} B} \\ {\vdots} & {\ddots} & {\vdots} \\ {a_{m 1} B} & {\cdots} & {a_{m n} B}\end{array}\right]
    $$
* 满足转置分配律
  $$
  (A \otimes B)^{T}=A^{T} \otimes B^{T}
  $$
* 满足双线性和结合律
$$
\begin{aligned} A \otimes(B+C)=A \otimes B+A \otimes C & \text { (if } B \text { and } C \text { have the same size), } \\(A+B) \otimes C=A \otimes C+B \otimes C & \text { (if } A \text { and } B \text { have the same size), } \\(k A) \otimes B & =A \otimes(k B)=k(A \otimes B), \\(A \otimes B) \otimes C & =A \otimes(B \otimes C) \end{aligned}
$$
