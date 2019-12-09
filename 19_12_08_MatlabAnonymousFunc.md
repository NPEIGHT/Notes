## Matlab Anonymous Function
多输入变量
```matlab
fun = @(x, y) (x^2 + y^2 + x*y);
fun(1,2);
```
多返回变量
```matlab
c = 10;
mygrid = @(x,y) ndgrid((-x:x/c:x),(-y:y/c:y));
[x,y] = mygrid(pi,2*pi);
```
很多函数支持匿名函数作为输入，例如`integral`  
```matlab
integral(@(x) (x.^2 + c*x + 1),0,1);
```
匿名函数支持嵌套
$$
g(c)=\int_{0}^{1}\left(x^{2}+c x+1\right) d x
$$
```matlab
g = @(c) (integral(@(x) (x.^2 + c*x + 1),0,1));
```
