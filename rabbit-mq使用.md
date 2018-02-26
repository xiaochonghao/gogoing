### 死信邮箱rabbitmq Dead-Letter-Exchange
DLX也是一下正常的Exchange同一般的Exchange没有区别，它能在任何的队列上被指定，实际上就是设置某个队列的属性，当这个队列中有死信时，RabbitMQ就会自动的将这个消息重新发布到设置的Exchange中去，进而被路由到另一个队列，publish可以监听这个队列中消息做相应的处理。

### flower配置启动
```
pip install flower
```
```
celery flower --port=5555 --address=127.0.0.1
```

### rabbitmq容器启动
```
docker pull rabbitmq:management
docker run -d --name mq-container -p 5672 -p 15672 rabbitmq:management
# default user: guest
# default pw: guest
```

### 启动celery命令
```
# 启动30个线程
celery -A conf worker -l info -c 30
```

### 启动定时任务
```
# 不用起多个进程，否则容易乱
celery -A conf beat -l info
```

### Flower监控
```
# 指定broker，监控任务执行情况
celery flower --port=5555 --address=127.0.0.1 --broker=amqp://guest:guest@164.52.33.18:5672//
```
### 项目中出现的问题
* win7开发环境不支持celery>=4.0版本