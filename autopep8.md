#PEP 8规范

***代码的可读性更重要***

##1. 代码布局：



1. 缩进

   每行缩进用四个空格

   对于连续行应该使用Python的隐式线或悬挂缩进对圆括号、括号和大括号包含的元素进行垂直对齐。当使用悬挂缩进时，应考虑以下事项：第一行不应有任何参数，应使用进一步缩进来清楚地将其区分为连续行。

   Yes:

   ```
   # 分隔符垂直对齐.
   foo = long_function_name(var_one, var_two,
                            var_three, var_four)

   # 使用更多的缩进用来区分.
   def long_function_name(
           var_one, var_two, var_three,
           var_four):
       print(var_one)

   # 悬挂缩进应该增加一行.
   foo = long_function_name(
       var_one, var_two,
       var_three, var_four)
   ```

   No:

   ```
   # 不使用垂直对其时，第一行不允许有参数.
   foo = long_function_name(var_one, var_two,
       var_three, var_four)

   # 缩排和缩进无法区分.
   def long_function_name(
       var_one, var_two, var_three,
       var_four):
       print(var_one)
   ```

   ***悬挂缩进应（ｍａｙ）多于４个空格！！！***

   **当if语句的条件部分足够长，需要跨多行编写时，在随后的行自然地加上四空格缩进，下面缩进是允许的但是不限于：**

   ```
   # 没有其他缩进.
   if (this_is_one_thing and
       that_is_another_thing):
       do_something()

   # 增加一条注释
   if (this_is_one_thing and
       that_is_another_thing):
       # Since both conditions are true, we can frobnicate.
       do_something()

   # 在条件行增加其他缩进
   if (this_is_one_thing
           and that_is_another_thing):
       do_something()
   ```

   **元组、列表等结构的布局：**

   ```
   my_list = [
       1, 2, 3,
       4, 5, 6,
       ]
   result = some_function_that_takes_arguments(
       'a', 'b', 'c',
       'd', 'e', 'f',
       )
   ```

   or it may be lined up under the first character of the line that starts the multiline construct, as in:

   ```
   my_list = [
       1, 2, 3,
       4, 5, 6,
   ]
   result = some_function_that_takes_arguments(
       'a', 'b', 'c',
       'd', 'e', 'f',
   )
   ```

2. 用Tab还是空格

   空格是更好的方法

   Tab只应该使用在代码以前使用tab进行缩进的情况下

   Python 3不允许tab和空格的混合缩进

3. 最大的行长

   每个行的最大长度时７９个字符

   限制所需的编辑器窗口宽度可以使多个文件并排打开，并且在使用相邻列中的两个版本的代码审查工具时工作得很好。

4. 断行应该在二进制运算符的前面还是后面？

   早期的标准，断行在运算符之后，这样会破坏可读性：

   ```python
   # No: 操作数和运算符相隔的太远
   income = (gross_wages +
             taxable_interest +
             (dividends - qualified_dividends) -
             ira_deduction -
             student_loan_interest)
   ```

   为了更好的匹配运算符和运算数：

   ```python
   # Yes: easy to match operators with operands
   income = (gross_wages
             + taxable_interest
             + (dividends - qualified_dividends)
             - ira_deduction
             - student_loan_interest)
   ```

5. 空白行

   顶层函数和类定义用两条空行隔开

   类里的方法用一个空行隔开

   可以用空行来隔开功能组，一段相关的话之间可以省略空行

   函数里可以使用空行来分隔逻辑部分

6. 源文件编码

   编写Python的核心代码时应该使用UTF-8编码（Python 2中使用ASCII）

7. 导入(import)

   **导入应该使用分开的行，如：**

   ```python
   Yes: import os
        import sys

   No:  import sys, os
   ```

   **虽然如下的方法也ok:**

   ```python
   from subprocess import Popen, PIPE
   ```

   **导入应该在文件的开头，只在在模块注释和文档字符串之后，在全局模块和常数之前**

   **导入应该按如下的顺序分组：**

   (1) 标准库的导入

   (2) 相关第三方库的导入

   (3) 本地应用，库的导入

   应该用空白行将每组分隔开

   **绝对导入时应该被提倡的，它的可读性更高，但是明确的相对导入也是可以接受的，它可以避免绝对导入时的冗长：**

   ```python
   # Absolute imports
   import mypkg.sibling
   from mypkg import sibling
   from mypkg.sibling import example

   # Relative imports
   from . import sibling
   from .sibling import example
   ```

   标准库代码应避免复杂的包布局，并始终使用绝对导入

   **当从类模型里导入类时，可以如下：**

   ```python
   from myclass import MyClass
   from foo.bar.yourclass import YourClass
   ```

   当导入时赵成本地名冲突，可以如下拼写：

   ```python
   import myclass
   import foo.bar.yourclass
   ```

   然后使用```myclass.MyClass``` and```foo.bar.yourclass.YourClass```

   应避免通配符导入 (`from <module> import *`)

8. 模块级的dunder名

   模块级的dunder（具有两个引导符和两个尾随下划线的名称，如：```__all__```,```__author__```,```__version__``` ）应该放在模块文档字符串之后，但是应该在所有```import```语句之前（除了```from __future__ import```），Python规定，future-imports必须出现在除了文档字符串的任意代码之前。

   例子如下：

   ```python
   """This is the example module.

   This module does stuff.
   """

   from __future__ import barry_as_FLUFL

   __all__ = ['a', 'b', 'c']
   __version__ = '0.1'
   __author__ = 'Cardinal Biggles'

   import os
   import sys
   ```

   ​

## 2. 字符串引号

在python中，单引号字符串和双引号字符串是一样的。选择一种，一直坚持下去就ok。

## 3. 表达式和语句的空白字符

1. 个人习惯

   **避免出现大量的空白字符：**

   >1. 括号内的括号之间
   >
   >   ```python
   >   Yes: spam(ham[1], {eggs: 2})
   >   No:  spam( ham[ 1 ], { eggs: 2 } )
   >   ```
   >
   >   ​
   >
   >2. 在逗号与后面的括号之间
   >
   >   ```python
   >   Yes: foo = (0,)
   >   No:  bar = (0, )
   >   ```
   >
   >3. 紧接在逗号、分号或者冒号之前
   >
   >   ```python
   >   Yes: if x == 4: print x, y; x, y = y, x
   >   No:  if x == 4 : print x , y ; x , y = y , x
   >   ```
   >
   >4. 然而，在一个切片中，冒号就像一个二进制运算符，在两边都应该有相等数量的空格（把它当作优先级最低的运算符）。在一个扩展的片，两个冒号必须有相同数量的空格应用。例外：当省略一个切片参数时，该空间被省略。
   >
   >   Yes:
   >
   >   ```python
   >   ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
   >   ham[lower:upper], ham[lower:upper:], ham[lower::step]
   >   ham[lower+offset : upper+offset]
   >   ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
   >   ham[lower + offset : upper + offset]
   >   ```
   >
   >   No:
   >
   >   ```python
   >   ham[lower + offset:upper + offset]
   >   ham[1: 9], ham[1 :9], ham[1:9 :3]
   >   ham[lower : : upper]
   >   ham[ : upper]
   >   ```
   >
   >5. 在函数调用的第一个左括号之前
   >
   >   ```python
   >   Yes: spam(1)
   >   No:  spam (1)
   >   ```
   >
   >6. 在序号和切片之前
   >
   >   ```python
   >   Yes: dct['key'] = lst[index]
   >   No:  dct ['key'] = lst [index]
   >   ```
   >
   >   ​
   >
   >7. 在赋值（或其他）操作符周围多个空格使其与另一个符对齐
   >
   >   Yes:
   >
   >   ```python
   >   x = 1
   >   y = 2
   >   long_variable = 3
   >   ```
   >
   >   No:
   >
   >   ```python
   >   x             = 1
   >   y             = 2
   >   long_variable = 3
   >   ```

   ​

2. 其它建议

   >1. 不要在任何地方尾随一个空格
   >
   >2. 总在在这些二进制运算符的两边加上空格:```assignment (`=`), augmented assignment (`+=`, `-=` etc.), comparisons (`==`, `<`, `>`, `!=`, `<>`, `<=`, `>=`, `in`, `not in`, `is`, `is not`), Booleans (`and`, `or`, `not`).```
   >
   >3. 如果运算式使用有不同优先级的运算符，可以考虑在最低级运算符周围加上空格。然而，不要只用一个空格，要在运算符两边都加上。
   >
   >   Yes:
   >
   >   ```python
   >   i = i + 1
   >   submitted += 1
   >   x = x*2 - 1
   >   hypot2 = x*x + y*y
   >   c = (a+b) * (a-b)
   >   ```
   >
   >   No:
   >
   >   ```python
   >   i=i+1
   >   submitted +=1
   >   x = x * 2 - 1
   >   hypot2 = x * x + y * y
   >   c = (a + b) * (a - b)
   >   ```
   >
   >4. 当```=```用于指示关键字参数或默认参数值时，不要使用空格
   >
   >   Yes:
   >
   >   ```python
   >   def complex(real, imag=0.0):
   >       return magic(r=real, i=imag)
   >   ```
   >
   >   No:
   >
   >   ```python
   >   def complex(real, imag = 0.0):
   >       return magic(r = real, i = imag)
   >   ```
   >
   >5. 函数注释应该使用正常的冒号规则，一定要在```->```箭头的两边使用空格
   >
   >   Yes:
   >
   >   ```python
   >   def munge(input: AnyStr): ...
   >   def munge() -> AnyStr: ...
   >   ```
   >
   >   No:
   >
   >   ```python
   >   def munge(input:AnyStr): ...
   >   def munge()->PosInt: ...
   >   ```
   >
   >6. 当将参数注释与默认值组合时，请在```=```符号周围使用空格（但仅适用于具有注释和默认值的参数）。
   >
   >   Yes:
   >
   >   ```python
   >   def munge(sep: AnyStr = None): ...
   >   def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...
   >   ```
   >
   >   No:
   >
   >   ```python
   >   def munge(input: AnyStr=None): ...
   >   def munge(input: AnyStr, limit = 1000): ...
   >   ```
   >
   >7. 复合语句（在同一行上的多个语句）通常被阻止。
   >
   >   Yes:
   >
   >   ```python
   >   if foo == 'blah':
   >       do_blah_thing()
   >   do_one()
   >   do_two()
   >   do_three()
   >   ```
   >
   >   Rather not:
   >
   >   ```python
   >   if foo == 'blah': do_blah_thing()
   >   do_one(); do_two(); do_three()
   >   ```
   >
   >8. 虽然有时可以在同一行上放置if/for/while，但对于多子句语句则不这样做。避免折叠这样长的行！
   >
   >   Rather not:
   >
   >   ```python
   >   if foo == 'blah': do_blah_thing()
   >   for x in lst: total += x
   >   while t < 10: t = delay()
   >   ```
   >
   >   Definitely not:
   >
   >   ```python
   >   if foo == 'blah': do_blah_thing()
   >   else: do_non_blah_thing()
   >
   >   try: something()
   >   finally: cleanup()
   >
   >   do_one(); do_two(); do_three(long, argument,
   >                                list, like, this)
   >
   >   if foo == 'blah': one(); two(); three()
   >   ```

   ​

## 4. 什么使用尾部符号

尾随逗号通常是可选的，除非它们在构成一个元素的元组时是强制性的（在Python 2中，它们对打印语句具有语义）。为了清晰起见，建议将后者包围在（技术冗余的）括号中。

Yes:

```python
FILES = ('setup.cfg',)
```

OK, but confusing:

```python
FILES = 'setup.cfg',
```

尾随逗号是多余的，当使用版本控制系统时，当值、参数或导入项的列表预期将随着时间而扩展时，它们通常是有用的。

模式是将每个值（等）放在一行上，总是添加一个尾随逗号，并在下一行添加括号。但是，在关闭符分隔符的同一行上有一个尾随逗号是没有意义的（除了在单例元组的上述情况下）。

Yes:

```python
FILES = [
    'setup.cfg',
    'tox.ini',
    ]
initialize(FILES,
           error=True,
           )
```

No:

```python
FILES = ['setup.cfg', 'tox.ini',]
initialize(FILES, error=True,)
```



## 5. 说明

与代码相悖的注释比没有注释更糟糕。当代码更改时，始终优先保留注释的最新内容！

注释应该是完整的句子。第一个词应该大写，除非它是一个以小写字母开头的标识符（不要改变标识符的情况）！。

块注释一般由一个或多个段落组成，每个句子由一个完整的句子组成，每个句子以一个段落结尾。

你应该在句子结束时使用两个空格，而不是在最后一句之后。

英语书写时，遵循Strunk和White。

来自非英语国家的Python程序员：请用英语写你的注释，除非你120%确定这些代码永远不会被不懂你语言的人读过。

1. 块注释

   块注释通常适用于跟踪它们的一些（或所有）代码，并缩进到与该代码相同的级别。注释块的每一行都从一个#和一个空格开始（除非它是缩进的文本里面的评论）。

2. 行内注释

   谨慎使用行内注释。

   行内注释是与语句在同一行上的注释。行内注释应该从语句中至少分隔两个空格。他们应该从一个#和一个空格开始。

   行内注释是不必要的，事实上，如果它们表述明显的话，则会分散注意力。不要这样做：

   ```python
   x = x + 1                 # Increment x
   ```

   但是有时候，它很有用:

   ```python
   x = x + 1                 # Compensate for border
   ```

3. 文件字符串

   好的文件字符串编写可以查看： [PEP 257](https://www.python.org/dev/peps/pep-0257).

   >1. 为所有的公共模块，函数，类和方法写文件字符串。文档字符串对非公开的方法不是必要的，但你应该有一个描述这个方法做什么的注释。此注释应该出现在def行之后
   >
   >2. [PEP 257](https://www.python.org/dev/peps/pep-0257) 介绍了好的文档字符串的约定。注意，最重要的是，```"""```结束多行的文档字符串应该独自一行，如：
   >
   >   ```python
   >   """Return a foobang
   >
   >   Optional plotz says to frobnicate the bizbaz first.
   >   """
   >   ```
   >
   >3. 只有一行的文档字符串，应该让结尾的`"""`在同一行.

   ​

## 6. 命名约定

Python库的命名约定有点混乱，所以我们永远不会得到完全的一致，尽管如此，这里是目前推荐的命名标准。新的模块和包（包括第三方框架）应该写入这些标准，但是现有的库有不同的风格，内部一致性是首选。

1. 最重要的原则

   API对用户可见的公共部分名称应遵循反映**使用**而非**实现**的约定。

2. 描述：命名风格

   现在有很多不同的命名风格，它能帮之我们识别哪种命名风格是正在被使用的，独立于他们现在在使用的那些。

   下面的这些命名方式都很重要：

   >1. b (单写小写字母)
   >
   >2. B (单写大写字母)
   >
   >3. 小写字母
   >
   >4. 小写字母与下划线
   >
   >5. 大写字母
   >
   >6. 大写字母与下划线
   >
   >7. 首字母大写（CapitalizedWords）
   >
   >   注意：在我们将首字母大写运用于缩写单词时，应该将缩写字母全都大写，HTTPServerError比HttpServerError更好。
   >
   >8. 混合情况(mixedCase)。不同于首字母大写的地方是：第一个单词小写，如mixedCase
   >
   >9. 首字母大写并具有下划线（最丑的）

   还有一种使用简短的唯一前缀将相关名称分组的样式，这在Python中不是很常用，只是为了完整性而提到它。例如:```os.stat()```返回一个元组，元组的内容一般会有一些名字类似于```st_mode, st_size, st_mtime 。```（这样做是为了强调符合POSIX系统调用结构，有助于程序员熟悉它。）

   此外,使用前导或尾随下划线的下列特殊形式（一般可以与任何情况约定相结合）是被认同的：

   >1. 单下划线开头：若“内部使用”指示，如：```from M import *```不会导入以此方式命名的对象。
   >
   >2. 单下划线结尾：用于避免与Python关键字发生冲突，如：
   >
   >   ```python
   >   Tkinter.Toplevel(master, class_='ClassName')
   >   ```
   >
   >3. 双下划线开头：此为私有成员，在命名一个类属性时，用于补全名称（name mangling），如：类FooBar中的属性```__boo```会变成```_FooBar_boo```)
   >
   >4. 双下划线开头和结尾：用户命名空间内的“magic”对象或属性。例如```_init__, __import__ , __file__```,千万不要发明这些名字，除非在文档中使用它们

   ​

3. 约定俗成的：命名约定

   >1. 应避免的名字：
   >
   >   不要将字符“l”（小写字母el）、“O”（大写字母oh）或“I”（大写字母eye）作为单个字符变量名。在某些字体中，这些字符与数字1和0不可区分。当试图使用“l”时，使用“L”代替。
   >
   >2. ASCII码兼容。标准库中使用的标识符必须是ASCII兼容的。参考 [policy section](https://www.python.org/dev/peps/pep-3131/#policy-specification) of [PEP 3131](https://www.python.org/dev/peps/pep-3131)中的描述。
   >
   >3. 包和模块的命名
   >
   >   模块的命名应该**简短且全小写**，在提高模块可读性的情况下可以使用下划线。Python包的命名也应该**简短且全小写**，尽管使用下划线是不被支持的。
   >
   >4. 当用C/C++写的扩展模块附带一个提供了更高等级接口（例如，更多的面向对象）的Python模块时，C/C++模块前加一个下划线，如```_socket```。
   >
   >5. 类命名
   >
   >   类命名通常应该使用**首字母大写**的约定
   >
   >   这种命名方法在如下情况下可能不被使用：主要是用来被调用的、文档化的接口
   >
   >   注意，这里有一个对于内置名的单独约定：大部分内置名是一个单词（或者两个），**首字母大写**的命名法只来**命名异常名和内置常数**。
   >
   >6. 类型的变量名
   >
   >   [PEP 484](https://www.python.org/dev/peps/pep-0484) 介绍类型的变量名应该使用**首字母大写**且**短**的名字：```T, AnyStr,Num```　，建议添加后缀```_co```或```_contra```用来声明协变量（covariant）或逆变（contravariant，如：
   >
   >   ```python
   >   from typing import TypeVar
   >
   >   VT_co = TypeVar('VT_co', covariant=True)
   >   KT_contra = TypeVar('KT_contra', contravariant=True)
   >   ```
   >
   >   ​
   >
   >7. 异常名
   >
   >   因为异常应该是类，所以类命名约定适用于这里。但是，你应该在异常名称上使用后缀“Error”（如果异常确实是一个错误）
   >
   >8. 全局变量名称
   >
   >   （希望这些变量只在一个模块内使用），这些约定与函数的约定大致相同。
   >
   >9. 函数和变量名
   >
   >   函数名应小写，必要时用下划线分隔，以提高可读性。
   >
   >10. 函数和方法的参数
   >
   >    总是使用```self```来作为实例方法的第一个参数
   >
   >    总是使用```cls```来作为类方法的第一个参数
   >
   >    如果函数参数的名称与保留关键字冲突，通常只附加一个尾部下划线，而不是使用缩写或拼写损坏。因此```class_```比```clss```更好。（最好是使用同义词避免这种冲突。）
   >
   >11. 方法名和实例变量
   >
   >    使用函数命名规则：**小写，用下划线分隔单词**，以提高可读性。
   >
   >    仅为非公共方法和实例变量使用**一个前导下划线**。
   >
   >    为了避免子类名称冲突，使用**双下划线**来调用Python的名字规则。
   >
   >    一般来说，双下划线应该只用来避免与类中的属性设计为子类名称冲突。
   >
   >    注：有关于__names使用一些争议（见下文）。
   >
   >12. 常数
   >
   >    常量通常定义在模块级，用大写字母写成，并用下划线分隔单词。例子： `MAX_OVERFLOW` `TOTAL`.
   >
   >13. 继承的设计
   >
   >    始终要明确：一个类方法和一个实例变量（统称为“属性”）应该是公有的还是私有的。如果有疑惑，选择非公有的方式，将其变成公有变量比把一个公有变量变成一个非公有的变量要容易。
   >
   >    公共属性是那些期望与类无关的客户机使用的属性，并承诺避免向后不兼容的更改。非公共属性是那些不打算被第三方使用的属性；您不能保证非公共属性不会改变甚至被删除。
   >
   >    我们这里不使用“私有”一词，因为Python中没有什么属性是私有的（没有一般不必要的工作量）。
   >
   >    另一类属性是“子类API”的一部分（通常用其他语言称为“受保护”）。有些类是为了继承而设计的，要么扩展或修改类的行为方面。在设计这样一个类时，要谨慎地决定哪些属性是公有的，哪些属性是子类API的一部分，而这些属性真正只供基类使用。
   >
   >    抱着这样的想法，如下有Pythonic规则：
   >
   >    >1. 公共属性应该没有前导下划线。
   >    >
   >    >2. 如果你的公共属性的名称与保留关键字冲突，附加一个单尾强调你的属性名称。这比缩写或损坏的拼写更好。（然而，尽管有这条规则，“CLS”对于任何已知的变量或参数都是首选的拼写，尤其是对类方法的第一个参数。）
   >    >
   >    >   注意１：参见上面的类方法的参数名推荐。
   >    >
   >    >3. 如果你的类是子类，你不想子类使用某些属性，可以考虑以双下划线开头并且结尾没有下划线的方式命名他们。这将调用Python的mangling算法，类的名字将会mangle成属性名。这有助于避免属性名冲突，如果子类不经意地包含具有相同名称的属性。
   >    >
   >    >   注意一：只能类名用作mangle名，所以当子类选择了同时选择了类名和属性名，将一样会有名字冲突。
   >    >
   >    >   注意二：名字矫正（mangling）可用于某些用途，如调试和```__getattr__()```，不太方便。然而名字矫正算法是有据可查的而且容易使用。
   >    >
   >    >   注意三：不是所有人都喜欢命名矫正，尽量在避免意外的命名冲突和高端调用者的潜在使用之间做出平衡

   ​

4. 公共和内部接口

   任何向后兼容性保证仅适用于公共接口。因此，用户能够清楚地区分公共接口和内部接口才是重要的事情。

   文档化的接口被认为是公开的，除非文档明确声明它们是临时或内部接口，不受通常的向后兼容性保证。所有未记录的接口都应该是内部的。

   为了更好地支持自省，模块应该使用```__all__```属性显式的在他们的公共API中声明命名。将```__all__```设置为一个空列表表示该模块没有公共API.

   即使使用了```__all__```进行了适当的设置，内部接口（包、模块或类）还是应该有一个**前置的下划线**。

   如果任何包含命名空间（包、模块或类）被认为是内部的，则接口也被认为是内部的。

   导入的名称应该始终被视为一个实现细节。其他模块必须不依赖于间接访问这些导入名，除非是模块API的一个明确的记录，如os.path或包的```__init__```模块暴露功能模块。

   ​

##7. 编程建议

>1. 代码的编写应该不依赖于其他Python工具（PyPy，Jython，IronPython、Cython，Psyco，等）的情况下
>
>   例如，不要依赖于CPython就地字符串连接的高效插件（式子为：```a += b or a = a + b```）。这种优化方法即使在CPython中也是有局限的（它只适用于某些类型）。在库的敏感部分，应该使用```''.join()```代替。这将确保字符串连接在不同的实现中以线性时间发生。
>
>2. 在比较单个元素如None时，应该使用```is or is not```，而不是使用相等运算符
>
>3.  另外，当你真的想表示```if x is not None```时，注意```if x```这种写法。例如：在测试一个变量或者参数是否默认为None时可以将其设为其它值，其它的值会有类型（如容器），在布尔语境中可能是false.
>
>4. 使用```is not```而不是```not...is```操作符，虽然这两种表达式在功能上完全相同，但前者更易于阅读且能优先被考虑。
>
>   Yes:
>
>   ```python
>   if foo is not None:
>   ```
>
>   No:
>
>   ```python
>   if not foo is None:
>   ```
>
>5. 当执行排序运算时有很多的比较操作，最好使用六种操作符（```__eq__, __ne__, __lt__, __le__, __gt__, __ge__```）而不是依赖于只能执行某种特定比较的其他代码。
>
>6. 为了节约成本，```functools.total_ordering()```装饰器提供了一个生成缺失比较方法的工具。
>
>   ​
>
>7. [PEP 207](https://www.python.org/dev/peps/pep-0207)表明，自反性规则（reflexivity）是由Python假定的。因此，编译器可以将```y>x与x<y交换，y>=x与x<=y交换```。而且可能会交换```x == y 或 x! = y```的参数。```sort()　和　min()```函数确定使用```<```操作符，而```max()```函数确定使用```>```操作符。然而，最好实现所有六个操作符，这样在其他上下文中不会出现混淆。
>
>8. 总是使用def语句，而不是赋值语句将lambda表达式直接绑定到标识符。
>
>   ```python
>   Yes:
>
>   def f(x): return 2*x
>
>   No:
>
>   f = lambda x: 2*x
>   ```
>
>   第一个形式意味着生成的函数对象的名称是“f”而不是泛型“< lambda >”。赋值语句的使用消除了lambda表达式在对比显式def语句所能提供的唯一好处（即它可以嵌入较大表达式中）。
>
>9. 在Python 2中抛出异常，应该使用```raise valueError('message')```而不是老版的```raise valueError, 'message'```，后者在Python 3中不合法。
>
>   在捕获异常时，尽可能地提及具体的例外，而不是使用一个空的例外：clause。
>
>   如，使用：
>
>   ```python
>   try:
>       import platform_specific_module
>   except ImportError:
>       platform_specific_module = None
>   ```
>
>   **空的except：会捕捉到```SystemExit```和```KeyboardInterrupt```异常**，使得```Control-C```终止代码变得更加困难，而且可能会掩盖其他问题。如果你想捕捉所有程序错误的异常信号，可以使用```except Exception:```，(**空的except相当于```except BaseException```)**。
>
>   很好的限制对空except使用的经验是：
>
>   >1. 如果异常处理程序将被打印出来或记录回溯，至少用户将知道发生了一个错误。
>   >2. 如果代码需要做一些清理工作，那么就让异常向上传播。```try...finally```可以更好地处理这个案子。
>
>   ​
>
>10. 当给捕捉到的异常绑定某个名字时，请使用Python 2.6中添加的显式名称绑定语法：
>
>    ```python
>    try:
>        process_data()
>    except Exception as exc:
>        raise DataProcessingFailedError(str(exc))
>    ```
>
>    这是Python 3中唯一支持的语法，并且避免了与旧的基于逗号的语法相关的歧义问题。
>
>11. 此外，对于所有```try...except```clauses，请将尝试子句限制为所需的绝对最小代码量。同样，这避免了掩盖错误。
>
>    Yes:
>
>    ```python
>    try:
>        value = collection[key]
>    except KeyError:
>        return key_not_found(key)
>    else:
>        return handle_value(value)
>    ```
>
>    No:
>
>    ```python
>    try:
>        # Too broad!
>        return handle_value(collection[key])
>    except KeyError:
>        # Will also catch KeyError raised by handle_value()
>        return key_not_found(key)
>    ```
>
>12. 无论何时获取和释放资源，都应该通过单独的函数或方法调用上下文管理器。例如:
>
>    ```python
>    Yes:
>
>    with conn.begin_transaction():
>        do_stuff_in_transaction(conn)
>        
>        
>    No:
>
>    with conn:
>        do_stuff_in_transaction(conn)
>    ```
>
>    ​
>
>13. 返回语句一致。函数中的所有返回语句都应该返回一个表达式，或者它们都不应该返回。如果任何返回语句返回一个表达式，则没有返回任何值的任何返回语句都应该显式地将此声明为返回无，并且在函数的结尾处应该出现一个显式返回语句（如果可以）。
>
>    ```python
>    Yes:
>
>    def foo(x):
>        if x >= 0:
>            return math.sqrt(x)
>        else:
>            return None
>
>    def bar(x):
>        if x < 0:
>            return None
>        return math.sqrt(x)
>      
>    No:
>
>    def foo(x):
>        if x >= 0:
>            return math.sqrt(x)
>
>    def bar(x):
>        if x < 0:
>            return
>        return math.sqrt(x)
>
>    ```
>
>    ​
>
>14. 字符串方法总是更快，并且使用Unicode字符串共享相同的API
>
>    ​
>
>15. 使用```''.startwith()```和```''.endwith()```而不是字符串切片来检查开头和结尾，如：
>
>    ```python
>    Yes: if foo.startswith('bar'):
>    No:  if foo[:3] == 'bar':
>    ```
>
>16. 对象类型的比较应该总是使用```isinstance()```函数代替直接比较类型。
>
>    ```python
>    Yes: if isinstance(obj, int):
>
>    No:  if type(obj) is type(1):
>
>    ```
>
>    在检测一个对象是不是一个字符串时，要时刻注意他可能是**unicode**类型，在python 2中str和unicode有相同的基类:```basestring```，所以你可以这样做：
>
>    ```python
>    if isinstance(obj, basestring):
>    ```
>
>    注意：在Python 3中，```unicode```和```basestring```将不再存在（只存在```str```），而且一个比特的对象将不再是一种字符串，它只是一个整形序列。
>
>17. 对于序列（字符串、列表、元组），使用空序列为false的判定方法：
>
>    ```python
>    Yes: if not seq:
>         if seq:
>
>    No: if len(seq):
>        if not len(seq):
>    ```

###1.函数注释

随着[PEP 484](https://www.python.org/dev/peps/pep-0484)被接受，函数注释的样式规则正在改变

>1. 为了向前兼容，Python 3代码中的函数注释最好使用[PEP 484](https://www.python.org/dev/peps/pep-0484)语法。
>
>2. 先前在PEP中推荐的注释样式将不在推荐使用
>
>3. 对于希望对函数注释作不同用途的代码，建议对窗体进行注释：
>
>   在文件的顶部；
>
>   ```python
>   # type: ignore
>   ```
>
>   ​
>
>   这告诉类型检查器忽略所有注释。
>
>4. 像linters一样，类型检查器是可选的，单独的工具。默认情况下，Python解释器不应该因为类型检查而发出任何消息，也不应该基于注释改变它们的行为。
>
>5. 不希望使用类型检查器的用户可以忽略它们。然而，预计第三方库包的用户可能希望在这些包上运行类型检查器。为此， [PEP 484](https://www.python.org/dev/peps/pep-0484) 建议使用存根文件:```.pyi```文件，它由类型检查器读取，以选择相应的```.py```文件。

### 2.变量注释

[PEP 526](https://www.python.org/dev/peps/pep-0526)引入变量注释，它们的样式建议与上面描述的函数注释类似：

> 1. 对模块级变量、类和实例变量以及本地变量的注释应该在冒号之后有一个空格。
>
> 2. 冒号前应该没有空格。
>
> 3. 如果赋值右边，那么等号应该两边都有一个空格。
>
>    ```python
>    Yes:
>
>    code: int
>
>    class Point:
>        coords: Tuple[int, int]
>        label: str = '<unknown>'
>          
>          
>    No:
>
>    code:int  # No space after colon
>    code : int  # Space before colon
>
>    class Test:
>        result: int=0  # No spaces around equality sign
>    ```
>
> 4. 尽管Python 3.6接受了PEP 526，但是变量注释语法是Python所有版本的存根文件中的首选语法（详情见 [PEP 484](https://www.python.org/dev/peps/pep-0484) ）















