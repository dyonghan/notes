# python高级特性

## iteration迭代

对list,tuple的遍历被称为迭代。对list实现类似Java那样的下标循环怎么办？Python内置的enumerate函数可以把一个list变成索引-元素对

```
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
```

### iterator迭代器

凡是可作用于for循环的对象都是**Iterable**类型；凡是可作用于`next()`函数的对象都是**Iterator**类型，它们表示一个惰性计算的序列。集合数据类型如`list`、`dict`、`str`等是Iterable但不是Iterator，不过可以通过`iter()`函数获得一个Iterator对象。

```
>>> isinstance(iter([]), Iterator)
True
```

Python的`for`循环本质上就是通过不断调用`next()`函数实现的。循环有`for in`和`while`，迭代只能用`for in`。

受到内存限制，列表容量肯定是有限的。generator生成器，属于iterator。生成方法：

```
g = (x * x for x in range(10))
```

函数定义中包含`yield`关键字, 用`next(g)`或`for n in g`获取值。想要拿到返回值，必须捕获`StopIteration`错误，返回值包含在`StopIteration`的`e.value`中。

## python并发

python multiprocessing模块封装了多进程和多线程，其中multiprocessing.Pool对应多进程，multiprocessing.dummy.Pool对应多线程。两者用法一致，以下是多线程的用法：

```python
from multiprocessing.dummy import Pool

pool=Pool(count)
for i in range(count):
    pool.apply_async(func, args=tuble
pool.close()
pool.join()
```

或

```python
from multiprocessing.dummy import Pool

pool = Pool(count)
pool.map(func, Iterable)
```

## 异常

```python
unable to find vcvarsall.bat
```

解决办法参考：

[http://www.cnblogs.com/youxin/p/3159363.html](http://www.cnblogs.com/youxin/p/3159363.html)
[http://blog.csdn.net/secretx/article/details/17472107](http://blog.csdn.net/secretx/article/details/17472107)
Microsoft Visual C++ Compiler for Python 2.7
http://aka.ms/vcpython27