# Python Notes

## 基础语法

```python
# input and output
name = input()
print(name)
```

    aaa
    aaa



```python
# logic 
print(True and False)
print(True or False)
print(not True)
```

    False
    True
    False


`str()`返回一个对象的string格式
`len()`计算一个string包含多少个字符
`int()`返回一个对象的整数格式


```python
a = 77
b = str(a)
c = int(b)
print(len(b))
print(a == c)
```

    2
    True


`list`是Python内置的一种数据类型，是一种有序的集合，可以随时添加或删除元素


```python
names = ['a', 'b', 'c']
print(names)
print(names[0])
print(names[1])
print(names[2])
print(names[-1]) # get the last
```

    ['a', 'b', 'c']
    a
    b
    c
    c



```python
# use pop() or pop(i) to delete
# pop() delete the last
names.pop()
print(names)
# use append() or insert(i, str) to add
# append() add the last
names.append('c')
print(names)
names.insert(1, 'd')
print(names)
```

    ['a', 'b']
    ['a', 'b', 'c']
    ['a', 'd', 'b', 'c']


`tuple`是另一种有序列表，可以理解为初始化后不可修改的`list`


```python
t0 = (1, 2)
t_empty = ()
# if tuple only contains one element, use ','
t1 = (1)
t2 = (1,)
print(t0)
print(t_empty)
print(t1)
print(t2)
```

    (1, 2)
    ()
    1
    (1,)


条件判断和循环，注意python用缩进确定代码块的规定


```python
age = 20
if age > 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```

    adult



```python
sum1 = 0
for i in range(100):
    sum1 = sum1 + i
print(sum1)

sum2 = 0
n = 99
while n > 0:
    sum2 = sum2 + n
    n = n - 1
    if n == 50:
        break
print(sum2)
```

    4950
    3675


Python中内置对dict的支持，dict在其他语言中一般称作map，使用key-value键值对存储，dict中的key必须是不可变对象。
用`in`判断一个key是否在dict中
用`get(key)`方法获得某key对应的value
用`pop(key)`方法删除一个key及其对应的value
用赋值的方法直接将key-value对放入dict


```python
d = {'Micheal': 95, 'Bob': 75, 'Tracy': 85}
print(d['Micheal'])
if 'Micheal' in d:
    print(True)
print(d.get('Bob'))
d['Fancy'] = 100
print(d)
```

    95
    True
    75
    {'Micheal': 95, 'Bob': 75, 'Tracy': 85, 'Fancy': 100}


Python中的函数可以在交互式命令行中通过`help(function_name)`查看用法
调用函数和C/C++中无异，注意一些常见的数据类型转换函数


```python
print(int('123'))
print(str(1.23))
print(bool(1))
print(bool(''))
```

    123
    1.23
    True
    False


Python中使用`def`语句定义函数，返回值用`return`语句返回。
假设如下例定义了一个函数，如果该函数保存为了一个func.py文件，在另一个.py文件中要调用my_function函数则需要语句`from func import my_function`来导入`my_function()`函数。
空函数可以用pass语句，pass可以用作占位符，在没想好怎么写函数代码时可以先放一个pass让代码跑起来。


```python
def my_function(x):
    if (x >= 0):
        return True
    else:
        return False
my_function(1)
```




    True



Python的函数返回值是有多个的情况下实际上是返回了一个tuple，而多个变量可以同时接收一个tuple，按位置赋对应的值，写起来很方便。


```python
import math

def move(x, y, step, angle = 0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

x, y = move(100, 100, 60, math.pi/6)
print(x, y)
r = move(100, 100, 60, math.pi/6)
print(r)
```

    151.96152422706632 70.0
    (151.96152422706632, 70.0)


定义函数参数时记住一点：默认参数必须指向不变对象。
可变参数定义时使用`def my_function(*numbers)`语句，在函数内部，参数numbers接收到的是一个tuple，同样，再调用时使用`my_function(*numbers)`将list或tuple的元素变成可变参数传进去，加*表示这个list或tuple的所有元素作为可变参数传进去。

递归函数和C/C++类似。

Python中的索引操作和Matlab类似
取一个list或tuple中下标a到b的元素可以用`L[0:3]`，表示从索引0开始取直到索引3，但不包括索引3。如果第一个索引是0，还可以省略。
用负号表示倒数。


```python
L = list(range(50))
print(L)
print(L[0:15])
print(L[1:15])
print(L[:15])
print(L[15:])
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
    [15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49]


List Comprehensions
通过列表生成式可以写出非常简洁的代码，在列表后用for和if高效地生成列表。
需要注意的是，跟在for之后的if是一个筛选条件，不能带else
在for之前的if则是一个判断条件，需要加上else以计算出一个结果


```python
print([x * x for x in range(1, 11)])
print([x * x for x in range(1, 11) if x % 2 == 1])
```

    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    [1, 9, 25, 49, 81]


generator，Python中一种一边循环一遍计算的机制，与列表生成器类似，但是不必创建完整的list，从而节约了内存。
有两种方法创建一个generator：
1. 把一个列表生成式的`[]`改为`()`
2. 函数实现


```python
# 创建了一个generator后，基本上永远不会调用next()，而是通过for循环来迭代
g = (x * x for x in range(10))
print(g)
for n in g:
    print(n)
```

    <generator object <genexpr> at 0x7fb88b6ed7b0>
    0
    1
    4
    9
    16
    25
    36
    49
    64
    81



```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        print(b)
        a, b, = b, a + b
        n = n + 1
    return 'done'
print(fib(6))
```

    1
    1
    2
    3
    5
    8
    done


该函数描述了斐波拉契数列的推算规则，要将fib函数变成generator，只需要把`print (b)`改成`yield b`就可以了。
此时fib不是普通函数而是generator。在执行过程中遇到`yield`就中断，下次又从该处继续执行。同样地，把函数改成generator后，我们基本上从来不会用next()来获取下一个返回值，而是直接使用for循环来迭代。


```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b, = b, a + b
        n = n + 1
    return 'done'

for n in fib(6):
    print(n)
```

    1
    1
    2
    3
    5
    8


可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`
可以用`isinstance()`判断一个对象是否为`Iterator`对象
生成器都是`Iterator`对象，但`list`, `dict`, `str`虽然是`Iterable`，却不是`Iterator`，可以使用`iter()`函数将`list`, `dict`, `str`等`Iterable`变成`Iterator`
Python的`Iterator`对象表示的是一个数据流，`Iterator`对象可以被`next()`函数调用并不断返回下一个数据，直到没有数据时抛出`StopIteration`错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过`next()`函数实现按需计算下一个数据，所以`Iterator`的计算是惰性的，只有在需要返回下一个数据时它才会计算。
`Iterator`甚至可以表示一个无限大的数据流，例如全体自然数。而使用`list`是永远不可能存储全体自然数的。
Python中的`for`循环本质上就是通过不断调用`next()`函数实现的。

## 面向对象入门

面向对象中最重要的概念就是class和instance，instance是根据class创建出来的对象，每个对象拥有相同的方法，但各自的数据可能不同。
下面的例子里，括号内表示该类是从哪个类继承下来的，如果没有合适的继承类，就使用`object`类，定义好之后就可以创建实例。
由于类起到模板的作用，因此创建实例时可以通过定义一个特殊的`__init__`方法，把一些必须绑定的属性强制填写进去。
`__init__`方法的第一个参数永远是`self`，`self`指向创建的实例本身，在`__init__`内部就可以把各种属性绑定到实力本身。
定义其他的方法print_s。


```python
class Student(object):
    
    def __init__(self, name, score):
        self.name = name
        self.score = score
        
    def print_s(self):
        print('%s: %s' % (self.name, self.score))
        
bart = Student('Bart', 90)
bart.print_s()
```

    Bart: 90


如果要让内部属性不被外部访问，可以在属性名称前加两个下划线。


```python
class Student1(object):
    
    def __init__(self, name, score):
        self.__name = name
        self.__score = score

alan = Student1('alan', 60)
alan.__name
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-12-e8a3e1805d04> in <module>
          6 
          7 alan = Student1('alan', 60)
    ----> 8 alan.__name
    

    AttributeError: 'Student1' object has no attribute '__name'


如果外部代码一定要获取不被外部访问的属性，可以增加一个`get_name`和`get_score`这样的方法。
有些时候，你会看到以一个下划线开头的实例变量名，比如`_name`，这样的实例变量外部是可以访问的，但是，按照约定俗成的规定，当你看到这样的变量时，意思就是，“虽然我可以被访问，但是，请把我视为私有变量，不要随意访问”。

继承的概念不算复杂，主要就是子类自动拥有父类的方法，并且继承有一个最大的好处就是多态。要判断class的类型，可以使用`isinstance()`方法。


```python
isinstance(bart, Student)
```




    True


