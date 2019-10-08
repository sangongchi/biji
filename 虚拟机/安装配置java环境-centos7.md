# Centos7安装配置java环境：

----

1.先查看本地是否自带java环境：

>  yum list installed |grep java

2.卸载自带的java（输入su，输入root超级管理员的密码，切换到root用户模式）

> yum -y remove java-1.8.0-openjdk* 
>
> yum -y remove tzdata-java*

3.查看yum仓库中的java安装包

> yum -y list java*

4.安装java：

>yum -y install java-1.8.0-openjdk*

5.查找Java安装路径

>which java

	ls -lrt /usr/bin/java（也就是上一步查询出来的路径），然后回车
	
	输入ls -lrt /etc/alternatives/java（也就是上一步查询出来的路径），然后回车
	
	从路径中可以看到在jvm目录下，输入cd /usr/lib/jvm，跳转到jvm的目录

>输入ls 列出当前目录下的文件和文件夹

6.配置Java环境变量

输入vi /etc/profile去编辑环境变量
添加如下：

```bash
export JAVA_HOME=/usr/lib/jvm/java-1.8.0
export JRE_HOME=$JAVA_HOME/jre  
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
```

保存退出

输入source /etc/profile，使配置立即生效
7. 检查Java安装和配置情况 输入java -version，然后回车

      

----

通过下载jdk上传安装的步骤：
1.通过xshell上传jdk安装包

2.tar -zxvf jdk-8u181-linux-x64.tar.gz 解压

3.复制到一个文件夹：cp -r jdk1.8.0_181/ /opt/java/

4.配置环境变量：同上

5.source /etc/profile，使配置立即生效

 2.vi命令：

   i:进入到插入模式 

   esc:退出插入模式

   :q! 退出不保存

   :wq 保存退出
————————————————
原文链接：https://blog.csdn.net/gexiaoyizhimei/article/details/95374890