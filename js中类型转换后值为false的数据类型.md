### js中值为false的数据类型

---

| 数据类型     | 对应bool值 |
| ------------ | ---------- |
| false        | false      |
| null         | false      |
| undefined    | false      |
| 空字符串\|‘’ | false      |
| 数字0        | false      |
| 数字NaN      | false      |

```js
var array = [false, null, undefined, '', 0, NaN]
for (let i = 0; i < array.length; i++) {
	if (!array[i]) {
        console.log(`${array[i]}类型转换对应的bool值为false`);
        /*==>false类型转换对应的bool值为false
            null类型转换对应的bool值为false
            undefined类型转换对应的bool值为false
            类型转换对应的bool值为false
            0类型转换对应的bool值为false
            NaN类型转换对应的bool值为fals*/
	}
}
```

