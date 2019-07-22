## Vue

### 1. 渲染函数(render) & JSX

1. Vue 推荐绝大多数情况下使用模板来创建你的HTML ，
2. 在一些场景中，你真的需要 JavaScript 的完全编程的能力，此时您可以使用渲染函数，它比模板更接近编译器

3. `render: h => h(App)` 是下面内容的缩写：

    - ```js
        render: function (createElement) {
            return createElement(App);
        }
        ES6 进一步缩写
        render (createElement) {
            return createElement(App);
        }
        //作者把 createElement 简写成 h。
        //Vue.js 里面的 createElement 函数，这个函数的作用就是生成一个 VNode节点，render 函数得到这个 VNode 节点之后，返回给 Vue.js 的 mount 函数，渲染成真实 DOM 节点，并挂载到根节点上。
        render (h){
            return h(App);
        }
        箭头函数缩写
        render: h => h(App);
        ```





### 2.slot 插槽

1. slot 是父组件与子组件的通讯方式可以将，父组件的内容显示在子组件中。

    在子组件中可以为slot 进行命名，来接收父组件中不同内容的数据

    - ```js
        <div id="app">
                <nba-team gname="凯尔特人" gname2="火箭">
                    <span slot="y">勇士队</span>  //这里为slot进行命名
                    <span slot="x">雄鹿队</span>
                    <span slot="m">猛龙队</span>
                </nba-team>
                <slo pname='koma'>你的东西不怎么地</slo>
                <slo pname='mike'>你的也是</slo>
                <slo pname='john'>你俩都好不到哪去</slo>
            </div>
            <script>
                Vue.component('nba-team',{
                    props:['gname','gname2'],
                    template:
                    `
                        <div>
                            <h3>欧文的球队：{{gname}}</h3>
                            <h3>哈登的球队：{{gname2}}</h3>
                            <div>西部季后赛队：<slot name="y"></slot></div>  //通过上边的名字进行值的获取
                            <h3>东部季后赛队：<slot name="x"></slot></h3>
                            <h3>东部季后赛队：<slot name="m"></slot></h3>
                        </div>
                    `
                    })
                Vue.component('slo',{
                    props:['pname'],  // 这里的props 传递的是pname的值 与slot无关
                    template:`
                        <div>
                            您好{{pname}} 
                            <slot></slot>  //使用slot 可以从父组件获取信息
                        </div>
                    `
                })
                new Vue({
                    el:"#app",
                })
            </script>
        ```

    - 作用于插槽

        - 待完善

### 3. vue store 和$store

> `$store` 是挂载在 Vue 实例上的（即Vue.prototype），而组件也其实是一个Vue实例，在组件中可使用 `this` 访问原型上的属性，template 拥有组件实例的上下文，可直接通过 `{{ $store.state.userName }}` 访问，等价于 script 中的 `this.$store.state.userName`。
> 至于 `{{ store.state.userName }}`，script 中的 `data` 需声明过 `store` 才可访问。
>
> - dispatch: 含有异步操作
>     - 存储 ：this.$store.dispatch('setTargetUser',friend);
>     - 取值： this.$store.getters.targetUser;
>
> - commit： 同步操作
>     - 存储：this.$store.commit('setTargetUser',friend);
>     - 取值：this.$store.state.setTargetUser
>
> 



