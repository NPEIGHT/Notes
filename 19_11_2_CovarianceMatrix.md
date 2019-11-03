## 协方差矩阵
* 对于由n个随机变量组成的列向量
  $$
  \mathbf{X}=\left[\begin{array}{c}{X_{1}} \\ {X_{2}} \\ {\vdots} \\ {X_{n}}\end{array}\right]
  $$
  它的协方差矩阵为
  $$
  \begin{aligned} \Sigma=& \mathrm{E}\left[(\mathbf{X}-\mathrm{E}[\mathbf{X}])(\mathbf{X}-\mathrm{E}[\mathbf{X}])^{\mathrm{T}}\right] \\ =&\left[\begin{array}{cccc}{\mathrm{E}\left[\left(X_{1}-\mu_{1}\right)\left(X_{1}-\mu_{1}\right)\right]} & {\mathrm{E}\left[\left(X_{1}-\mu_{1}\right)\left(X_{2}-\mu_{2}\right)\right]} & {\cdots} & {\mathrm{E}\left[\left(X_{1}-\mu_{1}\right)\left(X_{n}-\mu_{n}\right)\right]} \\ {\mathrm{E}\left[\left(X_{2}-\mu_{2}\right)\left(X_{1}-\mu_{1}\right)\right]} & {\mathrm{E}\left[\left(X_{2}-\mu_{2}\right)\left(X_{2}-\mu_{2}\right)\right]} & {\cdots} & {\mathrm{E}\left[\left(X_{2}-\mu_{2}\right)\left(X_{n}-\mu_{n}\right)\right]} \\ {\vdots} & {\vdots} & {\ddots} & {\vdots} \\ {\mathrm{E}\left[\left(X_{n}-\mu_{n}\right)\left(X_{1}-\mu_{1}\right)\right]} & {\mathrm{E}\left[\left(X_{n}-\mu_{n}\right)\left(X_{2}-\mu_{2}\right)\right]} & {\cdots} & {\mathrm{E}\left[\left(X_{n}-\mu_{n}\right)\left(X_{n}-\mu_{n}\right)\right]}\end{array}\right] \end{aligned}
  $$
  因此可以将其看作随机向量X的方差，作为标量随机变量方差的推广。或者是由随机向量中的每个标量元素间的协方差组成的矩阵。  
  尽管协方差矩阵很简单，可它却是很多领域里的非常有力的工具。它能导出一个变换矩阵，这个矩阵能使数据完全去相关(decorrelation)。从不同的角度看，也就是说能够找出一组最佳的基以紧凑的方式来表达数据。这个方法在统计学中被称为主成分分析(principal components analysis)，在图像处理中称为Karhunen-Loève 变换(KL-变换)