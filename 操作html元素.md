### 1.js操作元素

---

getElementById : 该方法返回指定ID 的第一个对象的引用

getElementsByClassName: 该方法返回所有**指定类名的集合**

> 1. $(selector).innerHTML=''   //该方法用于清空该选择器的所有元素

>  1. 元素内添加内容
>
>     - innerText     //文本内容
>         - ==元素.innerText="要追加的内容"== **这么做会覆盖原有的文本内容**
>     - innerHTML    // HTML内容
>         - 元素.innerHTML+="<h3>在原有内容的基础上添加h3的文本内容</h3>"
>     - appendChild
>         - 蒋创建的元素以及内容添加到页面或者元素中
>
>  2. 创建元素及内容
>
>      - 创建元素节点 ==createElement==
>
>          例： document.createElement(nodename)    **document.createment("BUTTON")** 括号中填写要创建的标签名称
>
>      - 创建内容 ==createTextNode==
>
>          document.createText("文本节点的文本")   
>
>  3. 删除元素
>
>      - removeChild()
>
>          - 通过id获取删除
>
>              ```javascript
>              var idObject = document.getElementById('sidebar');
>              if (idObject != null){
>                  idObject.parentNode.removeChild(idObject);
>              }
>              ```
>
>          - 通过class获取删除
>
>              ```javascript
>              var paras = document.getElementsByClassName('paginator');
>              for(i=0;i<paras.length;i++){
>                  //删除元素 元素.parentNode.removeChild(元素);
>                  if (paras[i] != null)
>                      paras[i].parentNode.removeChild( paras[i]);
>              }
>              ```
>
>          - 清空所有元素
>
>              ```javascript
>              function removeAllChild()  {
>                  var div = document.getElementById("div1");
>                  while(div.hasChildNodes()) //当div下还存在子节点时 循环继续
>                  {
>                      div.removeChild(div.firstChild);
>                  }
>              }
>              ```
>
>              清空所有元素的方法封装
>
>              ```javascript
>              function removeElement(element){
>                  elementp=element.parentNode;
>                  if(elementp){
>                      elementp.removeChilid(element)
>                  }
>              }
>              ```
>
>              
>
>  

###  2.jquery动态操作元素

---

>1. 创建元素
>
>`$(function(){`
>
>​	`var $h1=$("<h1></h1")`
>
>`})`
>
>2. 创建文本
>
>```javascript
>$(function(){
>   var $h1=$("<h1>文本内容</h1>")
>})
>```
>
>3. 创建属性
>
>`$(function(){`
>
>​	``var $h1=​$('<h1 class="red" title="biaoti">wenben</h1>')`
>
>`})`
>
>4. 使用jquery插入元素
>
>在节点内部插入内容
>
>   - append()方法  在被选元素的结尾（仍在内部）插入指定内容
>
>       - $(selector).append(content)
>
>       - $(selector).append(function(index,html))   
>
>         index - 可选。接受选择器的 index 位置。
>
>         html - 可选。接受选择器的当前 HTML。
>
>       - ```javascript
>         $(document).ready(function(){
>         $("button").click(function(){
>           $("p").append(function(n){
>             return "<b>This p element has index " + n + "</b>";
>           });
>         });
>         });
>         ```
>       ```
>       
>       - **$(content).appendto(selector)**
>       
>       **append()和appendto()  方法执行结果一样，但内容和选择器的书写位置不一样**
>       ```
>
>   - prepend()方法在被选元素的开头仍在内部  插入指定的内容
>
>       - prepend() prependto
>       - $(selector).prepend(content)
>       - $(selectot).prepend(function(index,html))   //function()中的参数可选
>       -  $(content).prepend(selector)
>
>   - **after() 方法在被选元素后插入指定的内容**
>
>   - **before() 方法在被选元素前插入指定的内容**
>
>     语法：$(selector).before(content)
>
>   - **insertAfter()把匹配的元素插入到另一个指定的元素集合的后面** 选择器外部
>
>     注释：如果该方法用于已有元素，这些元素会被从当前位置移走，然后被添加到被选元素之后。
>
>     语法：$(content).insertAfter(selector)
>
>   - **insertBefore()把匹配的元素插入到另一个指定的元素集合的前面** 选择器外部
>
>      注释：如果该方法用于已有元素，这些元素会被从当前位置移走，然后被添加到被选元素之前。
>
>   ​        语法：$(content).insertBefore(selector)
>
>[参考地址](https://blog.csdn.net/qq_27626333/article/details/51927022) 

### 3.修改dom属性

---

> 1. doucument.creatAttribute(attributename)  创建一个属性
> 2. removeAttribute：删除一个属性
> 3. document.getElementsByTagName("a")[0].getAttribute("target");  //获取元素属性值
> 4. document.getElementsByTagName("INPUT")[0].setAttribute("type","button"); //设置元素的属性 以及值
> 5. setAttributeNode() 方法用于添加新的属性节点 *element*.setAttributeNode(*attributenode*) //建立一个节点
> 6. getAttributeNode：获取一个节点作为对象
> 7. $(selector).attributes   获取元素的属性  返回一个对象
>
> ```javascript
> var att=document.createAttribute("class");  
> att.value="democlass"; //设置属性值
> document.getElementsByTagName("H1")[0].setAttributeNode(att);  //将设置的属性添加到对应的元素上
> ```