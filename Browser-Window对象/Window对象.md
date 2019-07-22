## Window对象属性

### 1. 常用的属性

==**存储数组的做法：**==

	var weekArray = ['周一'、'周二'、'周三'、'周四'、'周五']
存：localStorage.setItem('weekDay',JSON.stringify(weekArray));
取： weekArray = JSON.parse(localStorage.getItem('weekDay'));

#### 1.1 Storage

> 1. **Storage** 提供了访问特定域名下的会话存储或本地存储的功能，例如，可以添加、修改或删除存储的数据项。
>
> 2. 如果你想要==操作一个域名的会话存储==，可以使用 [`Window.sessionStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage)；
>
>     如果想要操作==一个域名的本地存储==，可以使用 [`Window.localStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/localStorage)。
>
> 3. 属性  Stotage.length   将返回一个整数，存储Storage 对象中数据项的数量   
>
> 4. 包含的方法
>
>     - [`Storage.key()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/key)
>
>         该方法接受一个数值 n 作为参数，并返回存储中的第 n 个键名。
>
>     - [`Storage.getItem()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/getItem)
>
>         该方法接受一个键名作为参数，返回键名对应的值。
>
>     - [`Storage.setItem()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/setItem)
>
>         该方法接受一个键名和值作为参数，将会把键值对添加到存储中，如果键名存在，则更新其对应的值。
>
>     - [`Storage.removeItem()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/removeItem)
>
>         该方法接受一个键名作为参数，并把该键名从存储中删除。
>
>     - [`Storage.clear()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/clear)
>
>         调用该方法会清空存储中的所有键名。

#### 1.2localStorage属性 （只读）

> 1. `localStorage` 属性允许你访问一个[`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 源（origin）的对象 [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage)；其存储的数据能在跨浏览器会话保留。`localStorage` 类似 [`sessionStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage)，但其区别在于：存储在 `localStorage` 的数据可以长期保留；而当页面会话结束——也就是说，当页面被关闭时，存储在 `sessionStorage` 的数据会被清除 。
>
> 2. `localStorage` 中的键值对总是以字符串的形式存储。 (需要注意, 和js对象相比, 键值对总是以字符串的形式存储意味着数值类型会自动转化为字符串类型)
>
> 3. 下面的代码片段访问了当前域名下的本地 [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage) 对象，并通过 [`Storage.setItem()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage/setItem) 增加了一个数据项目。
>
>     ```js
>     localStorage.setItem('myCat', 'Tom');
>     ```
>
>     该语法用于读取 `localStorage` 项，如下:
>
>     ```js
>     let cat = localStorage.getItem('myCat');
>     ```
>
>     该语法用于移除 `localStorage` 项，如下:
>
>     ```js
>     localStorage.removeItem('myCat');
>     ```
>
>     该语法用于移除所有的 `localStorage` 项，如下:
>
>     ```js
>     // 移除所有
>     localStorage.clear();
>     ```

#### 1.3sessionStorage 属性

> 1. `sessionStorage` 属性允许你访问一个 session [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage) 对象。它与 [`localStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/localStorage) 相似，不同之处在于 localStorage 里面存储的数据没有过期时间设置，而存储在 sessionStorage 里面的数据在页面会话结束时会被清除。页面会话在浏览器打开期间一直保持，并且重新加载或恢复页面仍会保持原来的页面会话。
>
> 2. ```js
>     // 保存数据到 sessionStorage
>      sessionStorage.setItem('key', 'value');
>     ```
>
>  // 从 sessionStorage 获取数据
>  let data = sessionStorage.getItem('key');
>
>  // 从 sessionStorage 删除保存的数据
>  sessionStorage.removeItem('key');
>
>  // 从 sessionStorage 删除所有保存的数据
>  sessionStorage.clear();
>  ```
> 
>   
>  ```

