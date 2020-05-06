# python基础特性

## 全局变量和局部变量

变量的作用域为变量定义所在的代码块（函数），若要在代码块内使用外部的变量，使用`global x`来声明，否则作为局部变量处理。代码块内类似`x = 1/[]/{}`的变量赋值语句都被当作变量定义，而`ls[0] = elem`或者`d['key'] = value`这种会被当作指针处理。

## list和tuple

```bash
>>> my_list = [[0] * 3] * 4
>>> my_list[0][1] = 1
>>> print my_list
[[0,1,0], [0,1,0], [0,1,0], [0,1,0]]
```
发现整个第二列都被赋值，查看python官方文档，发现`list * n—>n shallow copies of list concatenated`, `list*n`是list的n个浅拷贝的连接。`[[0] * 3] * 4`表示4个指向`[[0] * 3]`的引用，修改任何一个，都会修改4个元素。

tuple和list非常类似，均为有序列表，但是tuple一旦初始化就不能修改。不可变的tuple有什么意义？因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple。

只有1个元素的tuple定义时必须加一个逗号，来消除歧义：

```bash
>>> t = (1,)
>>> t
(1,)
```

## dict和set

dict内部存放的顺序和key放入的顺序是没有关系的。和list比较，dict有以下几个特点：

- 查找和插入的速度极快，不会随着key的增加而变慢；
- 需要占用大量的内存，内存浪费多。

而list相反：

- 查找和插入的时间随着元素的增加而增加；
- 占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。dict可以用在需要高速查找的很多地方，在Python代码中几乎无处不在，正确使用dict非常重要，需要牢记的第一条就是dict的key必须是不可变对象。
这是因为dict根据key来计算value的存储位置，如果每次计算相同的key得出的结果不同，那dict内部就完全混乱了。这个通过key计算位置的算法称为哈希算法（Hash）。
要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key。

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。


### 字符串与字典类型转换

- 字典(dict)转为字符串(string)
    我们可以比较容易的将字典(dict)类型转为字符串(string)类型。
    通过遍历dict中的所有元素就可以实现字典到字符串的转换：

    ```python
    for key, value in sample_dic.items():
       print"\"%s\":\"%s\""%(key, value)
    ```

- 字符串(string)转为字典(dict) 
    如何将一个字符串(string)转为字典(dict)呢?
    其实也很简单，只要用`eval()`或`exec()`函数就可以实现了。

    ```bash
    >>> a = "{'a': 'hi', 'b': 'there'}"
    >>> b = eval(a)
    >>> b
    {'a': 'hi', 'b': 'there'}
    >>>exec("c=" + a)
    >>> c
    {'a': 'hi', 'b': 'there'}
    >>>
    ```

### 高效合并dict

Merge two Python dictionaries
A new syntax for this, available as of Python 3.5, is

```python
z = {**x, **y}
```

In Python2

```python
z = x.copy()
z.update(y) # which returns None since it mutates z
```
