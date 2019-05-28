# 字典 #

字典是另一种可变容器模型，且可存储任意类型对象。

字典的每个键值 key=>value 对用冒号 : 分割，每个键值对之间用逗号 , 分割，整个字典包括在花括号 {} 中 ,格式如下所示：
```python
    d = {key1 : value1, key2 : value2 }
```

键一般是唯一的，如果重复最后的一个键值对会替换前面的，值不需要唯一。

```python
>>>dict = {'a': 1, 'b': 2, 'b': '3'}
>>>dict['b']
'3'
>>> dict
{'a': 1, 'b': '3'}
```

    注意：键是hash类型，必须不可变，可以用数字、字符串或元组充当，但用列表和字典就不行

___

## 1、访问字典里的值 ##
把相应的键放入到方括号中，如下实例:
```python
dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
print ("dict['Name']: ", dict['Name'])
print ("dict['Age']: ", dict['Age'])
```
如果用字典里没有的键访问数据，会输出错误。

---

## 2、修改字典 ##
向字典添加新内容的方法是增加新的键/值对，修改或删除已有键/值对如下实例:
```python
dict = {'Name': 'Qu', 'Age': 7, 'Class': 'First'}
 
dict['Age'] = 8               # 更新 Age
dict['School'] = "大学"  # 添加信息
 
 
print ("dict['Age']: ", dict['Age'])
print ("dict['School']: ", dict['School'])
```

---

## 3、删除字典元素 ##

能删单一的元素也能清空字典，清空只需一项操作。

显示删除一个字典用del命令，如下实例：

```python
dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
del dict['Name'] # 删除键 'Name'
dict.clear()     # 清空字典
del dict         # 删除字典
 
print ("dict['Age']: ", dict['Age'])
print ("dict['School']: ", dict['School'])
```

---

## 4、字典键的特性 ##
字典值可以是任何的 python 对象，既可以是标准的对象，也可以是用户定义的，但键不行。

两个重要的点需要记住：

**(1)  不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住，如下实例：**
```python
dict = {'Name': 'Runoob', 'Age': 7, 'Name': '小菜鸟'}
 
print ("dict['Name']: ", dict['Name'])

```

**(2)  键必须不可变，所以可以用数字，字符串或元组充当，而用列表就不行。**

---

## 5、字典内置函数&方法 ##
Python字典包含了以下内置函数：
|   序号    |	函数及描述|
|   ---    |	--- |
|   1	|   len(dict)<br>计算字典元素个数，即键的总数。|
|   2	|   str(dict)<br>输出字典，以可打印的字符串表示。|
|   3	|   type(variable)<br>返回输入的变量类型，如果变量是字典就返回字典类型。|

Python字典包含了以下内置方法：
|   序号	|   函数及描述|
|   ---	|   ---|
|   1	|   radiansdict.clear()<br>删除字典内所有元素|
|   2	|   radiansdict.copy()<br>返回一个字典的浅复制|
|   3	|   radiansdict.fromkeys()<br>创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值|
|   4	|   radiansdict.get(key, default=None)<br>返回指定键的值，如果值不在字典中返回default值|
|   5	|   key in dict<br>如果键在字典dict里返回true，否则返回false|
|   6	|   radiansdict.items()<br>以列表返回可遍历的(键, 值) 元组数组|
|   7	|   radiansdict.keys()<br>返回一个迭代器，可以使用 list() 来转换为列表|
|   8	|   radiansdict.setdefault(key, default=None)<br>和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default|
|   9	|   radiansdict.update(dict2)<br>把字典dict2的键/值对更新到dict里|
|   10	|   radiansdict.values()<br>返回一个迭代器，可以使用 list() 来转换为列表|
|   11	|   pop(key[,default])<br>删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。|
|   12	|   popitem()<br>随机返回并删除字典中的一对键和值(一般删除末尾对)。|
