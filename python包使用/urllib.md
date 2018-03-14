#### urllib.quote

```py
对字符串进行编码
data = 'name = ~a+3'  

data1 = urllib.quote(data)   
print data1 # result: name%20%3D%20%7Ea%2B3
```

#### urllib.unquote

```py
对字符串进行解码
print urllib.unquote(data1) # result: name = ~a+3
```

#### urllib.urlencode

```py
把key-value键值进行编码
>>> from urllib import urlencode
>>> data = {
...     'a': 'test',
...     'name': '魔兽'
... }
>>> print urlencode(data)
a=test&amp;name=%C4%A7%CA%DE
```

> 没有urldecode，解码的时候只有使用urlquote