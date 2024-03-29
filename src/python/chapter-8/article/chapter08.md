# 文件读写 #

**open() 方法**

open() 方法用于打开一个文件，并返回文件对象，在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 OSError。

注意：使用 open() 方法一定要保证关闭文件对象，即调用 close() 方法。

open() 函数常用形式是接收两个参数：文件名(file)和模式(mode)。

    open(file, mode='r')

完整的语法格式：

    open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)

参数说明:

- file: 必需，文件路径（相对或者绝对路径）。
- mode: 可选，文件打开模式
- buffering: 设置缓冲
- encoding: 一般使用utf8
- errors: 报错级别
- newline: 区分换行符
- closefd: 传入的file参数类型
- opener:

mode参数有：

|   模式    |	描述|
|   ---    |	---|
|   t	|   文本模式 (默认)。|
|   x	|   写模式，新建一个文件，如果该文件已存在则会报错。|
|   b	|   二进制模式。|
|   +	|   打开一个文件进行更新(可读可写)。|
|   U	|   通用换行模式（不推荐）。|
|   r	|   以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。|
|   rb	|   以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。|
|   r+	|   打开一个文件用于读写。文件指针将会放在文件的开头。|
|   rb+	|   以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。|
|   w	|   打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。|
|   wb	|   以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。|
|   w+	|   打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。|
|   wb+	|   以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。|
|   a	|   打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。|
|   ab	|   以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。|
|   a+	|   打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。|
|   ab+	|   以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。|

默认为文本模式，如果要以二进制模式打开，加上 b 。

**file对象**
file 对象使用 open 函数来创建，下表列出了 file 对象常用的函数：

|   序号	|   方法及描述|
|   ---	|   ---|
|   1    |  	file.close()<br>关闭文件。关闭后文件不能再进行读写操作。
|   2   |   file.flush()<br>刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。|
|   3   |   file.fileno()<br>返回一个整型的文件描述符(file descriptor FD 整型), 可以用在如os模块的read方法等一些底层操作上。|
|   4   |   	file.isatty()<br>如果文件连接到一个终端设备返回 True，否则返回 False。|
|   5	|   file.next()<br>Python 3 中的 File 对象不支持 next() 方法。<br>返回文件下一行。|
|   6   |   file.read([size])<br>从文件读取指定的字节数，如果未给定或为负则读取所有。|
|   7   |   file.readline([size])<br>读取整行，包括 "\n" 字符。|
|   8   |   file.readlines([sizeint])<br>读取所有行并返回列表，若给定sizeint>0，返回总和大约为sizeint字节的行, 实际读取值可能比 sizeint 较大, 因为需要填充缓冲区。|
|   9   |   file.seek(offset[, whence])<br>设置文件当前位置|
|   10  |   file.tell()<br>返回文件当前位置。|
|   11  |   file.truncate([size])<br>从文件的首行首字符开始截断，截断文件为 size 个字符，无 size 表示从当前位置截断；截断之后后面的所有字符被删除，其中 Widnows 系统下的换行代表2个字符大小。|
|   12  |   file.write(str)<br>将字符串写入文件，返回的是写入的字符长度。|
|   13  |   file.writelines(sequence)<br>向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。|

```python
#打开文件open()
f = open('test.txt','r+')
#或者with open() 这种方法操作完成后，会自动关闭不需要close()
with open('test.txt','r') as f:
   f.read()


#关闭文件
f = open('test.txt','r+',encoding='utf-8')
ret = f.read()
print(ret)
f.close()


#读取文件内容(可指定每次读取字字符)
f = open('test.txt','r+',encoding='utf-8')
ret = f.read(8)
print(ret)



#读取数据（可指定读取字符数），存为list显示
f = open('test.txt','r+',encoding='utf-8')
ret = f.readlines()
print(ret)
f.close()



#读取一行数据
f = open('test.txt','r+',encoding='utf-8')
ret = f.readline()
print(ret)
f.close()



#写入文件write()参数是字符串
f = open('test.txt','a+',encoding='utf-8')
f.write("abc")
ret = f.read()
print(ret)
f.close()



#写入文件，writelines()参数是序列，比如列表，它会迭代帮你写入文件
f = open('test.txt','a+',encoding='utf-8')
f.writelines(["aa","bb","cc"])
ret = f.read()
print(ret)
f.close()



#判断文件是否是统一tty设备
f = open('test.txt','r+',encoding='utf-8')
ret = f.isatty()
print(ret)  #False
f.close()



#判断是否可读（不可读则报错" No such file or directory: "）
f = open('test.txt','r+',encoding='utf-8')
ret = f.readable()
print(ret)  #True
f.close()



#指定文件中指针的位置
f = open('test.txt','r+',encoding='utf-8')
ret = f.read(8)     #先读取8个字符
print(ret)
f.seek(0)           #然后把指针移动到文件开头处
ret = f.read(8)     #在重新读取
print(ret)
f.close()



#获取指针位置
f = open('test.txt','r+',encoding='utf-8')
ret = f.read(8)     #先读取8个字符
print("pointer position：%s"%f.tell())     #查看当前指针位置
print(ret)
f.seek(0)           #重置指定到启始位
print("pointer position：%s"%f.tell())     #在查看指针位置
f.close()



#截断文件数据，仅保留指定之前数据（指定字节数）
f = open('test.txt','r+',encoding='utf-8')
f.truncate(8)   #文件只保留前8个字节数据，文件后面数据的全部删除
ret = f.read()
print(ret)
f.close()



#文件描述符
f.fileno()



#刷新文件内部缓冲区
#即将缓冲区中的数据立刻写入文件，同时清空缓冲区，不需要是被动的等待输出缓冲区写入。
#一般情况下，文件关闭后会自动刷新缓冲区，但有时你需要在关闭前刷新它，这时就可以使用 flush() 方法。
f.flush()

```

