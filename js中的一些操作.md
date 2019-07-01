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



