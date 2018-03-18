### 引入包

```python
from datetime import datetime, timedelta
```

### 重要方法

```python
cur_time_str = datetime.now().strftime("%Y%m%d %H:%M:%S")
time = datetime.strptime(cur_time_str, "%Y%m%d %H:%M:%S")
```

### 结合ORM

* 筛选条件一定注意是`datetime str`不是`datetime`类型

     ![datetime报错](/images/datetime.png)

* 查询返回的时间类型的结果是`datetime`类型