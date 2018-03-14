#### 利用dir\(\)方法查询...

* 使用dir\(\)函数可以查看对像内所有**属性**及**方法**。

#### 控制函数的参数个数

```py
import hashlib
import sys

def main():
    if len(sys.argv) != 2:
        sys.exit('Usage: %s file' % sys.argv[0])

    filename = sys.argv[1]
    m = hashlib.md5()
    with open(filename, 'rb') as fp:
        while True:
            blk = fp.read(4096) # 4KB per block
            if not blk: break
            m.update(blk)
    print m.hexdigest(), filename

if __name__ == '__main__':
    main()
```

#### dict.get

第二个参数为假如没有status属性的值，返回这个default值。

```py
status = extra.get("status", None)
```

#### 控制多个异常exceptions

```py
def is_uuid_like(val):
    """Returns validation of a value as a UUID.

    For our purposes, a UUID is a canonical form string:
    aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa
    """
    try:
        return str(uuid.UUID(val)) == val
    except (TypeError, ValueError, AttributeError):
        return False
```

### getattr\(\)函数

```py
def getattr(object, name, default=None)
    """
    getattr(object, name[, default]) -> value

    Get a named attribute from an object; getattr(x, 'y') is equivalent to x.y.
    """

demo:
from django.conf import settings as cdssettings

keys = ['CDS_URL', 'CDS_OSS_URL', 'CDS_SSH_URL', 'UPLOAD_URL', 'STATIC_I18N_EN_URL', 'STATIC_I18N_CH_URL',
            'FIREWALL_MODULE', 'APN_MODEL', 'IDC_MODEL', 'STATIC_URL']
for key in keys:     # 注意引号
    context[key] = getattr(cdssettings, key, "")   # 从settings.py文件中取key变量的value
```

### random函数

> 生成的随机字符串并非具有唯一性，需要再进一步进行判断
```py
def create_random_No(len_=6):
    '''
    生成随机数字
    :param len_:默认长度6
    :return:len_长度的随机数字
    '''
    num = ''
    for i in range(len_):
        num += str(random.randrange(10))
    logger.debug(num)
    return num
```

```py
def generate_random_str(length):
    '''
    生成数字加字符随机6位
    '''
    code_list = []
    for i in range(10):
        code_list.append(str(i))
    #for i in range(65, 91):
    #    code_list.append(chr(i))
    for i in range(97, 123):
        code_list.append(chr(i))        # chr()可以配合ord()函数使用
    random.seed(time.time())            # 使用random.seed()修改初始化种子
    s = random.sample(code_list, length)
    res = ''.join(s)
    return res
```

### MD5算法

```py
import hashlib

md5 = hashlib.md5('how to use md5 in python hashlib?')
print md5.hexdigest()

# 如果数据量很大，可以分块多次调用update()，最后计算的结果是一样的
md5 = hashlib.md5()
md5.update('how to use md5 in ')
md5.update('python hashlib?')
print md5.hexdigest()
```

### base64编码
就是用 64 个字符来表示二进制数据的方法。这 64 个字符包含小写字母 `a-z`、大写字母 `A-Z`、数字 `0-9` 以及符号`"+"、"/"`，其实还有一个 `"="` 作为后缀用途，所以实际上有 65 个字符。

Base64 可以将任意二进制数据编码到文本字符串，常用于在 URL、Cookie 和网页中传输少量二进制数据。

```py
import base64
# 编码
b64_data = base64.b64encode(_str)
# 解码      
data = base64.b64decode(b64_data)
```
