## 多元函数的泰勒展开
* 对于多元函数：
    $$
    f(a+h)=\sum_{k=0}^{m} \sum_{|\alpha|=k} \frac{\partial^{\alpha} f(a)}{\partial x^{\alpha}} h^{\alpha}+R_{m}
    $$
    $$
    R_{m}=\sum_{|\alpha|=m+1} \frac{\partial^{\alpha} f(a+\theta h)}{\alpha !} h^{\alpha}
    $$
    如果只取前三项，表示为：
    $$
    f(a+h)=f(a)+\frac{\partial f}{\partial x_{1}}(a) h_{1}+\ldots+\frac{\partial f}{\partial x_{n}}(a) h_{n}+\frac{1}{2} \sum_{i, j=1}^{n} \frac{\partial^{2} f}{\partial x_{i} \partial x_{j}}(a)+\ldots
    $$
    用雅各比矩阵和海森矩阵表示为：
    $$
    f(a+h)=f(a)+J f(a) h+\frac{1}{2}\left(h_{1}, \ldots h_{n}\right) H f(a)\left(\begin{array}{c}{h_{1}} \\ {\ldots} \\ {h_{n}}\end{array}\right)+\ldots
    $$ 
* 雅各比矩阵：
    $$
    \mathbf{J}=\left[\begin{array}{ccc}{\frac{\partial \mathbf{f}}{\partial x_{1}}} & {\cdots} & {\frac{\partial \mathbf{f}}{\partial x_{n}}}\end{array}\right]=\left[\begin{array}{ccc}{\frac{\partial f_{1}}{\partial x_{1}}} & {\cdots} & {\frac{\partial f_{1}}{\partial x_{n}}} \\ {\vdots} & {\ddots} & {\vdots} \\ {\frac{\partial f_{m}}{\partial x_{1}}} & {\cdots} & {\frac{\partial f_{m}}{\partial x_{n}}}\end{array}\right]
    $$
* 海森矩阵：
    $$
    \mathrm{H}=\left[ \begin{array}{cccc}{\frac{\partial^{2} f}{\partial x_{1}^{2}}} & {\frac{\partial^{2} f}{\partial x_{1} \partial x_{2}}} & {\cdots} & {\frac{\partial^{2} f}{\partial x_{1} \partial x_{n}}} \\ {\frac{\partial^{2} f}{\partial x_{2} \partial x_{1}}} & {\frac{\partial^{2} f}{\partial x_{2}^{2}}} & {\cdots} & {\frac{\partial^{2} f}{\partial x_{2} \partial x_{n}}} \\ {\vdots} & {\vdots} & {\ddots} & {\vdots} \\ {\frac{\partial^{2} f}{\partial x_{n} \partial x_{1}}} & {\frac{\partial^{2} f}{\partial x_{n} \partial x_{2}}} & {\cdots} & {\frac{\partial^{2} f}{\partial x_{n}^{2}}}\end{array}\right]
    $$