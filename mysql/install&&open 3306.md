## 安装MySQL

```bash
sudo apt-get install mysql-server 
sudo apt-get install mysql-client
sudo apt-get install libmysqlclient-dev
```

## 开放3306端口
首先确认3306端口是否对外开放，mysql默认状态下是不开放对外访问功能的。查看方法如下：

```
# netstat -an | grep 3306

tcp    0   0 127.0.0.1:3306      0.0.0.0:*         LISTEN
```

从上面可以看出，mysql的3306端口只是监听本地连接`127.0.0.1`。我们做下修改，使其对外其他地址开放。  
打开`/etc/mysql/my.cnf`文件

```
# vim /etc/mysql/my.cnf
```

找到`bind-address = 127.0.0.1`这一行，大概在47行，我们将它注释掉。

![mysql配置](/images/mysql.png)

## 授权用户远程访问

为了让访问mysql的客户端的用户有访问权限，我们可以通过如下方式为用户进行授权：  
首先进入mysql

```
# mysql -uroot -pyour_password
```

授权：

```
mysql>grant all privileges on *.* to user_name@'%' identified by'user_password';
```

## 重启mysql服务，使配置生效

重启方法很简单：

```
# /etc/init.d/mysql restart
```

通过以上三个步骤，基本上就会开启了mysql远程访问的权限，可以在本地通过Navicat进行连接了。如果有什么问题，可以留言大家一起讨论一下。

