#  Typescript

## 个人前言

`Typescript`   并不是一个新的语言,它的所有的语言都会被编译成JavaScript语言进行运行.
 它更像是`JavaScript`的约束,使得`JavaScript`能够想`java`等语言一样,有着自定义变量类型,强有力的约束等等.

比如在Ts文件中写如下代码，加以限制

```tsx
let age:number = 20;
// 注意下面行为会报 "不能将类型“string”分配给类型“number”
age = “20岁”
```

如果上方代码运行在Js中，则不会报错任何问题，在ts中有了各种各样的限制，能够让我们在编写代码的时候，提前就能发现一些我们的代码编写问题，省去了后续的查找错误的时间，节约人力精力。

（<s>可哲学的问题来，明明各种新科技，各种新技术都是为了更节约人的精力和时间成本创造出来的，但是人为什么越来越累，越来越忙，越来越自顾着自己在某个地方的一亩三耕地，并没有看见我们节约出了多少的时间用来自己的生活。</s>>）



---

## 环境搭建

首先去弄得官网安装node.js , 然后使用如下命令查看是否安装成功.

```bash
node -v
npm -v
```

然后修改node的下载源为淘宝源 (其实以前用的时候觉得原来的源也没啥问题,网上都这么改,还是改改吧)

```bash
npm config set registry https://registry.npm.taobao.org
```

然后修改 node 的全局安装位置,不能让它默认在C盘 , 不然晚上睡觉都睡不着.

使用如下两条命令,修改路劲(路径是个人node文件的安装路径)

```bash
npm config set prefix "D:\SoftWare\NodeFiles\node_global"
npm config set cache "D:\SoftWare\NodeFiles\node_cache"
```

然后配置环境变量 , win+q 搜索 环境变量.
首先系统环境变量中创建一个`NODE_PATH`,然后值为`D:\SoftWare\NodeFiles\node_modules` 
接着在系统变量中的path中,新增node文件的安装路径`D:\SoftWare\NodeFiles\`
最后在用户变量中的path中添加`D:\SoftWare\NodeFiles\node_global`
到此,环境变量就配置完成了

然后查看一下,在没修改前安装`Typescript`是如下默认配置:

```bash
$ npm list -g
C:\Users\arcan\AppData\Roaming\npm
├── typescript@4.9.5
└── webpack@5.75.0
```

修改成功后安装`Typescript`就会变成我们之前创建好的文件夹中

```bash
$ npm list -g
D:\SoftWare\NodeFiles\node_global
└── typescript@4.9.5
```

反正如果出现-4080的报错,那么使用如下命令:

```bash
npm cache clean --force
```

安装`Typescript` 

```bash
npm install -g typescript
```

最后使用`tsc -v ` , 测试看看是否安装成功

```bash
$ tsc -v
Version 4.9.5
```

但是windows系统，默认是禁止运行脚本的。我们需要在管理员的身份下运行 powershell 使用命令修改这一点。

```powershell
get-ExecutionPolicy
Restricted  #表示状态是禁止的

set-ExecutionPolicy 
RemoteSigned 

get-ExecutionPolicy  
RemoteSigned;
```



---

##   Use TypeScript 

首先需要使用命令，在项目中创建一个`tsconfig.json` 文件.这个里面是关于我们`Typescript`相关配置.

```powershell
tsc --init
```

这个` tsconfig.json` 内容很多,先了解基本有用的.

```json
"target": "ES2016",  // 指定编译成JavaScript的那个版本的语法,一般2016方便浏览器兼容
"rootDir": "./src",  // 指定源代码文件
"outDir": "./dist",  // 将ts编译后的js代码存放的位置
"removeComments": true, // 删除在ts代码中的注释,让js更加简短.
"noEmitOnError": true,  //当ts代码有问题的时候,不编译成JavaScript代码

"sourceMap": true,  // 每一行的ts代码映射的js代码,方便排查问题,生成index.js.map
```



调试ts的代码

![ts001.png](https://s2.loli.net/2023/03/01/A7FpXRSl3O8Dsy9.png)

需要在新生成的`launch.json`文件中添加一段代码,告诉vscode使用这个配置文件来构建我们的应用程序

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "启动程序",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}\\src\\index.ts",
            // 我们需要添加如下这句⬇⬇⬇⬇⬇⬇
            "preLaunchTask": "tsc:build - tsconfig.json",
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
}
```

注意,如果你的vscode下载了中文的简体包,汉化了.那么你需要添加的语句改为如下:

```json
"preLaunchTask": "tsc: 构建 - tsconfig.json",
```

配置好后，可以直接在 vscode 的终端中使用 node 运行指定路劲的 js 文件

```powershell
node ./dist/index.js 
```



### Typescript 常见基本类型

| JavaScript | Typescript |
| ---------- | ---------- |
| number     | any        |
| string     | unknown    |
| boolean    | never      |
| null       | enum       |
| undefined  | tuple      |
| object     |            |

---



关于 ? 、?? 、! 、!! 的基本介绍:

- 属性或参数中使用?表示该属性或参数为可选项
- ??表示只有当左侧为null和undefined时, 才会返回右侧的数
- 属性或参数中使用!表示表示强制解析（告诉typescript编译器，这里一定有值)
- 变量前使用!表示取反, 变量后使用!表示类型推断排除null、undefined从而使null 和undefined类型可以赋值给其他类型并通过编译
- !!表示将把表达式强行转换为逻辑值



#### any 

**我们应该尽量避免使用any去构建我们的项目**

我们创建变量,可以自定义它原本的类型

```tsx
// 数字中可以使用下划线,来让数字可读性更高
let num:number = 123_456_789;
let str:string = "aaaaaaaaaa";
let is_true:boolean = true;
```

如果创建一个变量,没有给任何值.那么会被ts默认为any类型的变量.你之后也可以给他赋值任何类型的值.

```typescript
let notOne;
notOne = 1;
notOne = "呵呵哒";
```

又比如有如下在JavaScript中正常的函数

```typescript
function heheda (document){
    console.log(document)
}
```

控制台会报错 

>应为标识符。ts(1003)[行10.列9]
>参数"document"”隐式具有"any”类型。ts(7006)[行10，列10]

要么在函数中给变量添加 any , 告诉计算机你知道你自己在做什么.

```typescript
function heheda (document:any){
    console.log(document)
}
```

或者在`tsconfig.json`中在Type Checking里将  ` noImplicitAny: false,`  

但是不推荐这么做,这么做的话带类型检查的ts脚本语言,那不就是失去了他的意义?

---



#### 数组

在JavaScript中,如果我向如下方式声明一个数组,是完全没毛病的.

```JavaScript
let nums = [1,2,"3"];
```

但是我们使用typescript就需要声明,给它加上一定的限制

```typescript
let nums:number [] = [1,2,3]
```

最重要的不是其他,而是我们直接输入 ` nums. ` 会弹出各种number数组相关的方法.这些都是已近写好的
同样我们创建一个字符串的数组,之后在数组名后加 . 就是相关字符串数组的各种相关的方法可供使用.

#### 元组

我们知道数组中元素的数据类型都一般是相同的（any[] 类型的数组可以不同）
如果存储的元素数据类型不同，则需要使用元组。元组中允许存储不同类型的元素，元组可以作为参数传递给函数。

```typescript
// 元组最常见的使用是一对,两个元素.
let user:[number,string] = [1,"张三"]
```

只设定了两个, 如果后面再加一个元素,则会提示报错.

同样和数组一样,使用`user[0].xxx` 你可以使用关于number类型数组的各种方法.

`user[1].` 你可以使用关于字符串类型的各种方法.

但是如上代码,你哪怕限制了,你依旧可以使用 push()方法,给这个已近限定好两个元素的元组再添加元素.
这个方法更像是暂时无法解决的一个bug,说不定以后的ts就不能这么搞了.

#### 枚举

我们要定义关于一个对象的多个标准的时候要生成多个变量

```JavaScript
let small = 1;
let middle = 2;
let large = 3;
```

但是枚举可以更见可视化,便捷一点。不设定第一个变量值的时候默认是0，后面两个依次递增。

如果设定为自定义的数字，后面两个也是依次递增，但是如果是设定字符串类型，则三个都需要写明值。

```typescript
enum Size { Small,Middle,Large };
// 使用的时候
let mySize:Size = Size.Middle;
```

上面两行对应的代码，转译成JavaScript代码就显得很冗长

```JavaScript
var Size;
(function (Size) {
    Size[Size["Small"] = 0] = "Small";
    Size[Size["Middle"] = 1] = "Middle";
    Size[Size["Large"] = 2] = "Large";
})(Size || (Size = {}));
;
let mySize = Size.Middle;
console.log(mySize);
```

但是有意思的是,在枚举前面添加 const 关键字,能够使得它编译成的JavaScript代码更加简洁

```typescript
const enum Size { Small,Middle,Large }
let mySize:Size = Size.Middle
console.log(mySize)
```

对应的JavaScript代码

```JavaScript
"use strict";
let mySize = 1;
console.log(mySize);
```

这是不是也再次说明,没有真正的谁优于谁,大道至简又是道不可悟.

#### 函数

先介绍`"noUnusedParameters": true,` 在  Type Checking  下的一个配置.

这个配置可以让你编码时如果没有使用函数中的参数,那么就会提示你参数未被使用.

聊聊函数其实就是和 Java 一样, 你可以通过修饰方法一样来修饰JavaScript中的函数法传入指定类型的参数和返回指定类型的值

当然我们应该了解的是,***当函数没有返回值的时候,它是默认返回undefined的***

```typescript
function mount (a:number,b:number):number{
    let c : number = a + b
    return c
}
```

如果只有一个参数是必要的,另外一个是可选的尼?
比如现在参数a是比如传入进函数使用的,但是参数b不一定需要用到,那么前面添加问号表示可不传.

```typescript
function mount (a:number,b?:number):number{
    let c : number = a + b
    return c
}
```

那么这里b没有被传过来,会报错啊!两种解决方法

第一,顺着这个方向想,如果传过来就使用,没传过来就默认为0不久好了.

```typescript
function mount (a:number,b?:number):number{
    let c : number = a + (b || 0)
    return c
}
console.log(mount(100))  // 100
console.log(mount(100,50)) // 150
```

第二 就是把上述的思路简化一下,我直接在写函数的时候就给他一个默认值

```typescript
function mount (a:number,b:number = 0):number{
    let c : number = a + b
    return c
}
console.log(mount(100))
console.log(mount(100,50))
```

---

#### 对象

一个标准的ts的对象声明并复制如下:

```typescript
let employee : {
    id: number,
    name: string  // name?: string 使得name非必要声明的成员.
} = {id:1,name:"LYG"}
```

可以看到,对象名后面是冒号而不是等号,并且很多属性同数组一样,是可以被指定类型的.

可以在对象成员前添加 readonly 使得成员只可读.

```JavaScript
let employee : {
    readonly id: number,
    name: string 
} = {id:1,name:"LYG"}
```



##### 对象别名

按照上文的对象声明,这个对象是不可复用的. 如果需要复用的话需要抽象出来.
这个是由需要用到 type 关键字来修饰对象了.

```typescript
type Employee = {
    id:Number,
    name:String,
    educationalExperience: String[],
    retire:(date:Date)=>void // 函数返回值为空
}

let Employee_one:Employee = {
    id:1,
    name:'张三',
    educationalExperience:["实验中学","实验高中","实验大学"],
    retire:(date:Date)=>{
        console.log(date)
    }
}
```



##### 联合类型

变量可以是设定好的几种类型之一，传过来后再针对专门的判断来使用。

```typescript
console.log("hallo")

function sayWeigth (Weigth: number | string): number{
    if(typeof Weigth === "number"){
        // 这个域里 Weigth 拥有number类型的方法
        return Weigth * 2
    }else{
        // 这个域里 Weigth 拥有string类型的方法
        return parseInt(Weigth) * 3
    }
}

let int_10 = sayWeigth(10)
let str_10 = sayWeigth("10")
console.log(`当是数字10时返回${int_10} , 当是字符串10时返回${str_10}`)
```



##### 交叉类型

必须是类型相同的才有相交的意义，比如卡车和货车都是汽车类，他们相交之后得到的新型车辆，就能够拥有卡车和火车各自的有点。userVip中可以拥有user 和 vip 的两种对象的成员。

```typescript
type user = { name: string; age: number };
type vip = { privilege: string };

let userVip: user & vip = {
  name: "zhangsan",
  age: 20,
  privilege: "高人一等",
};

// test01 nerve
type test01 = 'b' & 'a'
```

或者说是两种功能不同的函数需要交叉到一起使用

```typescript
type drag = {
  dragIt: () => void;
};
type size = {
  sizeIt: () => void;
};

let size_And_drag: drag & size = {
  dragIt: () => {
    console.log("叭啦叭啦...");
  },
  sizeIt: () => {
    console.log("叭啦叭啦...");
  },
};
```



##### 字面类型

这个可以设定自定义的值，规定添加了设定的变量只能接受你设定的数值作为值

```typescript
type Specify_numeric_value = 50 | 100;
// vaule_one 如果不是50 或者 100 就会报错。
let vaule_one:Specify_numeric_value = 100;
```



---

#### 类型断言

有些时候有些对象的值是可以获取的，但是编译器会报错，这个时候使用类型断言，告诉编译器你比它要牛逼得多得多得多，编译器此时也就不拦着你去使用这个变量了。

语法 ：值 as 类型 或者<类型>值
在tsx中必须使用 前者

![ts002.png](https://s2.loli.net/2023/03/07/Atd6rSwPgyh2ZeQ.png)

![ts002.png](https://s2.loli.net/2023/03/07/Atd6rSwPgyh2ZeQ.png)

---



#### **Unknown**

在函数中将一个参数设定成 unknow ， 那么如果调用这个对象没有的方法时，就会报错。

如果该对象是属于自己创建的类型，不属于js中自带的类型，那么就需要用到instanceof缩短范围。

xxx（对象）     instanceof       xxx（类型）

```typescript
function render(document:unknown){
    // 通过断言来缩小范围,使用typeof 或者instanceof
    if(typeof document === 'string'){
        // document.map() 报string上不存在map属性 
        // 将所有内容大写
        return document.toLocaleLowerCase()
    }
}
```



TypeScript 3.0中引入的 unknown 类型也被认为是 top type ，但它更安全。与 any 一样，所有类型都可以分配给unknown。

```js
let uncertain: unknown = 'Hello'!;
uncertain = 12;
uncertain = { hello: () => 'Hello!' };
```

我们只能将 unknown 类型的变量赋值给 any 和 unknown。

```js
let uncertain: unknown = 'Hello'!;
let notSure: any = uncertain;
```


它确实在很多方面不同于 any 类型。如果不缩小类型，就无法对 unknown 类型执行任何操作。

```js
function getDog() {
 return '22'
}

const dog: unknown = getDog();
dog.hello(); //Object is of type 'unknown'
```



**使用类型断言缩小未知范围.**

上述机制具有很强的预防性，但对我们的限制过于有限。要对未知类型执行某些操作，首先需要使用类型断言来缩小范围。

```js
const getDogName = () => {
 let x: unknown;
 return x;
};

const dogName = getDogName();
console.log((dogName as string).toLowerCase()); 
```

在上面的代码中，我们强制TypeScript编译器相信我们知道自己在做什么。

以上的一个重要缺点是它只是一个假设。它没有运行时效果，也不能防止我们在不小心的情况下造成错误。 比如下面的代码, 他实际上是错误的, 但却可以通过 typescript 的检测.

```js
const number: unknown = 15;
(number as string).toLowerCase();
```

TypeScript编译器接收到我们的数字是一个字符串的假设，因此它并不反对这样处理它。


**使用类型收缩**

一种更类型安全的缩小未知类型的方法是使用 类型收缩 。TypeScript 编译器会分析我们的代码，并找出一个更窄的类型。

```js
const dogName = getDogName();
 if (typeof dogName === 'string') {

  console.log(dogName.toLowerCase());

}
```

在上面的代码中，我们在运行时检查了 dogName 变量的类型。因此，我们可以确保只在 dogName 是变量时调用 toLowerCase函数。

除了使用 typeof，我们还可以使用 instanceof 来缩小变量的类型。

```js
type getAnimal = () => unknown;

const dog = getAnimal();
 
if (dog instanceof Dog) {
 console.log(dog.name.toLowerCase());
}
```

在上面的代码中，我们确保只有在变量是某个原型的实例时才调用 dog.name.toLowerCase。

TypeScript编译器理解这一点，并假设类型

---

#### never

首先never一般作为所有类型的子集，它本身表示的就是一个空集嘛，当编译器不知道这个类型是什么的时候，显示的将会是never

说白了，never就是编译器不知道返回什么，但是它总得让你知道是个什么情况，所以就返回never。

```typescript
type A = string | number | boolean;

// 设置成 any 让编译器不知道是什么类型.
// 因为工作中获取到的数据你也不知道是什么类型
let a: A = "hallo" as any;
if (typeof a === "string") {
  a.toLocaleLowerCase();
} else if (typeof a === "number") {
  a.toPrecision();
} else if (typeof a === "boolean") {
  a.valueOf();
} else {
  console.log("此时a不属于上述三个任何一种,此时的a是never");
}
```



值会永不存在的两种情况：

1. 如果一个函数执行时抛出了**异常**，那么这个函数永远不存在返回值（因为抛出异常会直接中断程序运行，这使得程序运行不到返回值那一步，即具有不可达的终点，也就永不存在返回了）；
2. 函数中执行无限循环的代码（**死循环**），使得程序永远无法运行到函数返回值那一步，永不存在返回。

当抛出异常就代表这个程序中断了，这个时候函数返回的就是never。

当一个函数中有个死循环（无穷性），让剩下的代码不能达到执行，那么也可设定 never

```typescript
// 异常
function err(msg: string): never {
    throw new Error(msg);
} 

// 死循环
function loopForever(): never {
    while (true) {};
} 
```

---

### 面向对象 - TS

在ts中创建类，使用面向对象的风格编写js代码

```typescript
class Account {
  // 在类中定义变量不需要写前修饰符了
  id: number;
  owern: string;
  balance: number;
  // 构造方法不用指定函数返回值
  constructor(id: number, owern: string, balance: number) {
    this.id = id;
    this.owern = owern;
    this.balance = balance;
  }
  // 定义方法前面也不用加function了
  deposite(amount: number): void {
    if (amount < 0) {
      throw new Error("Invalid amount");
    }
    this.balance += amount;
  }
}
```

可以给设置的变量前面添加修饰

```typescript
  readonly id: number;  //表示只读，只能在构造器中修改它
  owern: string;
  balance？: number;  //加问号表示这个成员是可选的
```

和java一样，也是具有如下三个修饰符

```
private 	设置后只有当前类能够访问该变量/函数
public      所有对象都可以访问该变量及方法
proteacted  只有当前类和继承当前类的子类可以访问该变量、方法
```

提一嘴，如果使用private修饰符修饰了变量，该变量前最好加一个下划线使得代码可读性高。
同时 proteacted 一般用的比较少，推荐少用 proteacted。
那么同java一样，需要写一个get，set方法。

同样也可以使用 private 添加到方法前面，使得方法只在类的内部被使用。

```typescript
getVaule():xxx {
    return this._xxx
}
```

便捷的方法声明一个类中的各种变量。直接在构造函数的参数列表使用修饰符修饰，就默认给你初始化了。

```typescript
class Account {
  constructor(
    public id: number,
    public owern: string, 
    private _balance: number) {
  }
}
```

上述虽说可以使用get set方法来获取，但是有个更加便捷的方式。
私有变量前面加下划线就是为了这种方式的使用，因为直接方法前加上 get / set 关键字就行
同时还防止了方法名和变量名重名的报错。

```typescript
class Test {
  constructor(
    public id: number,
    public name: string,
    private _money: number,
    protected home: string[]
  ) {}

  get money(): number {
    return this._money;
  }
  set money(vaule) {
    if (vaule < 0) throw Error("输入的值无效");
    this._money = vaule;
  }
}

let tt = new Test(1, "lyg", 1000, ["上海新房", "北京老房"]);
console.log(tt.money);
tt.money = 2000;
console.log(tt.money);
```

---

#### 索引签名

索引签名支持两种类型，分别是string 和 number类型。

{ [index: string]: { message: string } }

 index 除了可读性外，并没有任何意义。
例如：如果有一个用户名，你可以使用 { username: string}: { message: string }，这有利于代码可读。

往大白话说，就是这么设定就是这个数组要么只能全是数字/字符串并且后续添加的类型也只能是数字/字符串

现在，我们要记录不同人名分别在一个球场的座位号是多少。在对象中一个个加是很蠢的。

```typescript
class SeatAssignment {
  [seatNumber: string]: string;
}
let seats = new SeatAssignment();
seats.A001 = "Mosh";
seats.A002 = "jack";
seats[3] = "dawei";
console.log(seats);
// 输出 SeatAssignment { '3': 'dawei', A001: 'Mosh', A002: 'jack' }
```

---

#### 继承 extends



```typescript
class person {
  constructor(public firstName: string, public lastName: string) {}

  get fullName() {
    return this.firstName + " " + this.lastName;
  }

  walk() {
    console.log("walking");
  }
}
// 只凸显学生的特有属性，父类该有的由super调用声明。
class Student extends person {
  constructor(public studentId: number, firstName: string, lastName: string) {
    super(firstName, lastName);
  }

  takeTest() {
    console.log("taking a test");
  }
}

let stuA = new Student(100, "AAA", "ZZZ");
stuA.walk();
stuA.takeTest();
```

同样，typescript 同 java 一样，具备子类继承父类后，能够在子类中重写父类的方法。但是要加override关键字注明这个方法正在被重写。

```typescript
class person {
  constructor(public firstName: string, public lastName: string) {}
  get fullName() {
    return this.firstName + " " + this.lastName;
  }
  walk() {
    console.log("walking");
  }
}

class Teacher extends person {
  constructor(public teacerId: number, firstName: string, lastName: string) {
    super(firstName, lastName);
  }
  // 重写父类方法。
  override get fullName(): string {
    return "Professor" + this.firstName + " " + this.lastName;
  }
}

```



#### 多态

> 父类的对象变量可以接受任何一个子类的对象
>  从而用这个父类的对象变量来调用子类中重写的方法而输出不同的结果.

**产生多态的条件:** 1.必须存在继承关系  2.必须有方法重写

**多态的好处:** 利于项目的扩展【从局部满足了 开闭原则--对修改关闭,对扩展开放】

**多态的局限性:** 无法直接调用子类独有方法，必须结合instanceof类型守卫来解决

```typescript
class Person {
  constructor(public firstName: string, public lastName: string) {}
  get fullName() {
    return this.firstName + " " + this.lastName;
  }
}

class Student extends Person {
  constructor(public studentId: number, firstName: string, lastName: string) {
    super(firstName, lastName);
  }
}

class Teacher extends Person {
  constructor(public teacerId: number, firstName: string, lastName: string) {
    super(firstName, lastName);
  }
  override get fullName() {
    return "Professor  " + super.fullName;
  }
}

printName([new Student(1, "AAA", "BBB"), new Teacher(2, "BB", "CC")]);

function printName(people: Person[]) {
  for (let person of people) {
    console.log(person.fullName);
  }
}
```



#### 抽象 abstract

抽象方法只能够出现在抽象类中，并且该抽象方法需要被实现。

```typescript
abstract class Shape {
  constructor(public color: string) {}
  abstract render(): void;
}

class Circle extends Shape {
  constructor(public radius: number, color: string) {
    super(color);
  }
  override render(): void {
    console.log("this is  a circle");
  }
}
```







