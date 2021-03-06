## Python基础
**输入输出**

`print()`方法可以在屏幕上输出指定字符串。

多个字符串可用逗号","隔开。`print()`会依次打印字符串，遇到逗号时，会输出一个空格。

`print()`可以打印整数，或者计算结果：
    
    >>> print(1)
    1
    >>> print(1+2)
    3

`input()`方法可以让用户输入字符串，并存入到变量中。

    >>> str = input()
    String
    >>> str
    `String`

打印变量的内容可以直接输入变量名，也可以使用`print()`方法：

    >>> print(str)
    `String`

**数据类型和变量**

Python中能够直接处理的数据类型有：整数，浮点数，字符串,布尔值 ，空值等。 
  
字符串使用单引号`''`或者双引号`""`包裹，如果字符串内部含有`'`或者`"`，可使用`\`转义字符标识。    

`\n`表示换行，`\r`表示制表符，`\`本身也需要转义，`\\`表示的字符就是`\`。    

如果字符串中有多个字符都需要转义，需要加入很多`\`，为了简化，Python允许使用`r''`表示`''`内部的字符默认不转义：

    >>> print('\\\t\\')
    \    \
    >>> print(r`\\\t\\')
    \\\t\\ 

如果字符串内部含有很多换行，用`\n`写在一行里不好阅读，为了简化，Python允许使用`'''...'''`的格式表示多行内容：

    >>> print('''line1
    ... line2
    ... line3''')
    line1
    line2
    line3

在命令行中提示符由`>>>`变为`...`，提示可以接着上一行输入。如果在程序中，就是：

    print('''line1
    line2
    line3''')

多行字符串`'''...'''`还可以在前面加上`r`使用。

布尔值可以使用`and`、`or`、`not`运算。

空值是Python里的一个特殊值，用`None`表示，不能理解为0。

Python中的变量，变量名必须是大小写英文、数字和`_`的组合，不能用数字开头。Python的变量本身类型不固定，称为动态语言。

`/`除法计算的结果是浮点数。`//`地板除，结果为整数。`%`余数运算。

**字符串和编码**

`ord()`获取字符的字符码。    
`chr()`把编码转换为对应的字符。

     >>> ord('A')
     65
     >>> chr('65')
     'A'

如果知道字符的编码，还可以用十六进制这么写`str`:

    >>> '\u4e2d\u6587'
    '中文'

Python的字符串类型是`str`，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把`str`转换为以字节为单位的`bytes`。    

Python对`bytes`类型的数据用带`b`前缀的单引号或双引号表示：

    x = b'ABC'

以Unicode表示的`str`通过`encode()`方法可以编码为指定的`bytes`：

    >>> 'ABC'.encode('ascii')
    b'ABC'
    >>> '中文'.encode('utf-8')
    b'\xe4\xb8\xad\xe6\x96\x87'

纯英文的`str`可以用ASCII编码为`bytes`，内容是一样的，含有中文的`str`可以用UTF-8编码为`bytes`。含有中文的`str`无法用ASCII编码，因为中文编码的范围超过了ASCII编码的范围。    

在`bytes`中，无法显示为ASCII字符的字节，用`\x##`显示

反过来，如果我们从网络或者磁盘上读取了字节流，那么独到的数据就是`bytes`。要把`bytes`变为`str`,就需要用`decode()`方法：

    >>> b'ABC'.decode('ascii')
    'ABC'

要计算`str`包含多少个字符，可以用`len()`方法。

`len()`方法计算的是`str`的字符数，如果换成`bytes`，`len()`计算的就是字节数。（一个中文字符在UTF-8编码后通常占用3个字节，而英文字符只占用1个字节）

源代码中包含中文时，在保存代码时，就需要使用UTF-8编码保存。当Python解释器读取源代码时，为了让他按照UTF-8编码读取，通常在开头加上：

    #!/usr/bin/env python3
    # -*- coding: utg-8 -*-

第一行注释是为了告诉Linux/Mac OS系统，这是一个Python可执行程序，Windows系统会忽略这个注释。

第二行注释是为了告诉Python解释器，按照UTF-8编码读取源程序，否则源代码中的中文输出可能会乱码。

Python中，采用的格式化方式和C语言中一致，用`%`实现。

    >>> 'Hello,%s' % 'world'
    'Hello, world‘
    >>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
    'Hi, Michael, you have $1000000.'

在字符串内部，`%s`表示用字符串替换，`%d`表示用整数替换，有几个`%?`占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个`%?`，括号可以省略。

常见的占位符：

`%d` 整数     
`%f` 浮点数     
`%s` 字符串     
`%x` 十六进制整数     

其中，格式化整数和浮点数还可以指定是否补0和整数与小数的位数：

    >>> '%2d-%02d' % (3, 1)
    ' 3-01'
    >>> '%.2f' % 3.1415926
    '3.14'

如果不确定应该用什么，`%s`永远起作用，它会把任何数据类型转换为字符串。

如果字符串中`%`是一个普通的字符，那就需要转义，用`%%`来表示一个`%`。

**list和tuple**

**list-列表***

list是一种有序的集合，可以随时添加和删除其中的元素。

	>>> classmates=['Michel','Bob','Tracy']
	>>> classmates
	['Michael','Bob','Tracy']

变量`classmates`就是一个list。用`len()`可以得到这个list的个数。

可以用索引来访问list中的元素，索引从0开始。要获取最后一个元素，还可以使用`-1`作为索引，直接获取到最后一个元素。同理，倒数第二、第三个元素可以用索引`-2`、`-3`来获取。

list是一个可变的有序表，可以使用`append()`方法往list中追加元素到末尾。也可以使用`insert()`方法把元素插入到指定的位置。要删除list末尾的元素，用`pop()`方法。要删除指定位置的元素用`pop(i)`方法，`i`是索引位置。要把某个元素替换成别的元素，可以直接赋值给对应的索引位置。

list里面的元素的数据类型可以不同。list的元素也可为另一个list。(list嵌套的写法类似于多维数组。)如果一个list中一个元素也没有，就是一个空的list，它的长度为0。

**tuple-元组**

tuple和list非常类似，但是tuple一旦初始化，就不能修改。

tuple可以使用索引获取对应元素，但是不能赋值成另外的元素。**当定义tuple时，在定义的时候，tuple的元素就必须被确定下来**

如果定义一个空的tuple，可以写成`()`。Python规定，定义只有一个元素的tuple时，必须加一个逗号`,`来消除歧义。(因为`()`既可以表示tuple,又可以表示数学公式中的小括号。Python在显示中也会加一个`,`避免歧义。

tuple包含list作为元素时，list的元素可变。

**条件判断**

`if`语句。`else`后需要添加冒号`:`。`elif`是`else if`的缩写。

	if <条件>:
		<执行>
	elif <条件>：
		<执行>
	else:
		<执行>

`input()`方法返回的数据类型是`str`。

	s = input('birth:')
	birth = int(s);
	if birth < 2000:
		print('00前')
	else:
		print(`00后`)

**循环**

`for...in`循环

	names = ['Michael','Bob','Tracy']
	for name in names:
		print(name)

执行这段代码，会依次打印`names`的每一个元素：

	Micheal
	Bob
	Tracy

`range()`方法，可以生成一个整数序列。`range(5)`生成的序列就是从0开始小于5的整数。

`while`循环
	
	sum = 0
	n = 99
	while n>0:
		sum = sum + n
		n = n - 2
	print(sum)

`break`，在循环中，`break`可以提前退出循环。

`continue`，在循环中，`continue`可以跳过当前这次循环，直接开始下一次循环。

**dict和set**

字典：dict全称dictionary，在其他语言中也称为map，使用键-值存储，具有极快的查找速度。

	>>> d = {'Michael':95,'Bob':75,'Tracy':85}
	>>> d['Michael']
	95

`list`越大，查找越慢。`dict`不会随着字典大小的增加而变慢。

可以通过`in`判断key是否存在：

	>>> 'Thomas' in d
	False

也可以通过dict提供的`get`方法，如果key不存在，可以返回`None`，或者自己指定的Value:

	>>> d.get('Thoms')
	>>> d.get('Thoms',-1)
	-1

Python在返回`None`时，交互命令行不显示结果。

要删除一个key，用`pop(key)`方法，对应的value也会从dict中删除、

和`list`比较，`dict`有一下几个特点：
- 查找和插入的速度极快，不会随着key的增加而变慢；
- 需要占用大量的内存，内存浪费多。

而`list`正好相反：
- 查找和插入的时间随着元素的增加而增加；
- 占用空间小，浪费内存多。

`dict`的key必须是不可变对象。dict根据key来计算value的存储位置，这个算法称为哈希算法（Hash）。要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心的作为key。而list是可变的，就不能作为key。

`set`和`dict`类似，也是一组key的集合，但不存储value。由于key不能重复，所以在set中没有重复的key。

要创建一个set，需要提供一个list作为输入集合：

	>>> s = set([1,2,3])
	>>> s
	{1,2,3}

通过`add(key)`方法可以添加元素到set中，可以重复添加，但不会有效果。

通过`remove(key)`方法可以删除元素。

set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：

	>>> s1 = set([1,2,3])
	>>> s2 = set([2,3,4])
	>>> s1 & s2
	{2,3}
	>>> s1 | s2
	{1,2,3,4}

set和dict唯一的区别仅在于没有存储对应的value，但是set和dict原理一样，因此也不可以存入可变对象。

`list`的`sort()`方法可以对list进行排序，改变原有list。

`str`的`replace('1','2')`方法可以对str中的元素进行替换，原有str不发生改变。

**函数**

`abs`绝对值。

可以在交互式命令行通过`help(abs)`查看`abs`函数的帮助信息。

`abs()`有且仅有1个参数，但给出了2个。

`max()`函数可以接收任意多个参数，并返回最大的那个。

`int()`函数可以把其他类型数据转换为整数。

	>>> int('123')
	123
	>>> int(12.34）
	12
	>>> float('12.34')
	12.34
	>>> str(1.23)
	'1.23'
	>>> bool(1)
	True
	>>> bool('')
	False

函数名就是指向一个函数的引用，完全可以把函数名赋给一个变量，相当于给这个函数骑了一个"别名"：

	>>> a = abs # 变量a指向abs函数
	>>> a(-1) # 也可以通过a调用abs函数
	1

`hex()`函数，把一个整数转换成16进制表示字符串

**定义函数**

在Python中，定义一个函数要使用`def`语句，依次写出函数名、括号、括号中的参数和冒号`:`，然后在缩进块中编写函数体，函数的返回值用`return`语句返回。

自定义一个求绝对值的`my_abs`函数:

	def my_abs(x):
		if x >= 0:
			return x
		else:
			return -x

函数执行到`return`时，就执行完毕了，并将结果返回。如果没有`return`语句,函数执行完毕后也会返回结果,只是结果为`None`。

`return None`可以简写为`return`。

在Python交互环境中定义函数时,注意Python会出现`...`的提示。函数定义结束后需要按两次回车重新回到`>>>`提示符下。

如果已经把`my_abs()`的函数定义保存为`abstest.py`文件了，那么，可以在该文件的当前目录下启动Python解释器，用`from abstest import my_abs`来导入`my_abs()`函数，注意`abstest`是文件名。

空函数，定义一个什么事也不做的空函数，可以用`pass`语句

`pass`语句什么也不做。可以用来作为占位符，比如现在还没想好怎么写函数代码，就可以先放一个`pass`，让代码运行起来。缺少了`pass`代码运行就会有语法错误。

参数检查。

	def my_abs(x):
		if not isinstance(x,(int,float)):
			raise TypeError('bad operand type')
		if x >= 0:
			return x
		else:
			return -x

添加参数检查后，如果传入错误的参数类型，函数就可以抛出一个错误

返回多个值

	import math
	
	def mov(x,y,step,angle=0):
		nx = x + step * math.cos(angle)
		ny = y - step * math.sin(angle)
		return nx, ny

`import math`语句表示导入`math`包，并允许后续代码引用`math`包里的`sin`、`cos`等函数。

然后，我们可以同时获得返回值：

	>>> x, y = move(100, 100, 60, math.pi / 6)
	>>> print(x, y)
	151.96152422706632 70.0

但实际上，Python函数返回的仍然是单一值。多个返回值返回的是一个tuple。但在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置给对应的值。

**函数的参数**

`power(x)`函数中，参数`x`就是一个位置参数。当调用`power()`函数时，必须传入参数`x`。多个参数的函数，多个参数都是位置参数，调用函数时，传入的值按照顺序依次赋值。

默认参数

	def power(x, n=2):
		s = 1
		while n>0
			n = n - 1
			s = s * x
		return s

由于经常计算x的平方，所以，把第二个参数n的默认值设定为2。

调用函数时，如果不按顺序提供部分默认参数，需要把参数名写上。比如`enroll('Adam', 'M', city = 'Tianjin')`。

定义默认参数时，默认参数必须指向不变对象。 

**可变参数**的传入参数个数是可变的。

	def calc(numbers):
		sum = 0
		for n in numbers:
			sum = sum + n * n
		return sum

调用的时候，需要先组装出一个list或者tuple,如果利用可变参数，调用函数方式可以简化：

	def calc(*numbers):
		...

定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个`*`号。在函数内部，参数`numbers`接收到的是一个tuple,因此，函数代码完全不变。但是调用改参数时，可以传入任意个参数，包括0个。

如果已有list或tuple，Python允许在list或tuple前面加一个`*`号，把list或tuple的元素变成可变参数传进去。

**关键字参数**扩展函数的功能，除开必选参数外，还可以利用关键字参数。关键字参数也在dict前面加上`**`将dict变成关键字参数传入。

	def person(name, age, **kw):
		print('name:', name, 'age:', age, 'other:',kw)

对于关键字参数，函数的调用者可以传入任意不受限制的关键字参数。至于到底传入了哪些，就需要在函数内部通过`kw`检查。

	def person(name, age, **kw):
		if 'city' in kw:
			# 有city参数
			pass
		if 'job' in kw:
			# 有job参数
			pass
		print('name:', name, 'age:', age, 'other:', kw)

如果要限制关键字参数的名字，就可以用**命名关键字**参数

	def person(name, age, *, city, job):
		print(name, age, city, job)

和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。

调用方式如下：
	
	>>> person('Jack', 24, city='Beijing', job='Engineer')
	Jack 24 Beijing Engineer

如果函数定义已经有了一个可变参数，后面跟着的命名关键字参数就不再需要分隔符`*`了。

命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错。

命名关键字参数可以有缺省值。

在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名参数，这五种参数都可以组合使用。但是参数定义的顺序必须是：
> 必选参数、默认参数、可变参数、命名关键字参数、关键字参数。

**递归函数**

阶乘：

	def fact(n):
		if n=1:
			return 1
        return n * fact(n - 1)

使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈(stack)这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。

解决递归调用栈溢出的方法是通过`尾递归`优化，事实上尾递归和循环的效果是一样的，所以，把循环看成是一中特殊的尾递归函数也是可以的。

尾递归是指，在函数返回的时候，调用函数本身，并且在return语句中不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

**大多数编程语言没有针对尾递归做优化，Python解释器也是。所以，即使把上面的函数改成尾递归方式，也会导致栈溢出**






## 练习
递归练习： [汉诺塔](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431756044276a15558a759ec43de8e30eb0ed169fb11000#0)

## Tips    
1.`.py`文件的执行：    
`.py`文件在Win上不能直接运行，但在Mac和Linux上可以。
在`.py`文件的第一行加上特殊的注释：

     #!/usr/bin/env python3

然后通过命令给`.py`文件执行权限：

    chmod a+x filename.py

2.Python是大小写敏感的。

**Thanks**    

[Python教程--廖雪峰](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001431658624177ea4f8fcb06bc4d0e8aab2fd7aa65dd95000)
