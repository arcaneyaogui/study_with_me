# 目录

[TOC]



# React 学习笔记

##  0. 前言

>某方向根据JavaScript语法设计封装好的函数,然后根据创建者的规则进行调用,就是使用的框架.
>
>并没有什么深奥的,就是查文档,做编码的一个过程.开发者不是你,你只是一个搬运工.
>
>随意根本没必要去想着记忆框架的各种 api ,有了新的或者过时了,都是你的时间成本.



**单页面应用和多页面应用**

*单页面*  页面是不改变的,就是改变数据的调用.缺点就是第一次加载的时候时间花费更多一点.

*多页面* 就是点击网站中的其他地方跳转时,它会重新再进一个新的页面,那么像 html,css,js文件等文件都得重新下载并且再解析一遍.



在 `React` 中,不能直接赋值修改,必须通过一个方法,叫`setState`

在 `React` 中组件名不仅要开头大写,想class也是className,其中命名也是非常注重规则,这规则一般都是开头字母大写或者驼峰式命名法.





## 1.0 环境搭建

**window powershell的打开方式**

`win + r`  --> 输入 `powershell` , 既可以进入 ` powershell `  界面。

---

**安装 create-react-app ** 

`create-react-app` 包能够快速的创建一个 react 的环境, 很适合初学者.

因为 npx 帮助我们安装 `create-react-app` 包,初始化项目之后,会自动删除掉,所以不需要( -g )全局命令来安装.

临时在我们自定义的 react-basic 的文件夹中装一个名为 create-react-app 依赖包 

```powershell
npx  create-react-app  react-basic
```

报了一个警告,并且说我的npm版本过低,都给他娘的更新一下.

```
npm WARN deprecated tar@2.2.2: This version of tar is no longer supported, and will not receive security updates. Please upgrade asap.

npm notice New minor version of npm available! 8.1.2 -> 8.19.2
```



更新 `tar`

```
npm install -g tar
```

更新 `npm`

```
npm install -g npm@8.19.2
```



展示出一下的英文,表示这个东西是安装好了的

```
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd react-basic
  npm start

Happy hacking!
```

---

使用 `vscode` 打开 见 `package.json` 文件夹

我们可以看见这个项目的 `依赖描述`  和 `能够执行的命令 `.

```react
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```

最后执行 `npm start` 或者 `yarn start` 命令,项目将会在浏览器中运行一个react的项目,这个项目就是 react 的一个图标在转圈圈.

---

首先我们要了解 `react ` 的 `src` 文件夹下核心三个文件. `App.js`  `index.css`  `index.js`



**App.js**

```react
const name = "胡图图";
let getAge = ()=>{
  return 18;
}
let flag = true;

function App() {
  return (
    <div className="App">
      { name }
      { getAge() }
      { flag ? "是大耳朵" : "是小耳朵" }
    </div>
  );
}
export default App;
```



**index.js**

```react
//React: 框架的核心包
//ReactDom: 专门做渲染相关的包
// 在node_modules 文件下有 react,react-dom这两个文件夹.
import React from 'react';
import ReactDOM from 'react-dom';

// 应用的全局样式文件
import './index.css';
// 引入跟组件,一切组件的开始.
import App from './App';

// 渲染一个app的组件,到一个id为root的dom节点上
// 这个id为root的dom节点就在 public文件夹中的index.html页面中.
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

```



*注意:* 因为总是会报个警告,所以到了React 18 应该如下方式渲染一个根节点.

```React
import React from 'react'
import { StrictMode } from "react"
import { createRoot } from "react-dom/client"

const rootElement = document.getElementById("root")
const root = createRoot(rootElement)
root.render(
  <StrictMode>
    <App />
    <Test />
  </StrictMode>
)
```



**index.css**

```react
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}

```



然后因为我们是 `react 18` 所以在初学的时候写小功能需要去掉严格模式 

也就是名为`React.StrictMode` 的标签,会影响 `useEffect `的执行时机.

```
ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

---



## 1.1 插件

vscode 安装插件 `Prettier - Code formatter` ,再`setting.json`中配置.

柴柴老师配置网址: https://www.yuque.com/fechaichai/qeamqf/xbai87

这个配置适应 react 和 vue , emm... 虽然我都看不懂这些配置.

反正功能就是让你写框架的时候会有各种提示,让你书写更舒服.



`Error lens`[^1] 

[1]: 这个插件能够在编写的时候时时提示错误信息.

---

`yarn` 是 facebook 代替 npm 的一个包管理工具.

可以安装以下 yarn 

```
npm  install -g yarn
```





## 2.0 JSX 基础

`jsx` 实现了 JavaScript HTML CSS 的混写.

`jsx` 只是 JavaScript 的一种扩展.



### 注意事项

1. JSX 中有且只有一个根节点,如果不需要,请使用幽灵节点  `<></>` 代替 , 反正不能没有.
2. 所有的标签必须有闭合,不管是成段的闭合或者自闭合的标签.
3. 属性名采用驼峰命名法,比如:
   1. class ==> className
   2. for ==> htmlFor
4. 支持换行,但是换行建议使用小括号包裹上,方便语义清晰.并且表明那块是个独立的语义区域.
5. 注意 {/* 注释 */} 根目录中写代码注释也需要写到大括号中



### jsx 使用 js 表达式

**语法**  : { JavaScript 表达式 }

字符串 数值 布尔值 null undefined object 函数等,都行.

如果实在不确定这个是不是表达式,就是用 console.log 打印一下,有值,就说明这是一个表达式.

```react
const name = "胡图图";
let getAge = ()=>{
  return 18;
}
let flag = true;

function App() {
  return (
    <div className="App">
      { name }
      { getAge() }
      { flag ? "是大耳朵" : "是小耳朵" }
    </div>
  );
}
export default App;
```



### 列表渲染

```react
const list_map = [
  // id赋值的时候不能使用 001 这种
  {id:1,name:"独领风骚"},
  {id:2,name:"风骚绝伦"},
  {id:3,name:"绝伦逸群"}
]

function App() {
  return (
    <div className="App">
      // 遍历列表时,需要一个为number或者string类型的 key ,提高diff性能.
      // key 仅仅在框架中使用,不会出现在浏览器中.
      { list_map.map(list_map => <li key = {list_map.id}>{list_map.name}</li>) }
    </div>
  );
}
export default App;
```



### 条件渲染

技术方案: 三元表达式  逻辑&&运算

逻辑 && 运算的时候,前面要是为假就直接不执行了.属于一种比较简介的写法.

```react
const flag = true;
const flag_2 = false;

function App() {
  return (
    <div className="App">
      { flag ? (
      <div>
        <span>this is a span1</span>
      </div> ): null }
      { flag_2 && <span>this is a span2</span> }
      { flag && <span>this is a span3</span> }
    </div>
  );
}
export default App;
```



**复杂的判断逻辑**

遇见复杂的多分支的逻辑,请把它抽离为一个函数,用函数来处理这个逻辑。

而三元运算符的模板中调用函数就行。

比如通过你输入的1-3的数字,来判断你h1-h3标签.

```react
const getfun = (type)=>{
  if(type === 1){
    return <h1>这是H1级标签</h1>
  }
  if(type === 2){
    return <h2>这是H2级标签</h2>
  }
  if(type === 3){
    return <h3>这是H3级标签</h3>
  }
}

function App() {
  return (
    <div className="App">
      { getfun(1) }
    </div>
  );
}
export default App;

```



###  样式控制

**a.行内样式**

可直接在标签行内使用 `style`  标签 , 标签中的属性需要在写在大括号里面的大括号里.

属性值需要用单引号包裹,并且不同属性之间需要逗号分隔, `fontSize`  因为是key值,所以写成驼峰命名的形式.

```react
{ <span style={ { color:'red' , fontSize: '30px' } }></span> }
```

但是这样对于样式比较多的时候语义不清晰,不方便阅读.

同样可以把样式属性抽离出去,保持模板精简.

```react
const span_style ={ 
  color:'red' , 
  fontSize: '30px' 
}
```

只用渲染这个变量就行.

```react
{ <span style={ span_style }></span> }
```



**b.类名样式**

引入外部的 `css`  文件 , 在元素属性上绑定一个 `className` .

比如创建一个 `App.css` 然后导入文件,就可以引用该文件中的 类名css样式

`App.css`

```css
.active{
    color:'aquamarine';
    font-size: 50px;
}
```



`App.js`

记住,调用css文件中的类名时,使用的是 className 而不是 class .

```react
import './App.css'

const span_style ={ 
  color:'red' , 
  fontSize: '30px' 
}

function App() {
  return (
    <div className="App">
      { <span style={ span_style }>行内样式</span> }
      { <span className='active'>类名样式</span> }
    </div>
  );
}
export default App;
```



**动态控制样式**

一般使用条件来判断,然后配合三元表达式使用.

```react
className={item.attitude === 1 ? "like liked" : "like"}
```



## 3.0 组件基础

组件为JavaScript提供了一个抽象,提高代码的复用率.

- 函数组件
  - 组件的名称首字母必须大写,后面接驼峰式命名尽量不要有其他符号。
    - react会根据这个来判断是组件还是普通的HTML标签
  - 组件必须要有返回值，表示该组件的UI结构，如果不需要渲染任何内容，则返回null。
  - 组件就像HTML一样可以
- 类组件可以向HTML标签一样被渲染到页面中，渲染的内容就是函数的返回值。
- 函数名作为组件标签名称，可以成对出现也可以自闭合。



我在一次做小练习的过程中对于函数的命名出了开头大写还遇见过有趣的.

`Imported JSX component Plus_one must be in PascalCase or SCREAMING_SNAKE_CASE`

报这个的原因是因为组件名中有下划线.`Plus_One`,把下划线删除后,就没有报这个警告,这个虽然是报了个警告,但是直接导致我的事件点击无效果,不报警告后就行了.





### 3.1 函数组件

就如同写原生JavaScript函数一样,在return返回值中返回你要渲染的组件.

```react
function Hello(){
	return <div>hello world</div>
}
```



**渲染的方式**

以下两种方式,都是可以在跟标签中直接渲染出来的方式.

```
  <Hello/>       //自闭和
  <Hello><hello/>   //成对闭合
```

当你要返回多个标签的时候,需要一个根节点.

```react
import './App.css'

const span_style = {
  color: 'red',
  fontSize: '30px'
}

function Hello () {
  return (<>
    <br></br>
    <div>hello world<span>这是一个组件</span></div>
    <br></br>
  </>)
}

function App () {
  return (
    <div className="App">
      {<span style={span_style}>行内样式</span>}
      {<span className='active'>类名样式</span>}
      <Hello></Hello>
    </div>
  )
}
export default App;
```



### 3.2 类组件

>使用 ES6 语法中的 class 创建.

创建一个类组件,继承 `Component` 类

```react
import React from 'react'  //引入React

class Hellocomponent extends React.Component{
  render(){
    return <div>这个是类组件</div>
  }
}
```

渲染的方式和函数组件一样,直接使用标签就好.

*注意:*

- 类组件同样命名需要以大写字母开头
- 类组件应该继承 `React.Component`  父类,从而使用父类的方法或属性.
- 类组件必须提供render方法,render方法必须有返回值,表示组件的UI结构.



**bind() 修正 this指向**

一般来说,绑定当前函数的 this 生命组件中的回调函数时只需要和箭头函数配合就好

自动就会绑定this到当前的函数域中.

而类组件中,这个箭头函数的父级函数是 render ,然后render里面的 this 早已被 React 修正了, render 本身的 this 指向该父级类函数

```JavaScript
{  YourFunctionName = ()=>{   }   }
```

但是如果回调函数是用的普通函数声明方式申明

```JavaScript
YourFunctionName (){
	balabala...
}
```

则你需要在类组件中,使用一个 `constructor` 函数,用来舒适化,给当前类组件强制绑定this

```react
constructor(){
	super()
	this.YourFunctionName = this.YourFunctionName.bind(this)
}
```



*可以的话些项目永远写第一种写法*



### 3.3 组件状态

**函数组件**



>在 hook 出现之前,函数组件没有状态.



**类组件状态**

再类组件中创建一个对象,对象中保存自己自定义的组件状态.

注意下文中的 `state` 就是固定的名称,不是自定义的名称,

emm...  一开始我还以为是可以自己定义状态名称,然后我说咋用setState方法没反应.

setState继承自 React.Component , 必须使用setState方法修改.

```react
class Hellocomponent extends React.Component {
  state = {
    // 通过对象的语法定义各种状态
    name: "LYG",
    age: 18
  }

  change = () => {
    // 须通过setState()方法修改
    this.setState({
      name: "LYG2",
      age: 22
    })
  }

  render () {
    return (<div>
      this is Hellocomponent
      <br />
      {this.state.name + "\t" + this.state.age}
      <br />
      <button onClick={this.change}>修改状态</button>
    </div>)
  }
}
```



#### 状态中其他类型的数据修改

上文展示修改一般的值,一下再展示数组,对象等修改方式.

记住,永远不要想着直接修改值,而应该是想办法创建出我们想要的数据,然后覆盖回去.



**数组修改**

```react
  change_List = () => {
      // 展开数组后在数组后面加上要添加的,然后将这个新数组返回
    this.setState({ list: [...this.state.list, 4, 5] })
  }
```

删除数组 `filter()` , 再原生js中,很多数组的方法是不会修改数组原来是值的.

```react
  change_List = () => {
    this.setState({ 
        // 将数组中元素为 2 的删除
        list: this.state.list.filter(item => item!==2)
    })
  }
```





**对象修改**

```react
  change_Object = () => {
    this.setState({
      person: {
        ...this.state.person,
        // 会覆盖原来的 name 属性的值.
        name: "胡图图"
      }
    })
  }
```



对象的修改

```react
  change_Object = () => {
    this.setState({
      person: {
        ...this.state.person,
        // 会覆盖原来的 name 属性的值.
        name: "胡图图"
      }
    })
  }
```





## 4.0 事件绑定

函数组件中事件的绑定和使用.

```react
function Hello () {
  const fun = () => {
    alert("函数组件被触发!!")
  }

  return (<>
    <br></br>
    <div onClick={fun}>hello world<span>这是一个组件</span></div>
    <br></br>
  </>)
}
```



类组件中事件的绑定和使用,以下是一个标准的规范.

```react
class Hellocomponent extends React.Component {
  fun3 = () => {
    alert("类组件被触发")
  }

  render () {
    return <div onClick={this.fun3}>这个是类组件</div>
  }
}
```



这里有个有意思的,你如果在函数组件中使用this调用会报错.

同样,你再类函数中,直接用函数名同样会报错.

**事件对象 e的获取**

```react
  const fun = (e) => {
      // 阻止默认行为
      e.preventDefault()
  }
```



**传递自定义参数**

这个时候使用箭头函数,来获取这个参数

```react
function Hello () {
  const fun = (msg) => {
    //e.preventDefault()
    console.log("函数组件被触发!!")
  }

  return (<>
    <br></br>
    <div onClick={() => fun("this is a msg")}>hello world<span>这是一个组件</span></div>
    <br></br>
  </>)
}
```



直接使用使用函数名传参,回导致点都点不动,而且是控制台上直接打印了.

并不是我们预想中的先点击,然后再在控制台输出打印.

```react
function Hello () {
  const fun = (msg) => {
    console.log("函数组件被触发!!", msg)
  }

  return (<>
    <br></br>
    <div onClick={fun("this is a msg")}>hello world<span>这是一个组件</span></div>
    <br></br>
  </>)
}
```

而再前面加上箭头函数,就没任何问题.

```react
{ () => fun("this is a msg") }
```



同样既想要 e 又想要自己的参数,我们需要在箭头函数中也传入 e 

```react
{ (e) => fun(e,"this is a msg") }
```



**想要在事件中渲染函数的参数,就需要使用箭头函数**





## 5.0 表单处理



- 受控组件 (推荐使用)
  - input 框被 react 中的 state 一个属性控制了.
  - input框的 value 属性等,都属于input框的状态
- 非受控组件  (了解即可)



### 受控组件

```react
class PlusOne extends React.Component {
  state = { massage: 'LYG', size: 1 }

  chang_massage = (e) => {
    this.setState({
      size: this.state.size + 1,
      // e 是事件对象
      massage: e.target.value
    })
    console.log("内容被改变" + this.state.size + "次", e)
  }

  render () {
    return (<>
      { /*调用函数的时候不需要在括号后面添加 e*/}
      <input value={this.state.massage} onClick={this.chang_massage}></input>
    </>
    )
  }
}
```





### 非受控组件

操作原生 dom 的值, 手动获取输入框的值,就是组件中的属性值不与状态中的某个属性绑定。

需要用到  `createRef ` 的一个函数，使用这个函数需要从 ‘react’ 中导入

`createRef`   可以创建一个容纳 dom 对象的容器,导入函数使用大括号包裹.

```
import { createRef } from 'react'
```



获取非受控组件的值

```react
class PlusOne extends React.Component {
  massageref = createRef()
  getVaule = () => {
    console.log(this.massageref.current.value)
  }

  render () {
    return (
      <>
        { /*调用函数的时候不需要在括号后面添加 e*/}
        <input type='text' ref={this.massageref}></input>
        <button onClick={this.getVaule}>点击获取输入框的值</button>
      </>
    )
  }
}
```



如果打印 current 的话,我们会发现,我们定义下的 massageref 对象中的current就是 input 标签



## 6.0 组件通信

组件之间,数据之间的互相流转

- 父子关系 :  只把父组件的的数据传给子组件
  - 父组件添加属性  -- `state`
  - 子组件中 通过 `props` 接受父组件传来的数据.
    - 这个 `props` 不是固定的,但是约定俗成,一般就取名为`props`
- 兄弟关系 : 自定义时间模式产生技术方法 eventBus / 通过共同的父组件通信
- 其他关系 : mobx / redux / 基于hook的方案



### 父子关系-组件通信

下面代码分别展示了父组件和 子组件(函数组件) , 子组件(类组件) 交流信息的简单流程.

核心就是 `props` , 单项数据流 , 里面所有的数据都是只读的不能做修改,谁的数据谁修改。

props 可以传递任意的数据

```
数字,字符串 布尔值 数组 对象 函数 JSX
```



**父传子通信**

下面是基础的父子组件的通信代码.

```react
import React from 'react'
// 函数式子组件
function FSon(props) {
  console.log(props)
  return (
    <div>
      子组件1
      {props.msg}
    </div>
  )
}
// 类子组件
class CSon extends React.Component {
  render() {
    return (
      <div>
        子组件2
        {this.props.msg}
      </div>
    )
  }
}
// 父组件
class App extends React.Component {
  state = {
    message: 'this is message'
  }
  render() {
    return (
      <div>
        <div>父组件</div>
        <FSon msg={this.state.message} />
        <CSon msg={this.state.message} />
      </div>
    )
  }
}
export default App
```



props重点在于传输 `函数` 和 `JSX` 数据



**子传父通信**

父组件中有个函数,这个函数用来改变父组件中的状态。

子组件中拥有一个方法，用来调用改变父组件传过来的函数，并且这个父组件传过来的函数所需要的参数是子组件中这个函数或者其他方式提供的。

通过子组件提供的数据，回调函数，用来改变父组件的状态，这就是子传父的思想。

```react
// 函数式子组件
function FSon (props) {
  console.log(props)
  function handle () {
    props.changeMes("this is new message")
  }
  return (
    <div>
      {props.mes}
      {props.list.map(item => <p key={item}>{item}</p>)}
      <button onClick={handle} className="testCss">change</button>
    </div>
  )
}
```

父组件中的回调函数.

```react
  changeMes = (newMes) => {
    this.setState({
      message: newMes,
      list: [...this.state.list, 4, 5]
    })
  }
```



### 兄弟组件

兄弟组件之间是不能够直接通信的，但是可以通过共同的父组件进行一个第三方的转发数据。

>父组件通过传给子组件A带参函数,子组件A中调用该函数,把子组件A中的数据获取过来.
>
>子组件B一直接受的是父组件状态的数据,这个时候可以通过父组件作为中介,将获取来的值用来修改本身状态中的数据,这样子组件B直接获取到修改后的数据,间接达到将自己的数据修改成子组件A中的数据.

源代码如下:

```react
import React from 'react'
// 子组件A
class SonA extends React.Component {
  render () {return (<div>SonA,{this.props.initDdata}</div>)}
}
function SonB (props) {
  const Bmes = '我是B中的数据'
  return (
    <div><span>SonB</span><br></br>
      <button onClick={() => { props.getMes(Bmes) }}>打印sonB组件到控制台</button>
    </div>
  )
}
// 父组件
class App extends React.Component {
  state = {init_data: '初始值 000'}
  getMes = (Mes) => {
    console.log(Mes)
    this.setState({ init_data: Mes })
  }
  render () {
    return (
      <>
        <SonA initDdata={this.state.init_data} />
        <SonB getMes={this.getMes} />
      </>
    )
  }
}
export default App

```



###  跨组件通讯 context

>当组件是一个组件树的时候,一个上层组件能够任意和它的某一个下层组件进行通信.

使用`context`的时候,有一个固定的套路:

1- 创建Context对象 导出 Provider 和 Consumer对象 

Provider :作为数据的提供者(上层的组件)

Consumer : 作为数据的消费者(被上层组件链接的下层组件)

```javascript
import {createContext} from 'react' //先添加createContext方法
//可以直接创建一个对象用来接受这个方法
//contextNode 中包含 Provider, Consumer
const contextNode = createContext()

//当然你可以直接解构,将这两个变量直接分别接收出来.
const { Provider, Consumer } = createContext()
```

2- 使用Provider包裹上层组件提供数据 

```javascript
// 必须包裹上层组件中的返回组件 格式固定
<Provider value={this.state.message}>
    {/* 根组件 */}
</Provider>
```

3- 需要用到数据的组件使用Consumer包裹获取数据

```javascript
<Consumer >
    /* 固定格式 */
    {value => /* 基于 context 值进行渲染*/}
</Consumer>
```



createContext默认优先是 Provider vaule = { 传递的参数 } ,但是如果没有设置Provider ,那么会在去找createcontext创建的时候传过来的参数.然而这个默认餐宿可以传输一个类的实例对象.

```raact
const context = React.createContext(rootstore)
```





## 7.0 组件扩充

### children

双闭合的组件之中有内容,就会有`children`属性.

children 属性包含: 文本,标签,函数,jsx. 

children 属性常常用在 `高阶组件` 中,高阶组件相当于就是js中的高阶函数.

```react
//直接执行在函数组件中中
function TestChilsren ({ children }) {
  children()
  return (<div>我是测试标签</div>)
}

/* 直接再标签中传入函数 */
<TestChilsren>
	{() => { console.log("我表示可以传入函数") }}
</TestChilsren>
```





### props 校验

为阻止数值的格式传递的不匹配,需要使用props的时候有一个校验规则.

固定套路:

1. 添加 `props-types` 架包 , 使用其内置规则.
2. 在文件中导入 `prop-types` 包
3. 使用 `组件名.propTypes = {}` 给组件添加校验规则



```react
// 添加架包命令:  yarn add props-types

// 导入props校验包,里面包含各种内置的校验规则.
import PropTypes from "prop-types"
```



使用props内置的校验规则:

1. 常见类型：array、bool、func、number、object、string
2. React元素类型：element (就是jsx语法)
3. 必填项：isRequired
4. 特定的结构对象：shape({})

例子:

```react
// 定义propropTypes 注意 p 是小写
TestFun.propTypes = {
  // 定义list必须是数组
  list: PropTypes.array
}
```



**isRequired**

这个属性添加上去之后,你不传相应的数据,就会报一个警告.

开发中用的不频繁,但是开发组件库的话就用得比较多.

```react
TestFun.propTypes = { list: PropTypes.array.isRequired } 
```



官方文档: https://reactjs.org/docs/typechecking-with-proptypes.html

如果类型错误出了报错还会弹出一个警告,告诉你是那个组件有问题.

![image-20221205102007040](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20221205102007040.png)





### props 默认值

通过 `defaultProps` 可以给组件的props设置默认值，在未传入props的时候生效

传入数据的时候就以传入的数据为主,当没有传入相应数据的时候就使用默认值.

### 1. 函数组件

直接使用函数参数默认值

```jsx
function List({pageSize = 10}) {
  return (<div>此处展示props的默认值：{ pageSize }</div> )
}
// 不传入pageSize属性
<List />
```

### 2. 类组件

使用类静态属性声明默认值，`static defaultProps = {}`

```jsx
class List extends Component {
  static defaultProps = { pageSize: 1 }
  render() { return (<div>此处展示props的默认值：{this.props.pageSize }</div>)}
}
<List />
```



defaultProps属性定义默认值

这个方法不管是函数组件还是类组件都可以使用.

但是因为是旧方法,不推荐使用. 使用上述的方法,默认值都和组件没有分离,可读性较高.

```jsx
Test.defualtProps = {
    defualtSize:100
}
```









##  8.0 组件生命周期 [需要日后复习扩充]

组件的生命周期是指组件从被创建到挂载到页面中运行起来，再到组件不用时卸载的过程，注意，只有类组件才有生命周期（类组件-->实例化, 函数组件-->不需要实例化）

![img](E:/Z-%E9%9C%8D%E6%A0%BC%E6%B2%83%E5%85%B9%E5%9B%BE%E4%B9%A6%E9%A6%86/CS-%E8%AE%A1%E7%AE%97%E6%9C%BA/Web-%E5%89%8D%E7%AB%AF/React/React.assets/1654490712545-6bd28fa7-290b-48fb-8d51-bbf5578dad3f.png)



![组件生命周期](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/WebLearn/%E7%BB%84%E4%BB%B6%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)



### 挂载阶段

执行顺序: constructor >> render >> componentDidMount

*注意1:*  state在曾经是需要 ` this.state` 写入 `constructor` 函数中的,但是现在直接写在类组件的内部就行,不需要再专门的写入到` constructor` 函数之中.



*注意2:* 由于每次更改render函数内部的组件,render函数就会重新渲染一次,而如果直接在render中设置state(函数状态),那就就会导致这个语句设置,render就刷新一次,刷新一次,这个语句就会又设置,导致子子孙孙无穷尽也,一直循环.**不能再render中使用serState()**



*注意3:* 整个类组件的执行就是按照如上:  `constructor >> render >> componentDidMount` ,其中componentDidMount 函数是业务开发中使用最重要的.



| 钩子 函数         | 触发时机                                            | 作用                                                         |
| ----------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| constructor       | 创建组件时，最先执行，初始化的时候只执行一次        | 1. 初始化state  2. 创建 Ref 3. 使用 bind 解决 this 指向问题等 |
| render            | 每次组件渲染都会触发                                | 渲染UI（**注意： 不能在里面调用setState()** ）               |
| componentDidMount | 组件挂载（完成DOM渲染）后执行，初始化的时候执行一次 | 1. 发送网络请求  2.DOM操作                                   |



### 更新阶段

每次界面的改变,就是只有这两个函数在重新加载.

| 钩子函数           | 触发时机                  | 作用                                                         |
| ------------------ | ------------------------- | ------------------------------------------------------------ |
| render             | 每次组件渲染都会触发      | 渲染UI（与 挂载阶段 是同一个render）                         |
| componentDidUpdate | 组件更新后（DOM渲染完毕） | DOM操作，可以获取到更新后的DOM内容，**不要直接调用setState** |



### 卸载阶段

用来消除页面中的组件,也常用来消除定时器.

state中尽量保持精简原则:

1.如果数据需要影响到视图,则放在state中,用来控制.

2.数据存放的变量,不会影响视图,是指某些代码零食需要,则不放入state中,也方便使用componentWillUnmount 函数卸载时一同消除或者说是清理.

| 钩子函数             | 触发时机                 | 作用                               |
| -------------------- | ------------------------ | ---------------------------------- |
| componentWillUnmount | 组件卸载（从页面中消失） | 执行清理工作（比如：清理定时器等） |





## 9.0 Hooks

### 9.1 useState（）

useState() 介绍 , 从react中导入 usetate 后就可以使用.

它只能够出现在函数组件中,并且不能将它嵌套在 if / for 等其他域中使用它,它被使用的唯一地方应该是函数组件里面最外层的作用域中.

不在 if / for中使用,是因为它依赖hook执行的顺序,如果在 if / for 中使用它,会将顺序打乱.

```react
import {useState} from 'react'
```



通过解构赋值,可以获得一个状态和一个修改这个状态的方法. 其中解构赋值的时候名字可以自定义,但是它们两个的位置不能改变.前者应该是状态,后者就说修改这个状态的方法.

可以给useState的 ( ) 中赋值一个初始值,但是这个初始值只会在首次的时候生效。

```react
const [count, setcount] = useState(0)
const [flag, setFlag] = useState(flag)
const [list, setList] = useState([])
```



然后可以通过函数使用修改状态的方法,改变这个状态值.每用该方法改变一次,状态自动转变最新的值.

```react
onClick={() => setcount(count + 1)}
```



### 9.2 useEffect()

用于函数组件的副作用[^T].

- 无依赖项
- 有依赖项
  - 添加空数组,首次渲染执行一次.
- 特定依赖项
  - 特性的依赖项一旦改变就会执行.



注意,只要是在useEffect中用到的状态,一定是要写在依赖项中的.

useEffect 都是在组件 Dom 渲染更新完毕之后才执行.



```react
import { useState, useEffect } from "react"
function App () {
  const [age, setage] = useState(0)
  const [name, setname] = useState('张三')

  useEffect(() => {
    // 定义副作用
    console.log("副作用执行了!")
  }, [age])
  return (
    <dib>
      <button onClick={() => setname('李四')}>你现在的名字:{name}</button>
      <button onClick={() => setage(age + 1)}>你现在的年龄:{age}</button>
    </dib>)
}
export default App
```



[T]: 函数除了完成它的主要功能外,还完成了其他的功能,那么多余完成的功能就是这个函数的副作用.

随时获取页面 y 坐标的值.

```react
import { useState } from "react"
// 函数组件的名称要大写.
function UseWindowScroll () {
  cont[Y, setY] = useState(0)
  window.addEventListener('sroll', () => {
    const h = document.documentElement.scrollTop
    setY(h)
  })
  return [Y]
}
export default UseWindowScroll
```



如果传入一个初始状态值的时候,这个值需要计算才能够获得.

那么需要在useState中写明一个箭头函数的,在函数中计算出状态值.



```react
const [name, setName] = useState(()=>{   
  // 编写计算逻辑    return '计算之后的初始值'
})
```





### useEffect清理副作用

如果想要清理副作用 可以在副作用函数中的末尾return一个新的函数，在新的函数中编写清理副作用的逻辑

注意执行时机为：

1. 组件卸载时自动执行
2. 组件更新时，下一个useEffect副作用函数执行之前自动执行

```jsx
import { useEffect, useState } from "react"


const App = () => {
  const [count, setCount] = useState(0)
  useEffect(() => {
    const timerId = setInterval(() => {
      setCount(count + 1)
    }, 1000)
    return () => {
      // 用来清理副作用的事情
      clearInterval(timerId)
    }
  }, [count])
  return (
    <div>
      {count}
    </div>
  )
}

export default App
```



### 9.3 useEffect发送网络请求

不可以直接在useEffect的回调函数外层直接包裹 await ，因为**异步会导致清理函数无法立即返回**

```react
import { useState, useEffect } from "react"
function App () {
  useEffect(() => {
    function loadData () {
      const res = fetch('http://geek.itheima.net/v1_0/channels')
        .then(response => response.json)
        .then(data => console.log(data))
      console.log(res)
    }
    loadData()
  }, [])
  return (
    <div>
    </div>
  )
}
export default App
```



### 9.4 useRef

组件实例 : 指类组件,函数组件没有组件实例.

dom对象 :  标签

分别创建一个类组件和一个标签，并且在这两者中都标记上` ref  `

```react
      <Test ref={testRef}></Test>
      <h1 ref={h1Ref}>this is h1</h1>
```

那么关于这两者的信息,就会自动记录在useRef中的一个`  .current ` 中.

这个时候我们打印出这个` .current ` , 如果是类组件就会得到类组件相关的信息,如果是标签就会得到这个dom节点.

```react
import React, { useEffect, useRef } from 'react'
class Test extends React.Component {
  render () {
    return (
      <div>我是类组件</div>
    )
  }
}

function App () {
  const testRef = useRef(null)
  const h1Ref = useRef(null)
  useEffect(() => {
    console.log(testRef.current)
    console.log(h1Ref.current)
  }, [])

  return (
    <div>
      <Test ref={testRef}></Test>
      <h1 ref={h1Ref}>this is h1</h1>
    </div>
  )
}
export default App
```



控制台输出结果如下:

![1676290122275](D:/A_CODEFILES/Z_gitWarehouse/githubWarehouse/study_with_me/React%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/React.assets/1676290122275.png)



### 9.5 useContext 

使用 useContext 可以直接接受由context.Provider中传输的value值.

```react
import React, { createContext, useContext, useState } from 'react'

const context = createContext()

function ComA () {
    /* 和类组件的接受有点不同 */
  const count = useContext(context)
  return (
    <div>
      我是组件ComA
      <p>我是从App来的数据:{count}</p>
    </div>
  )
}
function ComC () {
  const count = useContext(context)
  return (
    <>
      <div>我是组件ComC</div>
      <p>我是从App来的数据:{count}</p>
    </>

  )
}
function App () {
  const [name, setName] = useState('张三')
  return (
    <context.Provider value={name}>
      <div>
        <ComA />
        <ComC />
      </div>
    </context.Provider>
  )
}
export default App
```



并且在使用useState中的修改方法的时候,这个传过去的状态值同样会改变

```react
const style_btn = {
  width: '100px',
  height: '50px',
  color: '#1bcac6'
}
function App () {
  const [name, setName] = useState('张三')
  return (
    <>
      <context.Provider value={name}>
        <div>
          <ComA />
          <ComC />
        </div>
      </context.Provider>
      <button style={style_btn} onClick={() => {
        setName(() => {
          let temp = name
          temp = temp + "*"
          return temp
        })
      }}>点击在文字后添加星号</button>
    </>
  )
}
export default App
```



Context如果要传递的数据 只需要在整个应用初始化的时候传递一次

就可以就可以选择在index.js文件里做数据提供

![1676293010837](D:/A_CODEFILES/Z_gitWarehouse/githubWarehouse/study_with_me/React%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/React.assets/1676293010837.png)

如果Context需要传递数据并且将来还需要在对数据做修改 底层组件也需要跟着一起变 那就的写到app.js页面,方便改动数据.





## 拓展点

### 1. 时间的获取

获取当下事件

```react
new Date();
```



比如现在有个对象如下

```JavaScript
time: new Date('2021-10-11 10:09:00')
```

获取这个对象可以创建一个方法.

注意,return后面的那个不是单引号,而是tap按键上的那个符号.

```JavaScript
function formatTime (time) {
  return `${time.getFullYear()}-${time.getMonth()}-${time.getDate()}`
}
```

假如不知道一个对象有那些方法,有个小窍门.

比如 `Date()` 对象在浏览器中的控制台中,输入 `new Date().` .

点后面就会弹出许多的关于这个对象的方法可以查看.



### 2. uuid -- 添加独一无二的id

使用 yarn 命令 , 安装这个 uuid,作用就是产生独一无二的id

```react
// 安装
yarn add uuid

// 导报,但是名字是v4,使用as重命名一下更加成语义化
import {v4 as uuid} from 'uuid'
```





### 3. 解构|赋值

>**解构赋值**语法是一种 Javascript 表达式。
>
>通过**解构赋值**，可以将属性/值从对象/数组中取出，赋值给其他变量。



**赋值**

```JavaScript
var a, b
// a 赋值为 10 , b赋值为 20
const [a , b] = [10 , 20]
```



**替换值**

```JavaScript
var a = 10, b = 20
// a 赋值为 20 , b赋值为 10
const [a , b] = [20 , 10]
```



**解构函数返回的数组**

```JavaScript
function f() {
  return [1, 2];
}

var a, b;
[a, b] = f();
console.log(a); // 1
console.log(b); // 2
```



**忽略某些返回值**

```JavaScript
function f() {
  return [1, 2, 3];
}

var [a, , b] = f();
console.log(a); // 1
console.log(b); // 3

// 忽略全部
[,,] = f();
```



**剩余全部赋值给一个**

```JavaScript
/*如果剩余元素右侧有逗号，会抛出 SyntaxError，因为剩余元素必须是数组的最后一个元素。*/
var [a, ...b] = [1, 2, 3];
console.log(a); // 1
console.log(b); // [2, 3]
```



**除了像上面那样解构数组,还可以解构对象**

用这种解构,就相当于把对象中的某种属性单独拿出来使用.

```react
 var { foo, bar } = { foo: "lorem",gee:"GGG",HAA:"HHH", bar: "ipsum" };
console.log(foo)  // lorem
console.log(bar)  // ipsum
```





### 4. JavaScript中函数可以自调用

```JavaScript
!function (a, b) { console.log(a + b) }(10, 20)
```





