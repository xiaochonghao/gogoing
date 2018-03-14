#### 压缩

```php
tar -zcvf **.tar.gz src_file_name
tar -jcvf **.tar.bz2 src_file_name

# -c  ：建立一个压缩档案的参数指令(create 的意思)；
# -f  : 使用文件名，-f后立即接文件名
# -v  : 压缩的过程中显示文件名
```

#### 解压缩

```php
tar -xzvf **.tar.gz
tar -xjvf **.tar.bz2

# -x  ：解开一个压缩档案的参数指令！

# 后面可以加上-C指定解压的目录
```

#### 清空日志

```
echo > api.log
```