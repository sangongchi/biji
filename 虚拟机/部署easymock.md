## 1. easymock部署条件

### 1. node环境

### 2.jdk环境

### 3.mongodb环境

### 4.redis环境

### 5. easymock下载部署

>  下载地址 ：1.git clone https://github.com/easy-mock/easy-mock.git
>
> 2. 创建production 配置
>
>     ```
>     cp config/default.json config/production.json
>     export NODE_ENV=production
>     ```
>
> 3. ==npm install==
>
> 4. ==npm run build==  编译
>
> 5. 启动需要安装  pm2  使用npm  全局安装即可
>
>     ##  运行
>
>     
>
>     
>
>     ###         启动
>
>     ```
>     pm2 start app.js -i 4
>     ```
>
>     ![img](https://static.oschina.net/uploads/space/2017/0908/193813_d2WC_123777.jpg)
>
>     
>
>     
>
>     ###         查看
>
>     ```
>     pm2 list
>     ```
>
>     ![img](https://static.oschina.net/uploads/space/2017/0908/193835_Kp7p_123777.jpg)
>
>     
>
>     
>
>     ##     访问
>
>     ```
>     http://192.168.1.6:7300
>     ```
>
>     ![img](https://static.oschina.net/uploads/space/2017/0908/195114_8TtQ_123777.jpg)