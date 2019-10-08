#### 1. 防火墙操作

> 1. 关闭防火墙
>
>     - `systemctl stop firewalld.service            #停止firewall`
>     - `systemctl disable firewalld.service        #禁止firewall开机启动`
>
> 2. 开启防火墙
>
>     - `firewall-cmd --reload`        # 重启防火墙
>     - `systemctl restart iptables.service` #重启防火墙使配置生效
>     - `systemctl enable iptables.service` #设置防火墙开机启动
>
> 3. 其他常用命令
>
>     - > 命令含义:
>         >
>         > --zone  #作用域
>         >   --add-port=80/tcp  #添加端口，格式为：端口/通讯协议
>         >   --permanent  #永久生效，没有此参数重启后失效
>
>     - `firewall-cmd --state`                          ##查看防火墙状态，是否是running
>     - `firewall-cmd --reload`                          ##重新载入配置，比如添加规则之后，需要执行此命令
>     - `firewall-cmd --get-zones`                      ##列出支持的zone
>     - `firewall-cmd --get-services`                    ##列出支持的服务，在列表中的服务是放行的
>     - `firewall-cmd --query-service ftp`              ##查看ftp服务是否支持，返回yes或者no
>     - `firewall-cmd --add-service=ftp`                ##临时开放ftp服务
>     - `firewall-cmd --add-service=ftp --permanent`    ##永久开放ftp服务
>     - `firewall-cmd --remove-service=ftp --permanent`  ##永久移除ftp服务
>     - `firewall-cmd --add-port=80/tcp --permanent`    ##永久添加80端口