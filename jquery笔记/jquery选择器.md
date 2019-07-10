### jquery选择器

---

| 语法                    | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| $(this)                 | 选择当前HTML元素                                             |
| $('p:first')            | 选择第一个p元素                                              |
| ==$('ul li:first')==    | 选择第一个ul元素下的第一个li元素                             |
| $('ul li:first-child')  | 选择每个ul元素下的第一个li元素                               |
| $('[href]')             | 选择所有带有href的属性                                       |
| $('a[target='_blank']') | 选择所有target属性值等于_blank的a元素                        |
| $(':button')            | 选择所有type="button" 的<input><button>元素（匹配所有的button） |
| $('tr:even')            | 选择偶数位置的tr元素                                         |
| $('tr:odd')             | 选择奇数位置的tr元素                                         |

