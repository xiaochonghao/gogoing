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

#### cat命令特殊使用

* `EOF`是“end of file”，表示文本结束符。

    ```
        # cat << EOF > test.sh   或者   # cat > test.sh << EOF
        > #!/bin/bash
        > #you Shell script writes here.
        > EOF
    ```
    结果如下：
    ```
        # cat test.sh
        #!/bin/bash
        #you Shell script writes here.
    ```
* EOF只是标识，不是固定的

    ```
        # 追加文件
        # cat << HHH > iii.txt    或者   # cat > iii.txt << HHH
        > sdlkfjksl
        > sdkjflk
        > asdlfj
        > HHH
    ```
    结果如下：
    ```
        # cat iii.txt
        sdlkfjksl
        sdkjflk
        asdlfj
    ```
* 非脚本中可以用`Ctrl-D`输出`EOF`的标识


#### chmod

```
-R : 对目前目录下的所有文件与子目录进行相同的权限变更(即以递回的方式逐个变更)
+x : 刚创建出来的文件没有执行的权限，需要加这个参数执行赋予脚本执行权限，或者使用参数775。
```

## shell脚本

* 在为shell脚本传递的参数中**如果包含空格，应该使用单引号或者双引号将该参数括起来，以便于脚本将这个参数作为整体来接收。**

    在有参数时，可以使用对参数进行校验的方式处理以减少错误发生：
    ```
        if [ -n "$1" ]; then
            echo "包含第一个参数"
        else
            echo "没有包含第一参数"
        fi
    ```
    注意：的是中括号 [] 与其中间的代码应该有空格隔开

* 特殊字符用来处理参数：
     
    参数处理 | 说明
    ---------|----------
    `$#` | 传递到脚本的参数个数

#### if .. then .. elif .. else .. fi

* 判断条件的参数

    参数 | 含义
    ------- | -------
     -eq | //等于
     -ne | //不等于
     -gt | //大于
     -lt | //小于
     ge | //大于等于
     le | //小于等于