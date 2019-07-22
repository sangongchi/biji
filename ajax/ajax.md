## 1.ajax学习

### 1.请求状态

> 1. xmlhttp.readyState的五种状态
>
>     - 0 (未初始化)： (XMLHttpRequest)对象已经创建，但还没有调用open()方法。
>
>         1 (载入)：已经调用open() 方法，但尚未发送请求。
>
>         2 (载入完成)： 请求已经发送完成。
>
>         3 (交互)：可以接收到部分响应数据。
>
>         4 (完成)：已经接收到了全部数据，并且连接已经关闭。
>
> 2. xmlhttp.status
>     - 200 OK      //客户端请求成功
>         400 Bad Request  //客户端请求有语法错误，不能被服务器所理解
>         401 Unauthorized //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 
>         403 Forbidden  //服务器收到请求，但是拒绝提供服务
>         404 Not Found  //请求资源不存在，eg：输入了错误的URL
>         500 Internal Server Error //服务器发生不可预期的错误
>         503 Server Unavailable  //服务器当前不能处理客户端的请求，一段时间后可能恢复正常

### 2.兼容各个浏览器的用法

> 1.为了应对所有的现代浏览器，包括 IE5 和 IE6，请检查浏览器是否支持 XMLHttpRequest 对象。如果支持，则创建 XMLHttpRequest 对象。如果不支持，则创建 ActiveXObject ：
>
> ```js
> 	var xmlhttp;
> 	if (window.XMLHttpRequest)
> 	{
> 		//  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
> 		xmlhttp=new XMLHttpRequest();
> 	}
> 	else
> 	{
> 		// IE6, IE5 浏览器执行代码
> 		xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
> 	}
> ```
>

### 3.请求数据

> 将请求发送至服务器，可以使用XMLHttpRequest 对象的 open() |send() 方法
>
> xmlhttp.open("GET","ajax_info.txt",true);
> xmlhttp.send();
>
> | 方法                   | 描述                                                         |
> | ---------------------- | ------------------------------------------------------------ |
> | open(method,url,async) | 规定请求的类型、URL、以及是否处异步处理请求, <br/>- method:请求的类型<br>-url : 文件在服务器的位置<br />-async :true(异步) 或false（同步） |
> | send(string)           | 将请求发送到服务器<br />- string 仅用于post请求              |
>
> 
>
> | 方法                             | 描述                                                         |
> | -------------------------------- | ------------------------------------------------------------ |
> | setRequestHeader(*header,value*) | 向请求添加 HTTP 头。<br />- *header*: 规定头的名称<br />- *value*: 规定头的值 |

### 4. 服务器响应

>1. 如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。
>
>| 属性         | 描述                       |
>| ------------ | -------------------------- |
>| responseText | 获得字符串形式的响应数据。 |
>| responseXML  | 获得 XML 形式的响应数据。  |

