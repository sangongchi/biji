## -1.reactRouter知识点笔记 

### 1. switch标签的作用

> 1. 有时我们在react Router中会使用 ==switch== 标签
>
>     - 有switch标签 则其中的<Router> 在路径相同的情况下，只会匹配第一个，可以避免重复匹配
>
>     - 无<switch> 的时候，当<router> 在路径相同的情况下全都会匹配，甚至匹配上级路由 
>
>         ```jsx
>          <BrowserRouter>
>              <div>
>                   <Route path="/Guide/ContactUs" component={ ContactUs } ></Route>
>                   <Route path="/Guide/ContactUs" component={ ContactUs } ></Route>
>                   <Route path="/Guide" component={ AboutUs } ></Route>
>              </div>
>         </BrowserRouter>
>         ```
>
>         - 匹配到了上级路由       ![1564899379211](H:\biji\typora_imgs\1564899379211.png)
>         - 前两张是没有添加switch的情况            ![1564899393668](H:\biji\typora_imgs\1564899393668.png)
>         - 加了switch的情况如下
>
>         ![1564899405610](H:\biji\typora_imgs\1564899405610.png)
>
>         

### 2.exact属性

> 1. exact 是Router 下的一条属性，exact  的值为bool值
>
> 2. <Route path='/' component={Home} />
>     <Route path='/page' component={Page}>
>     //  没有加exact 的这种情况下，如果匹配路由path='/page'，那么会把Home也会展示出来。
>
> 3. <Route exact path='/' component={Home} />
>     <Route path='/page' component={Page} />
>
>     //  添加后解决问题，exact 使得路由匹配更加严格一些。

### 3. router配置写法

```js
//路由组价配置
import React from 'react'
import { BrowserRouter as Router, Route } from 'react-router-dom'
import SiteIndex from "pages/site/index"
import About from "pages/About/About"

//可以在此处书写组件，也可以通过import的方式导入组件
class Inbox extends React.Component{
    render(){
        return(<h1>Inbox</h1>)
    }
}

//JSX方式书写  
class App extends React.Component{
    render(){
        return(
            <Router basename="/">
                <Route exact path='/' component={SiteIndex} />
                <Route exact path='/About' component={About}></Route>
                <Route exact path='/Inbox' component={Inbox}>
                    //子路由嵌套书写
                	<Route path="/messages/:id" component={Message} />
        			{/* 跳转 /inbox/messages/:id 到 /messages/:id */}
        			<Redirect from="messages/:id" to="/messages/:id" />
                </Route>
            </Router>
        )
    }
}
export default App;

不使用JSX语法
//也可以使用原生的Route 数组对象
const RouteConfig=[
    {
        path:'/',
        component:'App',
        indexRoute:{component:Moren}
        ChildRoutes:[
        	{
       	 		path:'/About',
        		component:About,
        		ChildRoutes:[
        				.....
        		]
    		}
        ]
    }
]
React.render(<Router routes={routeConfig}/>,document.body)
```

