## JSON数据笔记

### 1. JSON简介

---

> JSON可以使用ajax进行传输
>
> 1. JSON 语法规则
>
>     - 数据在名称/值对中（名称必需是字符串）
>     - 数据由逗号隔开
>     - 对象保存在对象中
>     - 数据保存在中括号中（数组可以包含多个对象）
>     - **JSON对象可以嵌套对象**
> 2. JSON 的值可以是:<b>数字，字符串，boll值，数组，对象，null</b>
> 3. JSON中不能存储Date 对象，如果需要存储Date对象，需要将其转换为字符串，之后再将其转换为Date
> 4. 可以使用delete删除对象或者数组中的元素（删除之后数组和对象的长度不变）
>
>  **delete 运算符并不是彻底删除元素，而是删除它的值，但仍会保留空间。**
>
>  **运算符 delete 只是将该值置为 undefined，而不会影响数组长度，即将其变为稀疏数组**

### 2.JSON.parse()

---

> 1. JSON.parse(text[,reviver])
>
>     - **将服务器接收的字符串数据转换为javascript对象**   从服务器接收一般是字符串数据
>
>     - **在js中想要首先将json数据复制给js变量需要加引号**，否则会报错
>         - `var text = '{ "name":"Runoob", "initDate":"2013-12-14", "site":"www.runoob.com"}';`
>          ` var obj = JSON.parse(text);`
>     - 参数 text必需 , 有效的json字符串
>     - reviver：可选  一个转换结果的函数，将为对象的每个成员调用此函数
>
>     * JSON  不允许包含函数，但可以先将函数转换为字符串存储，之后再转换为函数
>
>         - ```js
>             var text = '{ "name":"Runoob", "alexa":"function () {return 10000;}", "site":"www.runoob.com"}';
>             var obj = JSON.parse(text);
>             obj.alexa = eval("(" + obj.alexa + ")");
>             
>             //eval(string) 函数 用来计算某字符串，并执行其中的javascript代码
>             
>             document.getElementById("demo").innerHTML = obj.name + " Alexa 排名：" + obj.alexa(); 
>             
>             
>             ===>
>                 Runoob Alexa 排名：10000
>             ```

### 3.JSON.stringfy()

---

> 1. **将javascript对象转换为字符串**  向服务器发送一般是字符串数据
>
>     ```
>     JSON.stringify(value[, replacer[, space]])
>     ```

> 参数：
>
>     -  value: 必需，要转换的javascrip的值，通常为对象或者数组
>       
>     -  replacer ：可选 用于转换数组结果的函数或数组
>
> 1. 如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。
>
>     - ```js
>         var obj = { "name":"Runoob", "alexa":function () {return 10000;}, "site":"www.runoob.com"};
>             var myJSON = JSON.stringify(obj);
>             document.getElementById("demo").innerHTML = myJSON;
>         
>         ===>
>             {"name":"Runoob","site":"www.runoob.com"}
>         ```
>
>     - 为了保留json数据中的函数
>
>         - ```js
>             var obj = { "name":"Runoob", "alexa":function () {return 10000;}, "site":"www.runoob.com"};
>             obj.alexa = obj.alexa.toString();  //将方法先转换为字符串
>             var myJSON = JSON.stringify(obj);
>             document.getElementById("demo").innerHTML = myJSON;
>             
>             ===>
>                 {"name":"Runoob","alexa":"function () {return 10000;}","site":"www.runoob.com"}
>             ```
>
> 2. 如果 replacer 是一个数组，则仅转换该数组中具有键值的成员。成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。
>
> 
>
> 可选，文本添加缩进、空格和换行符，如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。space 也可以使用非数字，如：\t。
>

### 4.jsonp实现跨域

---

1. 原生js实现

    - ```html
        <!DOCTYPE html>
        <html>
        <head>
        <meta charset="utf-8">
        <title>JSONP 实例</title>
        </head>
        <body>
        <div id="divCustomers"></div>
        <script type="text/javascript">
        function callbackFunction(result, methodName)
        {
            var html = '<ul>';
            for(var i = 0; i < result.length; i++)
            {
                html += '<li>' + result[i] + '</li>';
            }
            html += '</ul>';
            document.getElementById('divCustomers').innerHTML = html;
        }
        </script>
        <script type="text/javascript" src="https://www.runoob.com/try/ajax/jsonp.php?jsoncallback=callbackFunction"></script>
        </body>
        </html>
        ```

    2. jquery 实现

        ```html
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8">
            <title>JSONP 实例</title>
            <script src="https://cdn.static.runoob.com/libs/jquery/1.8.3/jquery.js"></script>    
        </head>
        <body>
        <div id="divCustomers"></div>
        <script>
        $.getJSON("https://www.runoob.com/try/ajax/jsonp.php?jsoncallback=?", function(data) {
            
            var html = '<ul>';
            for(var i = 0; i < data.length; i++)
            {
                html += '<li>' + data[i] + '</li>';
            }
            html += '</ul>';
            
            $('#divCustomers').html(html); 
        });
        </script>
        </body>
        </html>
        ```

        