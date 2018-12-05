## 第2章 Python3 的一些新特性

### 2.1 __future__ 模块 

在 python3 引入了一些 python2 没有的关键字和特性，不过如果你想要在 python2 中使用这些特性，可以使用 `__future__` 模块将这些新特性导入。

例如， 假设我们想在 python2 中使用 python3 整数除法(`integer division`)特性， 我们可以加入下面这句话就可以：

```python
from __future__ import division
```

* 注：具体如何使用，进一步研究后面

### 2.2 print 函数

在 python3 中最值得注意的变化非 `print` 函数莫属， 在 python3 中 print 函数必须带上`()`, 而 python2 中可以不用带：

```python
print "Hello World"   # 只有 python2 能够使用，python3中会报错
print("Hello World")  # python3 能够使用，python2也可以这样使用
```

`print()` 函数默认会在输出加一个换行， 在 python2 里面，我们可以在输出的内容后面加一个 `,` 来避免这个默认的换行输出，而在 python3 中，我们可以给 print 函数传一个 `end=' '` 来将默认的换行替换成空格或者其他字符，比如替换成 `a` 就传 `end = 'a'` 参数：

```python
print "Hello World",           # python2 输出取消换行的方法
print("Hello World", end=" ")  # python3 输出取消换行的方法
``` 

### 2.3 键盘读入数据

在 python2 中，有两个函数可以用于从键盘读取数据， 分别是 `input()` 和 `raw_input()`。 对于 input() 函数, 如果输入的数据首末中没有 `' '` 或者 `" "`, 那么输入的数据将会被当成数字进行处理，如果无法解析成数字就会报错。如果有 `' '` 或者 `" "`, 则回当成字符串处理。而 `raw_input()` 函数则把所有的输入都认为是字符串。

```bash
Python 2.7.15rc1 (default, Nov 12 2018, 14:31:15)
[GCC 7.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.

>>> a = input('>> ')
>> 10
>>> a
10

>>> a = input('>> ')
>> 0x10
>>> a
16

>>> a = input('>> ')
>> ddd
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<string>", line 1, in <module>
NameError: name 'ddd' is not defined
>>>

>>> a = raw_input('>> ')
>> ssss
>>> a
'ssss'

>>> a = raw_input('>> ')
>> 'ssss'
>>> a
"'ssss'"
>>>
```

在 python3 中，`raw_input()` 函数被移除， 只留下 `input()` 函数，不过，所有的输入都被当成字符串识别。如果强行使用 `raw_input()` 则会报错。

```bash
Python 3.6.5 (default, Apr  1 2018, 05:46:30)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> a = input('>> ')
>> 10
>>> a
'10'
>>> a = input('>> ')
>> aaa
>>> a
'aaa'
>>> a = input('>> ')
>> "lll"
>>> a
'"lll"'
>>> a = raw_input('>> ')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'raw_input' is not defined
```

### 2.4 整数除法(Integer Division)

在 python2 中， 两个整数相除的结果是商向下取整，比如 `3/2 = 1`, 如果要想得到浮点除法的话，除数或者被除数必须至少有一个是浮点数， 即 `3.0/2` 或者 `3/2.0` 或者 `3.0/2.0` 的商是1.5， 也就是说在 python2 中整数除和浮点除是分开的。

但是在 python3 中，除法一律使用**浮点除**，即 `3/2 = 1.5`, 这对编程新手更加直观，因为不需要去记忆更多的东西:

```bash
$ python2
Python 2.7.15rc1 (default, Nov 12 2018, 14:31:15)
[GCC 7.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 3/2
1
>>> 3.0/2
1.5

$ python3
Python 3.6.5 (default, Apr  1 2018, 05:46:30)
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 3/2
1.5
>>> 3.0/2
1.5
```

### 2.5 Unicode 表示

在 python2 中，如果要对一个字符串存储成 unicode 编码，需要在前面加一个 u, 例如:

```python
s = u'hello world'
```

但是在 python3 中， 字符串默认被存储为 Unicode(utf-8) 字符串，这样的好处就是即便是中文，也能够正常表示，不会出错。以前在 python2 中，一不注意中文进去没进行编码就有可能报错， 这个在 python3 中就能够避免了。

### 2.6 移除 xrange() 函数

In Python 2 range() returns a list, and xrange() returns an object that will only generate the items in the range when needed, saving memory.

In Python 3, the range() function is removed, and xrange() has been renamed as range(). In addition, the range() object supports slicing in Python 3.2 and later.

### 2.7 raise exception

Python 2 accepts both notations, the 'old' and the 'new' syntax; Python 3 raises a SyntaxError if we do not enclose the exception argument in parenthesis.

```
raise IOError, "file error" #This is accepted in Python 2
raise IOError("file error") #This is also accepted in Python 2
raise IOError, "file error" #syntax error is raised in Python 3
raise IOError("file error") #this is the recommended syntax in Python 3
```

### 2.8 异常(Exceptions) 参数的改变

In Python 3, arguments to exception should be declared with 'as' keyword.

```
except Myerror, err: # In Python2
except Myerror as err: #In Python 3
```

### 2.9 next() 函数和 .next() 方法

In Python 2, next() as a method of generator object, is allowed. In Python 2, the next() function, to iterate over generator object, is also accepted. In Python 3, however, next(0 as a generator method is discontinued and raises AttributeError.

```
gen = (letter for letter in 'Hello World') # creates generator object
next(my_generator) #allowed in Python 2 and Python 3
my_generator.next() #allowed in Python 2. raises AttributeError in Python 3
```

### 2.10 2to3 特殊功能

在 python3 中有一个工具可以将 python2 的代码转换成 python3 的代码，这个工具叫做 `2to3.py`, 是 python3 自带的，通常安装在 `tools/scripts` 目录下.

```
Here is a sample Python 2 code (area.py):

def area(x,y = 3.14): 
   a = y*x*x
   print a
   return a

a = area(10)
print "area",a

To convert into Python 3 version:

$2to3 -w area.py

Converted code :

def area(x,y = 3.14): # formal parameters
   a = y*x*x
   print (a)
   return a

a = area(10)
print("area",a)

```
