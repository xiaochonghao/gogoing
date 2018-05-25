# 常用命令
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
    1. 2>&1 是将标准出错重定向到标准输出，这里的标准输出已经重定向到了out.file文件，即将标准出错也输出到out.file文件中。最后一个&， 是让该命令在后台执行。
    2. 试想2>1代表什么，2与>结合代表错误重定向，而1则代表错误重定向到一个文件1，而不代表标准输出；换成2>&1，&与1结合就代表标准输出了，就变成错误重定向到标准输出.
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

#### linux后台执行命令：`& `和 `nohub`

* `&` 实现后台运行

    ```
    command > out.file 2>&1 &
    ```
    缺点：当控制台关掉（退出账户时），作业就会停止运行。

* `nohup`(no hang up-非挂起)

    ```
    nohup command > myout.file 2>&1 &
    ```
    当前账户使用`exit`命令正常退出，能保证命令后台一直运行。如果缺省`myout.file`参数，将默认输出到名字为`nohup.out`的文件中。

# shell脚本

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

#### netstat基本用法

1. 列出所有连接

    ```
    $ netstat -a
    ```

2. 禁用反向域名解析，加快查询下速度

    ```
    $ netstat -ant
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN     
    tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN     
    tcp        0      0 192.168.1.2:49058       173.255.230.5:80        ESTABLISHED
    tcp        0      0 192.168.1.2:33324       173.194.36.117:443      ESTABLISHED
    tcp6       0      0 ::1:631                 :::*                    LISTEN
    ```

3. 只列出监听中的连接

    ```
    $ netstat -tnl
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN     
    tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN     
    tcp6       0      0 ::1:631                 :::*                    LISTEN
    ```
