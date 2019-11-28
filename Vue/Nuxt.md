## NUXT

### 1. 安装使用Nuxt 

---

#### 1.1 初始化项目(第一种方法)

> ```js
> vue init nuxt/模板 <你的项目名字>  安装响应模板的   
> vue init nuxt/koa demo   安装koa的Nuxt模板
> vue init nuxt/express demo1 安装express的nuxt模板   
> ```

#### 1.2 初始化项目2（第二种方法）

> 1. npx create-nuxt-app <项目名>
> 2. yarn create nuxt-app <项目名>

### 2.项目配置

---

#### 2.1项目的目录结构

> ```js
> |-- .nuxt                            // Nuxt自动生成，临时的用于编辑的文件，build
> |-- assets                           // 用于组织未编译的静态资源入LESS、SASS 或 JavaScript
> |-- components                       // 用于自己编写的Vue组件，比如滚动组件，日历组件，分页组件
> |-- layouts                          // 布局目录，用于组织应用的布局组件，不可更改。
> |-- middleware                       // 用于存放中间件
> |-- pages                            // 用于存放写的页面，我们主要的工作区域
> |-- plugins                          // 用于存放JavaScript插件的地方
> |-- static                           // 用于存放静态资源文件，比如图片
> |-- store                            // 用于组织应用的Vuex 状态管理。
> |-- .editorconfig                    // 开发工具格式配置
> |-- .eslintrc.js                     // ESLint的配置文件，用于检查代码格式
> |-- .gitignore                       // 配置git不上传的文件
> |-- nuxt.config.json                 // 用于组织Nuxt.js应用的个性化配置，已覆盖默认配置
> |-- package-lock.json                // npm自动生成，用于帮助package的统一性设置的，yarn也有相同的操作
> |-- package-lock.json                // npm自动生成，用于帮助package的统一性设置的，yarn也有相同的操作
> |-- package.json                    // npm包管理配置文件
> ```

#### 2.2 配置项目的ip和端口号 （需要重启服务）

> 1. 需要在 跟目录下的package.json 中对config进行配置
>
>     - ==/package.json==   将端口号修改为 1818 ip改为127.0.0.1
>
>         ```json
>           "config":{
>             "nuxt":{
>               "host":"127.0.0.1",
>               "port":"1818"
>             }
>           },
>         ```

#### 2.3 配置全局的CSS样式

> 1. 添加全局的样式可以再  nuxt.config.js  里进行操作
>
>     - 首先建立自己的css文件  一般放在 /assets/css/   文件中
>
>         /assets/css/normailze.css
>
>         ```css
>         html{
>             color:red;
>         }
>         ```
>
>     - /nuxt.config.js
>
>         ```js
>           css:['~assets/css/normailze.css'],
>         ```

#### 2.4 在nuxt.config.js 里对webpack 进行配置 （会覆盖webpack的基本配置）

> ```js
> build: {
>  //添加url-loader 在build中进行配置
>     loaders:[
>       {
>         test:/\.(png|jpe?g|gif|svg)$/,
>         loader:"url-loader",
>         query:{
>           limit:10000,
>           name:'img/[name].[hash].[ext]'
>         }
>       }
>     ],
>  
>     /*
>     ** eslint配置 ，可以根据自己的需要进行删除
>     */
>     extend (config, { isDev, isClient }) {
>       if (isDev && isClient) {
>         config.module.rules.push({
>           enforce: 'pre',
>           test: /\.(js|vue)$/,
>           loader: 'eslint-loader',
>           exclude: /(node_modules)/
>         })
>       }
>     }
>   }
> ```

### 3. 路由配置以及参数 传递

---

#### 3.1 动态路由

> ```js
> pages/
> --| _category/
> -----| _subCategory/
> --------| _id.vue
> --------| index.vue
> -----| _subCategory.vue
> -----| index.vue
> --| _category.vue
> --| index.vue
> ```
>
> ```js
> router: {
>   routes: [
>     {
>       path: '/',
>       component: 'pages/index.vue',
>       name: 'index'
>     },
>     {
>       path: '/:category',
>       component: 'pages/_category.vue',
>       children: [
>         {
>           path: '',
>           component: 'pages/_category/index.vue',
>           name: 'category'
>         },
>         {
>           path: ':subCategory',
>           component: 'pages/_category/_subCategory.vue',
>           children: [
>             {
>               path: '',
>               component: 'pages/_category/_subCategory/index.vue',
>               name: 'category-subCategory'
>             },
>             {
>               path: ':id',
>               component: 'pages/_category/_subCategory/_id.vue',
>               name: 'category-subCategory-id'
>             }
>           ]
>         }
>       ]
>     }
>   ]
> }
> ```
>
> 



