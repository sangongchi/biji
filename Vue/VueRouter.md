## vue-router 学习使用

### 1. 使用vue-router

---

- > 1. npm install vue-router -S
    >
    > 2. 在main.js 中引入  import VueRouter from 'vue-router'
    >
    >     或者新建一个 router.js  import VueRouter from 'vue-router' 
    >
    > 3. 安装使用插件：Vue.use(VueRouter)
    >
    > 4. 创建路由对象并配置路由规则 ==let router =new VueRouter({==
    >
    >     ​                                         	==[{path:'/home',component:Home}]})==
    >
    >     ​						==})==
    >
    > 5. 将路由对象传递给Vue实例 ，在 new Vue 中添加  router:router
    >
    > 6. 在app.vue中留坑  
    >
    >     ​			 <router-view></router-view>   //(路由出口，路由匹配到的组件将在这里渲染)
    >
    >     ​			

### 2.`$router 和$route`

- $router 是路由实例对象，即使用new VueRouter 创建的实例，包括了路由跳转的方法钩子函数等

    - $router 常见的跳转方法

    - > 1. router.go(n) 方法  ===`window.history.go`
      >
      >    - 这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 `window.history.go(n)`。
      >
      >    - ```js
      >      // 在浏览器记录中前进一步，等同于 history.forward()
      >      router.go(1)
      >      ```
      >   ```
      > 
      >   ```

      >    // 后退一步记录，等同于 history.back()
      >    router.go(-1)
      >
      >    // 前进 3 步记录
      >    router.go(3)

      >    // 如果 history 记录不够用，那就默默地失败呗
      >    router.go(-100)
      >    router.go(100) 
      >
      >    2. router.push 方法   ===`window.history.pushState`
      >
      >    - 想要导航到不同的 URL，则使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。
      >
      >    - ```js
      >      // 字符串
      >       router.push(``'home'``)
      >      ```
      >
      >    // 对象
      >    router.push({ path: ``'home'` `})
      >
      >    // 命名的路由
      >    router.push({ name: ``'user'``, ``params``: { userId: 123 }})
      >
      >    ```js
      >    // 带查询参数，变成 /register?plan=private
      >    router.push({ path: ``'register'``, query: { plan: ``'private'` `}})
      >    ```
      >
      >    3. router.replace 方法  ===`window.history.replaceState`
      >
      >     - router.replace 方法和router.push方法很像，唯一不同的是，他不会向history中添加新纪录，而跟它的方法名一样，替换掉当前的history记录 （不能使用后退按钮）

- $route 路由信息对象包含路由的信息参数

    - > 1. $route.path        //字符串，对应当前路由的路径，总是解析为绝对路径
      >
      > 2. $route.params    //     一个 key/value 对象，包含了 动态片段 和 全匹配片段，
      >     如果没有路由参数，就是一个空对象。
      >
      > 3. `$route.query`      //表示URL查询参数， 例如：/foo?user=1  则`$route.query`.user 值为1，如果没有查询参数则是空对象。（key/value对象）
      >
      > 4. $route.hash       //当前路由的 hash 值 (不带 #) ，如果没有 hash 值，则为空字符串。
      >
      > 5. $route.fullpath     完成解析后的 URL，包含查询参数和 hash 的完整路径
      >
      > 6. $route.matched   数组，包含当前匹配的路径中所包含的所有片段所对应的配置参数对象。
      >
      >     包含当前路由的所有嵌套路径片段的**路由记录**
      >
      > 7. $route.name       当前路径名字

### 3.vue-router传参的两个方法

| 声明式导航              | 编程式导航       |
| ----------------------- | ---------------- |
| <router-link :to="..."> | router.push(...) |

​	当你点击 `<router-link>` 时，这个方法会在内部调用，所以说，点击 `<router-link :to="...">` 等同于调用 	`router.push(...)`。

​	使用 `router.push` 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到	之前的 URL。

#### 3.1 编程式导航 

该方法的参数可以使一个字符串路径，或者一个描述地址的对象。

```js
// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
```



#### 3.2声明式导航

该方法传参的基本语法：

```js
<router-link :to="{name:xxx,params:{key:value}}">valueString</router-link>
```

### 4.路由守卫

> 4.1 全局守卫：beforeEach
>
> - ```js
>   const router = new VueRouter({ ... })
>   ```
> ```
> 
> ```

> ​	router.beforeEach((to, from, next) => {
> ​				// ...
> ​	})
>
> 
>
> - 每个守卫方法接收三个参数：
>
>     - **to: Route**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1)
>     - **from: Route**: 当前导航正要离开的路由
>     - **next: Function**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。
>         - **next()**: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。
>         - **next(false)**: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到 `from` 路由对应的地址。
>         - **next('/') 或者 next({ path: '/' })**: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true`、`name: 'home'` 之类的选项以及任何用在 [`router-link` 的 `to` prop](https://router.vuejs.org/zh/api/#to) 或 [`router.push`](https://router.vuejs.org/zh/api/#router-push) 中的选项。
>         - **next(error)**: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 [`router.onError()`](https://router.vuejs.org/zh/api/#router-onerror) 注册过的回调。
>
> **确保要调用 next 方法，否则钩子就不会被 resolved。**
>
> 4.2 后置守卫：afterEach
> 4.3 全局解析守卫：beforeResolve
> 4.4 路由独享守卫：beforeEnter
>
> 4.5 组内路由守卫：beforeRouteEnter,
>
> ​				beforeRouteUpdate,
>
> ​				beforeRouteLeave
>

### 5. 路由元

1. 定义理由可以配置路由元信息  meta字段

    - ```js
        const router = new VueRouter({
          routes: [
            {
              path: '/foo',
              component: Foo,
              children: [
                {
                  path: 'bar',
                  component: Bar,
                  // a meta field
                  meta: { requiresAuth: true }
                }
              ]
            }
          ]
        })
        ```

    - 访问meta字段，可以使用 $route.matched 数组

        - ```js
            router.beforeEach((to, from, next) => {
              if (to.matched.some(record => record.meta.requiresAuth)) {
                // 其上的some方法是ES6中的  ，表示数组中有一个为true返回为true，就为真
                // every() 方法表示 所有为真才返回true
                // this route requires auth, check if logged in
                // if not, redirect to login page.
                if (!auth.loggedIn()) {
                  next({
                    path: '/login',
                    query: { redirect: to.fullPath }
                  })
                } else {
                  next()
                }
              } else {
                next() // 确保一定要调用 next()
              }
            })
            ```

### 6.小知识点笔记

> 1. router-view
>
>     - ![router-view.png](https://user-gold-cdn.xitu.io/2017/5/3/ed2de15673673276b00e205c042048e4?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
>
>     - 上图创建页面和编辑页面使用的是同一个 component ，默认情况下，这两个页面切换时并不会触发 vue的 created 和 mounted 钩子，
>
>         - 解决办法：
>
>             - 通过  watch  $route 的变化来进行处理
>
>             - 可以在router-view 上加一个唯一的key保证路由切换的时，都会重新渲染触发钩子。
>
>                 - ```js
>                    <router-view :key="key">  </router-view>  computed: {     
>                     	key() 
>                     {         
>                          return this.$route.name !== undefined? this.$route.name + +new Date(): this.$route + +new Date()     
>                        
>                    ```
>
>                  }  
>                  }
>                  ```
>                 
>                  
>                  ```







