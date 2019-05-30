# 库-pyodbc #

## 1、连接数据库 ##
### (1) 直接连接数据库和创建一个游标（cursor) ###
```python
cnxn =pyodbc.connect('DRIVER={SQL Server};SERVER=localhost;DATABASE=testdb;UID=me;PWD=pass')
cursor =cnxn.cursor()
```

### (2) 使用DSN连接。通常DSN连接并不需要密码，还是需要提供一个PSW的关键字。 ###
```python
cnxn =pyodbc.connect('DSN=test;UID=username;PWD=password')
cursor =cnxn.cursor()
```

关于连接函数还有更多的选项，可以在pyodbc文档中的 connect funtion 和 ConnectionStrings查看更多的细节

## 2、数据查询（SQL语句为 select ...from..where） ##
- 所有的SQL语句都用cursor.execute函数运行。如果语句返回行，比如一个查询语句返回的行，你可以通过游标的fetch函数来获取数据，这些函数有（fetchone,fetchall,fetchmany）.如果返回空行，fetchone函数将返回None,而fetchall和fetchmany将返回一个空列。 
```python
cursor.execute("select user_id, user_name from users")
row =cursor.fetchone()
if row:
  print(row)
```

- Row这个类，类似于一个元组，但是他们也可以通过字段名进行访问。
```python
cursor.execute("select user_id, user_name from users")
row =cursor.fetchone()
print('name:', row[1])   # access by column index
print('name:', row.user_name) # or access by name
```

- 如果所有的行都被检索完，那么fetchone将返回None.
```python
while 1:
  row= cursor.fetchone()
  if not row:
    break
  print('id:', row.user_id)
```

- 使用fetchall函数时，将返回所有剩下的行，如果是空行，那么将返回一个空列。（如果有很多行，这样做的话将会占用很多内存。未读取的行将会被压缩存放在数据库引擎中，然后由数据库服务器分批发送。一次只读取你需要的行，将会大大节省内存空间）
```python
cursor.execute("select user_id, user_name from users")
rows =cursor.fetchall()
for row in rows:
  print(row.user_id, row.user_name)
```

- 如果你打算一次读完所有数据，那么你可以使用cursor本身。
```python
cursor.execute("select user_id, user_name from users")
for row in cursor:
  printrow.user_id, row.user_name
```

- 有很多SQL语句用单行来写并不是很方便，所以你也可以使用三引号的字符串来写
```python
cursor.execute("""
        select user_id, user_name
         from users
        where last_logon < '2001-01-01'
         and bill_overdue = 'y'
        """)
```

## 3、参数 ##
ODBC支持在SQL语句中使用一个问号来作为参数。你可以在SQL语句后面加上值，用来传递给SQL语句中的问号。
```python
cursor.execute("""
        select user_id, user_name
         from users
        where last_logon < ?
         and bill_overdue = ?
        """,'2001-01-01','y')
```

这样做比直接把值写在SQL语句中更加安全，这是因为每个参数传递给数据库都是单独进行的。如果你使用不同的参数而运行同样的SQL语句，这样做也更加效率。

## 4、数据插入 ##
数据插入，把SQL插入语句传递给cursor的execute函数，可以伴随任何需要的参数。
```python
cursor.execute("insert into products(id, name) values ('pyodbc', 'awesome library')")
cnxn.commit()

# 使用参数
cursor.execute("insert into products(id, name) values (?, ?)",'pyodbc', 'awesome library')
cnxn.commit()
```

注意调用cnxn.commit()函数：你必须调用commit函数，否者你对数据库的所有操作将会失效！当断开连接时，所有悬挂的修改将会被重置。这很容易导致出错，所以你必须记得调用commit函数。

## 5、数据修改和删除 ##
数据修改和删除也是跟上面的操作一样，把SQL语句传递给execute函数。但是我们常常想知道数据修改和删除时，到底影响了多少条记录，这个时候你可以使用cursor.rowcount的返回值。
```python
cursor.execute("delete from products where id <> ?",'pyodbc')
print(cursor.rowcount, 'products deleted')
cnxn.commit()
```

由于execute函数总是返回cursor，所以有时候你也可以看到像这样的语句：（注意rowcount放在最后面）
```python
deleted =cursor.execute("delete from products where id <> 'pyodbc'").rowcount
cnxn.commit()
```
同样要注意调用cnxn.commit()函数