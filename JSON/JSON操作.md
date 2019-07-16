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
>     - **在js中想要首先将json数据复制给js变量需要加引号**，否则会报错
>         - `var text = '{ "name":"Runoob", "initDate":"2013-12-14", "site":"www.runoob.com"}';`
>             ` var obj = JSON.parse(text);`
>
>     - 参数 text必需 , 有效的json字符串
>     - reviver：可选  一个转换结果的函数，将为对象的每个成员调用此函数
>     - 

### 3.JSON.stringfy()

---

> 1. ```
>     JSON.stringify(value[, replacer[, space]])
>     ```
>
>     - value: 必需，要转换的javascrip的值，通常为对象或者数组
>
>     - replacer ：可选 用于转换数组结果的函数或数组
>
>         如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。
>
>         如果 replacer 是一个数组，则仅转换该数组中具有键值的成员。成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。
>
>     - space:
>
>         可选，文本添加缩进、空格和换行符，如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。space 也可以使用非数字，如：\t。