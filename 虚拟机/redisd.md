### 查看redis的releases版本

首先安装redis之前，可以点击[这里](http://download.redis.io/releases/)，查看最新的releases版本。



![img](https://upload-images.jianshu.io/upload_images/13423234-efa24dd7e8018f0f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

最上面的版本太久了，继续往下翻看看最新版本是多少。



![img](https://upload-images.jianshu.io/upload_images/13423234-2f2ca5d6af43eab7.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

### 下载redis的稳定版本

根据上面的页面，获取下载链接，进行下载。

```cpp
wget http://download.redis.io/releases/redis-stable.tar.gz
```



![img](https://upload-images.jianshu.io/upload_images/13423234-ed8780378494564e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

### 解压redis安装包

```css
[root@server01 ~]# tar -zxvf redis-stable.tar.gz 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-6cb7a0ebb8228ae5.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)



![img](https://upload-images.jianshu.io/upload_images/13423234-9c5a774e144b20d8.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

### yum安装gcc依赖

```csharp
[root@server01 ~]# yum install gcc -y
```



![img](https://upload-images.jianshu.io/upload_images/13423234-f0dd121a4791792b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

### 编译安装

```csharp
[root@server01 ~]# cd redis-stable
[root@server01 redis-stable]# ls
00-RELEASENOTES  CONTRIBUTING  deps     Makefile   README.md   runtest          runtest-sentinel  src    utils
BUGS             COPYING       INSTALL  MANIFESTO  redis.conf  runtest-cluster  sentinel.conf     tests
[root@server01 redis-stable]# make MALLOC=libc 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-df8480d3f7abf7e4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)



![img](https://upload-images.jianshu.io/upload_images/13423234-e67014726c1ffc30.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

生成了src目录文件之后，进入src（源文件目录）继续编译，如下：

```bash
[root@server01 src]# make install
    CC Makefile.dep

Hint: It's a good idea to run 'make test' ;)

    INSTALL install
    INSTALL install
    INSTALL install
    INSTALL install
    INSTALL install
[root@server01 src]# 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-0f337b4fc7505f01.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

### 测试是否安装成功

```csharp
[root@server01 src]# pwd
/root/redis-stable/src
[root@server01 src]# ./redis-server 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-4ceef02eeedb0267.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)



![img](https://upload-images.jianshu.io/upload_images/13423234-905ca7638f408a7e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

### 配置redis

> 以后台进程方式启动：

1.修改/root/redis-stable/redis.conf： daemonize no 将值改为yes 保存退出

```csharp
[root@server01 redis-stable]# pwd
/root/redis-stable
[root@server01 redis-stable]# vim redis.conf 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-0712d7aa54253b57.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

将daemonize no 改为 yes



![img](https://upload-images.jianshu.io/upload_images/13423234-df51e85c6b63bba4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)



![img](https://upload-images.jianshu.io/upload_images/13423234-a17fbb4e7e651cf6.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

> 指定redis.conf文件启动

```ruby
[root@server01 src]# ./redis-server /root/redis-stable/redis.conf 
1335:C 05 Dec 2018 08:49:43.682 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1335:C 05 Dec 2018 08:49:43.682 # Redis version=5.0.2, bits=64, commit=00000000, modified=0, pid=1335, just started
1335:C 05 Dec 2018 08:49:43.682 # Configuration loaded
[root@server01 src]# 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-4cacb28c7779707b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

这时候redis服务已经后台运行了，下一步就需要配置使用密码认证以及远程访问的配置。

```csharp
[root@server01 src]# ps -ef | grep redis
root       1336      1  0 08:49 ?        00:00:00 ./redis-server 127.0.0.1:6379
root       1371   1313  0 09:00 pts/0    00:00:00 grep --color=auto redis
[root@server01 src]# 
```

### 设置redis远程连接

> 关闭selinux 以及 firewalld 或者 放行 6379 默认端口

```csharp
[root@server01 selinux]# service firewalld stop
[root@server01 selinux]# systemctl disable firewalld 
```

> 配置redis.conf中将bind 127.0.0.1 改为bind 0.0.0.0或者注释该行



![img](https://upload-images.jianshu.io/upload_images/13423234-5e417f23c12ce1c9.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

### 设置redis连接密码

> 在`redis.conf`中搜索`requirepass`这一行，然后在合适的位置添加配置



![img](https://upload-images.jianshu.io/upload_images/13423234-86d150ab41c9f9e7.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

> 更新`redis`配置

再次执行启动加载配置的命令即可。

```ruby
[root@server01 src]# ./redis-server /root/redis-stable/redis.conf 
1182:C 05 Dec 2018 09:09:58.721 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
1182:C 05 Dec 2018 09:09:58.721 # Redis version=5.0.2, bits=64, commit=00000000, modified=0, pid=1182, just started
1182:C 05 Dec 2018 09:09:58.721 # Configuration loaded
[root@server01 src]# 
[root@server01 src]# ps -ef | grep redis
root       1177      1  0 09:09 ?        00:00:00 ./redis-server 0.0.0.0:6379
root       1185   1147  0 09:11 pts/0    00:00:00 grep --color=auto redis
[root@server01 src]# 
```

### 设置开机自启动

> 关闭redis服务

```csharp
[root@server01 src]# ps -ef | grep redis
root       1177      1  0 09:09 ?        00:00:00 ./redis-server 0.0.0.0:6379
root       1185   1147  0 09:11 pts/0    00:00:00 grep --color=auto redis
[root@server01 src]# 
[root@server01 src]# ps -aux | grep redis
root       1177  0.0  0.2 144008  2028 ?        Ssl  09:09   0:00 ./redis-server 0.0.0.0:6379
root       1187  0.0  0.0 112708   976 pts/0    R+   09:11   0:00 grep --color=auto redis
[root@server01 src]# 
[root@server01 src]# kill -9 1177
[root@server01 src]# 
[root@server01 src]# ps -aux | grep redis
root       1189  0.0  0.0 112708   980 pts/0    R+   09:12   0:00 grep --color=auto redis
[root@server01 src]# 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-1ea0d47df4e84b3f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

> 查看`redis-stable/utils`目录下的启动脚本



![img](https://upload-images.jianshu.io/upload_images/13423234-38a396f71a04c582.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)



![img](https://upload-images.jianshu.io/upload_images/13423234-fd66643c6ea70e62.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

```bash
REDISPORT=6379
EXEC=/usr/local/bin/redis-server
CLIEXEC=/usr/local/bin/redis-cli

PIDFILE=/var/run/redis_${REDISPORT}.pid
CONF="/etc/redis/${REDISPORT}.conf"
```

> 查看 `/usr/local/bin` 目录是否存在redis执行文件



![img](https://upload-images.jianshu.io/upload_images/13423234-80701ab2ed056140.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

那么剩下就是需要设置配置文件了。

> 在/etc目录下新建redis目录

```csharp
[root@server01 utils]# mkdir -p /etc/redis
[root@server01 utils]# 
[root@server01 utils]# ls /etc/redis/
[root@server01 utils]# 
```

> 将/redis-stable/redis.conf 文件复制一份到/etc/redis目录下，并命名为6379.conf

```csharp
[root@server01 redis-stable]# pwd
/root/redis-stable
[root@server01 redis-stable]# 
[root@server01 redis-stable]# cp redis.conf /etc/redis/6379.conf
[root@server01 redis-stable]# 
[root@server01 redis-stable]# ls -ll /etc/redis/
total 64
-rw-r--r-- 1 root root 62203 Dec  5 09:32 6379.conf
[root@server01 redis-stable]# 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-c63adb703755975e.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

> 将redis的启动脚本复制一份放到/etc/init.d目录下

```csharp
[root@server01 utils]# cp redis_init_script /etc/init.d/redisd
[root@server01 utils]# 
[root@server01 utils]# ls -ll /etc/init.d/redisd 
-rwxr-xr-x 1 root root 1352 Dec  5 09:34 /etc/init.d/redisd
[root@server01 utils]# 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-939113d9413b97e5.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

> 设置redis开机自启动

```csharp
[root@server01 utils]# cd /etc/init.d/
[root@server01 init.d]# ls
functions  netconsole  network  README  redisd
[root@server01 init.d]# chkconfig redisd on
[root@server01 init.d]# 
```



![img](https://upload-images.jianshu.io/upload_images/13423234-1da235fb89be12f5.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

使用vim编辑redisd文件，在第一行加入如下两行注释，保存退出

```bash
#!/bin/sh
# chkconfig:   2345 90 10
# description:  Redis is a persistent key-value database
```

注释的意思是，redis服务必须在运行级2，3，4，5下被启动或关闭，启动的优先级是90，关闭的优先级是10。



![img](https://upload-images.jianshu.io/upload_images/13423234-5d1861a4c148dbf4.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

> 启动以及关闭redis

```csharp
[root@server01 init.d]# service redisd start
/var/run/redis_6379.pid exists, process is already running or crashed
[root@server01 init.d]# 
[root@server01 init.d]# service redisd stop
Stopping ...
(error) NOAUTH Authentication required.
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
Waiting for Redis to shutdown ...
^C
[root@server01 init.d]
```



![img](https://upload-images.jianshu.io/upload_images/13423234-2bb55b60ae8d4fb3.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

可以从上面看出，当配置了redis的密码之后，停止redis的时候是需要认证的。

> 配置启动脚本使用密码，解决`停止(NOAUTH Authentication required)`的问题

修改redis启动脚本

```ruby
[root@server01 ~]# vim /etc/init.d/redisd
# 修改添加 -a "密码"
#$CLIEXEC -p $REDISPORT shutdown
$CLIEXEC -a "newpwd"  -p $REDISPORT shutdown
```



![img](https://upload-images.jianshu.io/upload_images/13423234-be3134dd43b5749c.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)



![img](https://upload-images.jianshu.io/upload_images/13423234-2756039e3cfbb779.png?imageMogr2/auto-orient/strip|imageView2/2/w/1167/format/webp)

