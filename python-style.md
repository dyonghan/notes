# python风格

## 命名规范

The following naming styles are commonly distinguished: 

b (single lowercase letter)
B (single uppercase letter)
lowercase
lower_case_with_underscores
UPPERCASE
UPPER_CASE_WITH_UNDERSCORES
CapitalizedWords (or CapWords, or CamelCase -- so named because of the bumpy look of its letters [3] ). This is also sometimes known as StudlyCaps.
    Note: When using abbreviations in CapWords, capitalize all the letters of the abbreviation. Thus HTTPServerError is better than HttpServerError.
mixedCase (differs from CapitalizedWords by initial lowercase character!)

1. 模块名： 
    `lowercase / lower_case_with_underscores`，小写字母，单词之间用_分割. 如`ad_stats.py`
2. 包名： 
    `lowercase`，尽量不要使用_，部分系统不支持。就是文件夹名。
3. 类名： 
    `CapitalizedWords`，单词首字母大写。部分异常名和内建变量名也采用CapWords。如`AdStats`, `ConfigUtil`
4.异常名
    异常也是类，同类名。如果是错误，用“Error”后缀
5. 全局变量名： 
    `lowercase` / `lower_case_with_underscores`，类似函数的命名规范, 建议指模块内部使用的全局变量。可以通过`from M import *`调用，通过`__all__`机制限制调用。
6. 函数名：
    `lowercase` / `lower_case_with_underscores`，`mixedCase`仅在先前代码中这种风格占据优势的情况下使用，以保持向后兼容。如`get_name()`
7. 函数和方法参数
    Always use `self` for the first argument to instance methods. Always use `cls` for the first argument to class methods.
8. 方法名和实例变量
    `lowercase` / `lower_case_with_underscores`，类似函数的命名规范。可以采用`_`前缀标志内部使用。采用命名重整规则来避免和子类的命名冲突。
9. 常量
    `UPPERCASE` / `UPPER_CASE_WITH_UNDERSCORES`，用于模块水平。
10. 继承的设计 
    始终要确定一个类中的方法和实例变量是否要被公开. 通常, 永远不要将数据变量公开, 除非你实现的本质上只是记录. 人们总是更喜欢给类提供一个函数的接口作为替换 (Python 2.2 的一些开发者在这点上做得非常漂亮). 

    同样, 确定你的属性是否应为私有的. 私有与非公有的区别在于: 前者永远不会被用在一个派生类中, 而后者可能会. 是的, 你应该在大脑中就用继承设计好了你的类. 私有属性必须有两个前导下划线, 无后置下划线. 非公有属性必须有一个前导下划线, 无后置下划线. 

    公共属性没有前导和后置下划线, 除非它们与保留字冲突, 在此情况下, 单个后置下划线比前置或混乱的拼写要好, 例如: `class_`优于`klass`. 最后一点有些争议; 如果相比class_你更喜欢klass, 那么这只是一致性问题.

    > **注意**: 'cls' is the preferred spelling for any variable or argument which is known to be a class, especially the first argument to a class method.

另外，以下特殊形式可以和以上任何情况结合使用：

1. 弱“内部使用”标志 / 非公有属性： 
    以`_`开头，`from M import *`不会导入以下划线开头的对象/方法/实例变量，但是子类可以使用。如`_get_price()`, `_instance_var`
2. 类私有属性 / 方法： 
    以`__`开头（2个下划线），外部调用采用命名重整规则即, inside class `FooBar`,`__boo` becomes `_FooBar__boo`。一般情况下仅用于当属性可被子类继承时，避免与子类的命名冲突。如`__private_var`, `__get_name()`
3. 魔法对象或属性： 
    `__`开头，`__`结尾，一般为python的自有变量，不要以这种方式命名. 如`__doc__`, `__class__`
4. 下划线`_`后缀：
    和保留字冲突的时候使用
5. `__all__`机制

    ```python
    __all__=["fun","class"]
    ```

    `__all__`可用于模块导入时限制，如：`from module import *`，此时被导入模块若定义了`__all__`属性，则只有`__all__`内指定的属性、方法、类可被导入。若没定义，则模块内的所有非私有方法/属性/类将被导入。

## 术语

类的方法和实例变量统称为属性，a class's methods and instance variables (collectively: "attributes")。

python包含packages, modules, classes, functions, attributes等
