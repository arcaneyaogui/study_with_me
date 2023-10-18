# 创建项目
使用vue ui 创建项目，首先需要安装vue  ， 这个安装命令各种警告。
但是程序员准则之一，就是只要不报错，就是没问题  = _ = 
明明在装nvm的时候,将下载源都是切换到阿里源的,国内源不就是方便国内下载码,离谱的就是国内的镜像源,用国内的网一搞就下不动,反而开个代理的话下载顺畅多了。什么牛马？
```powershell
# 安装vue
npm install -g @vue/cli

#查看版本,判断是否成功
vue --version

#使用vue ui创建项目
vue ui
```

---

果不其然，我总是一开始就要出点问题的。习惯了
这个报错信息是说以前安装了旧版本的vue-cli ， 现在需要先卸载再安装
```powershell
npm ERR! code EEXIST npm ERR! 
path D:\SoftWare\NodeFiles\node_global\node_modules\@vue\cli\bin\vue.js npm ERR! dest 
D:\SoftWare\NodeFiles\node_global\vue npm ERR! EEXIST: file already exists, cmd shim 
'D:\SoftWare\NodeFiles\node_global\node_modules\@vue\cli\bin\vue.js' -> 'D:\SoftWare\NodeFiles\node_global\vue' npm ERR! File exists: 
D:\SoftWare\NodeFiles\node_global\vue 
npm ERR! Remove the existing file and try again, or run npm npm ERR! with --force to overwrite files recklessly. npm ERR! A complete log of this run can be found in: npm ERR! D:\SoftWare\NodeFiles\node_cache\_logs\2023-04-19T02_01_20_879Z-debug.log
```
vue-cli 卸载命令：
```powershell
npm uninstall -g vue-cli npm install -g @vue/cli
```

但是又遇见了个问题，就是我下载的各种包安装成功运行的时候总不成功。
```powershell
显示'xxxxxx' 不是内部或外部命令，也不是可运行的程序 或批处理文件
```
既然安装成功，运行不成功就只有一点，就是系统找不到那个包，安装nvm管理node之前，由于看过一篇教程，是教你如何将npm下载的npm包路径放到其他盘，不让他默认在C盘。其中有一步骤就是配置 `.npmrc `文件。
```powershell
prefix=D:\SoftWare\NodeFiles\node_global
cache=D:\SoftWare\NodeFiles\node_cache
registry=http://registry.npmjs.org/
proxy=null
```
而是我配置的这个设置，导致下载的npm安装的包总是在指定的路径上，而不是下载到nvm对应当前使用node版本号的文件中。就出现使用`node -v` 和 ` npm -v  `都没什么问题。但是就是不能运行指定的包。
我的解决办法也很粗暴，就是删掉 `.npmrc ` 文件，然后删除掉该路径的文件，然后重新下载需要的包，就ok了。
下载好@vue/cli , 居然可以使用vue ui 构建项目 , 这也太无脑了吧...好像是有点爽

---

说实话,真是离谱...         视频学着学着看到个接口测试工具,我靠,还是第一次接触.
先使用Apifox测试节点输入正常的数据是否能够返回相关数据,其实我也不太懂怎么用,怎么测....

---

如果前端存在跨域问题, 就是用token来维持用户的登录状态. token由服务器生成,前端发起请求之后返回.
如果不存在跨域问题,就是用cookie 和 session 来维持登录状态.
![1681894573566.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1681894579987-31bb5cfe-e317-475e-8e94-d0fb5df2cbe0.png#averageHue=%23f4f9f0&clientId=u9dab889c-ff16-4&from=paste&height=425&id=u3aeb240d&originHeight=467&originWidth=1081&originalType=binary&ratio=1.100000023841858&rotation=0&showTitle=false&size=132880&status=done&style=none&taskId=u17944632-67cb-46d3-85d5-6c3e1bca31b&title=&width=982.7272514272332)

在编写新项目代码的时候,应该首先检查该本地仓库是否干净.编写过程中的代码应该是创建新分支,写好后在合并到主分支.

---

##  In--Coding
创建登录组件（loginPage） ， 然后将组件配置到路由中，并重定向默认访问根目录下就是登录界面。
```vue
import Vue from 'vue'
import VueRouter from 'vue-router'
import loginPage from '../components/loginPage.vue'
Vue.use(VueRouter)
const routes = [
  //默认访问login页面,重定向.
  {path: '/', redirect:'/login'},
  // 设置路由 , 路径和对应的组件
  {path:'/login', name: 'loginPage',component:loginPage}
]
const router = new VueRouter({
  routes
})
export default router
```
在app组件中，需要配置路由站位符 ` <router-view></router-view> ` 
登录界面中,需要将登录框那部分的div居中,可以使用如下方法:
```css
// 让盒子居中
position: absolute;
left: 50%;
top: 50%;
transform: translate(-50%,-50%);
```
使用 Vue ui 创建的项目中安装的element插件，会在文件目录下有个 ` plugins` 文件，其中有个· ` element.js  ` 文件用来导入项目中要用的样式名称.
在这个 ` element.js  ` 声明后,再在项目中用到相关的样式就不会报错了
```javascript
import Vue from 'vue'
import { Button } from 'element-ui'
import { Form , FormItem } from 'element-ui'
import { Input } from 'element-ui'

// 每个导入的样式都要这样声明一下
Vue.use(Button)
Vue.use(Form)
Vue.use(FormItem)
Vue.use(Input)
```

box-sizing:border-box;  表明一个元素设置的宽度是否包含 border 和 padding , 注意: border-box 不包含 margin。
![1681962943669.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1681962950344-800827ba-14fc-474a-9d3e-956ae9330843.png#averageHue=%23e7e5e2&clientId=u01b73afe-e0a2-4&from=paste&id=u838d61c3&originHeight=303&originWidth=844&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25091&status=done&style=shadow&taskId=u76296d56-8182-44b5-b54e-fc0fd4a16a7&title=)

**添加图标
**suffix-icon="xxx"  添加后面的图标         prefix-icon="xxx"  添加前面的图标

---

### 数据绑定
然后再表单中的每个填写的数据需要用 `v-model `绑定,需要一个一个的对应.
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1681968914744-fc8783a5-6fb2-48b5-90f2-660836d4c65e.png#averageHue=%2323282f&clientId=u01b73afe-e0a2-4&from=paste&height=761&id=u74c8660c&originHeight=630&originWidth=955&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76716&status=done&style=none&taskId=uc8f0a0ac-263d-456e-8ef6-17f646906e4&title=&width=1153.1817626953125)

---

### 表单校验
为表单绑定验证跪着 , 然后咋data的return中添加自定义的校验规则:
```javascript
      <el-form :rules="loginFormRules"  >
          // 制定某一条校验适用于此处  prop="xxx"
          <el-form-item prop="username">
            <el-input 
            v-model="loginForm.username" 
            prefix-icon="el-icon-user-solid"
            ></el-input>
          </el-form-item>
    	</el-form>

			// 校验规则 
      loginFormRules:{
        username:[
            { required: true, message: '请输入个人的用户名名称', trigger: 'blur' },
            { min: 3, max: 5, message: '用户名长度在3-5个字符之间', trigger: 'blur' }
        ],
      },
```
 

---

### 表单重置
想要重置表单 , 就需要拿到表单的实例对象 , 那么就需要给表单添加 ref  属性并自定义实例对象名以便我们获取.
```javascript
<el-form  ref="loginFormRef"  class="login_form">  </el-form>

```
能欧获取表单的实例对象之后,就可以使用element的表单组件中的 ` resetFields ` 方法来重置表单属性.
### Form Methods
| 方法名 | 说明 | 参数 |
| --- | --- | --- |
| validate | 对整个表单进行校验的方法，参数为一个回调函数。该回调函数会在校验结束后被调用，并传入两个参数：是否校验成功和未通过校验的字段。若不传入回调函数，则会返回一个 promise | Function(callback: Function(boolean, object)) |
| validateField | 对部分表单字段进行校验的方法 | Function(props: array &#124; string, callback: Function(errorMessage: string)) |
| resetFields | 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果 | — |
| clearValidate | 移除表单项的校验结果。传入待移除的表单项的 prop 属性或者 prop 组成的数组，如不传则移除整个表单的校验结果 | Function(props: array &#124; string) |

点击取消按钮 , 实现表单中的数据重置.
```javascript
<el-form-item class="btns">
	<el-button type="primary" @click="check_loginForm">确定</el-button>
	<el-button type="info" @click="reset_loginForm">取消</el-button>
</el-form-item>

// 点击取消 重置表单
reset_loginForm(){
	// 还原data里的表单数据
	Object.assign(this.$data.loginForm, this.$options.data().loginForm);
	// 重置实例对象.
	this.$refs.loginFormRef.resetFields();
}
```

---

### axios全局挂载
```javascript
/**
 * 添加到vue.prototype.$http后
 * 可以在每一个组件上通过 this.$http 获取axios 
 * 不必每个页面都 import axios , $http是自定义的属性名
 */
import axios from 'axios'
// 配置根目录
axios.defaults.baseURL = 'http://127.0.0.1:8888/api/private/v1/';
Vue.prototype.$http = axios;
```
点击确定后,需要使用axios发起请求

1. 为什么箭头函数钱要加 async 和获取请求的前面为啥加 await?
   1. 因为不加的话,就会显示是 promise
2. post请求中, 一定要按照对应的文档传参.
```javascript
    // 直接使用validate检查 符合rules则表示成功，不符合则报错
    check_loginForm(){      
      this.$refs.loginFormRef.validate( async (valid) => {
        if(!valid) return;
          const result = await this.$http.post('login',this.loginForm);
          const res = result.data;
          if(res.meta.status !==200) return console.log("登录失败");
          console.log("登录成功");
      })
    },
```

---

### Message
```javascript
// 导入弹窗提示
import { Message } from 'element-ui'
/**
 * $message , $后面的名称自取，见名知意即可。
 * 等号后的 Message 不可变动。
 * 只要是全局运用到的，需要挂在到Vue原型上。
 */
Vue.prototype.$message = Message;
```

---

### 路由导航守卫

- beforeEach 函数接收三个参数 
   - to ： 要跳转到那个页面。
   - from ： 表示是从来个页面跳转而来 。
   - next ： 表示放行的函数。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1682041598089-04f04b4f-bf4a-42b2-9c92-8f34b702fd1d.png#averageHue=%23dee9f7&clientId=u3cd13b85-8b3f-4&from=paste&height=419&id=udd1f893d&originHeight=461&originWidth=917&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188134&status=done&style=none&taskId=u93af6a20-80bd-445c-bffe-840ead05e18&title=&width=833.6363455677824)

就是如果没登录成功，本地就不应该有远端服务器生成的token值。
因此可以判断是否有token值且判断token值是否为空来决定访问的路由是否放行。
但是此处的代码，其实你把token随便自己写都可以通过，不严谨， 没判断token值。
后期的话，可以向后端发送请求，判断token值是否正确。
```javascript
const routes = [
  //默认访问login页面,重定向.
  {path: '/', redirect:'/login'},
  // 设置路由 , 路径和对应的组件
  {path:'/login', name: 'loginPage',component:loginPage},
  {path:'/home', name: 'homePage',component:homePage}
]
const router = new VueRouter({ routes })

router.beforeEach((to,form,next)=>{
  // next() 放行  next('路劲')强制跳转
  if(to.path === '/login') return next();
  // 获取token 判断是否登录
  const tokenStr = window.sessionStorage.getItem('token');
  if(!tokenStr) return next('/login');
  next();
})
```

---

### 退出功能
退出系统的核心功能就是清空token值，当token被清空再访问就是强制在登录界面了。            
![image.png](https://cdn.nlark.com/yuque/0/2023/png/33584294/1682042783388-08bfc6c1-a32c-48fd-bbab-53a21dab1064.png#averageHue=%23e1ecfa&clientId=u3cd13b85-8b3f-4&from=paste&height=222&id=u8d3f5583&originHeight=244&originWidth=887&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99292&status=done&style=none&taskId=ub0cdda86-c973-4654-bd3a-02e95464a07&title=&width=806.3636188861756)
在一个退出按钮上绑定一个时间。
```javascript
  methods:{
    logout (){
      // 清空token
      window.sessionStorage.clear();
      //跳转页面
      this.$router.push('/login');
    },
  },
```

---

### 内容布局页面
浪费了几个小时的小插曲 = = 这里遇见一个问题 ：WebSocket connection to 'wss://localhost:8000/wss' failed
控制台经常报这个，谷歌，百度，bingAI都没解决，
最后想着反正是node_moudles中的一个包的问题吗，之前下载这个node_moudles的时候本来也是用的12版本的node下载的，后来直接删除，改成现在的18版本的node再下载一遍就他妈不报错了。

提一嘴 ， element组件的名称其实就可以当做类名去调用。牛逼
然后在这一段学习过程中学到个flex布局的标签，两端对其。
```css
.el-header{
	background-color: #373d41;
	display: flex;
	// 左右贴边对其
	justify-content: space-between;
}
```

说实话，我觉得写前端代码的时候，我发现最不好阅读的其实是html代码
看见弹幕中有个封装和插槽的概念， 这个到时候去了解一下。

---

### 请求拦截
axios请求拦截的作用在于，在发起请求时，和在收到服务器的相应时，在这个过程中先拦截下来，可以自定义自己的操作，属于一个预处理过程。
:::info
axios请求拦截 interceptors.request.use（）
:::
在该项目中，除登录的aip外，都是需要权限访问的api，所谓的权限也就是登录成功之后服务返回并保存在你本地的token令牌。而我们使用axios访问这些需要权限的api的时，我们发送请求时带给服务器端去验证，需要根据文档中的需求，在header中添加对应字段，并且给该字段赋值为本地的token。
```javascript
import axios from 'axios'
// 配置根目录
axios.defaults.baseURL = 'http://127.0.0.1:8888/api/private/v1/';
//挂在axios之前 ,定义一个拦截器
axios.interceptors.request.use(config=>{
	// 为headers（请求头）添加 Authorization 字段赋值为本地token
	config.headers.Authorization = window.sessionStorage.getItem('token')
	// 固定写法，最后一定要返回
	return config
})
Vue.prototype.$http = axios;
```

---

### 侧边栏
这部分的重点就是学会了如何实现v-for渲染从服务器获取到的二级菜单。

- index 配置不同的字符串值，如果一样点击一个列表展开值相同的都展开了。
- 渲染二级菜单是在每个一级菜单的item下进行渲染。
- 了解到了cursor样式
```javascript
<el-submenu :index=" item.id+' ' "  v-for="item in menuList" :key="item.id">
	<el-menu-item  :index=" itemTwo.id+' ' "  v-for="itemTwo in item.children" :key="itemTwo.id">


  //鼠标碰触 变小手
  cursor: pointer;
```

---

### 设置路由高亮
给二级菜单绑定事件：
```javascript
@click="sevaNavState('/'+itemTwo.path)"
```
然后再data中穿件一个专门用来存储显示高亮的那个路由值.,点击那个路由,就讲那个路由赋值给那个变量,然后再html中的element菜单组件中有个属性 `:default-active="activePath"`
主要是这个高亮的实现,居然是存储到session本地中,这个是我没想到的.
```javascript
//实现二级菜单点击高亮
sevaNavState(activePath){
  // 将路径保存到session会话
  window.sessionStorage.setItem('activePath',activePath);
  this.activePath = activePath;
}
```

---

element 的 布局 , row 和 col 是用来控制元素的位置和距离的.
` :gutter="20" ` 实现控制各个元素之间的间距.    
```javascript
    <!-- 面包屑 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    </el-breadcrumb>

    <!-- 搜索框 -->
    <el-card>
      <el-row :gutter="20">
        <el-col :span="10" >
          <el-input placeholder="请输入内容">
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </el-col>
        <el-col :span="6">
          <el-button type="primary" >搜索</el-button>
        </el-col>
      </el-row>
    </el-card>
```

---

### 状态转换
使用作用域插槽能够接受数据，并且`  scopr.row `就是当前这一行的数据,然后使用了插槽就会覆盖props,所以可以不写props
`border` 表示表格有边框   `stripe` 各行背景色不一.
```html
      <el-table :data="userslist" border stripe>
        <el-table-column type="index" label="#"></el-table-column>
        <el-table-column label="姓名" prop="username"> </el-table-column>
        <el-table-column label="邮箱" prop="email"> </el-table-column>
        <el-table-column label="电话" prop="mobile"> </el-table-column>
        <el-table-column label="角色" prop="role_name"> </el-table-column>
        <el-table-column label="状态">
          <template slot-scope="scope">
            <el-switch v-model="scope.row.mg_state"> </el-switch>
          </template>
        </el-table-column>
        <el-table-column label="操作"> </el-table-column>
      </el-table>
```

---

### 分页
这里由于明明定义了变量，但还是报未定义， /*eslint-disable*/直接忽略当前的语法报错。eslint检查真的很魔幻。
```vue
<!-- 分页区域 -->
<el-pagination
  @size-change="handleSizeChange"
  @current-change="handleCurrentChange"
  :current-page="queryInfo.pagenum"
  :page-sizes="[1, 3, 5, 7]"
  :page-size="queryInfo.pagesize"
  layout="total, sizes, prev, pager, next, jumper"
  :total="total">
</el-pagination>


 /*eslint-disable*/
  data(){
    return{ 
      queryInfo:{
        query:'',
        // 当前页数
        pagenum:1,
        // 当前每页显示多少条数据
        pagesize:5,
      },
      // 发起请求后获取的数据存放到 userslist
      userslist: [],
      // 总共有多少条数据
      total:0,
    }
  },
```

---

### 用户页面完善
 查询功能 ， 其实这里后台的查询语句，应该只实现了搜索用户的匹配查询，如果查电话号码是查不出来的。
```
// 双向绑定数据，作为查询关键字
v-model="queryInfo.query"
// 组件库提供搜索框叉号，点击清楚
clearable
// 清楚之后自动查询一遍
@clear="getUserList">

// 给搜索按钮添加查询事件
<el-button @click="getUserList"></el-button>
```
 
新增用户弹窗关闭窗口后文本框重置：
在dialog上绑定close事件，然后再事件中获取ref对象，调用` resetFields `
```javascript
this.$refs.addFormRef.resetFields();
```

然后点击确定天机按钮的时候,需要做一个欲校验 , 只有当表单中的所有框填有内容不违背格式,这个valid值才会是true
```javascript
this.$refs.addFormRef.validate((valid) => {if(!valid) return;})
```
然后调用 api 接口, 对数据库进行更新, 最后重新查询, 关闭当前的新增窗口.
```javascript
    // 欲校验 通过则新增用户
    addUsers(){
      this.$refs.addFormRef.validate( async (valid) => {
        if(!valid) return;
        const{data:res} = await this.$http.post(`users`,this.addForm);
        if(res.meta.status !== 201){
          return this.$message.error("添加用户失败");
        }else{
          this.$message.success("添加用户成功");
        }
        // 不关失败或者成功 , 将窗口隐藏.
        this.addUsersVisible = false;
        this.getUserList();
      })
    },
```

同样编辑用户之后,也是首先验证输入的信息是否正规 ==> 调用api , 并携带参数, 修改数据库中数据 ==> 检测返回状态码根据结果来显示界面 ==> 先关闭窗口再调用查询方法
```javascript
  	//更新用户信息
    editUserInfo(){
      this.$refs.editFormRef.validate( async (valid) => {
        if(!valid) return;
        const{data:res} = await this.$http.put(`users/${this.editForm.id}`,{
          email: this.editForm.email,
          mobile: this.editForm.mobile,
        });
        if(res.meta.status !== 200){
          return this.$message.error("更新失败");
        }else{
          this.editDialogVisible = false;
          this.getUserList();
          this.$message.success("更新成功");
        }
      })
    },
```

删除用户功能
```javascript
async removeUserById(Id){
      /**
       * 点击确认 , confirmResult接收返回值则为字符串的 confirm
       * 点击取消则返回一个error,用catch捕获抛出 , confirmResult依旧接受的一个字符串 cancel
       */
      const confirmResult = await this.$confirm('确认删除?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
      })
      .catch(err => err)
      if(confirmResult !== 'confirm'){
        return this.$message.info("删除操作取消");
      }
      // 调用删除接口
      const {data:res} = await this.$http.delete(`users/${Id}`);
      if(res.meta.status !== 200) {return this.$message.error("删除失败")}
      this.$message.success("删除成功");
      this.getUserList(); 
    },
```

---

### 用户权限 列表渲染
主要使用了 tag 标签， 然后 使用插槽获取当前表单的数据 ， 使用 type = “index”实现序列。
```javascript
      <!-- border 表格添加边框 ，stripe 隔行变色  -->
      <el-table :data="rightsList" border stripe>
        <el-table-column type="index"></el-table-column>
        <el-table-column lable="权限名称" prop="authName" ></el-table-column>
        <el-table-column lable="路径" prop="path" ></el-table-column>
        <el-table-column lable="权限等级" prop="level" >
          <template slot-scope="scope">
            <el-tag v-if="scope.row.level === '0' ">一级权限</el-tag>
            <el-tag type="success" v-else-if=" scope.row.level === '1' ">二级权限</el-tag>
            <el-tag type="warning" v-else-if=" scope.row.level === '2' ">三级权限</el-tag>
          </template>
        </el-table-column>
      </el-table>
```
