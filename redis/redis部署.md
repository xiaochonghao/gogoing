# centos安装步骤

官网： https://redis.io/download

# redis配置

## 设置环境变量

```
vim /etc/profile
```
最后一行加上
```
# redis env
export REDIS=/root/redis-4.0.9/src
export PATH=$PATH:$REDIS
```
启用环境变量
```
source /etc/profile
```

## 自启动打开

```
vim redis.conf

# /daemonize设置成yes
daemonize yes
```

## 开启远程访问

```
# /bind 注掉
# bind 127.0.0.1
```

通过以下命令，可从另一台服务器访问

```
redis-cli -a password -h hostip
```

## 增加密码认证

```
# /requirepass 增加
requirepass [mypassword]
```
效果：
```
root@VM-60-191-ubuntu:~# redis-cli
127.0.0.1:6379> keys *
(error) NOAUTH Authentication required.
```
正确姿势：
```
root@VM-60-191-ubuntu:~# redis-cli -a [mypassword]
127.0.0.1:6379> keys *
1) "key2"
```

### 指定配置文件，重启redis服务

```
redis-server ./redis.conf
```