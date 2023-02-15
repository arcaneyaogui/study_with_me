# Router6 + Mobx入门

前置准备:

1. create-react-app 初始化好一个React项目
2. 下载 yarn 管理工具,方便下载和管理. 



使用命令下载router6

```react
yarn add react-router-dom@6
```



直接在App.js代码中,写下如下代码,实现一个小dome

```react
import Home from './Hoem'
import About from './About'

// 路由配置
import { BrowserRouter, Link, Route, Routes } from 'react-router-dom'

function App () {
  return (
    // 声明一个非hash模式的路由
    <BrowserRouter>
      {/**指定跳转的组件,to用来配置路由地址 */}
      <Link to="/">首页</Link>
      <Link to="/about">关于</Link>
      {/**路由出口,路由对应的组件会在这里进行渲染 
       * path:路径,element:组件 path-->element*/}
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  )
}
export default App
```



我们发现,点击首页,点击关于,就会进行网址中路由的改变.



![1676295841342](D:/A_CODEFILES/Z_gitWarehouse/githubWarehouse/study_with_me/React-router6/React-router6.assets/1676295841342.png)



![1676295841345](D:/A_CODEFILES/Z_gitWarehouse/githubWarehouse/study_with_me/React-router6/React-router6.assets/1676295841345.png)



---



## BrowserRouter

>用于包裹整个应用,一个react应用只需要使用一次.
>
>更像是一种初始化的作用

路由模式分别有 : HashRouter(哈希路由)  和 BrowserRouter(浏览器路由)

根据上文中的小例子可以直接用HashRouter替换BrowserRouter,整个运行不会受影响.问题就是路径中会多出一个 # 号。



## Link

最终Link渲染出来的是一个传统的 a 链接。

to ==》 用来写路由地址属性的

```react
      {/**指定跳转的组件,to用来配置路由地址 */}
      <Link to="/">首页</Link>
      <Link to="/about">关于</Link>
```



## Routes

提供一个路由接口，这个接口中那个路由满足条件，那么就会被渲染。

```react
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
```



## Route

用于指定导航链接，完成路由匹配。

```react
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
```

---



## 编程式导航

### useNavigate 钩子函数

继续创建一个Login页面,我们可以让这个页面点击跳转到about页面

```react
import { useNavigate } from 'react-router-dom'
function Login () {
  // 获得一个跳转函数
  const navigate = useNavigate()
  // 跳转到指定页面
  function goAbout () {
    //{replace: true}替换模式,这样登录后浏览器点击回退不会回退到登录页面。
    navigate('/about', { replace: true })
  }
  return (
    <div>
      Login
      <button onClick={goAbout}>跳转</button>
    </div>
  )
}
export default Login
```



重点代码

```react
  // 获得一个跳转函数
  const navigate = useNavigate()
  
  //{replace: true}替换模式,这样登录后浏览器点击回退不会回退到登录页面。
  // 如果不添加replace,默认就是叠加模式.
  navigate('/about', { replace: true })
```



### 携带参数跳转

#### searchParams 传参

Login页面中的跳转函数添加如下

```react
navigate('/about?id=1001', { replace: true })
```

注意,这个字符串中的问号等等符号,一定要是英文的符号!!!

在 about 页面中,获取这个路由中为 id 的值.

```react
import { useSearchParams } from "react-router-dom"
/*useSearchParams同样属于Hooks,所以要在函数中使用下面两句.*/
 let [params] = useSearchParams()
 let id = params.get('id')
```

所以如果路由路径中包括多个id,则获取第一个为准.

#### Params 传参

Login页面中的跳转函数添加如下

```react
navigate('/about/1001', { replace: true })
```

注意,一定要去路由接口Routes中找到对应的Route打一个配合.

提前占个位置:

```react
<Routes>
   <Route path="/" element={<Home />} />
   <Route path="/about/:id" element={<About />} />
   <Route path="/Login" element={<Login />} />
</Routes>
```

然后在about页面中,接受这个参数

```react
import { useParams } from "react-router-dom"

/*同样,下面两行代码要在函数组件中使用*/
let Params = useParams()
let id = params.id
```



---



## 嵌套路由

二级路由 : 一个页面中的下级跳转页面

1.首先写好对应的二级路由的 js 文件 , 并引入文件

```react
import Borad from './Borad'
import Article from './Article'
```



2.然后在该父级路由的Route中写明这两个路由的Route , **二级路由path不需要有斜杠**.

```react
<Route path="/Layout" element={<Layout />} >
    <Route path="Borad" element={<Borad />} />
    <Route path="Article" element={<Article />} />
</Route >
```



3.在这两者的父级路由:Layout中写明,告诉react这个js文件是这两个路由的出口.

```react
import { Outlet } from "react-router-dom"
function Layout () {
  return (<> 
    我是 : layout 页面
    <br></br>
    <Outlet />
  </>)
}
export default Layout
```



4.这接着在 Layout 后级添加 /Borad 或者 /Article , 就可以跳转到对应页面.



页面应该有一个默认渲染的二级路由 , 只用修改二级路的一个地方.

添加index属性,把自己的path干掉,就是默认渲染的路由.

```react
<Route path="/Layout" element={<Layout />} >
    <Route index element={<Borad />} /> // 默认路由Borad
    <Route path="Article" element={<Article />} />
</Route >
```





### 404路由配置

将 path 路径改成 * 号 , 即可.

```react
<Route path="*" element={<NotFount />} />
```



# Mobx

>就是一个集中状态管理工具, 比redux好用.
>类似于 vuex 于 vue的关系
>
>它其实是一个独立的响应式库,但是一般用于和React绑定使用.
>
>1.编写无模板的极简代码描述意图
>
>2.构架自由,可移植



因为要绑定使用,所以除了Mobx本身还需要一个中间部件.

![1676434871107](D:/A_CODEFILES/Z_gitWarehouse/githubWarehouse/study_with_me/React-router6/React-router6.assets/1676434871107.png)



使用 create-react-app 创建一个用来学习mobx的项目

```powershell
npx create-react-app react-mobx
```

在项目终端中 添加mobx 和 中间部件 mobx-react-lite

```shell
yarn add mobx mobx-react-lite
```



因为下面的学习使用的都是函数组件,如果常用类组件,但是要使用到mobx,则需要下载的中间部件不是mobx-react-lite , 而是 mobx-react



---



**计数器实现**

`  makeObservable(target, annotations?, options?)   `

我们数据和修改方法,都放在mobx中,创建个store文件鱼store文件夹下的Count.js

```react
import { makeAutoObservable } from 'mobx'
class CounterStore {
  // 定义数据
  count = 0
  list = [1, 2, 3, 4, 5, 6]
  // constructor 适用于构造和初始化class对象的特殊方法.
  // 一个类中只能由一个构造方法,可以使用super调用父类
  constructor() {
    // 把数据变成响应式
    makeAutoObservable(this)
  }
  // 定义action函数,用来修改数据
  addCount = () => {
    this.count++
  }
  //定义list计算属性
  get filterList () { return this.list.filter(item => item > 2) }
  addList = () => { this.list.push(-1, -3, 7, 8) }
}
// 实例化 ,导出给react使用
const counterStore = new CounterStore()
export { counterStore }
```

其中需要在构造函数中使用 'makeAutoObservable(this)'  将类中的数据变成响应式.

>这个函数可以捕获*已经存在*的对象属性并且使得它们可观察。
>
>任何 JavaScript 对象（包括类的实例）都可以作为 `target` 被传递给这个函数。 一般情况下，`makeObservable` 是在类的构造函数中调用的，并且它的第一个参数是 `this` 。 `annotations` 参数将会为每一个成员映射。需要注意的是，当使用 [装饰器]时，`annotations` 参数将会被忽略。



当方法与数据都在mobx中设定好之后,我们可以在react中使用他们

```react
import { counterStore } from './store/Counter'
import { observer } from 'mobx-react-lite'

function App () {
  return (
    <div>
      我是 App 组件.
      <br></br>
      {counterStore.count}
      <button onClick={counterStore.addCount}>+点击添加+</button>

      <hr></hr>
      <br></br>
      {/*react数组不能直接渲染,做个拼接.*/}
      {counterStore.filterList.join('-')}
      <br></br>
      <button onClick={counterStore.addList}>+点击改变+</button>
    </div>
  )
}
// 使用observe包裹app组件,使得变成响应式.
export default observer(App)
```



其中,我们需要引入需要的中间件和数据

```react
import { counterStore } from './store/Counter'
import { observer } from 'mobx-react-lite'
```

接着,我们需要使用 observe 包裹使用的组件,使得变数据改变,该组件也会刷新.

---



## Mobx模块化

在store中创建好拥有各自功能的模块组件

组件中因为需要响应式,都需要添加 makeAutoObservable



计数的组件

```react
import { makeAutoObservable } from 'mobx'

class CounterStore {
  // 定义数据
  count = 0
  // constructor 适用于构造和初始化class对象的特殊方法.
  // 一个类中只能由一个构造方法,可以使用super调用父类
  constructor() {
    // 把数据变成响应式
    makeAutoObservable(this)
  }
  // 定义action函数,用来修改数据
  addCount = () => {
    this.count++
  }
}
export { CounterStore }
```



添加数组的组件

```react
import { makeAutoObservable } from "mobx"

class ListStore {
  list = ['react', 'JavaScript', 'html']
  constructor() {
    makeAutoObservable(this)
  }
  addList = (params) => {
    this.list.push('angular')
  }
}
export { ListStore }
```



然后将这些拥有各自功能的组件,在store中的 index.js 文件中组装

```react
// 用于组合子模块,封装导出.
import { ListStore } from "./list.Store"
import { CounterStore } from "./counter.store"
import React from "react"
//声明一个root
class RootStore {
  constructor() {
    //对模块进行实例化
    this.counterStore = new CounterStore()
    this.listStore = new ListStore()
  }
}
const rootstore = new RootStore()
const context = React.createContext(rootstore)
const useStore = () => React.useContext(context)
export { useStore }
```



组装之后,利用context通信的手段获取这个类的实例化,赋值给一个常量,导出这个常量,给与其他所有页面渲染的组件使用.

```react
import { observer } from 'mobx-react-lite'
import { useStore } from './store/index'
function App () {
  // 解构到实例对象即可,不然可能会破坏响应式.
  const { counterStore, listStore } = useStore()
  return (
    <div>
      我是 App 组件.
      <br></br>
      {counterStore.count}
      <button onClick={counterStore.addCount}>+点击添加+</button>

      <hr></hr>
      <br></br>
      {/*react数组不能直接渲染,做个拼接.*/}
      {listStore.list.join('-')}
      <br></br>
      <button onClick={listStore.addList}>+点击改变+</button>
    </div>
  )
}
// 使用observe包裹app组件,使得变成响应式.
export default observer(App)
```

