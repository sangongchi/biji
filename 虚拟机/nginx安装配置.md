### 1.nginx安装配置

---

> 1. ```bash
>   yum -y install gcc gcc-c++ autoconf pcre-devel make automake
>   yum -y install wget httpd-tools vim
>   ```



> 2. ``` yum list | grep nginx```
>
> 上述语句查询域名源是否存在nginx
>
> 3. 没有的话可以自行配置 yum源
> > vim /etc/yum.repos.d/nginx.repo
>
>   >[nginx]
>   >name=nginx repo
>   >baseurl=http://nginx.org/packages/centos/7/$basearch/
>   >gpgcheck=0
>   >enabled=1
>   >//上述的centos/7  表示操作系统以及版本号
>
> > yum install nginx
>
>  >
>  >2. nginx -v  //查询版本
>  >
>  >3. ```text
>  >  rpm -ql nginx    //可以用来查询nginx 的安装目录
>  >  // rpm 是linux 的包管理器，-q 表示你询问模式 -l 代表返回列表
>  >  ```
>
> 5. cd /etc/nginx
>
> vim nginx.conf
> #运行用户，默认即是nginx，可以不进行设置
> user  nginx;
> #Nginx进程，一般设置为和CPU核数一样
> worker_processes  1;   
> #错误日志存放目录
> error_log  /var/log/nginx/error.log warn;
> #进程pid存放位置
> pid        /var/run/nginx.pid;
>
> events {
> worker_connections  1024; # 单个后台进程的最大并发数
> }
>
> http {
> include       /etc/nginx/mime.types;   #文件扩展名与类型映射表
> default_type  application/octet-stream;  #默认文件类型
> #设置日志模式
>
> log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
> '$status $body_bytes_sent "$http_referer" ''
> "​$http_user_agent" "$http_x_forwarded_for"';


​      
> ​	access_log  /var/log/nginx/access.log  main;   #nginx访问日志存放位置
>
> ​	sendfile        on;   #开启高效传输模式
> ​	#tcp_nopush     on;    #减少网络报文段的数量
>
> ​	keepalive_timeout  65;  #保持连接的时间，也叫超时时间
>
> ​	#gzip  on;  #开启gzip压缩
>
> ​	include /etc/nginx/conf.d/*.conf; #包含的子配置项位置和文件
> ```bash
> 
> vim default.conf
> 
> ​```bash
> server {
> listen       80;   #配置监听端口
> server_name  localhost;  //配置域名
> 
> #charset koi8-r;     
> #access_log  /var/log/nginx/host.access.log  main;
> 
> location / {
> root   /usr/share/nginx/html;     #服务默认启动目录
> index  index.html index.htm;    #默认访问文件
> }
> 
> #error_page  404              /404.html;   # 配置404页面
> 
> # redirect server error pages to the static page /50x.html
> #
> error_page   500 502 503 504  /50x.html;   #错误状态码的显示页面，配置后需要重启
> location = /50x.html {
> root   /usr/share/nginx/html;
> }
> 
> # proxy the PHP scripts to Apache listening on 127.0.0.1:80
> #
> #location ~ \.php$ {
> #    proxy_pass   http://127.0.0.1;
> #}
> 
> # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
> #
> #location ~ \.php$ {
> #    root           html;
> #    fastcgi_pass   127.0.0.1:9000;
> #    fastcgi_index  index.php;
> #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
> #    include        fastcgi_params;
> #}
> 
> # deny access to .htaccess files, if Apache's document root
> # concurs with nginx's one
> #
> #location ~ /\.ht {
> #    deny  all;
> #}
> }
> ```

