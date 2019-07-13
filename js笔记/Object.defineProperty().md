### 1.枚举属性：

> 枚举的属性会影响以下三个函数的结果：
>
> - ==for...in==      使用for..in循环时，返回的是所有能够通过对象访问的、可枚举的属性，既包括存在于实例中的属  -性，也包括存在于原型中的实例。这里需要注意的是使用for-in返回的属性因各个浏览器厂商遵循的标准不一致导- -致对象属性遍历的顺序有可能不是当初构建时的顺序。（**实例+原型中的可枚举属性**）
>
> - ==Object.keys(object)==    说明该方法只能返回对象本身具有的可枚举属性。（字符串数组）
>
>      object ,可以是您创建的对象或现有文档对象模型 (DOM) 对象(包含属性和方法的对象)。 
>
> ​        数组中属性名的排列顺序和使用 [`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环遍历该对象时返回的顺序一致 。如果对象的                                                键-值都不可枚举，那么将返回由键组成的数组         **但不包括原型中的属性**
>
> - ==JSON.stringify==   此方法也只能读取对象本身的可枚举属性，并序列化为JSON字符串,得到string类型
> - ![img](https://images2017.cnblogs.com/blog/1158910/201710/1158910-20171017105509912-1136366898.png)

###  2.ObjectDefineProperty

---

- ```
    Object.defineProperty(object, propertyname, descriptor)
    /*
    	object  :必需  要在其上添加或修改属性的对象 可能是javascript对象或者 dom对象
    	propertyname:必需  一个包含属性名称的字符串
    	decriptor: 必需  属性描述符。他可以针对数据属性或范文器属性
    */
    ```

- ObjectDefineProperty的作用
    - 用于给对象新增属性，和修改对象的属性
        - 向对象添加新属性。 当对象不具有指定的属性名称时，发生此操作。
        - 修改现有属性的特性。 当对象已具有指定的属性名称时，发成此操作。

- 描述符对象中会提供属性定义，用于描述数据属性或访问器属性的特性。 描述符对象是` Object.defineProperty` 函数的参数。

    若要向对象添加多个属性或修改多个现有属性，可使用 `Object.defineProperties `函数 (JavaScript)。

### 3.Object.getOwnProperty-----

---

> 1. **Object.getOwnPropertyNames(obj)**
>
>     - 返回一个数组，该数组对元素是obj自身拥有的枚举或不可枚举属性名称的字符串。数组中的不可枚举属性的顺序未定义
>
>     - ```javascript
>         var obj={0:'a',1:'b',2:'c'}
>         var pro= Object.getOwnPropertyNames(obj)
>         console.log(pro)
>         pro.forEach(function(val,index,arry){      //val 属性  index  当前属性的索引值   arry  该对象
>         	console.log(`${index}:${val}==>${obj[val]}----${arry}`)
>         })
>         ```
>
> 2. **Object.getOwnPropertyDescriptor(obj,prop)**     （obj->要查找的目标对象  prop  目标对象内置属性名称）
>
>     - 该方法返回指定对象上一个自有属性对应的属性描述符。（自由属性指的是直接赋予该对象的属性，不需要从原型链上进行查找的属性）
>
>     - ```javascript
>         o={bar:42}
>         Object.defineProperty(o,'baz',{
>         	value:8654202,
>         	writable:false,
>         	enumerable:false
>         })
>         d=Object.getOwnPropertyDescriptor(o,'baz')
>         d2=Object.getOwnPropertyDescriptor(o,'bar')
>         console.log(d)
>         console.log('------')
>         console.log(d2)
>         ```
>
>     - **Object.getOwnPropertyDescriptors(obj)**
>
>         - 所指定对象的所有自身属性的描述符，如果没有任何自身属性，则返回空对象。
>
>         - ```javascript
>             o={bar:42}
>             Object.defineProperty(o,'baz',{
>             	value:8654202,
>             	writable:false,
>             	enumerable:false
>             })
>             d=Object.getOwnPropertyDescriptors(o)
>             console.log(d)
>             ----
>             /*{ bar:
>                { value: 42,
>                  writable: true,
>                  enumerable: true,
>                  configurable: true },
>               baz:
>                { value: 8654202,
>                  writable: false,
>                  enumerable: false,
>                  configurable: false } }*/
>             
>             ```
>
>         - 







### 4. Object.getPropertyOf()

> 1. 该方法返回指定对象的原型（内部【Prototype】属性的值） 返回给定对象的原型。如果没有继承属性，则返回 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null) 。
> 2. `Object.getPrototypeOf(object)`
> 3. 

### 5.JS对象的描述符

1. > 下边属性定义为false时
    >
    > configurable:  变量不可配置，（为该变量定义配置会报错） 变量不可被删除和修改
    >
    > enumerable:  变量不能在遍历器例如（for...in）和Object.key() 中被读取出来，不可以被遍历
    >
    > writable:        变量不可被重新赋值
    >
    > 可以简答的理解为： configurable  控制是否可以删除   writable 控制是否可以修改  

    

- js对象中有两种描述符： 数据描述符和存取描述符
- 注意事项：
    - 1. 数据描述符合存储描述符都具备configurable（控制是否可以删除） 、enumerable（控制是否可以枚举） 属性
    - 2. 描述符不具备value、writetable、set和get任意一个关键字都被视作一个数据描述符
        3. （value或writable）和（get和set）不能同时存在，然后只要定义了set和get或其中一个都是存取描述符![img](https://img2018.cnblogs.com/blog/746178/201811/746178-20181125151939264-1945621286.png)

    - > 1. 可写入性：writeable
        >
        >     当writeable   的值为false以后，无法再对属性value进行直接赋值修改，但是人可以使用Object.defineProperty()方法进行修改。
        >
        > ```javascript
        > Object.defineProperty(obj, 'a', {
        >     value: 1,
        >     writable: false,
        >     enumerable: true,
        >     configurable: true
        > });
        > console.log(Object.getOwnPropertyDescriptor(obj, 'a'));  // {value: 1, writable: false, enumerable: true, configurable: true}
        > console.log(obj.a);  // 1
        > 
        > // 尝试修改a的值
        > // 方法1，直接赋值
        > obj.a = 2;
        > 
        > console.log(Object.getOwnPropertyDescriptor(obj, 'a'));  // {value: 1, writable: true, enumerable: true, configurable: true}
        > console.log(obj.a);  // 1
        > 
        > // 方法2，Object.defineProperty
        > Object.defineProperty(obj, 'a', {
        >     value: 3,
        >     writable: false,
        >     enumerable: true,
        >     configurable: true
        > });
        > 
        > console.log(Object.getOwnPropertyDescriptor(obj, 'a'));  // {value: 3, writable: false, enumerable: true, configurable: true}
        > console.log(obj.a);  // 3
        > ```
        >
        > 2. configurable()
        >
        >     - **总结以上信息，可配置性configurable有如下特征：**
        >
        >         1. configurable值为true时，可以删除属性值；configurable值为为false时，不能删除属性值；
        >
        >         2. configurable值为true时，可以修改任意描述符属性值；configurable值为false时，修改规则遵循3，4，5。
        >
        >         3. configurable值为为false时，如果writable值为true，可以使用Object.defineProperty()方法改变value值；configurable值为为false时，如果writable值为false，不能使用Object.defineProperty()方法改变value值；
        >
        >         4. configurable值为false时，如果writable值为true，可以修改其为false；configurable值为false时，如果writable值为false，不能修改其为true；
        >
        >         5. configurable值为false时，除3，4两种情况，不可修改描述符属性值。
        >
        >             
        >
        >         链接：https://www.jianshu.com/p/85fd56441621

### 6.访问器属性描述符

---

get方法   读取属性时会触发隐藏的getter操作，设置了get或set方法的属性，会自动变为访问器属性，不在从value中读取属性值。用Object.getOwnPropertyDescriptor方法也不再返回value和writable。

```js
var obj={
	get a(){
		return 1
	}
}
console.log(Object.getOwnPropertyDescriptor(obj,'a'));/*{ get: [Function: get a],
															set: undefined,
															enumerable: true,
															configurable: true }*/ 
console.log(obj.a) //1

----
var obj = {
    _a: 1,
    _doubleA: 2
};
Object.defineProperty(obj, 'a', {
    get: function() {
        return this._a;
    },
    // set方法能接收用户传入的值，并利用该值对对象的任一属性做操作
    set: function(val) {
        this._a = val;
        this._doubleA = 2 * this._a;
    }
});

console.log(Object.getOwnPropertyDescriptor(obj, 'a'));  
// {get: ƒ, set: ƒ, enumerable: false, configurable: false}
console.log(Object.getOwnPropertyDescriptor(obj, '_a'));  
// {value: 1, writable: true, enumerable: true, configurable: true}
console.log(Object.getOwnPropertyDescriptor(obj, '_doubleA')); 
// {value: 2, writable: true, enumerable: true, configurable: true}
console.log(obj.a);  // 1
console.log(obj._a); // 1
console.log(obj._doubleA); // 2


```

### 7.不同方法创建对象属性以后的属性描述符默认值

> 1. 对象字面量指定属性
>
>     ```js
>     // 普通的对象字面量定义方法,是数据属性，writable，enumerable和configurable默认都是true
>     var obj1 = {
>         a: 1
>     };
>     // 对象字面量中指定某个属性的get方法或者set方法，是访问器属性，enumerable和configurable默认是true，get或者set仅指定一者的情况下另一个为undefined
>     var obj2 = {
>         get a() {
>             return 1;
>         }
>     }
>     console.log(Object.getOwnPropertyDescriptor(obj1, 'a')); // {value: 1, writable: true, enumerable: true, configurable: true}
>     console.log(Object.getOwnPropertyDescriptor(obj2, 'a')); // {get: ƒ, set: undefined, enumerable: true, configurable: true}
>     ```
>
> 2. 构造函数
>
>     ```js
>     // 构造函数定义方法,是数据属性，writable，enumerable和configurable默认都是true
>     function Obj() {
>         this.a = 1;
>     }
>     var obj = new Obj;
>     console.log(Object.getOwnPropertyDescriptor(obj, 'a')); // {value: 1, writable: true, enumerable: true, configurable: true}
>     ```
>
> 3. **Object.create()方法** (该方法其实是在一个空对象的原型上添加属性并返回该对象)
>
>     ```
>     var obj = Object.create({a:1});
>     // 返回一个空对象
>     //  console.log(obj); // {}
>     console.log(Object.getOwnPropertyDescriptor(obj, 'a'));  // undefined
>     // 返回的对象，其原形上面该属性为数据属性，writable，enumerable和configurable默认都是true
>     console.log(Object.getOwnPropertyDescriptor(obj.__proto__, 'a')); // {value: 1, writable: true, enumerable: true, configurable: true}
>     ```
>
> 4. Object.defineProperty() 方法
>
>      
>
>     ```js
>     var obj = {};
>     
>     // Object.defineProperty()方法指定的属性，如果描述符对象为空，默认是数据属性，value默认是undefined，writable，enumerable和configurable默认都是false
>     Object.defineProperty(obj, 'a', {
>     });
>     console.log(Object.getOwnPropertyDescriptor(obj, 'a'));  // {value: undefined, writable: false, enumerable: false, configurable: false}
>     
>     // Object.defineProperty()方法指定的数据属性，value默认是undefined，writable，enumerable和configurable默认都是false
>     Object.defineProperty(obj, 'b', {
>         value: 1
>     });
>     console.log(Object.getOwnPropertyDescriptor(obj, 'b'));  // {value: 1, writable: false, enumerable: false, configurable: false}
>     
>     // Object.defineProperty()方法指定的访问器属性，set或者get未指定默认是undefined，enumerable和configurable默认都是false
>     Object.defineProperty(obj, 'c', {
>         get: function() {
>             return 1;
>         }
>     });
>     console.log(Object.getOwnPropertyDescriptor(obj, 'c'));  // {get: ƒ, set: undefined, enumerable: false, configurable: false}
>     
>     // 用Object.defineProperties()方法同时定义的多个属性，与Object.defineProperty()方法定义的表现相同
>     Object.defineProperties(obj, {
>       'd': {
>         value: true,
>         writable: true
>       },
>       'e': {
>         value: 'Hello',
>         writable: false
>       }
>       // etc. etc.
>     });
>     console.log(Object.getOwnPropertyDescriptor(obj, 'd'));  // {value: 1, writable: false, enumerable: false, configurable: false}
>     console.log(Object.getOwnPropertyDescriptor(obj, 'e'));  // {get: ƒ, set: undefined, enumerable: false, configurable: false}
>     ```