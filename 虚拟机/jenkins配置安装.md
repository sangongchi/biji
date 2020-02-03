### jenkins 安装（自动化构建）

---

####  1.首先需要安装java（jdk 1.8）

```bash
yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel #安装openjdk
```

#### 2.下载rpm包

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

#### 3.导入密钥   若之前已从Jenkins导入过密钥，“rpm--import”将失败

```bash
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

#### 4.安装jenkins

```
yum install -y jenkins
```

#### 5. 配置jenkins

```bash
#打开配置文件
vim /etc/sysconfig/jenkins

#jenkins默认接口是 8080 ，需要换端口可以通过修改文件中的
JENKINS_PORT="端口号"

#密码  /var/lib/jenkins/secrets/initialAdminPassword        

```

#### 6.jenkins文件路径

>1. /usr/lib/jenkins/jenkins.war # jenkins安装目录，WAR包会放在这里
>2. /etc/sysconfig/jenkins # 配置文件
>3. /var/lib/jenkins/ # 默认的JENKINS_HOME
>4. /etc/rc.d/init.d/jenkins #启动脚本
>5. /var/log/jenkins/jenkins.log #Jenkins 日志文件

#### 7.jnkins 相关的nginx配置

>```nginx
>upstream jenkins {
>  server 127.0.0.1:8080 fail_timeout=0;
>}
> 
>server {
>  listen 80;
>  server_name jenkins.XX.com;
>  return 301 https://$host$request_uri;
>}
> 
>server {
>  listen 443 ssl;
>  server_name jenkins.XX.com;
> 
>  ssl_certificate /etc/nginx/ssl/server.crt;
>  ssl_certificate_key /etc/nginx/ssl/server.key;
> 
>  location / {
>    proxy_set_header        Host $host:$server_port;
>    proxy_set_header        X-Real-IP $remote_addr;
>    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
>    proxy_set_header        X-Forwarded-Proto $scheme;
>    proxy_redirect http:// https://;
>    proxy_pass              http://jenkins;
>    # Required for new HTTP-based CLI
>    proxy_http_version 1.1;
>    proxy_request_buffering off;
>    proxy_buffering off; # Required for HTTP-based CLI to work over SSL
>    # workaround for https://issues.jenkins-ci.org/browse/JENKINS-45651
>    add_header 'X-SSH-Endpoint' 'jenkins.XX.com:50022' always;
>  }
>}
>```
>
>

#### jenkins卸载

>  卸载
>
> 1. rpm -e jenkins *#rpm卸载*
> 2. rpm -ql jenkins *#检查是否卸载成功*
> 3. find / -iname jenkins | xargs -n 1000 rm -rf 彻底删除残留文件



