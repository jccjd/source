---
date: 2019-9-22
tags:
- Python
categories:
- Python
---
#### python的函数参数传递

python的所有变量都可以理解是内存中一个对象的“引用”,类型是属于对象的，而不是变量。对象有两种，“可更改与不可更改。在python中，string,tuples,和numbers是不可更改的对象，而list，dict，set等则是可以修改的对象。
#### python的标准数据类型
```python
numbers(int long float complex)
string
List
Tuple
Dictionary
```
##### string
   重点是对string的切片

    从左到右0 - n：0,1,2,3....
    从右到左-n - -1:-n,...-3,-2, -1
    切片时要头下标和尾下标和步长
##### list
可以存放更多的数据类型，切片方式和string类似

```python
list = [ 'runoob', 786 , 2.23, 'john', 70.2 ]
tinylist = [123, 'john']
print list               # 输出完整列表
print list[0]            # 输出列表的第一个元素
print list[1:3]          # 输出第二个至第三个元素
print list[2:]           # 输出从第三个开始至列表末尾的所有元素
print tinylist * 2       # 输出列表两次
print list + tinylist    # 打印组合的列表
```
#### python元类（metaclass)
用于orm的单例模式，对数据库对象实现保护，确保全局只有一个数据库对象
metaclass，直译为元类，简单的解释就是：

当我们定义了类以后，就可以根据这个类创建出实例，所以：先定义类，然后创建实例。
但是如果我们想创建出类呢？那就必须根据metaclass创建出类，所以：先定义metaclass，然后创建类。

连接起来就是：先定义metaclass，就可以创建6类，最后创建实例。
所以，metaclass允许你创建类或者修改类。换句话说，你可以把类看成是metaclass创建出来的“实例”。
#### @staticmethod，和@classmethod
python有三种方法即静态方法(staticmethod)，类方法(classmethod)和实例方法

```python
def foo(x):
print("executing foo(%s)"%(1))
class A(object):
    def foo(self,x):
        print("executing foo(%s,%s)"%(self,x))
    @classmethod
    def class_foo(cls,x):
        print("executing class_foo(%s,%s)"%(cls,x))
    @staticmethod
    def static_foo(x):
        print("executing static_foo(%s)"%x)
```

#### 类变量和实例变量
##### 类变量：
    是可以在类的所有实例之间共享的值（也就是说，它们不是单独分配给每个实例的）
##### 实例变量：
    实例化之后，每个实例单独拥有的变量。
##### python自省
自省就是面向对象的语言所写的程序在运行时，所能知道对象的类型，简单一句就是运行时能够获得对象的类型，比如type(),dir(),getattr(),hasattr(),isinstance()

#### python中的单下划线和双下划线
__function__:一种约定，python内部的名字，用来区别其他用户自定义的命名，以防止冲突，如__init__,__del__,等python内置函数

_foo:一种约定用来指定变量私有，程序员用来指定私有变量的一种方式，不能用from module import * 导入

__foo:解释器用_classname__foo来代替这个名字，以区别和其他类相同的命名，它无法直接像公有成员一样随便访问，通过对象名，类名__xx来访问

#### 迭代器和生成器
将列表生成式中[]改成()之后数据结构将改变，从列表变为生成器

列表的容量是有限的，而且，创建一个包含百万元素的列表，不仅是占用很大内存空间的，

在python中我们可以采用生成器：边循环，边计算的机制
#### *args and **kwargs
当你不确定你的函数里将要传递多少参数时你可以用*args，它可以传递任意数量的参数

```python
     def print_everything(*args):
        for count, thing in enumerate(args):
                 print '{0}. {1}'.format(count, thing)
    print_everything('apple', 'banana', 'cabbage')
    0. apple
    1. banana
    2. cabbage
```
**kwargs允许你使用没有事先定义的参数名：

```python
     def print_everything(**kwargs):
        for count, thing in kwargs(args):
                 print '{0}. {1}'.format(count, thing)
    print_everything(apple = 'fruit', cabbage = 'vegetable')
    cabbage = vegetable
    apple = fruit
```
也可以混合使用，在使用时*args 和**kwargs必须是有顺序的
#### 鸭子类型
#### python中的重载
函数重载主要是为了解决两个问题
- 1.可变参数类型
- 2.可变参数个数

一个基本的设计原则是，仅仅当两个函数除了参数类型和参数个数不同以外，其功能是完全相同的，此时才使用函数重载
，如果两个函数的功能其实不同，那么不应当使用重载，而应当使用一个名字不同的函数

python可以接受任何类型的参数，如果函数的功能相同，那么不同的参数类型在python中很可能是相同的代码，没有必要做成两个函数

如果参数个数不同，python中的缺省参数，对于那些缺少的参数设定为缺省参数，

所以python是不需要重载的

#### python中的作用域
python中，一个变量的作用域总是由在代码中被赋值的地方所决定的

当python遇到一个变量的话他会按照这样的顺序进行搜索

本地作用域（local）- 当前作用域被嵌入的本地作用域（Enlosing)-全模块/全局作用域-内置作用域（built-in)

#### GIL线程全局锁
线程全局锁（Global Interpreter Lock),即Python为了保证线程安全而采取的独立线程运行的限制，就是一个核只能在同一时间运行一个线程，

对于io密集型任务，python的多线程起到作用，但对于cpu密集型任务，Python的多线程几乎占不到任何优势，还有可能因为争夺资源而变慢

#### 协程
简单点说协程是线程和进程的升级版吗，进程和线程都面临着内核态和用户态的切换问题而耗费许多时间，而协程就是用户自己控制切换的时机

#### 闭包

闭包（closeure）是函数式编程的重要语法结构，闭包也是一种组织代码的结构，它同样提高了代码的可重复实用性。
当一个内嵌函数引用其外部作用域的变量，我们就会得到一个闭包，闭包必须满足一下几点：

    1，必须有一个内嵌函数
    2，内嵌函数必须引用外部函数中的变量
    3，外部函数的返回值必须是内嵌函
#### lambda函数
匿名函数，通常用在函数式编程中
#### Python函数式编程
Python函数式编程支持
filter函数的功能相当于过滤器。调用一个布尔函数bool_func来迭代遍历每个seq中的元素，返回一个使bool——seq返回值为true的元素的序列

map函数是对一个序列的每个项依次执行函数

reduce函数是对一个序列的每个项迭代调用函数
#### Python中的拷贝
引用和copy(),deepcopy()的区别
#### python垃圾回收机制
python GC 主要使用引用计数（reference counting) 来跟踪和回收垃圾。在引用计数的基础上，通过“标记-清除”（mark and sweep) 解决容器对象可能产生的循环引用问题，通过“分带回收（generation collection)以空间换时间提高垃圾回收效率
##### 引用计数
pyObject是每个对象必有的内容，其中ob_refcnt就是作为引用计数。当一个对象有新的引用时，它的ob_refcnt就会增加，当引用它的对象被删除，
它的ob_refcnt就会减少，引用计数为0时，该对象生命就结束了
##### 标记清除机制
基本思路是先按需分配，等到没有空闲内存的时候从寄存器和程序栈上的引用出发，遍历以对象为节点，以引用为边构成图，把所有可以访问到的对象打上标记，然后清理一遍内存空间，把所有没标记的对象释放
##### 分代技术
分代回收的整体思想是：将系统中所有内存块根据其存活时间划分不同的集合，每个集合就成为一个代，垃圾回收频率随着代的存活时间的增加而减小，存活时间通常利用经过几次垃圾回收来度量

Pytho默认定义了三代对象集合，索引数越大，对象存活时间越长

当某些内存块m经过了3次垃圾收集的清洗之后还存活时，我们将内存块M划分到一个集合A中去，而新分配的内存都划分到集合B中去。当垃圾收集开始工作时，大多数情况都只对集合B进行垃圾回收，而对集合A进行垃圾回收要隔很长时间，就使得垃圾回收机制需要处理的内存少了，效率自然提高，
在这个过程中，集合B中的某些内存由于存活时间长而会被转移到集合A中，当然，集合A中实际上也存在一些垃圾，这些垃圾的回收会因为这种分代的机制而被延迟。
#### Python的list
#### Python的is
is是对比地址 ==是对比值
#### read，readline 和readlines
- read读取整个文件
- readline读取下一行,使用生成器方法
- readlines读取整个文件到一个迭代器以供我们遍历
#### Python2和Python3的区别
## range and xrange
- xrange的内存性能更好
- 都在循环中使用

当使用range时会生成一个list开辟一大块空间，而xrange则会生成一个可迭代的对象

Python3中没有xrange，range和Python2中的xrange相同
#### cls 和self

(在p2中)self 表示一个具体的实例本身.

cls表示这个类本身
類先調用__new__方法返回該類的實例對象這個實例對象就是__init__方法的第一個參數self

即self是__new__的返回值

py3中沒有區別
