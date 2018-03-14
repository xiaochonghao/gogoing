#### 根据Dockerfile创建镜像

```php
# . 表示自动识别当前目录下可用的Dockerfile
$ sudo docker build -t img_name:tag .
```

#### 提交container定制镜像

```
sudo docker commit -m '修改的信息' container_name image_name:tag
```

#### 上传镜像到仓库（company：direpose.capitalonline.net）

* 上传镜像-&gt;repository（**！如果该repository不存在的话，会自动创建**）

```php
$ sudo docker images 
REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
mgm_db                      base                96244ef9009e        5 hours ago         544.3 MB
ubuntu                      16.04               14f60031763d        2 weeks ago         119.5 MB

# 打tag，注意格式：用户名/repository_name:TAG
$ sudo docker tag 96 xiaochonghao/mgm_db:v0

# push镜像到xiaochonghao用户的mgm_db仓库中，如果xiaochonghao/mgm_db在仓库中不存在，则执行这条命令他过程中会自动创建repository
$ sudo docker push xiaochonghao/mgm_db:v0
The push refers to a repository [docker.io/xiaochonghao/mgm_db]
793707dbc2c3: Pushed 
26b126eb8632: Mounted from library/ubuntu 
220d34b5f6c9: Mounted from library/ubuntu 
8a5132998025: Mounted from library/ubuntu 
aca233ed29c3: Mounted from library/ubuntu 
e5d2f035d7a4: Mounted from library/ubuntu 
v1: digest: sha256:73f9e04a5ab4f5a823574e4fc4a4cfefc7fa573af22fd0122a8839905552b372 size: 1570
```

### 不通过docker pub账号，在主机之间传输镜像

* You will need to save the docker image as a tar file:

  ```
  # 这里的image name可以随便起名字
  docker save -o <save image to path> <image name>
  ```

* copy image to new system with `scp`

  ```
  ex:
  scp /tmp/oss_web_image root@10.13.2.133:/tmp/
  ```

* load the image into docker

  ```
  docker load -i <path to image tar file>
  ```

#### 查看docker镜像的详细信息

```
docker inspect [docker-image]
```

#### 查看docker镜像的修改历史记录

```
docker history [docker-image]

eg.
$ docker history test/b
IMAGE               CREATED             CREATED BY                                      SIZE
c0daf4be2ed4        3 hours ago         /bin/sh -c touch /opt/b.txt                     8 B
9977b78fbad7        3 hours ago         /bin/sh -c apt-get install -y apache2           54.17 MB
e83b3bf07b42        3 hours ago         /bin/sh -c apt-get update                       20.67 MB
9cd978db300e        3 months ago        /bin/sh -c #(nop) ADD precise.tar.xz in /       204.4 MB
6170bb7b0ad1        3 months ago        /bin/sh -c #(nop) MAINTAINER Tianon Gravi <ad   0 B
511136ea3c5a        10 months ago  
```

#### 回退docker镜像版本

```
If we want to make a rollback and remove the last layer (maybe the file should be called c.txt instead of b.txt) 
we can do 
so by tagging the layer 9977b78fbad7:
$ docker tag 9977b test/b
Let’s take a look at the new history:

$ docker history test/b
IMAGE               CREATED             CREATED BY                                      SIZE
9977b78fbad7        3 hours ago         /bin/sh -c apt-get install -y apache2           54.17 MB
e83b3bf07b42        3 hours ago         /bin/sh -c apt-get update                       20.67 MB
9cd978db300e        3 months ago        /bin/sh -c #(nop) ADD precise.tar.xz in /       204.4 MB
6170bb7b0ad1        3 months ago        /bin/sh -c #(nop) MAINTAINER Tianon Gravi <ad   0 B
511136ea3c5a        10 months ago                                                       0 B
Our last layer is gone and with the layer the text file b.txt!
```
