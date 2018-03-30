
# Centos7 firewall命令

* 查看已经开放的端口：
    ```
    firewall-cmd --list-ports
    ```
* 开启端口
    ```
    firewall-cmd --zone=public --add-port=80/tcp --permanent

    –zone #作用域
    –add-port=80/tcp #添加端口，格式为：端口/通讯协议
    –permanent #永久生效，没有此参数重启后失效
    ```
* 关闭端口

    ```
    firwall-cmd --zone=public --remove-port=6379/tcp --permanent
    ```

* 重启防火墙
    ```
    firewall-cmd --reload #重启firewall
    systemctl stop firewalld.service #停止firewall
    systemctl disable firewalld.service #禁止firewall开机启动
    firewall-cmd --state #查看默认防火墙状态（关闭后显示notrunning，开启后显示running）
    ```
* 查看防火墙状态
    ```
    firewall-cmd --state    # 关闭后显示notrunning，开启后显示running
    ``` 

# CentOS 7 以下版本 iptables 命令
如要开放80，22，8080 端口，输入以下命令即可
```
/sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT
/sbin/iptables -I INPUT -p tcp --dport 22 -j ACCEPT
/sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
```
然后保存：
```
/etc/rc.d/init.d/iptables save
```
查看打开的端口：
```
/etc/init.d/iptables status
```
关闭防火墙 
1） 永久性生效，重启后不会复原
```
开启： chkconfig iptables on
关闭： chkconfig iptables off
```
2） 即时生效，重启后复原
```
开启： service iptables start
关闭： service iptables stop
```
查看防火墙状态：
```
service iptables status
```