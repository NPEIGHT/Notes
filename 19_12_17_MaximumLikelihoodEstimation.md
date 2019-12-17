## Maximum Likelihood Estimation (MLE)
* 估计模型参数，使得极大似然函数取得最大值
$$
\mathrm{L}\left(\theta | x_{1}, \ldots, x_{n}\right)=f_{\theta}\left(x_{1}, \ldots, x_{n}\right)
$$
* 对于一个模型，有一些观测数据$y_1,y_2$，需要估计位置的模型参数$\theta$，使用MLE，即令$P(y_1,y_2;\theta)$最大
* 对数形式：假设每个观测值是相互独立的，那么似然函数可以写成概率密度的乘积，直接计算最大值不方便，利用对数来简化计算