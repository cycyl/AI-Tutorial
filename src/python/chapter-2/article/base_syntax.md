# 基础语法 #

## 1、编码 ##

默认情况下，Python 3 源码文件以 UTF-8 编码，所有字符串都是 unicode 字符串。 当然你也可以为源码文件指定不同的编码：

```python
# -*- coding: cp-1252 -*-
```

上述定义允许在源文件中使用 Windows-1252 字符集中的字符编码，对应适合语言为保加利亚语、白罗斯语、马其顿语、俄语、塞尔维亚语。

因为 Python 的诞生比 Unicode 标准发布的时间还要早，所以最早的Python 只支持 ASCII 编码，普通的字符串 'ABC' 在 Python 内部都是 ASCII 编码的。

Python 在后来添加了对 Unicode 的支持，以 Unicode 表示的字符串用`u'...'`表示。

为了节约资源，出现了把Unicode编码转化为“可变长编码”的UTF-8编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。如果你要传输的文本包含大量英文字符，用UTF-8编码就能节省空间（ASCII码可以看成是UTF-8的一部分，所以大量只支持ASCII编码的历史遗留软件可以在UTF-8编码下继续工作）。现在的python 3.7 已经把utf-8当作默认编码方式。

## 2、标识符 ##

标示符（IDentifier）是指用来标识某个实体的一个符号。在不同的应用环境下有不同的含义。
在日常生活中，标示符是用来指定某个东西、人，要用到它，他或她的名字；在数学中解方程时，我们也常常用到这样或那样的变量名或函数名；

**在编程语言中，标识符是用户编程时使用的名字，对于变量、常量、函数、语句块也有名字；我们统统称之为标识符。**

- 第一个字符必须是字母表中字母或下划线 _ 。
- 标识符的其他的部分由字母、数字和下划线组成。
- 标识符对大小写敏感。

在 Python 3 中，非 ASCII 标识符也是允许的了。

## 3、保留字 ##
保留字即关键字，我们不能把它们用作任何标识符名称。Python 的标准库提供了一个 keyword 模块，可以输出当前版本的所有关键字：

```python
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```

## 4、注释 ##
Python中单行注释以 # 开头，实例如下：

```python
#!/usr/bin/python3
 
# 第一个注释
print ("Hello, Python!") # 第二个注释
```

多行注释可以用多个 # 号，还有 ''' 和 """：

```python 
#!/usr/bin/python3
 
# 第一个注释
# 第二个注释
 
'''
第三注释
第四注释
'''
 
"""
第五注释
第六注释
"""
print ("Hello, Python!")
```

## 5、行与缩进 ##
python最具特色的就是使用缩进来表示代码块，不需要使用大括号 {} 。

缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数。实例如下：

```python
if True:
    print ("Answer")
    print ("True")
else:
    print ("Answer")
  print ("False")    # 缩进不一致，会导致运行错误
```

## 6、多行语句 ##
Python 通常是一行写完一条语句，但如果语句很长，我们可以使用反斜杠(\)来实现多行语句，例如：

```python
total = item_one + \
        item_two + \
        item_three
```

在 [], {}, 或 () 中的多行语句，不需要使用反斜杠(\)，例如：
```python
total = ['item_one', 'item_two', 'item_three',
        'item_four', 'item_five']
```

注意：三引号也可以实现多行显示，其本质是在字符串中增加换行。

----

## 9、布尔值 ##

布尔值和布尔代数的表示完全一致，一个布尔值只有 `True` 、 `False `两种值，要么是 `True`，要么是 `False`，在 Python 中，可以直接用 True、False 表示布尔值（请注意大小写），也可以通过布尔运算计算出来。

布尔值可以用 `and`、`or` 和 `not` 运算。

`and` 运算是与运算，只有所有都为 True，and 运算结果才是 True。

`or` 运算是或运算，只要其中有一个为 True，or 运算结果就是 True。

`not` 运算是非运算，它是一个单目运算符，把 True 变成 False，False 变成 True。

----

## 10、空值 ##

基本上每种编程语言都有自己的特殊值——空值，在 Python 中，用 None 来表示。

----

## 11、空行 ##
函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。

空行与代码缩进不同，空行并不是Python语法的一部分。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

**记住：** 空行也是程序代码的一部分。

----

## 12、等待用户输入 ##
执行下面的程序在按回车键后就会等待用户输入：
```python
input("\n\n按下 enter 键后退出。")
```

以上代码中 ，"\n\n"在结果输出前会输出两个新的空行。一旦用户按下 enter 键时，程序将退出。

----

## 13、同一行显示多条语句 ##
Python可以在同一行中使用多条语句，语句之间使用分号(;)分割，以下是一个简单的实例：
```python
import sys; x = 'runoob'; sys.stdout.write(x + '\n')
```
----
## 14、Print 输出 ##
print 默认输出是换行的，如果要实现不换行需要在变量末尾加上 end=""：
```python
print( 123, end=" " )
```
### (1) 打印字符串 ###
```python
print("My name is %s" %("Alfred.Xue"))
#输出效果：
My name is Alfred.Xue
```

### (2) 打印整数 ###
```python
print("I am %d years old." %(25))
#输出效果：
I am 25 years old.
```

### (3) 打印浮点数 ###
```python
print ("His height is %f m"%(1.70))
#输出效果：
His height is 1.700000 m
```

### (4) 打印浮点数（指定保留两位小数） ###
```python
print ("His height is %.2f m"%(1.70))
#输出效果：
His height is 1.70 m
```

### (5) 指定占位符宽度 ###
```python
print ("Name:%10s Age:%8d Height:%8.2f"%("Alfred",25,1.70))
#输出效果：
Name:    Alfred Age:      25 Height:    1.70
```

### (6) 指定占位符宽度(左对齐) ###
```python
print ("Name:%-10s Age:%-8d Height:%-8.2f"%("Alfred",25,1.70))
#输出效果：
Name:Alfred     Age:25       Height:1.70
```

### (7) 指定占位符(只能用0当占位符？) ###
```python
print ("Name:%-10s Age:%08d Height:%08.2f"%("Alfred",25,1.70))
#输出效果：
Name:Alfred     Age:00000025 Height:00001.70
```

### (8) 科学计数法 ###
```python
format(0.0026,'.2e')
#输出效果：
'2.60e-03'
```

**字符串格式化代码：**

| 格式 |	描述 |
| ---- | ---- |
|%%	| 百分号标记 |
|%c	| 字符及其ASCII码 |
|%s	| 字符串 |
|%d	| 有符号整数(十进制)|
|%u	| 无符号整数(十进制)|
|%o	| 无符号整数(八进制)|
|%x	| 无符号整数(十六进制)|
|%X	| 无符号整数(十六进制大写字符)|
|%e	| 浮点数字(科学计数法)|
|%E	| 浮点数字(科学计数法，用E代替e)|
|%f	| 浮点数字(用小数点符号)|
|%g	| 浮点数字(根据值的大小采用%e或%f)|
|%G	| 浮点数字(类似于%g)|
|%p	| 指针(用十六进制打印值的内存地址)|
|%n	| 存储输出字符的数量放进参数列表的下一个变量中|

----

## 15、import 与 from...import ##
在 python 用 `import` 或者 `from...import` 来导入相应的模块。

将整个模块(somemodule)导入，格式为： `import somemodule`

从某个模块中导入某个函数,格式为： `from somemodule import somefunction`

从某个模块中导入多个函数,格式为： `from somemodule import firstfunc, secondfunc, thirdfunc`

将某个模块中的全部函数导入，格式为： `from somemodule import *`