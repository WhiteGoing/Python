- ​
- ```
  ISO8859 不是一个标准，而是一系列的标准，这套字符集与编码系统的共同特色是，以同样的码位对应不同字符集。
  ```

```
ISO8859-1 字符集，也就是 Latin-1，是西欧常用字符，包括德法两国的字母。
ISO8859-2 字符集，也称为 Latin-2，收集了东欧字符。
ISO8859-3 字符集，也称为 Latin-3，收集了南欧字符。
Effective Python
```

- ​
- ```
  Pylink:python源码分析工具，（http://www.pylink.org）
  ```

```
python 2 ： str  ---→  包含原始8字节字符
			unicode --→  包含Unicode字符
python 3 ： bytes  ---→  包含原始8字节字符
			str --→  包含Unicode字符
python程序核心部分应该使用Unicode字符类型（也就是Python3中的str和Python2中的unicode）
def to_unicode(unicode_or_str):
    '''
    :param unicode_or_str: unicode or str string
    :return: unicode string
    '''
    if isinstance(unicode_or_str, str):
        value = unicode_or_str.decode('utf-8')
    else:
        value = unicode_or_str
    return value
在python 3中，给open函数添加类名为encoding的新参数，而这个新参数的默认值类型为‘utf-8’，所以，python 3向文件中写入二进制数据时，应该里‘wb’模式开启文件
with open('/tmp/1.bin', 'wb') as f:
	f.write(os.urandom(10))
同样，读取二进制数据也应该为‘rb’
```

- ​
- ```
  or用法
  ```

```
a = [1,2,34,4,'']
b = a[4] or 0
print b
```

- ​
- ```
  python编程时，尽量将复杂的表达式移入辅助函数中。
  ```

- ​
- ```
  交换两数据时不要用中间变量
  ```

```
a = 3
b = 4
a,b = b,a
```

- ​
- ```
  build-in 函数通常较快，add(a,b) 要优于 a+b
  ```

- ​
- ```
  python常见技巧，逆序字符串(切片的步进值为-1)：
  ```

```
x = ‘abcdefg’
y = x[::-1]
print y
```

- ​
- ```
  用列表推导 来取代map和filter
  ```

- ​
- ```
  用生成器表达式来改写数据量较大的列表推导
  ```

```
列表推导的缺点：在推导过程中，对序列中的每个值，可能都要创建一个仅含一项元素的全新列表。
生成器：把实现列表推导的那种写法放在一对圆括号中，就构成生成器。
使用生成器的好处是：可以相互组合，将上一个生成器的返回值作为下一生成器的输入值。（注意，生成器的结果只能消费一次）
a = [[1,2,3],[4,5]]
it = (len(x) for x in a)
calculate = ((x, x**0.5) for x in it)
print next(calculate)
print next(calculate)
```

- ​
- ```
  尽量用enumerate取代range
  ```

- ​
- ```
  用zip函数同时遍历两个迭代器
  ```

```
注意：1、Python 2中的zip并不是迭代器（Python 3是），故每次迭代所产生的值汇聚成元组，并把元组构成的列表完整的返回给用户，故数据量大时，应该使用itertools里的内置模块izip函数
2、在不能确定迭代列表大小时应该使用itertools里的zip_longest函数，否则只会按照最短的列表输出结果
a = ['a', 'b', 'c']
b = [1, 2, 3]
for i, j in zip(a, b):
    print i, j
print dict(zip(a, b))
from itertools import chain
for i in chain(a, b):
    print i
```

- ​
- ```
  不要在for和while循环的后面写else模块，不直观
  ```

```
在循环中使用break则不执行else模块，如果for遍历的容器是空的则立即执行else模块，while False：也会直接执行else模块
```

- ​
- ```
  合理使用try/except/else/finally模块
  ```

```
1、try/finally：能确保可靠的关闭文件，注意，open()不能写在try：里
handle = open('/tmp/1.txt') # May raise IOError
try:
    data = handle.read() # May raise UnicodeDecodeError
finally:
    handle.close() # Always runs after try:
2、try/except/else/：可以清晰的描述出哪些异常由自己的代码来处理，哪些异常会传播到上一级。
如果try没有发生异常，那么就执行else块。有了这种else块，我们就可以尽量缩减try块内的代码量，更易于读。
import json
def load_json_key(data, key):
    try:
        result_dict = json.loads(data) # May raise ValueError
    except Exception as a:
        print a
    else:
        return result_dict[key]
c = [1, 2, 3]
cc = json.dumps(c)
print load_json_key(cc, 1)
3、混合使用
```

- ​
- ```
  尽量用异常来表示特殊情况，而不要返回None
  ```

- ​
- ```
  了解如何在闭包里使用外围作用域中的表量
  ```

- ​
- ```
  参数迭代
  ```

```
class ReadVisits(object):
    def __init__(self, data_path):
        self.data_path = data_path
    def __iter__(self):                ###自己定义的迭代
        with open(self.data_path) as f:
            for line in f:
                yield int(line)
def normalize(numbers):
    total = sum(numbers)
    print total
    result = []
    for value in numbers:
        print value
        percent = 100 * value / total
        result.append(percent)
    return result

path = '/home/fwq/Desktop/test.txt'
visits = ReadVisits(path)
percentages = normalize(visits)
print percentages
##Python在执行for I in foo循环时，会调用iter(foo),内置的iter又会调用foo.__iter__这个特殊的方法，该方法必须返回迭代对象，而那个迭代器本身则实现了名为__next__的特殊方法。此后，for循环会在迭代器对象上反复调用内置的next函数，直至其耗尽产生StopIteration异常。
```

- ​
- ```
  用数量可变的位置参数时要注意
  ```

```
1、由于def fun(*c)中，Pyhon必须把所有数据放在一个元组里（计算c的实参是一个迭代器），再传入函数，所以当参数数量比较少时，才应该令函数接受*args的变长参数
2、在扩展这种*argsi函数时，只能使用关键字形式指定的参数
```

- ​
- ```
  用None和文档字符串来描述具有动态默认值的参数
  ```

```
def log(when = None): pass7
```

- ​
- ```

  ```

1、*.tar用 tar -xvf 解压

2、*.gz用 gzip-d或者gunzip解压

3、*.tar.gz和*.tgz用 tar -xzf 解压

4、*.bz2用 bzip2-d或者用bunzip2解压

5、*.tar.bz2用tar-xjf 解压

6、*.Z用 uncompress解压

7、*.tar.Z用tar -xZf 解压

8、*.rar用 unrar e解压

9、*.zip用 unzip 解压

 .gz

解压1：gunzipFileName.gz

解压2：gzip-d FileName.gz

压缩：gzipFileName

.tar.gz

解压：tarzxvf FileName.tar.gz

压缩：tarzcvf FileName.tar.gz DirName

\---------------------------------------------

.bz2

解压1：bzip2-d FileName.bz2

解压2：bunzip2FileName.bz2

压缩：bzip2 -z FileName

.tar.bz2

解压：tarjxvf FileName.tar.bz2

压缩：tarjcvf FileName.tar.bz2 DirName

\---------------------------------------------

.bz

解压1：bzip2-d FileName.bz

解压2：bunzip2FileName.bz

压缩：未知

.tar.bz

解压：tarjxvf FileName.tar.bz

压缩：未知

\---------------------------------------------

.Z

解压：uncompressFileName.Z

压缩：compressFileName

.tar.Z

解压：tarZxvf FileName.tar.Z

压缩：tarZcvf FileName.tar.Z DirName

\---------------------------------------------

.tgz

解压：tarzxvf FileName.tgz

压缩：未知

.tar.tgz

解压：tarzxvf FileName.tar.tgz

压缩：tarzcvf FileName.tar.tgz FileName

\---------------------------------------------

.zip

解压：unzipFileName.zip

压缩：zipFileName.zip DirName

\---------------------------------------------

.rar

解压：rara FileName.rar

压缩：rar e FileName.rar 