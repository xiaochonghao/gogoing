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

### 重定向符、文件描述符

* 文件描述符：
    
    ```
        0 —— stdin（标准输入）
        1 —— stdout （标准输出）
        2 —— stderr （标准错误）
    ```

* 重定向操作 
    
    ```
        > —— 先清空文件，再写入内容
        >> —— 将内容直接追加到现有文件的尾部
    ``` 

* 使用示例：
    
    ```
        # 将stderr单独定向到一个文件，将stdout重定向到另一个文件
        cmd 2>stderr.txt 1>stdout.txt

        # 将stderr转换成stdout，使得stderr和stdout都被重新定向到同一个文件中：
        cmd> output.txt 2>&1
        # 或者下面两条命令，等效
        cmd &> output.txt
        cmd >& output.txt
    ```

    ```
        # 特殊文件，屏蔽stderr输出
        ls 123.txt 2> /dev/null
    ```