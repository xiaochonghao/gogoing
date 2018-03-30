## settings文件之间的关系

如果没有在`settings.py`文件定义某个变量，只在`settings_test.py`定义了，那么要想在`settings_pro.py`中生效，必须在`settings_pro.py`文件中重新定义该变量。

或者直接在`settings.py`中定义全了，一劳永逸。