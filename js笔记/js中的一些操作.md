## js中的一些操作笔记



#### 1.typeof 操作符

---

> typeof 操作符用来检测变量的数据类型
>
> 1. typeof "join"                                //返回 string
>
> 2. typeof 3.14                                 //返回number
>
> 3. typeof false                                //==> boolean
>
> 4. typeof [1,2,3,4]                          //==>object  **数组是一种特殊的对象类型**
>
> 5. typeof {name:"join",age:21}    //==>object
>
> 6. typeof null                                  //null表示空对象的引用  ==>object
>
> 7. typeof undefined                      // 是一个没有值得变量  ==>undefined
>
>     ​              
>
>     ​         *null 和undefined 值相等 但类型不等*

* undefined :是所有没有赋值变量的默认值，自动赋值
* null：主动释放一个变量引用的对象，表示一个变量不在指向任何对象地址



### 2.js数组对象的一些操作

---

#### reduce方法 

```
arr.reduce(callback,[initialValue])
```

定义：为数组中的每一个元素依次执行回调函数，不包括被删除或从未被赋值的元素

> ```js
> callback （执行数组中每个值的函数，包含四个参数）
> 
>     1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
>     2、currentValue （数组中当前被处理的元素）
>     3、index （当前元素在数组中的索引）
>     4、array （调用 reduce 的数组）
> 
> initialValue （作为第一次调用 callback 的第一个参数。）
> ```

### 3.js中字符串的一些操作

---

3. substring方法 用于提取字符串中介于两个指定的下标之间的字符
    - **substring(start,stop)**  //两个参数都是非负整数  ，最后一个参数可省略（那么返回的字符串会一直到字符串末尾）

### 4.文档操作手册

---

> 1.   **$(selector).empty()**    empty() 方法从被选元素移除所有内容，包括文本和子节点
> 2.   **$(selector).text()**        text() 方法设置或者返回被选元素的文本内容
>

### 5.DOM元素操作手册

---

> 1. **$(selector).index()**    index() 方法返回相对于其他指定元素的index位置（如果未找到 index() 返回 -1 ）
>
>      $(selector).index(element)  

### 6.特殊操作

---

#### 1. Object.assign() 方法：

>**Object.assign()** 方法用于将所有可枚举属性从一个或多个源对象复制到目标对象。返回目标对象
>
>Object.assign(target,...sources) 
>
>```js
>const target = {a:1,b:2}
>const source = {b:4,c:5}
>const returnTarget =Object.assign(target,source);
>console.log(returnTarget) //Object { a: 1, b: 4, c: 5 }
>//注意，Object.assign 不会跳过那些值为 [null] 或 [undefined]的源对象.
>```
>
>如果目标对象中的属性具有相同的键，则属性将被源中的属性覆盖。后来的源的属性将类似地覆盖早先的属性。
> `Object.assign` 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。该方法使用源对象的`[[Get]]`和目标对象的`[[Set]]`，所以它会调用相关 getter 和 setter。因此，它分配属性，而不仅仅是复制或定义新的属性。如果合并源包含getter，这可能使其不适合将新属性合并到原型中。为了将属性定义（包括其可枚举性）复制到原型，应使用[`Object.getOwnPropertyDescriptor()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor)和[`Object.defineProperty()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 。
> `String`类型和`Symbol`类型的属性都会被拷贝。
>
>链接：https://www.jianshu.com/p/e22113e3f614

#### 2.appendChild()和insertBefore()方法（都可以进行子节点的插入动作）

> 1. appendChild()方法 ：
>
> 定义：向节点的子节点列表的末尾添加新的子节点 （如果节点中已经有插入节点，那么这个子节点会从节点中删除，并直接插入到尾部）
>
> 2. insertBefore() 方法： ***node*.insertBefore(*要插入的节点对象,要插入位置对象节点*)**
>
>  定义向已有的子节点前插入一个新的子节点。
>
>  ```js
>  <!DOCTYPE html>
>  <html>
>  <head>
>  <meta charset="utf-8">
>  </head>
>  <body>
>  
>  <ul id="myList"><li>Coffee</li><li>Tea</li><li>Water</li><li>Milk</li></ul>
>  
>  <p id="demo">单击该按钮改变列表项的顺序</p>
>  <button onclick="myFunction()">点我</button>
>  <script>
>  function myFunction(){
>  	var list=document.getElementById("myList");
>  	var node=list.getElementsByTagName("li");
>  	list.insertBefore(node[3],node[1]);
>  }
>  </script>
>  
>  </body>
>  </html>
>  ```
>

### 7.for...in 和 for 和 for ...of

---

> 1. `for...in`循环出的是key，`for...of`循环出的是value
>
> 2. for...in   **遍历对象** 
>
>     - 用来遍历数组的下标类型为string
>
>     - 缺陷：
>         - 索引是字符串型的数字，因而不能直接进行几何运算
>         - 遍历顺序可能不是实际的内部顺序
>         - **for in会遍历数组所有的可枚举属性，包括原型。例如的原型方法method和name属性**
>
> 3. for...of **遍历数组**
>
>     - for...of 遍历的数组的元素值
>         - for..of适用遍历数/数组对象/字符串/map/set等拥有迭代器对象的集合.但是不能遍历对象,因为没有迭代器对象.与forEach()不同的是，它可以正确响应break、continue和return语句
>
> >如果是想用 for...of遍历普通对象的属性，可以通过和Object.key()搭配使用，先获取对象的所有key的数组
> >
> >```javascript
> >var student={
> >    name:'wujunchuan',
> >    age:22,
> >    locate:{
> >    country:'china',
> >    city:'xiamen',
> >    school:'XMUT'
> >    }
> >}
> >for(var key of Object.keys(student)){
> >    //使用Object.keys()方法获取对象key的数组
> >    console.log(key+": "+student[key]);
> >}
> >```
>
> 4. for