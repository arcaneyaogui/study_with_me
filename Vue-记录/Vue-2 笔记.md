## Vue 基础
v-once: 一次插值
v-model：绑定数据源
v-on ： 绑定事件/绑定函数
v-bind ： 绑定标签上的属性

| ```
<button v-bind:disabled="isButtonDisabled">Button</button>
```
 |
| --- |

如果 isButtonDisabled 的值是 null、undefined 或 false，则 disabled attribute 甚至不会被包含在渲染出来的 <button> 元素中。

Object.freeze()，这会阻止修改现有的 property，也意味着响应系统无法再_追踪_变化。
###  v-model
双向绑定数据
```javascript
<div id="root">
  <P V-text="message"></P>
  <P>{{message}}</P>
  <input type="text" v-model="message">
</div>
  <script>
  var vm = new Vue({
  el:'#root',
  data:{
    message:'我是data中的message'
  },
})
  </script>
```
其他内容绑定
```javascript
    <H1>v-model 案例</H1>
    <br>
    <div id="root">
        <P V-text="message"></P>
        <P>{{message}}</P>
        <p>v-model:<input type="text" v-model="message"></p>
        <!-- 鼠标离开文本框之后变化 -->
        <p>v-model.lazy:<input type="text" v-model.lazy="message"></p>
        <!-- 只能输入数字,但是一开始空白时直接输入字符串就失效. -->
        <p>v-model.number:<input type="text" v-model.number="message"></p>
        <!-- 去掉文本框中的空格,只去掉左右的,字符串中间的不会改动 -->
        <p>v-model.trim:<input type="text" v-model.trim="message"></p>
        <br/>
        <hr/>
        <p>{{text_context}}</p>
        <textarea  cols="50" rows="10" v-model="text_context"></textarea>
        <br/>
        <hr/>
        <p>多选框绑定数组</p>
        <input type="checkbox" id="it_Istrue" v-model="isTure">{{isTure}}</div>
        <br/>
        <hr/>


    </div>

    <script>
        var vm = new Vue({
            el:'#root',
            // 构造器
            data:{
                message:'我是data中的message',
                text_context:"文本域内容",
                isTure:false,
            },
        })
    </script>
```

### v-bind
绑定样式与属性，配合三元运算符更方便。
```javascript
    <style>
        .classA{
            color: red;
        }
        .classB{
            color: orange;
        }
        .classimg{
            width: 500px;
            height: 500px;
        }
    </style>


    <H1>v-bind 案例</H1>
    <br>
    <div id="root">
        <img :class='classImg' v-bind:src="img1" alt="">
        <br>
        <!-- v-bind缩写 -->
        <a :href="webUrl" target="_blank">搜索主页</a>
        <p :class="{classB:isOk }">尝试根据不同条件改变字体颜色1</p>
        <p :class="{classA:isOk }">尝试根据不同条件改变字体颜色2</p>
        <p :class="isOk?class_A:class_B">尝试根据不同条件改变字体颜色3</p>
        <input type="checkbox" id="is_Ok" value="isOk" v-model="isOk">
        <label for="isOk">isOk=={{isOk}}</label>

    </div>
    <script>
        var vm = new Vue({
            el:'#root',
            // 构造器
            data:{
                isTure:false,
                img1:'/imgs/111.jpg',
                webUrl:'https://0x3.com/',
                className:'classA',
                class_A:'classA',
                class_B:'classB',
                isOk:true,
                classImg:'classimg'
            },
        })
    </script>
```

### v-pre | v-once | v-clock
```javascript
    <div id="root">
        <H3>v-pre: 原样熏染</H3>
        <p v-pre>{{message}}</p>
        <p>{{message}}</p>

        <H3>v-once: 渲染一次</H3>
        <p v-once>{{message}}</p>
        <p>{{message}}</p>
        <input type="text" v-model="message">

        <H3>v-clock: 页面加载完成后再渲染</H3>
        <p v-clock>{{message}}</p>
        <img :class="img_class" src="/imgs/111.jpg" alt="XXX">
    </div>

    <style>
        .imgclass{
            width: 600px;
            height: 300px;
        }
    </style>

    <script>
        var vm = new Vue({
            el:'#root',
            // 构造器
            data:{
                message:'我是message数据',
                img_class:'imgclass'
            },
        })
    </script>
```

## Vue 自定义 api
自定义指令有五个生命周期（也叫钩子函数），分别是 bind,inserted,update,componentUpdated,unbind

1. bind:只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个绑定时执行一次的初始化动作。
2. inserted:被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于document中）。
3. update:被绑定于元素所在的模板更新时调用，而无论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新。
4. componentUpdated:被绑定元素所在模板完成一次更新周期时调用。
5. unbind:只调用一次，指令与元素解绑时调用。
```javascript
<body>
    <H1>v-directive 案例</H1>
    <br>
    <div id="root">
        <p v-Loading="color">{{data_loding}}</p>
        <button @click="add">加载</button>
        <button onclick='unbind()'>解绑</button>
    </div>

    <style>
        button{
            margin-top: 10px;
            margin-left: 20px;
            width: 100px;
            height: 50px;
        }
    </style>
      
    <script>
        // 解绑
        function unbind(){ 
            // 注意 解绑是下面的var root = new Vue中的root调用的$destroy()
            root.$destroy();
        }
        //自定义的指令需要双引号
        Vue.directive('Loading',{
                bind:function(el,binding,vnode){//被绑定
                    console.log('1 - bind');

                    el.style='color:'+binding.value;
                },
                inserted:function(){//绑定到节点
                    console.log('2 - inserted');
                },
                update:function(){//组件更新
                    console.log('3 - update');
                },
                componentUpdated:function(){//组件更新完成
                    console.log('4 - componentUpdated');
                },
                unbind:function(){//解绑
                    console.log('5 - bind');
                }
            }
        )
        var root = new Vue({
            el:'#root',
            // 构造器
            data:{
                data_loding:0,
                color:'red',
            },
            methods:{
                add:function(){
                    console.log("执行！！！")
                    this.data_loding++;
                },
            },
        })
    </script>
</body>
</html>
```

### directive提供加载思路
提供一种加载的思路，使用的就是vue自定义的api。

- el: 指令所绑定的元素，可以用来直接操作DOM。
- binding: 一个对象，包含指令的很多信息。
- vnode: Vue编译生成的虚拟节点。
```javascript
<body>
    <H1>v-directive 案例</H1>
    <br>
    <div id="root">
        <p v-Loading="isLoading">{{data_loding}}</p>
        <button @click="update">加载</button>
    </div>

    <style>
        button{
            margin-top: 10px;
            margin-left: 20px;
            width: 100px;
            height: 50px;
        }
    </style>
    <script>
        //自定义的指令需要双引号
        Vue.directive('Loading',{
            // 回调用两次这个方法
            update(el,binding,vnode){
                console.log(el);
                console.log(binding);
                console.log(vnode);
                if(binding.value){
                    const div = document.createElement('div')
                    div.setAttribute('id','Loading')
                    div.style.position = 'fixed'
                    div.style.left = 0
                    div.style.top = 0
                    div.style.width = '100%'
                    div.style.height = '100%'
                    div.style.display = 'flex'
                    div.style.justifyContent = 'center'
                    div.style.alignItems  = 'center'
                    div.style.color = 'white'
                    div.style.background = 'rgba(0,0,0,.7)'
                    document.body.append(div)
                }
                else{
                    document.body.removeChild(document.getElementById('Loading'))
                }
            }
        })

        var vm = new Vue({
            el:'#root',
            // 构造器
            data:{
                data_loding:' ',
                isLoading:false,
            },
            methods:{
                update:function(){
                    this.isLoading = true;
                    setTimeout(()=>{
                        this.data_loding = "用户数据";
                        this.isLoading = false;
                    },3000)
                },
            },
        })
    </script>
</body>
```

### v-set
有时候按钮调用方法修改数组不一定能够在页面中显示出来。这个时候使用Vue.set 修改能够保证被Vue监听到.
```javascript
<body>
    <H1>v-model 案例</H1>
    <br>
    <div id="root">
        <p>{{age}}</p>
        <button onclick="addAge()">+++</button>

        <br><hr>

        <ul>
            <li v-for="item in arr">{{item}}</li>
        </ul>
        <button onclick="changeArr()">+++</button>
    </div>

    <script>
        function addAge(){
            outdata.age++;
            console.log(`你的年龄为 : ${outdata.age}`);

            root.age++;
            console.log(`你的年龄为 : ${outdata.age}`);

            Vue.set(outdata,'age',outdata.age+10)
            console.log(`你的年龄为 : ${outdata.age}`);
        }
        function changeArr(){
            //root.arr[1] = "FF"; 点击没反应
            Vue.set(outdata.arr,1,'FFF')
        }
        var outdata = {
            name:'AAA',
            age:10,
            arr:["AA","BB","CC","DD","EE"],
        }
        var root = new Vue({
            el:'#root',
            // 构造器
            data:outdata,
        })
    </script>
</body>
```

## vue -- 生命周期
```javascript
<body>
  <h1>构造器的声明周期</h1>
  <hr>
  <div id="app">
  {{message}}
  <p><button @click="jia">加分</button></p>
  </div>
  <button onclick="app.$destroy()">销毁</button>

  <script type="text/javascript">
  var app=new Vue({
  el:'#app',
  data:{
    message:1
  },
  methods:{
    jia:function(){
      this.message ++;
    }
  },
  beforeCreate:function(){
    console.log('1-beforeCreate 初始化之后');
  },
  created:function(){
    console.log('2-created 创建完成');
  },
  beforeMount:function(){
    console.log('3-beforeMount 挂载之前');
  },
  mounted:function(){
    console.log('4-mounted 被创建');
  },
  beforeUpdate:function(){
    console.log('5-beforeUpdate 数据更新前');
  },
  updated:function(){
    console.log('6-updated 被更新后');
  },
  activated:function(){
    console.log('7-activated');
  },
  deactivated:function(){
    console.log('8-deactivated');
  },
  beforeDestroy:function(){
    console.log('9-beforeDestroy 销毁之前');
  },
  destroyed:function(){
    console.log('10-destroyed 销毁之后')
  }

})
  </script>
</body>
```


## Template 模版
### 在声明的对象中创建template
```javascript
var app=new Vue({
  el:'#app',
  data:{
    message:1
  },
	template：`<p>这是在组件中申明模版</p>`  //注意这是破折号
}
```

### 在html中声明模版
```javascript
<!-- 在html中生命的template需要添加id -->
<template id = "temp">
  <p>我只在html中的template</P>  
</template>

var app=new Vue({
  el:'#app',
  data:{
    message:1
  },
	template："#temp"
}
```

### 在script中声明模版
这个script主要的好处是可以将模版进行引用
```javascript
<!-- 在script中声明的template 不仅需要制定text属性 也需要添加id -->
<script text="x-template" id="temp">
  <p> 我只在script中的template </P> 
</script>

var app=new Vue({
  el:'#app',
  data:{
    message:1
  },
	template："#temp"
}
```

## 组件
### 全局注册
全局注册的conponent标签,只注册一个
```javascript
<div id="app">
    <eeee></eeee>
</div>

<script type="text/javascript">
    //注册全局组件
    Vue.component('eeee',{
        template:`<div style="color:red;">全局化注册的eeee标签</div>`
    })
    var app=new Vue({
        el:'#app',
        data:{
        }
    })
</script>
```
### 局部注册
```javascript
<div id="app">
    <eeee></eeee>
    <fff></fff>
    <ggg></ggg>
</div>

<script type="text/javascript">
    //注册全局组件
    Vue.component('eeee',{
        template:`<div style="color:red;">全局化注册的eeee标签</div>`
    })
    var app=new Vue({
        el:'#app',
        data:{
        },
        components:{
            "fff":{
                template:`<div>我是针对某一个vue对象的局部组件 fff</div>`
            },
            "ggg":{
                template:`<div>我是针对某一个vue对象的局部组件 ggg</div>`
            }
        }
    })
</script>
```
### 外部引入
固定的写法,可以将这个组件在其他的文件中直接通过路径引用.
```javascript
<template>
  <div class="operationsCenter">
  </div>
</template>

<script>
import { axios } from "@/global";
export default {
// data类似于react中的state,用于存放数据.
  data() {
    return {
      },
      // 定义一个rules属性，用于存储表单验证规则
      rules:{
      },
    };
  },

  mounted() {
  },
  created () {
  },
  computed:{},
  methods: {},
  },
};
</script>

<style scoped>

</style>
```
## propsData
使用这个可以直接在相关的外面来给自定义的扩展传值.
```javascript
    <div id="root">
        <YAOGUI></YAOGUI>
    </div>
    <script type="text/javascript">
        var YAOGUI = Vue.extend({
            template:`<div>我是{{message}}标签,我的特点是:--{{meg}}</div>`,
            data:function(){
                return{
                    message:"YAOGUI",
                }
            },
            // 需要使用单引号包裹接受到的值,中括号包裹
            props:['meg']
        });
        // 使用propsData传值,大括号包裹props,同样大括号包裹传递的值
        new YAOGUI({propsData:{meg:"非常英俊"}}).$mount('YAOGUI');
    </script>
```
在组件中使用props['参数名'] 的方式传值
```javascript
    <div id="app">
      <panda here="China"></panda>
    </div>

    <script type="text/javascript">
        var app=new Vue({
            el:'#app',
            components:{
                "panda":{
                    template:`<div style="color:red;">Panda from {{ here }}.</div>`,
                    props:['here']
                }
            }
        })
    </script>
```

## Methods
关于鼠标的一些悬停啊,点击啊.交互事件啊一般都放在这个里面.
$event 这个在点击事件中传入此参数,能够获取很多关于鼠标的坐标啊,屏幕坐标啊等详细信息.
不同的作用域内,调用methods中的方法,那个click写法不一样
```javascript
    <div id="root">
       <button>{{a}}</button>
       <p><button @click="add(2)">add</button></p>
       <p><btn @click.native="add(2)"></btn></p>
    </div>
    <button onclick="root.add(3)">外部访问构造器里的方法</button>

    <script type="text/javascript">
        Vue.component("btn",{
            template:'<button>外部组件</button>'
        })
        var root=new Vue({
            el:'#root',
            data:{
                a:1
            },
            methods:{
                add:function(num){
                    this.a+=num;
                 }
            },
        })
    </script>
```

## watch
说白了一个值的改变，它能够记录改变前的值（oldVal）与改变后的值（newVal），尤其是用来设定不数据渲染不容的界面的时候。
```javascript
 <div id="root">
        <p>{{wendu}}</p>
        <p>{{jianyi}}</p>
       <p><button @click="add(5)">升高温度</button></p>
       <p><button @click="reduce(5)">降低温度</button></p>
    </div>

    <script type="text/javascript">

        var root=new Vue({
            el:'#root',
            data:{
                wendu:20,
                jianyi:"适合穿春秋装"
            },
            methods:{
                add:function(num){
                    this.wendu+=num;
                 },
                 reduce:function(num){
                    this.wendu-=num;
                 }
            },
            watch:{
                wendu:function(newVal,oldVal){
                    if(newVal < 10){
                        this.jianyi = "到冬天了,要穿袄子"
                    }else if (newVal > 30) {
                        this.jianyi = "到夏天了,要穿短袖"
                    } else {
                        this.jianyi = "气温能够忍受."
                    }
                }
            }
        })
    </script>
```
也可以将watch写在构造器的外边。
```javascript
root.$watch:{
                wendu:function(newVal,oldVal){
                    if(newVal < 10){
                        this.jianyi = "到冬天了,要穿袄子"
                    }else if (newVal > 30) {
                        this.jianyi = "到夏天了,要穿短袖"
                    } else {
                        this.jianyi = "气温能够忍受."
                    }
                }
            }
```
## Mixins

1. 构造器核心功能已近写好了,这个功能是这个项目临时需要的功能,那么我写入到Mixins之中.
2. 我有很多公共的方法,好几个构造器都需要用到,不可能每个构造器都去写一遍,可以写到这个Mixins中,然后各个构造器调用就行.
3. 执行顺序是 全局混入 ==> 外部混入 ==> 原生代码.
```javascript
    <script type="text/javascript">
        var aaa={
            created:function(){
                console.log('我是外部被混入的');
            }
        }
        //全局混入
        Vue.mixin({
            created:function(){
                console.log('我是全局被混入的');
            }
        })
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },
            created:function(){
                console.log('我是原生的');
            },
            mixins:[aaa]
        })
    </script>
```

## extends
extend后面只能是个对象,和Mixins不一样,Mixins后面是个数组,说米昂extends只能有一个.
然后当项目中你的插值有冲突的时候,可以使用 delimiters 选项自定义插值的写入格式.
```javascript
    <div id="app">
        {{message}}
        <p><button @click="add">add</button></p>
    </div>

    <script type="text/javascript">
        var bbb={
            created:function(){
                console.log("我是被扩展出来的");
            },
            methods:{
                add:function(){
                    console.log('我是被扩展出来的方法！');
                }
            }
        };
        var app=new Vue({
            el:'#app',
            data:{
                message:'hello Vue!'
            },
            methods:{
                add:function(){
                    console.log('我是原生方法');
                }
            },
            extends:bbb,
            delimiters:['${','}']
        })
    </script>
```


## vue和其他技术混用
只能在mount 和 update的生命周期中才能够使用jquery.
