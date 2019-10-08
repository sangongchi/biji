### react声明周期

---

#### 1. 常用的声明周期

- 组件挂载时（constructor）

    > 1. class 的构造器。继承父类Component 可以做一些基本的绑定操作
    > 2. 磁珠可以绑定  ref、给事件绑定 this、或是state、

- 组件挂在完成时 ==`componentDidMount()`==

    > - 组件挂载后 官方的话说就是已经插入`dom`节点 我们需要做一些绑定的操作可以在这里
    > - 方便做一些订阅或是监听在这里
    > - 绑定的`ref`在这是拿不到的
    > - 我们也可以在这里做一些修改`state`的操作 那将会触发再次`render`(并非浏览器页面的再次渲染) 但尽量避免这么干 至于为什么 这还用说吗
    > - 和`constructor`一样 只会触发一次

- 组件更新时 ==`shouldComponentUpdate()`==





> render()

- 更新组件的`props`和`state`返回一个React元素/节点
- 但`render`是一个纯函数 没有副作用 所以我们不要在`render`里做`this.setState`类似这种操作
- 不负责最后的渲染工作
- `null`和`boolean`不会被渲染