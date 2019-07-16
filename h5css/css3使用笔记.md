### 1.box-shadow盒子阴影

---

> 1. 书写形式 box-shadow:**h-shadow v-shadow** blur spread color inset; // 后边几个参数是可选的 
>     - 参数依次对应 **水平偏移量  垂直偏移量（允许为负值）**  模糊距离  阴影大小 颜色  内阴影 （默认为外阴影）；
>

### 2.css选择器

| 选择器                     | 示例                                                      | 说明                                                        |
| -------------------------- | --------------------------------------------------------- | ----------------------------------------------------------- |
| A,B                        |                                                           | 同时匹配A和B                                                |
| A B                        |                                                           | 后代选择器 选择所有A元素中的B元素                           |
| A>B                        |                                                           | 选择所有父级是A元素的B元素                                  |
| A+B                        |                                                           | 选择所有紧接着A元素之后的B元素(兄弟元素之间)                |
| [attribute]                |                                                           | 选择所有含attribute属性的元素                               |
| [attribute=value]          |                                                           | 选择所有属性等于该属性值得元素                              |
| ==[attribute~=value]==     | [title~=flower]                                           | 选择标题包含flower的素有元素                                |
| ==[attribute\|=language]== | [lang\|=en]                                               | 选择lang属性以en为开头的所有元素 (用在HTML头部元素的匹配上) |
| [attribute$=value]         | a[src$=".pdf"]                                            | 选择每一个src属性以**.pdf**结尾的元素                       |
| [attribute *= value]       | a[src*="runoob"]                                          | 选择每一个src属性中含有 **runoob** 的元素                   |
| [*attribute*^=*value*\]    | a[src^="https"]                                           | 选择每一个src属性以**https**开头的元素                      |
| :last-child                |                                                           | 选择某元素下的最后一个子元素                                |
| :first-child               |                                                           |                                                             |
| :only-child                | p:only-child                                              | 选择每个p元素是其父级的唯一子元素                           |
| :nth-child(n)              | p:nth-child(n)                                            | 选择p元素下的第n个子元素   可以做奇数和偶数                 |
| :root                      |                                                           | 选择文档的根元素                                            |
| :valid 和:invalid          | input:valid（假设是邮箱，他会匹配输入的邮箱输入是否合法） | 用于匹配输入的值是否为合法的元素                            |

### 3. background

---

>background：bg-color bg-image position/bg-size bg-repeat bg-origin bg-clip bg-attachment initial|inherit;
>
>​			样色	图片	位置		是否重复   定位区域 边框绘制区域 是否固定	
>
>**1. background-clip: border-box|padding-box|content-box**
>
>
>
>