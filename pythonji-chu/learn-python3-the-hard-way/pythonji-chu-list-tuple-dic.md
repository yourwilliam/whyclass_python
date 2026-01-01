# Python基础List,Tuple,Dic

## Python基础——list,tuple,dic

Python中的list/tuple/dict/set数据类型详解 Python内部内置了一些数据类型与结构，可以方便在编程时候的使用。

### list

List存储一系列的有序集合，并且元素内容可变（可更改、删除、添加）。

```python
> > > fruits=['apple','orange','pear','banana']
> > > fruits[0]
> > > 'apple'
> > > fruits[-1]
> > > 'banana'
```

由上可知可以使用下标进行list元素的索引，正数下标为正向索引，负数下标为反向索引，fruits\[-1]就是倒数第一个元素。并且可以使用+操作符进行list列表的串接。

```python
> > > otherFruits=['kiwi','strawberry']
> > > fruits+otherFruits
> > > ['apple', 'orange', 'pear', 'banana', 'kiwi', 'strawberry']
```

由于list是一个可变的有序列表，所以可以向其中添加、删除、更改元素。

```
> > > fruits.pop()        //删除末尾的元素
> > > 'banana'
> > > fruits                //banana已经被删除
> > > ['apple', 'orange', 'pear']
> > > fruits.append('grapefruit')    //向列表末尾增添元素
> > > fruits
> > > ['apple', 'orange', 'pear', 'grapefruit']
> > > fruits[-1]='pineapple'           //更改列表中的某一个值
> > > fruits
> > > ['apple', 'orange', 'pear', 'pineapple']
> > > fruits.insert(2,'watermelon')   //向列表中第二个元素位置插入一个元素
> > > fruits
> > > ['apple', 'orange', 'watermelon', 'pear', 'pineapple']
> > > fruits.pop(2)         //删除指定位置的元素，用pop(i)
> > > 'watermelon'
> > > fruits
> > > ['apple', 'orange', 'pear', 'pineapple']
```

也可以利用切片操作符列出相邻的元素，fruits\[start:stop]或者fruits\[:stop]或者fruits\[start:]这三种形式。 欲获得更多有关list的信息，可以使用帮助文件。

```python
> > > dir(list)
> > > ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__delslice__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getslice__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__setslice__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
> > > help(list.reverse)
> > > Help on method_descriptor:


reverse(...)
    L.reverse() -- reverse *IN PLACE*
```

### tuple

另一个与list很像的数据类型是tuple，除了它一旦被创建就是不可更改的。注意tuple在创建时使用圆括号，而list在创建时使用的是方括号。 一旦tuple被创建，我们可以使用fruits\[0]，fruits\[-1]去正常的索引元素，但是不能更改元素。不可变的tuple有什么意义？因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple。

```python
> > > fruits=('apple','pear','grape')
> > > fruits[0]
> > > 'apple'
> > > fruits[-1]
> > > 'grape'
> > > fruits[0]='pineapple'
> > > Traceback (most recent call last):
> > >   File "<stdin>", line 1, in <module>
> > > TypeError: 'tuple' object does not support item assignment
> > > a,b,c=fruits
> > > a
> > > 'apple'
> > > b
> > > 'pear'
> > > c
> > > 'grape'
```

注意：只有1个元素的tuple定义时必须加一个逗号，来消除歧义。因为()不仅用来表示tuple数据结构，还可以用来数学中的公式。这就产生了歧义，因此，Python规定，在t(1)这种情况下，按小括号进行计算，计算结果自然是1。

```python
> > > t=(1,)
> > > t
> > > (1,)
```

最后看一个“可变的”tuple：

···py

> > > t = ('a', 'b', \['A', 'B']) t\[2]\[0] = 'X' t\[2]\[1] = 'Y' t ('a', 'b', \['X', 'Y']) \`\`\`

表面上看，tuple的元素确实变了，但其实变的不是tuple的元素，而是list的元素。tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。

### dict

Dictionary存储了从一种对象（key）到另一种对象（value）的映射关系，key必须是不可变的对象（字符串、数字或者tuple），而value对象则是可变的任意数据类型。Dict的创建采用花括号。 注意：dict中的key的顺序不是固定的，即没有确定的元素顺序，编程的时候也不应该依赖于dict中的元素顺序。

```python
> > > studentsIds={'kuth':90,'turing':99,'nash':80}             
> > > studentsIds['turing']
> > > 99
> > > studentsIds['nash']=60   //更改元素的value值
> > > studentsIds
> > > {'turing': 99, 'nash': 60, 'kuth': 90}
> > > del studentsIds['turing']   //删除某个指定元素
> > > studentsIds
> > > {'nash': 60, 'kuth': 90}
> > > studentsIds['bug']=['time',90,(1,2)]   //添加某个元素，注意元素的value可以为任意数据类型
> > > studentsIds
> > > {'nash': 60, 'kuth': 90, 'bug': ['time', 90, (1, 2)]}
> > > studentsIds.keys()     //列出dict的键值
> > > ['nash', 'kuth', 'bug']
> > > studentsIds.values()  //列出dict的元素的值
> > > [60, 90, ['time', 90, (1, 2)]]
> > > studentsIds.items()   //列出dict的所有条目
> > > [('nash', 60), ('kuth', 90), ('bug', ['time', 90, (1, 2)])]
> > > len(studentsIds)        //显示dict的长度，都可以使用len函数来确定
> > > 3
```

在进行dict操作的时候，为避免key不存在而造成的错误，可以使用以下两个方法：

* 通过in来判断key是否存在：

```python
> > > 'nash' in studentsIds
> > > True
> > > 'tom' in studentsIds
> > > False
```

通过dict提供的get方法，如果key不存在，可以返回None，或者自己指定的value：

```python
> > > studentsIds.get('nash')     //存在，则返回key对应的value
> > > 60
> > > studentsIds.get('nash',-1)
> > > 60
> > > studentsIds.get('tom',-1)  //不存在，则返回自定义的-1或者none（什么也不返回）
> > > -1
> > > studentsIds.get('tom')
```

和list比较，dict有以下几个特点：

* 查找和插入的速度极快，不会随着key的增加而增加；
* 需要占用大量的内存，内存浪费多。

而list相反：

* 查找和插入的时间随着元素的增加而增加；
* 占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。 dict可以用在需要高速查找的很多地方，在Python代码中几乎无处不在，正确使用dict非常重要，需要牢记的第一条就是dict的key必须是不可变对象。这是因为dict根据key来计算value的存储位置，如果每次计算相同的key得出的结果不同，那dict内部就完全混乱了。这个通过key计算位置的算法称为哈希算法（Hash）。要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key。 可以使用dir(dict)和help(dict.xxx)来显示更详细的帮助信息。

### set

set是另一种包含无序不重复元素的数据结构，就如同dict中的key一样，只不过其相对于dict只有key，而没有与key相对应的value。 因此set中的元素和dict中的key一样，只能是string，number和tuple等不可变的元素，而不能是list。 在创建set的时候，需要提供一个list作为输入。

```python
> > > shapes=['circle','triangle','rectangle','circle']
> > > setOfShapes=set(shapes)      //以list作为输入创建一个set
> > > setOfShapes
> > > set(['circle', 'triangle', 'rectangle'])   //发现list中重复的元素已经被去除
> > > setOfShapes.add('polygon')   //添加元素
> > > setOfShapes
> > > set(['circle', 'triangle', 'polygon', 'rectangle'])
> > > 'circle' in setOfShapes          //判断元素是否在set中
> > > True
> > > 'rhombus' in setOfShapes
> > > False
> > > favoriteShapes=['circle','triangle','hexagon']
> > > setOfFavoriteShapes=set(favoriteShapes)
> > > setOfShapes-setOfFavoriteShapes     //set由于是可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作
> > > set(['polygon', 'rectangle'])
> > > setOfShapes&setOfFavoriteShapes
> > > set(['circle', 'triangle'])
> > > setOfShapes|setOfFavoriteShapes
> > > set(['triangle', 'polygon', 'circle', 'hexagon', 'rectangle'])
```

再议不可变对象

str是不变对象，而list是可变对象。对于可变对象，比如list，对list进行操作，list内部的内容是会变化的，比如：

```python
> > > a = ['c', 'b', 'a']
> > > a.sort()
> > > a
> > > ['a', 'b', 'c']
> > > 1
> > > 2
> > > 3
> > > 4
> > > 而对于不可变对象，比如str，对str进行操作呢：

> > > a='abc'
> > > a.replace('a','A')
> > > 'Abc'
> > > a
> > > 'abc'
> > > b=a.replace('a','A')
> > > b
> > > 'Abc'
```

当我们调用a.replace('a', 'A')时，实际上调用方法replace是作用在字符串对象’abc’上的，而这个方法虽然名字叫replace，但却没有改变字符串’abc’的内容。相反，replace方法创建了一个新字符串’Abc’并返回，如果我们用变量b指向该新字符串，就容易理解了，变量a仍指向原有的字符串’abc’，但变量b却指向新字符串’Abc’了。所以，对于不变变量，调用对象的任何自身的方法，都不会更改该对象自身的内容，但这些方法会创建新的对象并返回，这就保证了不可变对象本身永远是不可变的。

## 使用详解

### 一、字典Dictionary

> 语法形式：aDict={‘a’:1, ‘b’:2, ‘c’:3, ‘d’:4, ‘e’:5} Python手册说明：[https://docs.python.org/2.7/library/stdtypes.html#dict](https://docs.python.org/2.7/library/stdtypes.html#dict)

* Dictionary是Python内置数据类型，定义了”键-值”间的一一对应关系。
* 每个元素都是key-value对，整个元素集合用**大括号**扩起来。
* 可通过key获取对应值，但不能根据value获取key。
* **key不能相同**，相同key则将覆盖就值。
* key大小写敏感，value可支持任意数据类型（字符串、整数、对象或其他Dictionary）。
* del可通过key删除字典中特定元素`del dict[k]`。
* clear将清空字典中所有元素，空的大括号表示没有元素的字典。

### 二、列表List

> 语法形式：aList=\[1,2,3,4,5]

* List中元素是可变的。
* List是使用**中括号**括起来的有序元素集合。
* List列表索引从0开始。
* 负数索引表示从List的尾部开始向前存取元素，list\[-1]表示最后一个元素，可以理解list\[-n]=list\[len(list)-n]
* List\[m:n]表示List中m<=k\<n的子集，被称为slice，详见[手册](https://docs.python.org/2.7/library/stdtypes.html#typesseq)。
* List\[:]返回与List中元素相同的一个新list，List\[1:]取1-len(List)中所有元素
* List列表方法：insert()插入新的元素，append()在尾部追加新元素、列表，extend()将一个列表扩展到原列表中,index()返回首个出现的元素索引，k in list返回是否存在
* List可通过+连接两个列表，等价于list.extend(anotherList)。
* List中**元素可以相同**。

### 三、元组Tuple

> 语法形式：aTuple=(1,2,3,4,5)

* Tuple元组是不可变的List，不能改变元组中的元素值。
* 创建Tuple的形式与List相同，区别在于将\[]换为()。
* Tuple元组没有append、extend、remove、pop、index等方法，但可使用in判断元素是否存在。
* 空元组可以用()表示，但只有一个元素的元组为避免歧义应当使用(n,)表示，而避免只用(n)的形式，Python可能误解为加了小括号的数字n。
* 列表和元组的相互转化：`atuple=tuple(alist)`和`alist=list(atuple)`
* 无关闭分隔符：任何以逗号分隔的无符号对象都认为是元组，如`x,y = 1,2`则`print "Value of x,y:", x, y`
* Tuple好处：速度比List快，代码安全。

Python元组包含了以下内置函数:

```
1. cmp(tuple1, tuple2)：比较两个元组元素。
2. len(tuple)：计算元组元素个数。
3. max(tuple)：返回元组中元素最大值。
4. min(tuple)：返回元组中元素最小值。
5. tuple(seq)：将列表转换为元组。
```

## **list**

1.list可以放进tuple (易知）

2.list可以放入dict作为value，但不可以作为key

```
>>> key = [1, 2, 3]
>>> d[key] = 'a list'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

3.list不可以放入set，如：

```
>>> l = [1,2,3]
>>> s = set([2,3,4])
>>> s.add(l)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

但是可以用为输入集合如:

```
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```

4.list可以放入list（易知）

## tuple

1.tuple可以放入list （易知）

2.tuple可以放入dict作为key，同时可以作为value（只有不含list，tuple，set，dict的tuple可以当为key）

```
>>> t = (1,2,3)
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d[t] = 90
>>> d
{'Tracy': 85, 'Bob': 75, 'Michael': 95, (1, 2, 3): 90}
```

3.tuple可以放入set （只有不含list，tuple，set，dict的tuple可以放进set）

```
>>> c = (1,[2,3])
>>> s = set([2,3,4])

>>> s.add(c)

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

4.tuple可以放入tuple（易知）

## **dict**

1.dict可以放入tuple

```
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> t = (1,2,d)
>>> t
(1, 2, {'Tracy': 85, 'Bob': 75, 'Michael': 95})
```

2.dict可以放入list

```
>>> d = {'Michael': 95, 'Bob': 75}
>>> l =[1,2,d]
>>> l
[1, 2, {'Bob': 75, 'Michael': 95}]
```

3.dict不可放入set

```
>>> d = {'Michael': 95, 'Bob': 75}
>>> s = set([1,2,3])
>>> s.add(d)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'dict'
```

4.dict可以放入dict作为value，但不可以作为key

```
>>> d = {'Michael': 95, 'Bob': 75}
>>> di = {'chael': 45, 'ob': 5}
>>> di['chael'] = d
>>> di
{'chael': {'Bob': 75, 'Michael': 95}, 'ob': 5}
>>> di[d] = 40
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'dict'
```

## **set**

1.set可以放入tuple

```
>>> s = set([1,2,3])
>>> t = (3,4,s)
>>> t
(3, 4, {1, 2, 3})
```

2.set可以放入list(易知)

3.set可以放入dict作为value，但不可以作为key

```
>>> s = set([1,2,3])
>>> di = {'chael': 45, 'ob': 5}
>>> di[s] = 67
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'set'
```

4.set不可以放入set

```
>>> s = set([1,2,3])
>>> s1 = set([5,6])
>>> s.add(s1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'set'
```

## conclusion

总结一下：

1.list可存放：tuple、dict、set、list

2.tuple可存放：list、dict、set、tuple

3.set可存放：tuple (不含list，tuple，set，dict的tuple)

4.dict的key可存放：tuple (不含list，tuple，set，dict的tuple)

5.dict的value可存放：list、tuple、set、dict

## 几个概念

*   **tuple的“不变”**

    看一个“可变的”tuple：

    ```
    >>> t = ('a', 'b', ['A', 'B'])
    >>> t[2][0] = 'X'
    >>> t[2][1] = 'Y'
    >>> t
    ('a', 'b', ['X', 'Y'])
    ```

    这个tuple定义的时候有3个元素，分别是`'a'`，`'b'`和一个list。不是说tuple一旦定义后就不可变了吗？怎么后来又变了？

    我们先看看定义的时候tuple包含的3个元素：

    ![tuple-0](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Le53R7Ru_ySSwFmZyv0%2Fuploads%2FXGoSICM0vrXBTQQ4QMR2%2Ffile.png?alt=media)

    当我们把list的元素`'A'`和`'B'`修改为`'X'`和`'Y'`后，tuple变为：

    ![tuple-1](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-Le53R7Ru_ySSwFmZyv0%2Fuploads%2FNTLhEr2vUilyqvSTd7Ru%2Ffile.png?alt=media)

    表面上看，tuple的元素确实变了，但其实变的不是tuple的元素，而是list的元素。tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向`'a'`，就不能改成指向`'b'`，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！

    理解了“指向不变”后，要创建一个内容也不变的tuple怎么做？那就必须保证tuple的每一个元素本身也不能变
*   **不可变对象**

    str是不变对象，而list是可变对象。要记住：**dict和set中的key都是不可变对象！**

    对于可变对象，比如list，对list进行操作，list内部的内容是会变化的，比如：

    ```
    >>> a = ['c', 'b', 'a']
    >>> a.sort()
    >>> a
    ['a', 'b', 'c']
    ```

    而对于不可变对象，比如str，对str进行操作呢：

    ```
    >>> a = 'abc'
    >>> a.replace('a', 'A')
    'Abc'
    >>> a
    'abc'
    ```

    虽然字符串有个`replace()`方法，也确实变出了`'Abc'`，但变量`a`最后仍是`'abc'`，应该怎么理解呢？

    我们先把代码改成下面这样：

    ```
    >>> a = 'abc'
    >>> b = a.replace('a', 'A')
    >>> b
    'Abc'
    >>> a
    'abc'
    ```

    要始终牢记的是，`a`是变量，而`'abc'`才是字符串对象！有些时候，我们经常说，对象`a`的内容是`'abc'`，但其实是指，`a`本身是一个变量，它指向的对象的内容才是`'abc'`：

    ```
    ┌───┐                  ┌───────┐
    │ a │─────────────────>│ 'abc' │
    └───┘                  └───────┘
    ```

    当我们调用`a.replace('a', 'A')`时，实际上调用方法`replace`是作用在字符串对象`'abc'`上的，而这个方法虽然名字叫`replace`，但却没有改变字符串`'abc'`的内容。相反，`replace`方法创建了一个新字符串`'Abc'`并返回，如果我们用变量`b`指向该新字符串，就容易理解了，变量`a`仍指向原有的字符串`'abc'`，但变量`b`却指向新字符串`'Abc'`了：

    ```
    ┌───┐                  ┌───────┐
    │ a │─────────────────>│ 'abc' │
    └───┘                  └───────┘
    ┌───┐                  ┌───────┐
    │ b │─────────────────>│ 'Abc' │
    └───┘                  └───────┘
    ```

    所以，对于不变对象来说，调用对象自身的任意方法，也不会改变该对象自身的内容。相反，这些方法会创建新的对象并返回，这样，就保证了不可变对象本身永远是不可变的。
