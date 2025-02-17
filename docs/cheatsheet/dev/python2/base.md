> 提示：本文档以`python2.7`版本为例

## 安装

Linux 下安装

```bash
wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tgz
tar -zxvf Python-2.7.12.tgz
cd Python-2.7.12
./configure
make all
make install && make clean && make distclean
/usr/local/bin/python2.7 -V
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python2.7 /usr/bin/python
```

解决`Yum`无法使用的问题:

```bash
sed  -i "s#/usr/bin/python#/usr/bin/python2.6.6#g" /usr/bin/yum
```

安装`pip`

```bash
yum install python-pip            # centos安装pip
sudo apt-get install python-pip   # ubuntu安装pip
```

安装`pip2.7`

```bash
yum install -y openssl openssl-devel

vim Python-2.7.12/Modules/Setup.dist
找到下面这句，去掉注释
#zlib zlibmodule.c -I(prefix)/include−L(exec_prefix)/lib -lz

重新编译安装Python

curl -sS https://bootstrap.pypa.io/get-pip.py | python
```

pip 常用命令

> python 2.7 版本的 pip 命令是 pip2.7

```bash
pip freeze                      # 查看包版本
pip install Package             # 安装包 ex:pip install requests
pip install django==1.9         # 指定版本安装
pip install --upgrade Package   # 更新一个软件包
pip uninstall Package           # 卸载软件包
pip show --files Package        # 查看安装包时安装了哪些文件
pip show --files Package        # 查看哪些包有更新
pip list                        # 查看pip安装的包及版本
```

## 查看帮助

```python
help('modules')	                # 查看python所有模块
help(object)                    # 查看对象的详细文档
help(object.method)             # 查看对象的属性帮助信息
dir([object])                   # 查看对象的属性
```

## 调试

```
python -m trace -t err.py
import pdb
pdb.set_trace()
python -m pdb err.py
strace -p pid                   # 用系统命令跟踪系统调用
```

## 语句和语法

- 井号(`#`) 表示之后的字符为 python 注释。
- 三引号(`'''...'''`) 三引号之间的内容为 python 注释。
- 反斜线(`\\`) 继续上一行。
- 分号(`;`) 将两个语句连接在一行中。
- 冒号(`:`) 将代码块的头和体分开
- 语句（代码块） 用缩进块的方式体现，不同的缩进深度分割不同的代码块，通常以 tab 或者空格为缩进单位。

## python 中关键字

```python
import keyword
keyword.iskeyword(str)       # 字符串是否为python关键字
keyword.kwlist               # 返回pytho所有关键字
['and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'exec', \
'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'not', 'or', 'pass', 'print', \
'raise', 'return', 'try', 'while', 'with', 'yield']
```

## 内建类型

### 数值型

- int: 普通整型, [-2147483648,2147483647], 支持 8 进制 055, 16 进制 0xff 表达, 如 1，2, 3, 100，-100
- long: 长整型,可以无限..如 1000000000000L
- float: 浮点型, 都是双精浮点,支持科学计数法. 如 1.0, 1. , 1.0e-10
- complex: 复数型, 实际是两个双精度浮点. 1+2j,
- bool: 逻辑型, True , False (分别相当于 1,0)

PS:

- int(‘6.000000000000000000e+00’)类型转换会报错,float(‘6.000000000000000000e+00’)则可以

### 序列型(Sequence),集合,字典

- list: 列表型(可变序列型)，如[1, '2', '3']
- tuple: 元组型(不可变序列型)，如(1, 2, '3')
- set: 可变集合型,另有不可变集合型 frozenset. 如 set([1, 2, 3])
- dict: 字典型， 如 {'name': 'xiao', 'age': 20}
- str: 字符串型(不可变序列型)， 如'hello', "world", "I'm ok", 'I\'m ok'
- unicode: 字符串型(不可变序列型) 如 u'中国'
- bytearray: 字节数组(可变序列型) 如 bytearray([1,2,3])

### 常见重要基础类型

- file: 文件型,通过句柄进行操作.
- 函数: 自定义如 function 类, 内建 builtin_function_or_method, 对象方法 method_descriptor 或 function
- 对象: object 等
- 模块 module: 包括模块和包
- iterator: 迭代器类型
- Exception 和 Error: 异常和错误

### 特殊类型

- NoneType: None, 缺值.bool 可以转为 False,str 转为 str,int 不能转.
- NotImplementedType: NotImplemented, 未执行, 出现在数字处理方法.bool 后成 True. 少见
- ellipsis: Ellipsis, 用于表明存在”…“语法.bool 后成 True. 少见

## 变量

```python
>>> a = 1	                                    # 赋值
>>> a = b = c = 1                               # 多重赋值
>>> a += 1                                      # 增量赋值，操作符`+=  -= *= /= %= **= <<= >>= &= ^= |=`
>>> a, b, c = 1, '2', 3.0                       # 多元赋值
>>> a = 0 or 2 or 1                             # 布尔运算赋值,a值为True既不处理后面,a值为2.  None、字符串''、空元组()、空列表[],空字典{}、0、空字符串都是false
>>> num = input("input:")                       # 接收用户输入数据
>>>name = raw_input("input:").strip()	        # 接收用户输入数据，并转换为str类型
>>> _tmp = 'tmp'	                            # 类中的私有变量
>>> PI = 3.14159265359	                        # 定义常量
>>> global x	                                # 定义全局变量
>>> locals()	                                # 所有局部变量组成的字典
{'a': 2, 'c': 3.0, 'b': '2', 'space': [], '__builtins__': <module '__builtin__' (built-in)>, 'lists': ['aa', 'c', 'd', 'www', 1, 3], '__package__': None, '_tmp': 'tmp', '__name__': '__main__', 'PI': 3.1415926535900001, '__doc__': None}
>>> locals().values()	                        # 所有局部变量值的列表
[2, 3.0, '2', [], <module '__builtin__' (built-in)>, ['aa', 'c', 'd', 'www', 1, 3], None, 'tmp', '__main__', 3.1415926535900001, None]
>>> import os
>>> os.popen("date -d @{0} +'%Y-%m-%d %H:%M:%S'".format(12)).read()    # 特殊情况引用变量 {0} 代表第一个参数
'1970-01-01 08:00:12\n'
```

## 字符串

```python
>>> r = r'C:\some\name'	               	# 输出时以原始字符串打印
>>> u = u'中文'                         # 定义为unicode编码
>>> big = """abcd
efg
"""                                     # 三引号赋值
>>> astr = 'hello, world!'              # 单引号赋值
>>> astr = "hello, world!"              # 双引号赋值
>>> 'hello' + ' python.'            	# 连接字符串
'hello python.'
>>> '1 ' * 3                            # 重复字符串
'1 1 1 '
>>> ','.join(['hello', ' world'])       # join 连接字符串，返回字符串
'hello, world'
>>> 'ab,cde,fgh,ijk'.split(',')         # 分割字符串，返回列表
['ab', 'cde', 'fgh', 'ijk']
>>> "Yes,\" he said."                   # \ 转义"
'Yes," he said.'
>>> 'hello' ' world'	                # 相邻的字符串，会自动连接在一起
'hello world'
>>> str(range(4))                       # 序列转换为字符串
'[0, 1, 2, 3]'
>>> len(astr)                           # len函数，返回字符串的长度
11
>>> 'hello, world'.index('w')           # 从左查找字符串，返回字符串第一次出现的位置，找不到返回ValueError错误；rindex从右查找
7
>>> 'hello, world'.find('l')            # 从左查找字符串，返回字符串第一次出现的位置，找不到返回 < 0的值；rfind从右查找
2
>>> 'hello, world'.find('l123')
-1
>>> cmp('hello', 'world')               #　比较字符串，相同返回0
-1
>>> cmp('hello', 'hello')
0

>>> '456' in '12345678'                 # 判断字符串是否在另外一个字符串中
True
>>> '456' not in '12345678'
False

>>> 'JCstrlwr'.upper()                  # 将字符串转换为大写
'JCSTRLWR'
>>> 'JCstrlwr'.lower()                  # 将字符串转换为小写
'jcstrlwr'

>>> s = ' hello, world! '
>>> s.strip()                           # 去除字符串左右两端空格
'hello, world!'
>>> s.lstrip()                          # 去除字符串左端空格
'hello, world! '
>>> s.rstrip()                          # 去除字符串右端空格
' hello, world!'
>>> 'hello, world'.replace('world', 'python')       # 字符串替换
'hello, python'

>>> sStr1 = 'strcpy'
>>> sStr2 = sStr1                       # 复制字符串
>>> sStr1 = 'strcpy2'
>>> print sStr2
strcpy

>>> 'abcdefg'[::-1]                     # 翻转字符串
'gfedcba'

```

PHP 中 addslashes 的实现

```python
def addslashes(s):
    d = {'"':'\\"', "'":"\\'", "\0":"\\\0", "\\":"\\\\"}
    return ''.join(d.get(c, c) for c in s)

s = "John 'Johny' Doe (a.k.a. \"Super Joe\")\\\0"
print s
print addslashes(s)
```

只显示字母与数字

```python
def OnlyCharNum(s,oth=''):
    s2 = s.lower();
    fomart = 'abcdefghijklmnopqrstuvwxyz0123456789'
    for c in s2:
        if not c in fomart:
            s = s.replace(c,'');
    return s;

print(OnlyStr("a000 aa-b"))
```

截取字符串

```python

str = '0123456789'
print str[0:3]							# 截取第一位到第三位的字符
print str[:]	                    	# 截取字符串的全部字符
print str[6:]	                    	# 截取第七个字符到结尾
print str[:-3]	                    	# 截取从头开始到倒数第三个字符之前
print str[2]	                    	# 截取第三个字符
print str[-1]	                    	# 截取倒数第一个字符
print str[::-1]	                    	# 创造一个与原字符串顺序相反的字符串
print str[-3:-1]	                	# 截取倒数第三位与倒数第一位之前的字符
print str[-3:]	                    	# 截取倒数第三位到结尾
print str[:-5:-3]	                	# 逆序截取，具体啥意思没搞明白？

```

建议

- 在字符串连接的使用尽量使用 join() 而不是 +。
- 当对字符串可以使用正则表达式或者内置函数来处理的时候，选择内置函数。如 str.isalpha()，str.isdigit()，str.startswith((‘x’, ‘yz’))，str.endswith((‘x’, ‘yz’))
- 对字符进行格式化比直接串联读取要快，因此要

使用：`out = "<html>%s%s%s%s</html>" % (head, prologue, query, tail)`

避免：`out = "<html>" + head + prologue + query + tail + "</html>"`

## 列表

> 列表元素的个数最多 536870912

```python
>>> space = []
>>> lists = list(['1','2'])
>>> lists = [1, 1.0, ['a', 'b'], 'c', 'd']
>>> lists[2] = 'aa'
>>> a  = lists[:]                           # 拷贝list
>>> lists.insert(4,'www')                   # 在第4个位置插入一条记录
>>> lists.append('aaa')                     # 追加一条记录
>>> lists.pop()                             # 删除最后一条记录
'aaa'
>>> lists.pop(1)                            # 删除第1个记录
1.0
>>> lists.sort()                            # 排序列表
>>> lists.count('2')                        # 统计元素出现的次数
0
>>> lists.extend([1,2,3])                   # 合并列表
>>> del lists[0]                            # 删除第1个元素
>>> lists.remove(2)                         # 删除2这个元素

>>> ','.join(['hello', ' world'])           # 将列表转换成字符串 用逗号分割
'hello, world'
>>> list(set(['qwe', 'as', '123', '123']))  # 将列表通过集合去重复
['qwe', '123', 'as']
>>> eval("['1','a']")                       # 将字符串当表达式求值,得到列表
['1', 'a']
>>> len(lists)                              # 返回列表的元素个数
6

>>> lists[::-1]                             # 倒着打印 对字符翻转串有效
[3, 1, 'www', 'd', 'c', 'aa']
>>> lists[2::3]                             # 从第二个开始每隔三个打印
['d', 3]
>>> lists[:-1]                              # 排除最后一个
['aa', 'c', 'd', 'www', 1]
>>> lists[-1]                               # 打印最后一个
3
>>> lists[-3:-1]                            # 从倒数第3个，开始打印到-1位置，即倒数第2个；最后一个为-0
['www', 1]


for i, n in enumerate(['a','b','c']):	    # enumerate 可得到每个值的对应位置
    print i,n
```

列表去重复

```python
>>> ids = [1,4,3,3,4,2,3,4,5,6,1]
>>> list(set(ids))
[1, 2, 3, 4, 5, 6]

>>> {}.fromkeys(ids).keys()
[1, 2, 3, 4, 5, 6]
```

列表去重复，并保留原顺序

```python
>>> ids = [1,4,3,3,4,2,3,4,5,6,1]
>>> func = lambda x,y:x if y in x else x + [y]
>>> reduce(func, [[], ] + ids)
[1, 4, 3, 2, 5, 6]
```

## 元组

> `tuple`一旦初始化就不能修改

```python
>>> t = ()	                                # 空元组
>>> t = tuple()
>>> t = (1, )	                            # 只有1个元素的元组
>>> zoo = ('wolf', 'elephant', 'penguin')
>>> zoo[0]
'wolf'
>>> zoo[1:3]
('elephant', 'penguin')
>>> t = (1,2) + (3,4)
>>> t
(1, 2, 3, 4)
>>> t = ('1',) * 4
>>> t
('1', '1', '1', '1')
```

## 字典

```python
>>> ab = {
... 'hello' : '',
... 'test' : 'test@test.com',
... }
>>> ab['c'] = 80	                        # 添加字典元素
>>> ab.pop('c')	                            # 删除字典元素
80
>>> del ab['test']	                        # 删除字典元素
>>> ab.keys()	                            # 查看所有键值
>>> ab.values()	                            # 打印所有值
>>> ab.has_key('a')	                        # 查看键值是否存在
>>> ab.items()	                            # 返回整个字典列表
>>> ab.get('c', '')	                        # 返回元素的值，没有的话返回空

a = {1: {1: 2, 3: 4}}
b = a
b[1][1] = 8888	                            # a和b都为 {1: {1: 8888, 3: 4}}
import copy
c = copy.deepcopy(a)	                    # 再次赋值 b[1][1] = 9999 拷贝字典为新的字典,互不干扰
a[2] = copy.deepcopy(a[1])	                # 复制出第二个key，互不影响  {1: {1: 2, 3: 4},2: {1: 2, 3: 4}}
```

根据键进行排序

```python
>>> dic = {'a':3 , 'b':2 , 'c': 1}
>>> dic
{'a': 3, 'c': 1, 'b': 2}
>>> sorted(dic.iteritems(), key = lambda a:a[0], reverse = True)
[('c', 1), ('b', 2), ('a', 3)]
>>> sorted(dic.iteritems(), key = lambda a:a[0], reverse = False)
[('a', 3), ('b', 2), ('c', 1)]
>>> dic
{'a': 3, 'c': 1, 'b': 2}
```

> 排序之后原字典没有变化，顺序依旧。reverse 参数默认为 `False`

根据键值进行排序

```python
>>> sorted(dic.iteritems(), key = lambda a:a[1], reverse = False)
[('c', 1), ('b', 2), ('a', 3)]
>>> sorted(dic.iteritems(), key = lambda a:a[1], reverse = True)
[('a', 3), ('b', 2), ('c', 1)]
```

Python 字典中使用了 hash table，因此查找操作的复杂度为 O(1)，而 list 实际是个数组，在 list 中，查找需要遍历整个 list，其复杂度为 O(n)，因此对成员的查找访问等操作字典要比 list 更快。

```python
from time import time

t = time()
list = ['a', 'b', 'is', 'python', 'jason', 'hello', 'hill', 'with', 'phone', 'test',
        'dfdf', 'apple', 'pddf', 'ind', 'basic', 'none', 'baecr', 'var', 'bana', 'dd', 'wrd']
list = dict.fromkeys(list, True)
print list
filter = []
for i in range(1000000):
    for find in ['is', 'hat', 'new', 'list', 'old', '.']:
        if find not in list:
            filter.append(find)
print "total run time:"
print time() - t
```

将 list 转化为 dict 后速度提升了将近一半。

## Set

> `key`不能重复, 不存储`value`。

```python
>>> s = set([1, 2, 3])	                    # 定义
>>> s.add(4)	                            # 添加元素
>>> s.remove(4)	                            # 删除元素
>>> d['Adam'] = 67	                        # 赋值
>>> d.get('Thomas', -1)	                    # 获取
>>> d.pop('Bob')	                        # 删除元素
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2	                                # 与操作
set([2, 3])
>>> s1 | s2	                                # 或操作
set([1, 2, 3, 4])
```

list 交集

> set 的 union， intersection，difference 操作要比 list 的迭代要快。因此如果涉及到求 list 交集，并集或者差的问题可以转换为 set 来操作。

```python
# 使用list：
from time import time
t = time()
lista=[1,2,3,4,5,6,7,8,9,13,34,53,42,44]
listb=[2,4,6,9,23]
intersection=[]
for i in range (1000000):
    for a in lista:
        for b in listb:
            if a == b:
                intersection.append(a)

print "total run time:"
print time()-t

# 使用set：
from time import time
t = time()
lista=[1,2,3,4,5,6,7,8,9,13,34,53,42,44]
listb=[2,4,6,9,23]
intersection=[]
for i in range (1000000):
    list(set(lista)&set(listb))
print "total run time:"
print time()-t
```

## 运算符

- `**` 指数 (最高优先级)
- `~ + -` 按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@)
- `\* / % //` 乘，除，取模和取整除
- `\+` - 加法减法
- `\>> <<` 右移，左移运算符
- `&` 位 'AND'
- `^ |` 位运算符
- `<= < > >=` 比较运算符
- `<> == !=` 等于运算符
- `= %= /= //= -= += *= **=` 赋值运算符
- `is, is not` 身份运算符
- `in, not in` 成员运算符
- `not, or, and` 逻辑运算符

## 条件判断

```
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```

```python
>>> 1 if True else 0						# 三元操作符
1
```

## 循环

```python

break           # 跳出循环
continue        # 跳出本次循环，进入下一轮循环
pass            # 不做任何事情
exit() 	        # 结束脚本运行

sum = 0
for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    sum = sum + x
print sum

>>> for i in [1,2]:	                        # 循环执行完后，才会执行else中的代码，break会跳出else
...   print i
... else:
...   print 'ok.'
...
1
2
ok.


sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print sum
```

流程结构简写

`[ 执行代码 for 变量 in 迭代器 [表达式]]`

```python

>>> [ i * 2 for i in [8,-2,5]]
[16, -4, 10]

>>> [ i for i in range(8) if i %2 == 0 ]
[0, 2, 4, 6]
```

## 迭代：`Iterable`

> 如果给定一个`list`或`tuple`，我们可以通过`for`循环来遍历这个`list`或`tuple`，这种遍历我们称为迭代（`Iteration`）。

通过`collections`模块的`Iterable`类型判断一个对象是可迭代对象。

```python
>>> from collections import Iterable
>>> isinstance('abc', Iterable)
True
>>> isinstance([], Iterable)
True
>>> isinstance({}, Iterable)
True
>>> isinstance(range(10), Iterable)
True
>>> isinstance(1, Iterable)
False
```

## 迭代器：`Iterator`

> 可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`。

- 凡是可作用于`for`循环的对象都是`Iterable`类型；
- 凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；
- 集合数据类型如`list`、`dict`、`str`等是`Iterable`，但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。
- Python 的 for 循环本质上就是通过不断调用 next()函数实现的。

使用 isinstance()判断一个对象是否是 Iterator 对象：

```python

>>> from collections import Iterator
>>> isinstance('abc', Iterator)
False
>>> isinstance([], Iterator)
False
>>> isinstance({}, Iterator)
False
>>> isinstance(iter('abc'), Iterator)
True
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter({}), Iterator)
True
```

通过 next()函数访问迭代器的下一个值，直到最后抛出 StopIteration 错误表示无法继续返回下一个值了。

```python
>>> lists = [123, 'xyz', 12.12]
>>> i = iter(lists)
>>> i.next()
123
>>> i.next()
'xyz'
>>> i.next()
12.119999999999999
>>> i.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>>

```

## 列表生成式

> 列表生成式即`List Comprehensions`，是 Python 内置的非常简单却强大的可以用来创建`list`的生成式。

语法

```python

[expr for iter_var in iterable]
[expr for iter_var in iterable if cond_expr]
```

```python

>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

>>> seq = [11, 10, 9, 9, 10, 10]
>>> [x for x in seq if x % 2]
[11, 9, 9]

>>> [(x+1,y+1) for x in range(3) for y in range(5)]
[(1, 1), (1, 2), (1, 3), (1, 4), (1, 5), (2, 1), (2, 2), (2, 3), (2, 4), (2, 5), (3, 1), (3, 2), (3, 3), (3, 4), (3, 5)]

>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> [k + '=' + v for k, v in d.items()]
['y=B', 'x=A', 'z=C']

```

## 生成器:generator

创建生成器

- 只要把一个列表生成式的`[]`改成`()`，就创建了一个`generator`, `next()`函数可以不断获得下一个返回值。
- 如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个`generator`。

工作原理

它是在`for`循环的过程中不断计算出下一个元素，并在适当的条件结束`for`循环。对于函数改成的`generator`来说，遇到`return`语句或者执行到函数体最后一行语句，就是结束`generator`的指令，`for`循环随之结束。
普通函数调用直接返回结果, `generator`函数的“调用”实际返回一个`generator`对象。

定义生成器

```python

>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x7d8730>

>>> def odd():
...     print('step 1')
...     yield 1
...     print('step 2')
...     yield(3)
...     print('step 3')
...     yield(5)
...
>>> odd()
<generator object odd at 0x7d8780>
```

通过 next()函数访问下一个值

```python
>>> o = odd()
>>> o.next()
step 1
1
>>> o.next()
step 2
3
>>> o.next()
step 3
5
>>> o.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

for 循环生成器

```python

>>> oo = odd()
>>> for i in oo:
...   print i
...
step 1
1
step 2
3
step 3
5
```

## 字符串编码

字符串实质是字符的一个集合,而字符则以数字形式储存. 最早的计算机在设计时采用**8**个比特（`bit`）作为一个字节（`byte`），所以，一个字节能表示的最大的整数就是`255`, 两个字节可以表示的最大整数是`65535`，3 个字节最大整数是`16711425`, 4 个字节可以表示的最大整数是`4294967295`. 三个字节就足够多了…

### ASCII

由于计算机是美国人发明的，因此，最早只有 127 个字母被编码到计算机里，也就是大小写英文字母、数字和一些符号，这个编码表被称为`ASCII`编码，比如大写字母`A`的编码是`65`，`Z`编码`90`; 小写字母 a 编码 97, z 的编码是 122。这种编码一个字符只需一个字节, 对于英文字符而言足够了.这也是最基础的字符集..

[ASCII 对照表](http://tool.oschina.net/commons?type=4)

### GB2312 等 local 语言编码

为了解决如汉字等其他语言的编码问题, 出现了如 GB2312 码等, 用于把中文编进去. 这些编码最少需要两个字节,一般向下兼容 ASCII 码.
然而.各国有各国的标准，就会不可避免地出现冲突，结果就是，在多语言混合的文本中，显示出来会有乱码。

### Unicode

Unicode 把所有语言都统一到一套编码里，这样就不会再有乱码问题了, 便于统一使用.Unicode 标准在不断发展，但最常用的是用两个字节表示一个字符（如果要用到非常偏僻的字符，就需要 4 个字节）。现代操作系统和大多数编程语言都直接支持 Unicode。Python 中 unicode 的编码字节数取决于编译时环境.

### UTF-8

如果统一成 Unicode 编码，乱码问题从此消失了。但是，如果你写的文本基本上全部是英文的话，用 Unicode 编码比 ASCII 编码需要多一倍的存储空间，在存储和传输上就十分不划算。本着节约的精神，又出现了把 Unicode 编码转化为“可变长编码”的 UTF-8 编码。UTF-8 编码把一个 Unicode 字符根据不同的数字大小编码成 1-6 个字节，常用的英文字母被编码成 1 个字节，汉字通常是 3 个字节，只有很生僻的字符才会被编码成 4-6 个字节。如果要传输的文本包含大量英文字符，用 UTF-8 编码就能节省空间.

- 在计算机内存中，统一使用 Unicode 编码，当需要保存到硬盘或者需要传输的时候，就转换为 UTF-8 编码。
- 用记事本编辑的时候，从文件读取的 UTF-8 字符被转换为 Unicode 字符到内存里，编辑完成后，保存的时候再把 Unicode 转换为 UTF-8 保存到文件：

### Python 的字符串编码

ascii

Python2 默认使用`ascii`编码. Python3 默认使用`unicode`进行编码. 即使使用 ascii 编码, 在编码转换时中间总是经过 unicode.

```python
ord('a') #->97
chr(97) #->a
```

unicode

unicode.encode 和 decode 是两个 unicode 字符串的重要方法,可以将其强行转换为别的编码,encode 是 unicode->other, decode 是 other-> unicode.

```python
print u"你好!"
# -> 你好!
u"你好"
# -> u'\u4f60\u597d'
print unichr(0x4f60)
# -> 你

# unicode to other

u"你好!".encode('utf-8')
# -> '\xe4\xbd\xa0\xe5\xa5\xbd!'
u"你好!".encode('gb2312')
# -> '\xc4\xe3\xba\xc3!'

# other to unicode
print '\xe4\xbd\xa0\xe5\xa5\xbd!'.decode('utf-8')
# -> 你好!
```

## 字符串格式化

`%[(name)][flags][width].[precision]typecode`

- (name): 命名,用于字典控制赋值
- flags: 可以有+,-,’ ‘或 0。+表示右对齐。-表示左对齐。’ ‘为一个空格，表示在正数的左侧填充一个空格，从而与负数对齐。0 表示使用 0 填充。
- width: 显示宽度,总长度,会补齐空格.
- precision: 表示小数点后精度.

```python
>>> print "I'm %s. I'm %d year old" % ('Hom', 30)
I'm Hom. I'm 30 year old
>>> a = "I'm %s. I'm %d year old" % ('Hom', 30)
>>> print a
I'm Hom. I'm 30 year old
>>> print "I'm %(name)s. I'm %(age)d year old" % {'name':'Hom', 'age':30}
I'm Hom. I'm 30 year old
>>> print "%+10x" % 10
        +a
>>> print "%04d" % 10
0010
>>> print "%6.3f" % 2.3
 2.300
>>> print "%.*f" % (4, 1.2)
1.2000

```

### 格式符

- %s 字符串 (采用 str()的显示)
- %r 字符串 (采用 repr()的显示)
- %c 单个字符
- %b 二进制整数
- %d 十进制整数
- %i 十进制整数
- %o 八进制整数
- %x 十六进制整数
- %e 指数 (基底写为 e)
- %E 指数 (基底写为 E)
- %f 浮点数
- %F 浮点数，与上相同
- %g 指数(e)或浮点数 (根据显示长度)
- %G 指数(E)或浮点数 (根据显示长度)

要是想输出`%`则要使用`%%`进行转义操作.

#### 字符串 format 方法

```
>>> '{0},{1}'.format('kzc',18)
'kzc,18'
>>> '{1},{1}'.format('kzc',18)
'18,18'
>>> '{1},{0},{1}'.format('kzc',18)
'18,kzc,18'
>>> '{name},{age}'.format(age=18,name='kzc')
'kzc,18'
>>> p=['kzc',18]
>>> '{0[0]},{0[1]}'.format(p)
'kzc,18'

>>> class Person:
...     def __init__(self,name,age):
...             self.name,self.age = name,age
...     def __str__(self):
...             return 'This guy is {self.name},is {self.age} old'.format(self=self)
...
>>> print Person('kzc',18)
This guy is kzc,is 18 old

```

## 文件处理

文件打开模式

- w 以写方式打开，
- a 以追加模式打开 (从 EOF 开始, 必要时创建新文件)
- r+ 以读写模式打开
- w+ 以读写模式打开 (参见 w )
- a+ 以读写模式打开 (参见 a )
- rb 以二进制读模式打开
- wb 以二进制写模式打开 (参见 w )
- ab 以二进制追加模式打开 (参见 a )
- rb+ 以二进制读写模式打开 (参见 r+ )
- wb+ 以二进制读写模式打开 (参见 w+ )
- ab+ 以二进制读写模式打开 (参见 a+ )

写文件

```python
i={'ddd':'ccc'}
f = file('poem.txt', 'a')
f.write("string")
f.write(str(i))
f.flush()
f.close()
```

```python
log = open('/root/test','a')
log.write("string")
log.close()
```

读文件

```python
f = file('/etc/passwd','r')
c = f.read().strip()        # 读取为一个大字符串，并去掉最后一个换行符
for i in c.spilt('\n'):     # 用换行符切割字符串得到列表循环每行
    print i
f.close()

```

```python
f = file('/etc/passwd','r')
while True:
    line = f.readline()    # 返回一行
    if len(line) == 0:
        break
    x = line.split(":")                  # 冒号分割定义序列
    #x = [ x for x in line.split(":") ]  # 冒号分割定义序列
    #x = [ x.split("/") for x in line.split(":") ]  # 先冒号分割,在/分割 打印x[6][1]
    print x[6],"\n",
f.close()
```

```python
f = file('/etc/passwd')
c = f.readlines()       # 读入所有文件内容,可反复读取,大文件时占用内存较大
for line in c:
    print line.rstrip(),
f.close()
```

```python
for i in open('b.txt'):   # 直接读取也可迭代,并有利于大文件读取,但不可反复读取
    print i,
```

```python
# 自动关闭文件、线程锁的自动获取和释放等
with open('a.txt') as f:
    for i in f:
        print i
    print f.read()        # 打印所有内容为字符串
    print f.readlines()   # 打印所有内容按行分割的列表
```
