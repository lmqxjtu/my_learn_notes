# python记录

## 1、列表、元组、字典

### 列表

添加

```shell
.append 往列表的结尾处添加一个元素
.insert 通过下标往列表的指定位置添加一个元素
.expend 往列表的结尾处 添加多个元素
```

删除

```shell
.remove 删除列表中的指定元素
.pop 删除/弹出指定下标位置的元素，默认删除列表中最后一个元素
.clean 删除列表中所有数据
.del 是个语句，del 列表名[]/del 列表名
```

查询

```shell
.index 在列表找到第一个匹配的元素，返回下标位置
.count 查询指定元素的数量
```

修改

```shell
用下标找到元素，重新赋值
li = [1,2,3,4,5,6]
li[2] = 33 # 修改一个元素
li[3],li[4],li[5] = 44,55,66 # 修改多个元素
```

### 元组

https://www.runoob.com/python/python-tuples.html

### 字典

https://www.runoob.com/python/python-dictionary.html

## 2、python直接赋值、浅拷贝、深度拷贝

- **直接赋值：**其实就是对象的引用（别名）。
- **浅拷贝(copy)：**拷贝父对象，不会拷贝对象的内部的子对象。
- **深拷贝(deepcopy)：** copy 模块的 deepcopy 方法，完全拷贝了父对象及其子对象。

**字典浅拷贝实例**

```shell
>>>a = {1: [1,2,3]}
>>> b = a.copy()
>>> a, b
({1: [1, 2, 3]}, {1: [1, 2, 3]})
>>> a[1].append(4)
>>> a, b
({1: [1, 2, 3, 4]}, {1: [1, 2, 3, 4]})
```

深度拷贝需要引入 copy 模块：

```shell
>>>import copy
>>> c = copy.deepcopy(a)
>>> a, c
({1: [1, 2, 3, 4]}, {1: [1, 2, 3, 4]})
>>> a[1].append(5)
>>> a, c
({1: [1, 2, 3, 4, 5]}, {1: [1, 2, 3, 4]})
```

**解析**

1、**b = a:** 赋值引用，a 和 b 都指向同一个对象。

![img](https://www.runoob.com/wp-content/uploads/2017/03/1489720931-7116-4AQC6.png)

**2、b = a.copy():** 浅拷贝, a 和 b 是一个独立的对象，但他们的子对象还是指向统一对象（是引用）。

![img](https://www.runoob.com/wp-content/uploads/2017/03/1489720930-6827-Vtk4m.png)

**b = copy.deepcopy(a):** 深度拷贝, a 和 b 完全拷贝了父对象及其子对象，两者是完全独立的。

![img](https://www.runoob.com/wp-content/uploads/2017/03/1489720930-5882-BO4qO.png)

**更多实例**

以下实例是使用 copy 模块的 copy.copy（ 浅拷贝 ）和（copy.deepcopy ）:

**实例**

```shell
#!/usr/bin/python
# -*-coding:utf-8 -*-
 
import copy
a = [1, 2, 3, 4, ['a', 'b']] #原始对象
 
b = a                       #赋值，传对象的引用
c = copy.copy(a)            #对象拷贝，浅拷贝
d = copy.deepcopy(a)        #对象拷贝，深拷贝
 
a.append(5)                 #修改对象a
a[4].append('c')            #修改对象a中的['a', 'b']数组对象
 
print( 'a = ', a )
print( 'b = ', b )
print( 'c = ', c )
print( 'd = ', d )
```

以上实例执行输出结果为：

```
('a = ', [1, 2, 3, 4, ['a', 'b', 'c'], 5])
('b = ', [1, 2, 3, 4, ['a', 'b', 'c'], 5])
('c = ', [1, 2, 3, 4, ['a', 'b', 'c']])
('d = ', [1, 2, 3, 4, ['a', 'b']])
```

## 3、列表、元组、字典、set区别

![image-20200811200647589](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200811200647589.png)

#### 1、列表

列表是处理一组有序的数据结构，可以读写，添加和删除，或者搜索列表里的元素。因为可以添加和删除，所以称为可变的数据类型，即这种类型是可以被改变的，并且列表可以嵌套。

```shell
res = [1,2,'yihang']
#增加元素：extend和append
res.append(1)
res.extend('6')
#删除元素：del，pop，切片，remove
del res[1]
res.pop(1)#删除该位置上的元素，没有指定则是最后一个元素
res = res[:2]+res[3:]#切片
res.remove(2)#删除指定值的元素
#更改元素
res[1] = 100 #
#查元素
print(res[0])
print(res[1]) 
```

注意：如果想添加的一个元素是一个列表，那么append是将这个这个列表作为一个元素添加进来，而extend是将列中的元素一个一个添加进去

#### 2、元组

元组跟列表非常相似，用（）来表示，但是元组是不可变的，不能修改元组。元组可以嵌套。

```shell
>>> zoo=('wolf','elephant','penguin')
>>> zoo.count('penguin')
1
>>> zoo.index('penguin')
2
>>> zoo.append('pig')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'append'
>>> del zoo[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object doesn't support item deletion

```

#### 3、字典

字典是通过键值对的方式就数据存储下来，键必须是唯一的键值对在字典中以这样的方式标记：d = {key1 : value1, key2 : value2 }。注意它们的键/值对用冒号分割，而各个对用逗号分割，所有这些都包括在花括号中。另外，记住字典中的键/值对是没有顺序的。如果你想要一个特定的顺 序，那么你应该在使用前自己对它们排序

```shell
dict1={'zhang':'张家辉','wang':'王宝强','li':'李冰冰','zhao':'赵薇'}
#字典的操作，添加，删除，打印
dict1['huang']='黄家驹'
del dict1['zhao']
for firstname,name in dict1.items():
    print firstname,name
```

结果

```shell
结果：
li 李冰冰
wang 王宝强
huang 黄家驹
zhang 张家辉
```

定义dict.fromkeys(range(30）,value) 可以形成一个双列的列表相当于java中的map，这个键值对列表存储子dict中取键可以通过循环 for eachkey in dict.keys(): 把所有的键赋值到eachkey中去取值可以通过循环 for eachkey in dict.values(): 把所有的值赋值到eachkey中去取键值对站线程元组的形式 for eachItem in dict.item(): 把所有的键值对转化成元组的方式赋值给eachItem中

#### 4、集合

- 特性：与字典类似，但只包含键，而没有对应的值，包含的数据不重复。
- 创建：s = set(list or tuple or string)。重复的值在集合中只存在一个。如：
  　　　　列表list：s = set([1,2,3,3]) ->s = set([1,2,3])
  　　　　元组tuple：s = set((1,2,3)) ->s = set([1,2,3])
  　　　　字符串string：s = set(“abc”) ->s = set([“a”,“b”,“c”])

## 4、python字符串内置方法

### 1、大小写转换

### ① capitalize()

capitalize() #字符串首字母大写

```ruby
>>> str0 = 'hello World'
>>> str0.capitalize()
'Hello world'
```

### ②upper()， lower()

upper() #将字符串的所有小写字符转化为大写`
lower() #将字符串的所有大写字符转化为小写

```ruby
>>> str1 = 'Hello World'
>>> str1.upper()
'HELLO WORLD'
>>> str1.lower()
'hello world'
```

### ③swapcase()

swapcase() #将字符串中的大写字符改为小写，小写字符改为大写

```ruby
>>> str1 = 'Hello World'
>>> str1.swapcase()
'hELLO wORLD'
```

### 2、内容判断

### ①startswith()，endswith()

startswith() #判断字符串是否以指定参数开始，返回True或False
endswith() #判断字符串是否以指定参数结束，返回True或False

```shell
>>> str1 = 'Hello World'
>>> str1.startswith('h')
False
>>> str1.endswith('d')
True
```

tip:判断时大小写是要区分的，可以添加第二、三个参数来限定范围。

### ②isupper()，islower()

isupper() #如果字符串中的字母均为大写返回True，否则返回 False
islower() #如果字符串中的字母均为小写返回True，否则返回 False

```ruby
>>> str1 = 'Hello World'
>>> str2 = '123asdxfgs...'
>>> str1.isupper()
False
>>> str2.islower()
True
```

tip:字符串中可以含数字和特殊字符

### ③isalpha()，isdigit()，isalnum()

isalpha() #如果字符串中只包含字母返回 True，否则返回 False
isdigit() #如果字符串中只包含数字返回 True，否则返回 False
isalnum() #如果字符串中只包含字母或数字返回 True，否则返回 False

```ruby
>>> str3 = '123456789'
>>> str2 = '123asdxfgs...'
>>> str3.isalpha()
False
>>> str3.isdigit()
True
>>> str2.isalnum()
False
```

### 3、内容查找

### find()，rfind()，index()，rindex()

find() #查找指定参数是否在字符串中，查找成功返回字符下标，失败则返回-1
rfind() #功能和find()一致，但查找方向从右边开始
index() #和find功能一样，但查找失败会产生错误
rindex() #功能和index()一致，但查找方向从右边开始

```ruby
>>> str2 = '123asdxfgs...'
>>> str2.find('123')
0
>>> str2.find('1234')
-1
>>> str2.index('x')
6
>>> str2.index('b')
Traceback (most recent call last):
  File "<pyshell#33>", line 1, in <module>
    str2.index('b')
ValueError: substring not found
>>> str4 = 'test88ooo88'
>>> str4.find('88')
4
>>> str4.rfind('88')
9
```

### 4、替换、添加、删除

### ①strip()，lstrip()，rstrip()

strip() #默认删除字符串前后的空格，若加上参数，则改为删除字符串前后的该参数`
 `lstrip() #去掉字符串前面的空格，若加上参数，则改为删除字符串前的该参数`
 `rstrip() #删除字符串末尾的空格，若加上参数，则改为删除字符串后的该参数

```ruby
>>> str5 = 'content'
>>> str5.lstrip()
'content'
>>> str5.rstrip()
'content'
>>> str5.strip()
'content'
>>> str5.strip('t')
'content'
>>> str6 = '123and123'
>>> str6.strip('123')
'and'
>>> str6.lstrip('123')
'and123'
```

tip:`strip()`只能删除字符串前后的指定内容，不能误解为删除该字符串中所有的该字符，若想实现此功能，建议使用`replace()`。

### ②replace()

replace(old,new[,count]) #将字符串中的所有old用new替换，若使用count参数，则替换次数不超过count次。

```ruby
>>> str7 = 'xxHxexlxxlxo Wxxxxorld'
>>> str7.replace('x', '')
'Hello World'
>>> str7.replace('x', 'A')
'AAHAeAlAAlAo WAAAAorld'
>>> str7.replace('x', 'A', 1)
'AxHxexlxxlxo Wxxxxorld'
```

### ③format()

format() #格式化字符串

```ruby
>>> "姓名：{}， 性别：{}".format('张三','男')
'姓名：张三， 性别：男'
>>> "姓名：{a}， 性别：{b}".format(b='男',a='张三')
'姓名：张三， 性别：男'
```

tip:常与{}一起使用，参数个数由自己决定。

### ④join()

join() #以原字符串作为分隔符，插入到参数中每个字符之间。

```ruby
>>> str_break = 'xx'
>>> str_break.join('AB')
'AxxB'
>>> str_break.join('ABC')
'AxxBxxC'
```

### 5、分割

### ①split()， rsplit()

split() #以第一个参数为分隔符分割字符串,返回一个列表
rsplit() #和split()功能相同，但是从右边开始分割

```ruby
>>> str8 = 'AxxBxxC'
>>> str8.split('xx')
['A', 'B', 'C']
>>> str8.split('x')
['A', '', 'B', '', 'C']
>>> str8.split('xxx')
['AxxBxxC']
```

tip:可以加上第二个参数限制次数。

```ruby
>>> str8.split('xx', 1)
['A', 'BxxC']
```

### ②partition()，rpartition()

partition() #将字符串从参数处分成'参数前'，'参数'，'参数后'三段，返回一个三元元组
 rpartition() #功能和partition()一致，但从右边开始

```ruby
>>> str8 = 'AxxBxxC'
>>> str8.partition('xx')
('A', 'xx', 'BxxC')
>>> str8.rpartition('xx')
('AxxB', 'xx', 'C')
>>> str8.partition('zzz')
('AxxBxxC', '', '')
```

tip:若找不到参数，则返回`('字符串', '', '')`

### 六. 计数

### count()

count() #参数为字符串的一个子串，返回该子串出现的次数

```ruby
>>> str8 = 'AxxBxxC'
>>> str8.count('xx')
2
```

tip:可以加上第二，三个参数来限定范围。

### 七、其他

### center()

center() #将某字符串居中，并以指定字符填充至指定长度。

```ruby
>>> "test".center(20, '*')
'********test********'
```

## 5、python的函数、类、模块、包、库

![image-20200811205347783](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200811205347783.png)

### 一、函数

　　一个拥有名称、参数和返回值的代码块。

　　需要主动调用，否则不会执行，可以通过参数和返回值与其它程序进行交互

### 二、类

　　用来描述具有相同的属性和方法的对象集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例

　　方法：类中定义的函数

　　类变量（属性）：类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体（方法）之外。类变量通常不作为实例变量使用，类变量也称作属性

　　实例化：创建一个类的实例，类的具体对象

### 三、模块

　　Python模块（Module），就是一个Python文件，以.py结尾，包含了Python对象定义和Python语句

　　模块可以让你更有逻辑的组织你的代码段

　　将相关的代码分配到一个模块里，可以让你的代码更好用，更易懂

　　模块内能定义函数，类，和变量，模块里也能包含可执行的代码

### 四、包

　　在Python语言中，一个.py文件就可以叫做一个模块(model)。如果a.py中有一个功能在b.py中被引用，那么a.py就算是一个模块。在Python中不止有模块，还有另外一个概念，叫做包（package），包是作为目录存在的，包的另外一个特点就是文件中有一个__init__.py文件，包可以包含模块，也可以包含包

### 五、库

​       具有相关功能模块的集合。这也是Python的一大特色之一，即具有强大的标准库、第三方库以及自定义模块。

## 6、内嵌函数和闭包

https://blog.csdn.net/beautiful77moon/article/details/87023824

### 1.内嵌函数：在函数中定义函数

```shell

#代码段1
>>> def fun1():
	print('外层函数正在被调用')
	def fun2():
		print('内层函数正在被调用')
 
>>> fun1()
外层函数正在被调用
 
#代码段2
>>> def fun1():
	print('外层函数正在被调用')
	def fun2():
		print('内层函数正在被调用')
	fun2()
	
>>> fun1()
外层函数正在被调用
内层函数正在被调用
 
>>> fun2()    #内嵌函数直接被调用
Traceback (most recent call last):
  File "<pyshell#12>", line 1, in <module>
    fun2()
NameError: name 'fun2' is not defined

```

注：①内嵌函数不能再外层函数被调用的过程中自动被调用 ②内部函数不能被外部直接使用，需要通过其外层函数的调用发挥作用

### 2.闭包：出现在嵌套函数中，指的是内层函数引用到了外层函数的变量，就形成了闭包

```shell
>>> def funX(x):
	def funY(y):
		return x*y
	return funY     #返回内层函数
 
>>> funX(2)(5)      #对闭包的调用
10
 
#注：
>>> m=funX(2)       #只对外层函数进行了调用
>>> type(m)         #所以函数的返回类型及m的类型为function
<type 'function'>
>>> m(3)            #继续对内层函数进行调用
6
```

### 3.在函数内部修改全局变量的值：global关键字

```shell
>>> num=3
>>> def count():
	global num
	num=5
	print(num)
 
>>> count()
5
>>> num
5
```

注：能不直接访问全局变量尽量不要访问，如需使用全局变量可以使用函数进行传参。

### 4.在内嵌函数中修改外部函数的局部变量：nonlocal关键字

```shell
>>> def fun1():
	x=5
	def fun2():
		nonlocal x
		x+=7
		return x
	return fun2
 
>>> fun1()()
12
```

### 练习

**练习1：以下是闭包的一个例子，目测一下会打印什么内容？**

```shell
#例子1：
def funX():
	x=5
	def funY():
		nonlocal x
		x+=1
		return x
	return funY
a=funX()
print(a())
print(a())
print(a())
 
#例子2：
def funX():
	x=5
	def funY():
		nonlocal x
		x+=1
		return x
	return funY
a=funX()
print(a())
a=funX()
print(a())
a=funX()
print(a())
```

```shell
#例子1结果：
6
7
8
#例子2结果：
6
6
6
```

注：例子2中局部变量x在每次调用时都被重新赋值了，所以结果都是6。但是例子1中，a=funX()的时候，只要a变量没有被重新赋值，funX()就没有被释放，也就是说局部变量x没有被重新初始化。

注：当全局变量不适用时，可以考虑使用闭包更安全更稳定

## lambda表达式

**三个特性**

lambda函数有如下特性：

lambda函数是匿名的：所谓匿名函数，通俗地说就是没有名字的函数。lambda函数没有名字。

lambda函数有输入和输出：输入是传入到参数列表argument_list的值，输出是根据表达式expression计算得到的值。

lambda函数一般功能简单：单行expression决定了lambda函数不可能完成复杂的逻辑，只能完成非常简单的功能。由于其实现的功能一目了然，甚至不需要专门的名字来说明。

下面是一些lambda函数示例：

lambda x, y: x*y；函数输入是x和y，输出是它们的积x*y
lambda:None；函数没有输入参数，输出是None
lambda *args: sum(args); 输入是任意个数的参数，输出是它们的和(隐性要求是输入参数必须能够进行加法运算)
lambda **kwargs: 1；输入是任意键值对参数，输出是1



例1:传入多个参数的lambda函数

```
def sum(x,y):
      return x+y
```

用lambda来实现：

```
p = lambda x,y:x+y
print(p(4,6))
```

例2：传入一个参数的lambda函数

```
a=lambda x:x*x
print(a(3))       # 注意：这里直接a(3)可以执行，但没有输出的，前面的print不能少 
```

例3：多个参数的lambda形式：

```
a = lambda x,y,z:(x+8)*y-z
print(a(5,6,8))
```

1，lambda 函数不能包含命令，

2，包含的表达式不能超过一个。

### filter

**filter()** 函数用于过滤序列，过滤掉不符合条件的元素，返回由符合条件元素组成的新列表。

该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判断，然后返回 True 或 False，最后将返回 True 的元素放到新列表中。

> **注意:** Pyhton2.7 返回列表，Python3.x 返回迭代器对象，具体内容可以查看：[Python3 filter() 函数](https://www.runoob.com/python3/python3-func-filter.html)

#### 语法

以下是 filter() 方法的语法: 

function筛选条件，iterable筛选对象

```
filter(function, iterable)
```

#### 参数

- function -- 判断函数。
- iterable -- 可迭代对象。

#### 返回值

返回列表。

#### 实例

以下展示了使用 filter 函数的实例：

**过滤出列表中的所有奇数：**

```shell
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
def is_odd(n):
    return n % 2 == 1
 
newlist = filter(is_odd, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(newlist)
```

输出结果 ：

```
[1, 3, 5, 7, 9]
```

#### 过滤出1~100中平方根是整数的数：

```shell
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
import math
def is_sqr(x):
    return math.sqrt(x) % 1 == 0
 
newlist = filter(is_sqr, range(1, 101))
print(newlist)
```

输出结果 ：

```
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```



### Python map() 函数

#### 描述

**map()** 会根据提供的函数对指定序列做映射。

第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

#### 语法

map() 函数语法：

```
map(function, iterable, ...)
```

#### 参数

- function -- 函数
- iterable -- 一个或多个序列

#### 返回值

Python 2.x 返回列表。

Python 3.x 返回迭代器。

#### 实例

以下实例展示了 map() 的使用方法：

```shell
>>>def square(x) :            # 计算平方数
...     return x ** 2
... 
>>> map(square, [1,2,3,4,5])   # 计算列表各个元素的平方
[1, 4, 9, 16, 25]
>>> map(lambda x: x ** 2, [1, 2, 3, 4, 5])  # 使用 lambda 匿名函数
[1, 4, 9, 16, 25]
 
# 提供了两个列表，对相同位置的列表数据进行相加
>>> map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
[3, 7, 11, 15, 19]
```

## 异常处理

### 异常

https://www.runoob.com/python/python-exceptions.html

python提供了两个非常重要的功能来处理python程序在运行中出现的异常和错误。你可以使用该功能来调试python程序。

- 异常处理: 本站Python教程会具体介绍。
- 断言(Assertions):本站Python教程会具体介绍。

try的工作原理是，当开始一个try语句后，python就在当前程序的上下文中作标记，这样当异常出现时就可以回到这里，try子句先执行，接下来会发生什么依赖于执行时是否出现异常。

- 如果当try后的语句执行时发生异常，python就跳回到try并执行第一个匹配该异常的except子句，异常处理完毕，控制流就通过整个try语句（除非在处理异常时又引发新的异常）。
- 如果在try后的语句里发生了异常，却没有匹配的except子句，异常将被递交到上层的try，或者到程序的最上层（这样将结束程序，并打印默认的出错信息）。
- 如果在try子句执行时没有发生异常，python将执行else语句后的语句（如果有else的话），然后控制流通过整个try语句。

![image-20200812105747000](C:\Users\limengqian\AppData\Roaming\Typora\typora-user-images\image-20200812105747000.png)

### 断言

https://www.runoob.com/python3/python3-assert.html

Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。

断言可以在条件不满足程序运行的情况下直接返回错误，而不必等待程序运行后出现崩溃的情况，例如我们的代码只能在 Linux 系统下运行，可以先判断当前系统是否符合条件。

![img](https://www.runoob.com/wp-content/uploads/2019/07/assert.png)

以下为 assert 使用实例：

```shell
>>> assert True     # 条件为 true 正常执行
>>> assert False    # 条件为 false 触发异常
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError
>>> assert 1==1    # 条件为 true 正常执行
>>> assert 1==2    # 条件为 false 触发异常
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError

>>> assert 1==2, '1 不等于 2'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError: 1 不等于 2
>>>
```

以下实例判断当前系统是否为 Linux，如果不满足条件则直接触发异常，不必执行接下来的代码：

**实例**

```shell
import sys
assert ('linux' in sys.platform), "该代码只能在 Linux 下执行"

# 接下来要执行的代码
```

### with语句

https://www.jianshu.com/p/20fd3335648a

#### with语句的作用

先说说为什么会出现with，本来可以用try  except finally来解决的问题，为什么要用with语句呢？
 因为两个原因，其一，python是一门简短精悍的语言，提倡简洁的编码风格，也可以理解为pythonic。其二，with使用了上下文管理器，可以自动获取上下文相关内容，让开发者更专注于业务。

#### with语句的语法

> with expression as targer:
>  code body

expression是一个表达式，可以是一个函数，也可以是一个对象，但是如果是函数，函数必须返回一个实现了上下文管理器协议的对象，如果是一个对象，这个对象必须是上下文管理器对象。
 target，是**enter**方法的返回值。
 好了，目前知道这些就够了。

#### 有哪些创建的with用法

**1. 操作文件**



```dart
import os

with open('/usr/file.txt') as f:
    for line in f:
        print(line)
```

当操作文件时，with获取了应用上下文，在结束时会自动执行close函数来关闭文件。

**2. 操作数据库**

我们以Mysql为例，提示：这段代码使用pymysql模块，所以需要先安装，pip install pymysql即可。
如果总是没有反馈结果，可以翻墙，然后再次执行pip install pymysql命令就行了。

```ruby
from pymysql import connect

class OpenDB():
    def __init__(self, username, password, database):
        self.conn = connect(host="localhost", port=3306, user=username, password=password, database=database, charset='utf-8')
        self.cs = self.conn.cursor()

    def __enter__(self):
        return self.cs    # 返回游标

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.conn.commit()      # 提交sql操作
        self.cs.close()             # 关闭游标
        self.conn.close()         # 关闭数据库连接

with OpenDB('root', '123456', 'test_database') as d:
    sql = "select * from test_database"
    d.execute(sql)
    content = d.fetchall()

for temp in content:
    print(temp)
```

首先导入pymysql模块中的connect对象，用来初始化数据库的连接。
然后程序创建了一个实现了上下文管理器协议的对象OpenDB，它有两个属性，一个保存了数据库的连接，另一个报错了数据库的游标，因为要通过游标来执行sql语句。

也许你会问，这个d是什么？
d是**enter**方法的返回值，嗯，很明显，这里的d是指向数据库游标的，所以才有了d.execute(sql)这一句执行sql的代码。
d.fetchall()用来匹配所有的查询结果。
最后用一个for in来遍历查询结果。

## 图形界面入门EasyGui

https://www.cnblogs.com/wu-wu/p/11435463.html



## 面向对象编程

self的作用

https://blog.csdn.net/weixin_33782386/article/details/94205352

## 小结

https://zhuanlan.zhihu.com/p/172168165

```shell
三个基本概念
1. 结构化（函数、模块、包）
2. 面向对象（类及派生类、重载）
3. 虚拟环境（版本管理、环境隔离）

四类基本操作
1. 数据操作（各种数据类型的操作）
2. 文件操作（文件打开读写关闭等操作）
3. 模块操作（导入使用、模块查寻等操作）
4. 并发操作（进程与线程、锁/信号号/安全队列等）

五大基本语句（5）
1. 赋值语句（变量、对象、赋值运算符）
2. 输入输出语句（print, input函数）
3. 条件判断语句（if-elif-else语句）
4. 循环语句(遍历循环for-in-else、条件循环while-else、break/continue)
5. 异常处理语句(try-except-else-finally)

六种数据类型（6）
1. 数字类型（int,bool,float,complex）
2. 字符串（str）
3. 列表（list）
4. 元组（tuple）
5. 字典（dict）
6. 集合（set）
```

