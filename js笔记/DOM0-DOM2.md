#### 1. 0级dom

> 1. 两种形式，
>
>     - 在标签内写 onclick() 事件
>
>     - js中  onclick=function(){}
>
>         ```js
>         <input id="myButton" type="button" value="Press Me" οnclick="alert('thanks');" >
>             
>            document.getElementById("myButton").onclick = function () {
>             alert('thanks');
>         } 
>         ```
>
>         
>
>     

#### 2. 2级dom

> 1. addEventListener()和removeEventListener()              添加移除事件处理程序
>
> 2. 两个方法都有3个参数（事件名，处理程序函数，true|false）
>
>     第三个函数： 为true，表示在捕获阶段调用，为false  表示在冒泡阶段调用
>
>     - addEventListener():可以为元素添加多个事件处理程序，触发时会按照添加顺序依次调用。
>
>     - removeEventListener():不能移除匿名添加的函数。
>
>     - ```js
>         document.getElementById("myTest").attachEvent("onclick", function(){alert(1)});
>         //等价于
>         document.getElementById("myTest").addEventListener("click", function(){alert(1)}, false);
>         ```
>
> 3. 2级dom包含3个事件：  事件捕获阶段、处于目标阶段和事件冒泡阶段
> 4. dom2 事件不会覆盖，dom0 事件后边会覆盖前面