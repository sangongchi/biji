### 1.mock语法

---

#### 1.mock的语法规范包括两部分

> 1. 数据模板定义规范（Data Template Definition，DTD）
> 2. 数据占位符定义规范（Data Placeholder Definition，DPD）

- DTD部分学习

    - 数据模板中的每个属性由三个部分构成：属性名、生成规则、属性值：

        > 1. `'name|rule':value`
        > 2. 属性名和生成规则之间用竖线 | 分隔
        > 3. 生成规则有7种格式
        >     - `'name|min-max': value`
        >     - `'name|count': value`
        >     - `'name|min-max.dmin-dmax': value`
        >     - `'name|min-max.dcount': value`
        >     - `'name|count.dmin-dmax': value`
        >     - `'name|count.dcount': value`
        >     - `'name|+step': value`
        >
        > 4. 属性值可以包含占位符  @占位符

    - 生成规则以及示例

        1. 属性值是字符串 String

            - `'name|min-max': string`

                通过重复 `string` 生成一个字符串，重复次数大于等于 `min`，小于等于 `max`。

            - `'name|count': string`

                通过重复 `string` 生成一个字符串，重复次数等于 `count`。

        2. 属性值是数字 Number

            - `'name|+1': number`

                属性值自动加 1，初始值为 `number`。

            - `'name|min-max': number`

                生成一个大于等于 `min`、小于等于 `max` 的整数，属性值 `number` 只是用来确定类型。

            - `'name|min-max.dmin-dmax': number`

                生成一个浮点数，整数部分大于等于 `min`、小于等于 `max`，小数部分保留 `dmin` 到 `dmax`位。

            ```js
            Mock.mock({
                'number1|1-100.1-10': 1,
                'number2|123.1-10': 1,
                'number3|123.3': 1,
                'number4|123.10': 1.123
            })
            // =>
            {
                "number1": 12.92,
                "number2": 123.51,
                "number3": 123.777,
                "number4": 123.1231091814
            }
            ```

        3. 属性值是布尔类型  Boolean

            - `'name|1': boolean`

                随机生成一个布尔值，值为 true 的概率是 1/2，值为 false 的概率同样是 1/2。

            - `'name|min-max': value`

                随机生成一个布尔值，值为 `value` 的概率是 `min / (min + max)`，值为 `!value` 的概率是 `max / (min + max)`。

        4. 属性值是对象 Object

            - `'name|count': object`

                从属性值 `object` 中随机选取 `count` 个属性。

            - `'name|min-max': object`

                从属性值 `object` 中随机选取 `min` 到 `max` 个属性。

            - ```js
                Mock.mock({
                    "demo11|2-4": {
                        "110000": "北京市",
                        "120000": "天津市",
                        "130000": "河北省",
                        "140000": "山西省",
                        "150000": "宁夏省",
                        "160000": "陕西省"
                    }
                })
                 
                // 结果：
                {
                    "demo11": {
                        "120000": "天津市",
                        "130000": "河北省",
                        "140000": "山西省"
                    }
                }
                ```

        5. 属性值是数组 Array

            - `'name|1': array`

                从属性值 `array` 中随机选取 1 个元素，作为最终值。

            - `'name|+1': array`

                从属性值 `array` 中顺序选取 1 个元素，作为最终值。

            - `'name|min-max': array`

                通过重复属性值 `array` 生成一个新数组，重复次数大于等于 `min`，小于等于 `max`。

            - `'name|count': array`

                通过重复属性值 `array` 生成一个新数组，重复次数为 `count`。

            - ```js
                
                // 代码：
                Mock.mock({
                    "demo13|1": [
                        "AMD",
                        "CMD",
                        "UMD"
                    ]
                })
                 
                // 结果：
                {
                    "demo13": "CMD"
                }
                 
                // eg：对象数组中随机选取一个元素
                 
                // 代码：
                Mock.mock({
                    "demo14|1": [
                        {
                            "1":"一",
                            "2":"二",
                            "3":"三"
                        },
                        {
                            "4":"四",
                            "5":"五",
                        },
                        {
                            "6":"六",
                            "7":"七"
                        }
                    ]
                });
                    
                // 结果：
                {
                    "demo14": {
                        "6": "六",
                        "7": "七"
                    }
                }
                ```

            - 

        6. 属性值是Function

            - ![1567916388392](H:\biji\typora_imgs\1567916388392.png)

            - ```
                'name': function
                ```

                执行函数 `function`，取其返回值作为最终的属性值，函数的上下文为属性 `'name'` 所在的对象。

        7. 属性值是正则表达式 RegExp

            - ```
                'name': regexp
                ```

                根据正则表达式 `regexp` 反向生成可以匹配它的字符串。用于生成自定义格式的字符串。

                ```js
                Mock.mock({
                    'regexp1': /[a-z][A-Z][0-9]/,
                    'regexp2': /\w\W\s\S\d\D/,
                    'regexp3': /\d{5,10}/
                })
                // =>
                {
                    "regexp1": "pJ7",
                    "regexp2": "F)\fp1G",
                    "regexp3": "561659409"
                }
                ```

- ## 数据占位符定义规范 DPD

    1. *占位符* 只是在属性值字符串中占个位置，并不出现在最终的属性值中。

        *占位符* 的格式为：

        ```
        @占位符
        
        
        
        @占位符(参数 [, 参数])
        ```

        **注意：**

        1. 用 `@` 来标识其后的字符串是 *占位符*。
        2. *占位符* 引用的是 `Mock.Random` 中的方法。
        3. 通过 `Mock.Random.extend()` 来扩展自定义占位符。
        4. *占位符* 也可以引用 *数据模板* 中的属性。
        5. *占位符* 会优先引用 *数据模板* 中的属性。
        6. *占位符* 支持 *相对路径* 和 *绝对路径*。

        ```js
        Mock.mock({
            name: {
                first: '@FIRST',
                middle: '@FIRST',
                last: '@LAST',
                full: '@first @middle @last'
            }
        })
        // =>
        {
            "name": {
                "first": "Charles",
                "middle": "Brenda",
                "last": "Lopez",
                "full": "Charles Brenda Lopez"
            }
        }
        ```

#### 2. Mock占位符

- @ip -> 随机输出一个ip；
- @id -> 随机输出长度18的字符，不接受参数；
- “array|1-10” -> 随机输出1-10长度的数组，也可以直接是固定长度；
- “object|2” -> 输出一个两个key值的对象，
- “@image()” 返回一个占位图url，支持size, background, foreground, format, text；
- ![img](https://img-blog.csdnimg.cn/20181105225824713.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzI1NDc2Ng==,size_16,color_FFFFFF,t_70)

#### 3.自定义响应

![1567916463173](H:\biji\typora_imgs\1567916463173.png)