### 在Django中编写脚本

* 常用的头部处理
    ```py
    # -*- coding: utf-8 -*-
    import logging
    from datetime import datetime, timedelta
    import sys
    import os
    from os.path import abspath, dirname
    import django

    MODE = 'settings_test'
    if len(sys.argv) > 1:
        if sys.argv[1] == 'test':
            MODE = 'settings_test'
        if sys.argv[1] == 'dev':
            MODE = 'settings'
        if sys.argv[1] == 'pro':
            MODE = 'settings_pro'

    sys.path.append(dirname(dirname(dirname(abspath(__file__)))))  # 把manage.py所在目录添加到系统目录
    os.environ['DJANGO_SETTINGS_MODULE'] = 'resop.%s' % MODE  # 设置setting文件

    if django.VERSION >= (1, 7):  # 自动判断版本，初始化Django环境
        django.setup()
    ```
* 编码问题
    
    1. 文件开头的：`# -*-  coding=utf8  -*-`

        python的默认脚本文件都是以`utf8`编码的，当文件中有非`utf8`编码范围内的字符的时候就要使用“编码提示”来修正。

    2. `sys.setdefaultencoding('utf-8')`

    ![脚本编码问题](/images/脚本编码.png)