## Apache

---

### 1.Apache 配置多个域名的方法

> apache安装完默认是不开启虚拟服务器的，如果希望在本地apache上面配置虚拟服务器，类似于在网上买的虚拟主机，可以按照以下步骤进行配置：
>
> 1,修改本机的hosts文件，如下
>
>  示例：
> 127.0.0.1 localhost
> 127.0.0.1 xlb.com
>
> 127.0.0.1 xlb2.com
>
> 2,打开Apache的安装目录，找到httpd.conf文件，分别去掉下面两行文字前面的#号。　　
> LoadModule vhost_alias_module modules/mod_vhost_alias.so
> 去掉#意思是启用apache的虚拟主机功能。　　
> Include conf/extra/httpd-vhosts.conf　　
> 去掉这一行的#意思是从conf/extra/httpd-vhosts.conf这个文件导入虚拟主机配置。
>
> 3，打开extra目录内的httpd-vhosts.conf文件，把默认的配置
>
> <VirtualHost *:80>
>     ServerAdmin [webmaster@dummy-host.localhost](http://blog.csdn.net/harryxlb/article/details/6873765)
>     DocumentRoot "/www/docs/dummy-host.localhost"
>     ServerName dummy-host.localhost
>     ServerAlias http://www.dummy-host.localhost/
>     ErrorLog "logs/dummy-host.localhost-error_log"
>     CustomLog "logs/dummy-host.localhost-access_log common"
> </VirtualHost>
>
> <VirtualHost *:80>
>     ServerAdmin webmaster@dummy-host2.localhost
>     DocumentRoot "/www/docs/dummy-host2.localhost"
>     ServerName dummy-host2.localhost
>     ErrorLog "logs/dummy-host2.localhost-error_log"
>     CustomLog "logs/dummy-host2.localhost-access_log common"
> </VirtualHost>
>
> 改成自己想要的目录和域名
>
> <VirtualHost *:80>
>     ServerAdmin webmaster@dummy-host.localhost
>     DocumentRoot "D:/wamp/www/"
>     ServerName localhost
>     ServerAlias localhost
>     ErrorLog "logs/localhost-error_log"
> </VirtualHost>
> <VirtualHost *:80>
>     ServerAdmin webmaster@dummy-host.localhost
>     DocumentRoot "D:/wamp/www/web/"
>     ServerName test.com （填主域名）
>     ServerAlias *.test.com (这里的服务器别名可以支持泛解析，即所有的子域名都可以解析绑定到该虚拟主机)
>     ErrorLog "logs/localhost-error_log"
> </VirtualHost>
>
> 如果 弄完之后 出现403错误 那 在httpd.conf里找到：
> <Directory />
> Options FollowSymLinks ExecCGI Indexes
> AllowOverride None
> Order deny,allow
> Deny from all
> Satisfy all
> </Directory>
>
> 更改为
> <Directory />
> Options FollowSymLinks ExecCGI Indexes
> AllowOverride None
> \# Order deny,allow
> \# Deny from all
> \# Satisfy all
> </Directory>
>
> 上面配置完之后，就可以在浏览器输入xlb.com访问你设定好的目录下面的站点了