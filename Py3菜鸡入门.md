# 面向对象
## 类方法
类方法需要一个*self*参数（名称没有限制，但必须是第一个参数），表示类的实例
```python
class Example:
    def _init_(self): #实例化时自动调用该方法
        self.data = [1,2,3] 
    def prt(self, input): #包含输入参数的方法
        print("Class data:", self.data, "\nInput data:", input)

x = Example()
x.prt(1234)
#输出：
#Class data: [1, 2, 3] 
#Input data: 1234
```
类的私有属性，私有方法名前加`__`，，只能在类内部调用

## 继承
```python
class Parent:
    def myMethod(self, input):
        print("Parent: ", input)

class Child(Parent):
    def myMethod(self, input): #对父类方法进行重写
        print("Child: ", input)

x = Child()
x.myMethod(123) #调用子类方法
super(Child, x).myMethod(123)   #使用super()，从子类调用父类的方法

#输出：
#Child:  123
#Parent:  123
```
进行多继承时，如果子类中没有调用的方法而父类中有，在多个父类中**从左到右**搜索  
类支持对运算符的重载

## 类型注解
Py3的新feature，方便看别人的🐎
```python
def foo(x: int, y: int)->int:
    return x + y
```
就是冒号表示参数类型，->表示返回类型，解释器完全不管你写的类型，只是给人看的  
用一些trick也可以添加类型的检验

## 迭代器
任何实现了`__iter__`和`__next__`方法的对象都是迭代器，`__iter__`返回迭代器自身，`__next__`返回容器中的下一个值，如果容器中没有更多元素了，则抛出StopIteration异常
```python
class Fib:
    def __init__(self):
        self.prev = 0
        self.curr = 1

    def __iter__(self):
        return self

    def __next__(self):
        value = self.curr
        self.curr += self.prev
        self.prev = value
        return value

>>> f = Fib()
>>> list(islice(f, 0, 10))  #islice(seq, start, stop, step), itertool
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```
两个基本方法：`iter()`和`next()`可以用于创建迭代器/输出迭代器元素，字符串、列表、元组都可以用来创建迭代器

## 生成器
生成器的重点在于`yield`，它返回的是迭代器而不是某个值。在调用生成器运行的过程中，每次遇到`yield`时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行`next()`方法时从当前位置继续运行

```python
def fib():
    prev, curr = 0, 1
    while True:
        yield curr
        prev, curr = curr, curr + prev

>>> f = fib()
>>> list(islice(f, 0, 10))
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```
多使用迭代器和生成器有助于节省资源

## 装饰器
>在？搞点FP  

装饰器本质上是一个 Python 函数或类，它可以让其他函数或类在不需要做任何代码修改的前提下增加额外功能，装饰器的返回值也是一个函数/类对象
```python
def decorator(func):
    def wrapper():
        print("Decorated!")
        return func()
    return wrapper

def foo():
    print("I'm foo\n")

>>> foo = decorator(foo)
>>> foo()
Decorated!
I'm foo
```
使用@简化装饰器的调用：
```python
def decorator(func):
    def wrapper():
        print("Decorated!")
        return func()
    return wrapper

@decorator
def foo():
    print("I'm foo\n")

#foo = decorator(foo)省略这一句
>>> foo()
Decorated!
I'm foo
```
对于带有参数和关键字参数的函数，使用`*args`和`**kwargs`给wrapper指定参数：
```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Decorated!")
        return func(*args, **kwargs)
    return wrapper

@decorator
def foo(name, num=0):
    print("Num is %d" % num)
    print("I'm %s" % name)

>>> foo('abc',num=10)
Decorated!
Num is 10
I'm abc
```