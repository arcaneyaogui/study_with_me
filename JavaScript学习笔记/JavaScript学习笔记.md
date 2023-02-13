# JavaScript

JavaScript 疑惑保留区域

1. 函数被`new` 关键字调用和普通调用有什么不同?
2. 函数中prototype属性的作用?来源?
3. 函数中call() apply()的这两个方法详解
4. 函数一章中的尾调用优化不是很理解
5. 对象的访问器属性





**重点掌握**

首先基础语法过一遍,掌握就好.

1. this 用法，相关原理
2. 原型/原型链
3. 闭包
4. 面向对象相关
5. 同步异步/回调/promise/async、await
6. 模块化 CommonJS, AMD



JavaScript中有一个严格模式 '"use strict"; 

可以写在整个函数的开头,让整个脚本都处于该模式下.

同样也可以单独下载某个函数中,让这个函数中的代码处于严格模式下.

严格模式具体的作用,请移步MDN网址观看

>https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode







## JavaScript 值传递

**_注意: JavaScript中只有值传递,没有引用传递._*



值传递(pass by value)：

在调用函数时，将实际参数复制一份传递到函数中，这样在函数中对参数进行修改，就不会影响到原来的实际参数；

引用传递(pass by reference):

在调用函数时，将实际参数的地址直接传递到函数中。这样在函数中对参数进行的修改，就会影响到实际参数；


## JavaScript简介

- JavaScript可以直接插入HTML文件中.
- **JavaScript是解释型语言,是一行一行的执行下去的.**
- **在HTML中必须使用 < script > 标签包含JavaScript代码.**
- JavaScript的三个组成部分
   - ECMAScript 描述了该语言的语法和基本对象.
   - 文档对象模型(DOM) 描述处理网页内容的方法和接口.
   - 浏览器对象模型(BOM) 描述与浏览器进行交互的方法和接口.



**简单数据类型与复杂数据类型的区分**

简单类型: 就是再存储临时变量中存储的值是自己本身

包括 string number boolean undefined null



复杂类型: 在存储变量时仅仅存储的是地址(引用),通过new关键字创建对象.

例如 Object Array Date Math Number String Boolean function  RegExp(正则表达式)



### 注释写法

~~~JavaScript
// 这是单行注释

/*
这是
多行
注释
*/
~~~



### a.语句



JavaScript的语句需要用到分号结尾.

~~~javascript
var box = 1 + 2;
~~~



多个语句可以写在一行之内

```JavaScript
var a = 1 + 2; var b = 'abc';
```



分号前面没有任何内容,JavaScript就会视为空语句.

~~~JavaScript
;;; //这就是三个空语句
~~~



表达式不需要分号结尾,一旦在表达式后面添加封号,JavaScript会视为语句,从而产生一些没有意义的语句.



### b.变量

JavaScript区分大小写, A 和 a 是两个给不同的变量.

```JavaScript
var a = 1;
var A = 2;
```



如果只是声明但是没有赋值,那么这个变量的值就是undefined.

~~~JavaScript
var a;
~~~



**undefined表示无意义**



赋值的时候也可以不写  var

~~~JavaScript
a = 1;
~~~

 

> 但是，不写`var`的做法，不利于表达意图，而且容易不知不觉地创建全局变量，所以建议总是使用`var`命令声明变量。



同时声明多个变量

~~~JavaScript
var a,b;
~~~



#### 【重点】

**JavaScript是一种动态类型语言,变量可以随时更改类型.**

```JavaScript
var a = 10;
a = 'hello';
```



**如果用var重新声明一个已近存在的值是无效的.**

**但是，第二次声明的时候进行了赋值，则会覆盖掉前面的值。**



 #### let变量声明



**使用let声明得变量,再作用域外不能被使用.**

```JavaScript
if (true) {
   var Name = 'Matt';
   // 输出 Matt
   console.log(Name);
}
// 同样输出Matt
console.log(Name);

// -- let声明区块变量

if (true) {
   let let_name = 'jeck';
   // 输出 jeck
   console.log(let_name);
}
// 未定义
console.log(let_name);

```



同意作用域中,let不能重复声明同一标识符

而var可以,但是不同作用域,但let在不同的作用域就可以声明同一标识符.

```JavaScript
// 在作用域中,var可以重复声明同一表示符
var Name = 'Tom2';
console.log(Name);

if (true) {
   var Name = 'Matt';
   // 输出 Matt
   console.log(Name);
}
// 同样输出Matt
console.log(Name);

// -- let声明区块变量

let let_name = 'Jery';
console.log(let_name);
// 报错,同一作用域,let不能重复声明同一标识符
// let let_name = 'Jery';

if (true) {
   let let_name = 'jeck';
   // 输出 jeck
   console.log(let_name);
}
// 输出Jery
console.log(let_name);

```



##### let声明变量不提升

```JavaScript
// 输出undefined,说明Name对象被创建.
console.log(Name);
var Name = 'Tom1';

// 报错,let_Name么有被创建
console.log(let_Name);
let let_Name = 'Jery1';
```



##### let搭配for实现遍历的好处

当for循环碰见setTimeout()函数的时候,你会发现,for循环是在`setTimeout()`函数之后运行的,这个时候使用`let` 和 使用 `var`声明变量最后输出结果是不一样的

`在使用var时最常见得问题是最迭代变量得奇特声明和修改`

```JavaScript
设置三秒后弹出一个弹窗
setTimeout("alert('对不起, 要你久候')", 3000 )
*/

for (let i = 0; i < 5; ++i) {
   // 用到了箭头函数
   setTimeout(() => console.log('let' + i), 0);
}
// 访问不到for循环括号里得 i 变量
// console.log(i);

for (var i = 0; i < 5; ++i) {
   // 用到箭头函数
   setTimeout(() => console.log('var' + i), 0);
}
// 访问不到for循环括号里得 i 变量
console.log('呵呵哒' + i);

/*
输出结果:

呵呵哒5  //console居然最先输出
 let0
 let1
 let2
 let3
 let4
 var5

*/
```





#### **var声明变量提升**

>JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。



解释解释,就是JavaScript在所有代码运行中,会首先进行变量的声明;



*比如我们有下面两个代码*

**a. 变量声明在语句下方**

~~~JavaScript
console.log(a);
var a = 10;
~~~

这个语句不会报错,因为由于变量提升,他的实际执行顺序如下

~~~JavaScript
var a;
console.log(a);
a = 10;
~~~

因为输出语句,在 a的赋值语句之前运行,所以我们控制台上不会显示出a的值.



**b.变量声明在语句上方**

~~~JavaScript
var a = 10;
console.log(a);
~~~

这中语句赋值在输出语句上方的代码,就能够在控制台打印出a的值.



#### const声明

C语言中也有const用来声明常量

JavaScript中const和let基本相同,既不允许同一作用域下重复声明

也是域内声明得话域外访问不到

有以下两点特点.

- **声明变量得时候必须初始化变量**
- 尝试修改const声明得变量会报错



const如果声明对象,是可以修改其属性的

```JavaScript
const person = {
   Name: 'Tom',
   age: 18
};
// 输出 Tom
console.log(person.Name);
person.Name = 'Jery';
// 输出Jery
console.log(person.Name);
```



**某种意义上来说,有了let 和 const,我们已经可以不使用var 来声明变量了.**



#### 标识符命名规则

- 第一个字符**必须**是任意字母(包括其他语言的字母),以及,美元符号($)和下划线( _ );
- 第二个字符出了任意字母,美元符号,下划线之外,还可以用数值0~9.



### c.区块

JavaScript使用大括号将许多相关的语句组合在一起,称为区块.

但是区块对 var 命令来说,JavaScript的区块不构成单独的作用域.

~~~JavaScript
{
   var a = 10;
}
// 我们在区块外依旧能够使用 a b
console.log(a);
~~~



### d.标签(跳转)

在语句前加标签,相当于定位,可以跳转到该语句.

~~~javascript
top:
	for(var i=0;i<10;i++){
        if((i-2)===0){
            // 当i=2时,直接跳出循环.
            break top;
        }
        console.log(i);
    }
~~~



**双层循环中使用标签**



**break**

下面代码为双重循环区块，`break`命令后面加上了`top`标签（注意，`top`不用加引号），满足条件时，直接跳出双层循环。如果`break`语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。



~~~JavaScript
top:
	for(var i = 0; i < 3; i++ ){
        for(var j = 0; j < 3; j++){
            if(i===1 && j===1) break top;
            console.log('i='+ i + ', j=' + j);
        }
    }

~~~





**continue**

continue 同样和 break 一样可以配合标签使用

continue后面有标签时,满足条件则可以直接跳过循环进行下一次**外循环**

continue后面没有标签的时候,则只能跳过此次循环,执行下一次**内循环**.



~~~JavaScript
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) continue top;
      console.log('i=' + i + ', j=' + j);
    }
  }
~~~



**使用标签跳出区块**

当使用break跳出区块时,并不是重新又从区块开始运行,而是**直接运行区块下面的代码**.



```JavaScript
foo: {
  console.log(1);
  break foo;
  console.log('本行不会输出');
}
console.log(2);
```





## 1. 数据类型



- 数值(number)
   - 整数 和 小数
- 字符串(string)
   - ' HOLLE WOURLD '
-  布尔值(Boolean)
   - true and  flase
- undefined
   - 表示 "未定义" 或者 "不存在";
- null : 表示空值
- 对象(object) : 各种值得组成集合



数值、字符串、布尔值这三种类型，合称为**原始类型**（primitive type）的值，即它们是最基本的数据类型，不能再细分了。

对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。

至于`undefined`和`null`，一般将它们看成两个特殊值。



### 1.1  确定值的类型



确定值的类型有三种方式,分别是两种运算符和一种方法



- typeof 运算符
- instanceof 运算符
- Object.prototype.toString 方法



#### 1.1.1 typeof

原始的数据类型分别返还他们的名称.

~~~javascript
typeof 123       // "number"
typeof '123'    // "string"
typeof false   // "boolean"
~~~



函数返回function

~~~JavaScript
function f() {}
typeof f
// "function"
~~~



返回undefined类型就时undefined

```JavaScript
typeof undefined
// "undefined"
```



typeof 返回 window {} [] 都是object;

这也就是说明在JavaScript中**空数组**的类型时object , JavaScript内部,数组的本质上只是一种特殊的对象.

~~~JavaScript
typeof window // "object"
typeof {} // "object"
typeof [] // "object"

~~~



`null`的类型是`object`，这是由于历史原因造成的。1995年的 JavaScript 语言第一版，只设计了五种数据类型（对象、整数、浮点数、字符串和布尔值），没考虑`null`，只把它当作`object`的一种特殊值。后来`null`独立出来，作为一种单独的数据类型，为了兼容以前的代码，`typeof null`返回`object`就没法改变了。

```javascript
typeof null // "object"
```



**typeof 通常用于判断**

**用于检查一个变量是否存在值**

~~~JavaScript
// 错误的写法
if (v) {
  // ...
}
// ReferenceError: v is not defined

// 正确的写法
if (typeof v === "undefined") {
  // ...
}
~~~


### 1.2 null and undefined

null 和 undefined 很相似,以下两个赋值语句写法产生的效果几乎等价.

~~~JavaScript
var a = null;

var b = undefined;
~~~



比如见如下代码, **null 和 undefined 都会自动转化成false**.

```JavaScript
var a = null;
var b = undefined;

if (!a) {
   console.log('undefined>>a is false');
}
/*
上面代码等价于此代码
if (!undefined) {
   console.log('undefined is false');
}
*/

if (!b) {
   console.log('null>>b is false');
}
/*
上面代码等价于此代码
if (!null) {
   console.log('null is false');
}
*/

```



但是为何会有这两个这么相似得值呢,根据文档得教学,是因为历史原因.



>1995年 JavaScript 诞生时，最初像 Java 一样，只设置了`null`表示"无"。根据 C 语言的传统，`null`可以自动转为`0`。
>
>```
>Number(null) // 0
>5 + null // 5
>```
>
>上面代码中，`null`转为数字时，自动变成0。
>
>但是，JavaScript 的设计者 Brendan Eich，觉得这样做还不够。首先，第一版的 JavaScript 里面，`null`就像在 Java 里一样，被当成一个对象，Brendan Eich 觉得表示“无”的值最好不是对象。其次，那时的 JavaScript 不包括错误处理机制，Brendan Eich 觉得，如果`null`自动转为0，很不容易发现错误。
>
>因此，他又设计了一个`undefined`。区别是这样的：`null`是一个表示“空”的对象，转为数值时为`0`；`undefined`是一个表示"此处无定义"的原始值，转为数值时为`NaN`。
>
>```
>Number(undefined) // NaN
>5 + undefined // NaN
>```
>
>

**做一个小小总结**

**关键就是 null转化数值是0 , undefined转化数值是NaN**

null正因为转化成数值是0 所以加一个数值他就是那个数值得本身,但是undefined加任何数值都是NaN.

>NaN 含义
>
>>*NaN*（Not a Number，非数）是计算机科学中数值数据类型的一类值，表示未定义或不可表示的值



#### 什么时候是undefined

*1. 变量声明未赋值*

```JavaScript
var i;  //此时 i 是 undefined
```



*2. 调用函数时,未提供该提供得参数*

调用函数时,未提供该提供得参数,此时该**参数**等于undefined

```JavaScript
var f = fun_name();
console.log(f);  // 输出 undefined

/*
函数被调用时,生成得形参,没有实际得值传入,这个生成得形参默认就会被赋值成undefined.
*/
function fun_name(g) {
   return g;
}
```



*3. 对象没有赋值属性*

~~~JavaScript
// 对象没有赋值的属性
var  o = new Object();
o.p // undefined
~~~



*4. 函数没有返回值,默认返回undefined*

```JavaScript
// 函数没有返回值时，默认返回 undefined
function f() {}
f() // undefined
```





### 1.3 布尔值

#### 1.3.1 逻辑运算符

- 前置逻辑运算符： `!` (Not)
- 相等运算符：`===`，`!==`，`==`，`!=`
- 比较运算符：`>`，`>=`，`<`，`<=`



#### 1.3.2 [自动转化false]



**以下的六个值,都会自动转化成false,**

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- `""`或`''`（空字符串）

见下面代码:

```JavaScript
if ('') {
  console.log('true');
}
// 没有任何输出
```



但是空数组,和空对象都是 true 

```JavaScript
if ([]) {
  console.log('true');
}
// true

if ({}) {
  console.log('true');
}
// true
```





### 1.4 整数和小数

JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，`1`与`1.0`是相同的，是同一个数。

```JavaScript
1 === 1.0  // true
```



- 第1位：符号位，`0`表示正数，`1`表示负数
- 第2位到第12位（共11位）：指数部分
- 第13位到第64位（共52位）：小数部分（即有效数字）



####  1.4.1 数值精度

JavaScript中一个数得指数不能超过52位

超过这个位数,再进行运算会出错,不准确.

~~~JavaScript
var number_a = null;
number_a = Math.pow(2, 53);
console.log(number_a); //9007199254740992

var number_b = null;
number_b = number_a + 1; //9007199254740992
/*
number_b = number_a + 2; //9007199254740994

number_b = number_a + 3; //9007199254740996
*/

console.log(number_b);
~~~



 #### 1.4.2 数值范围

因为64位的浮点指数部分长度是11的二进制位,所以做大表示数的值是2的2047次方(2的11次方减一),然后一半用来表示负数.

2<sup>1024</sup> ~ 2<sup>-1023</sup> (开区间) 就是JavaScript表示数的大小

当大于或者等于最大值的收,会返回 Infinity
当小于或者等于最小值的时候会返回 0

```JavaScript
var number_a, number_b;

number_a = Math.pow(2, 1024) // Infinity
console.log(number_a)

number_b = Math.pow(2, -1075) // 0
console.log(number_b)
```



看看如下代码

 `0.5`连续做25次平方，由于最后结果太接近0，超出了可表示的范围，JavaScript 就直接将其转为0。

~~~JavaScript
var x = 0.5;

for(var i = 0; i < 25; i++) {
  x = x * x;
}

x // 0
~~~



#### 1.4.3 数值表示



**JavaScript 内部会自动将八进制、十六进制、二进制转为十进制**

- 十进制：没有前导0的数值。
- 八进制：有前缀`0o`或`0O`的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。
- 十六进制：有前缀`0x`或`0X`的数值。
- 二进制：有前缀`0b`或`0B`的数值。





**JavaScript自动将数值用科学计数法表示的两种情况**

1.  小数点前的数字多于 21 位
2. 小数点后的 0 多余五个



#### 1.4.4 特殊值

##### 正负 0

**0%任何数 都会 等于 0**



JavaScript有一位被当作符号位,也就是任何一个数都会有一个对应的负值,几乎所有情况 +0 和 -0 都会被当作是等价的,但是当这两个 0 作为分母的时候,返回值是不相同的

~~~
(1 / +0) === (1 / -0) // false
~~~

上面的代码之所以出现这样结果，是因为除以正零得到`+Infinity`，除以负零得到`-Infinity`，这两者是不相等的



##### NaN

0 除以 0 会得到 NaN

```
0 / 0       //NaN
```



将字符串解析成数字的时候会出现NaN

```
5 - 'x'      // NaN
```





需要注意的是，`NaN`不是独立的数据类型，而是一个特殊数值，它的数据类型依然属于`Number`，使用`typeof`运算符可以看得很清楚。

```
typeof NaN           // 'number'
```





**NaN不等于任何值,包括它本身**

```
NaN === NaN // false
```



**NaN当作布尔值使用时是false**

```
Boolean(NaN) // false
```



**NaN与任何值进行运算,得到的结果都是NaN**

~~~
NaN + 32 // NaN
NaN - 32 // NaN
NaN * 32 // NaN
NaN / 32 // NaN
~~~





##### Infinity 【重点】

**Infinity一般用来表示两个场景.**

1. 一个正值太大或者一个负值太小
2. 非0数值 除以 0

```
// 场景一
Math.pow(2, 1024)
// Infinity

// 场景二
0 / 0 // NaN
1 / 0 // Infinity
```





**Infinity有正负之分**

正 Infinity 和 -Infinity 是不等价的

```JavaScript
Infinity === -Infinity // false
```



`Infinity`大于一切数值（除了`NaN`），

`-Infinity`小于一切数值（除了`NaN`）。



**Infinity 表示正无穷, -Infinity表示负无穷.**

那么什么时候得到正负的 Infinity

- 非 0 的正数除以 -0 得到负无穷.
- 负数 除以 -0 得到 正无穷.



符号 和 0 相同的数,那么得到的就是Infinity , 如果这个数和 0 的符号相反,得到的数就是 -Infinity . 

```JavaScript
// Infinity
console.log(1 / 0);

// -Infinity
console.log(-1 / 0);

// -Infinity
console.log(1 / -0);

// Infinity
console.log(-1 / -0);
```





**Infinity 的运算规则**

Infinity 和 其他一般数值数运算符合计算规则

~~~JavaScript
5 * Infinity 		// Infinity
5 - Infinity 		// -Infinity
Infinity / 5 		// Infinity
5 / Infinity 		// 0
~~~



0乘以`Infinity`，返回`NaN`；

0除以`Infinity`，返回`0`；

`Infinity`除以0，返回`Infinity`

```JavaScript
0 * Infinity 		// NaN
0 / Infinity 		// 0
Infinity / 0 		// Infinity
```





**`Infinity`加上 或 乘以`Infinity`，返回的还是`Infinity`。**

```javascript
Infinity + Infinity 	// Infinity
Infinity * Infinity 	// Infinity
```



**`Infinity`减去或除以`Infinity`，得到`NaN`。**

```JavaScript
Infinity - Infinity 	// NaN
Infinity / Infinity 	// NaN
```



**`Infinity`与`null`计算时，`null`会转成0，等同于与`0`的计算。**

```JavaScript
null * Infinity 	// NaN
null / Infinity	 	// 0
Infinity / null 	// Infinity
```



**`Infinity`与`undefined`计算，返回的都是`NaN`。**

```JavaScript
undefined + Infinity // NaN
undefined - Infinity // NaN
undefined * Infinity // NaN
undefined / Infinity // NaN
Infinity / undefined // NaN
```



### 1.5  parselnt（）

语法

```JavaScript
parseInt(string, radix);
/*
string 必须填写得值,要被解析成数字得字符串

radix 表示要解析数字得基数,该值介于2-36之间.
如果该值超过36或者小于2,那么返回的值就是 NaN
*/
```





parseInt方法，用于将字符串转化成整数

```JavaScript
var a = null;
// 将字符串转为数字
a = parseInt('110');  // 110
console.log(a);

//当有空格,空格会被自动剔除
a = parseInt('       330');
console.log(a);

// 遇到不能转为数字的符号停止转化
// 直接返回已近转化好的数字
a = parseInt('1.10');  // 1
console.log(a);
a = parseInt('2*10');  // 2
console.log(a);

//除非这个符号是 + - 号后面跟着数字
a = parseInt('+110');
console.log(a);
a = parseInt('-110');
console.log(a);

//单纯的正负号依旧是返回NaN
a = parseInt('+');
console.log(a);
a = parseInt('-');
console.log(a);

// 如果是0x开头,则会按照16进制解析
a = parseInt('0x10') // 16
console.log(a);

// 如果是 0 开头 则按照 10进制解析
a = parseInt('0016') // 16
console.log(a);
```



特殊情况,因为有些数字再特定情况下自动转为科学技术法.

1.  小数点前的数字多于 21 位
2. 小数点后的 0 多余五个

像这种情况,会**按照科学技术法的写法**来读取数字

```JavaScript
parseInt(1000000000000000000000.5) // 1
// 等同于
parseInt('1e+21') // 1

parseInt(0.0000008) // 8
// 等同于
parseInt('8e-7') // 8
```



**parseInt 方法的进制属性**

我们可以在这个字符串后面设定这个数值按照何种进制输出.

```JavaScript
parseInt('1000', 2)    //把读取的数按照2进制输出 >> 8
```

同理,16进制,8进制都可以

```JavaScript
parseInt('1000', 6) // 216
parseInt('1000', 8) // 512
```





### 1.6 parseFloat()

parse: 解析   float: 浮点,浮动

对比上方得parseInt()方法,我们基本就能够知道这个方法是针对将字符串解析成浮点型.

```JavaScript
parseFloat('3.14')    //3.14
```



parseFloat() 这方法和parseInt()这方法不一样,它会对科学计数法进行正常的解析.

```JavaScript
parseFloat('314e-2') // 3.14
parseFloat('0.0314E+2') // 3.14
```



同样,如果字符串中有着不能够解析成浮点类型得字符串,那么这个函数就会停止解析,并且返回已近解析好的函数.

```JavaScript
parseFloat('3.14aaabbb') // 3.14
```



同样,parseFloat会自动过滤掉前方的空格

```JavaScript
parseFloat('\t\v\r  12.34\n ')   // 12.34
```



遇见第一个不能转化得字符,就直接返回NaN,有个特殊的可以看看,就是parseFloat会将空字符串转为NaN

```javascript
parseFloat([]) // NaN
parseFloat('FF2') // NaN
parseFloat('') // NaN
```





### 1.7 isNaN()

isNaN() 用来判断一个值是否是NaN,如果是就返回true,如果不是就返回false

```JavaScript
var a = 10;
var b = 10;
var c = 'hahaha';
var d = NaN;

// 判断数值 -- false
console.log(isNaN(a));
//判断表达式 -- false
console.log(isNaN(b - a));
// NaN和任何数运算都是NaN
console.log(isNaN(a + d));
//只要是字符串都会转成数值NaN,然后判断陈NaN
console.log(isNaN(c));
```



isNaN()方法因为字符串都会转化成数值NaN,这种情况面对数组和对象同理.

```JavaScript
isNaN({}) // true
// 等同于
isNaN(Number({})) // true

isNaN(['xzy']) // true
// 等同于
isNaN(Number(['xzy'])) // true
```



但是对于空数组或者只有一个数值成员的数组,isNaN返回的是false.

```JavaScript
isNaN([]) // false
isNaN([123]) // false
isNaN(['123']) // false
```



所以使用isNaN()方法的时候,最好像判断以下类型

```JavaScript
function myIsNaN(value) {
  return typeof value === 'number' && isNaN(value);
}
```



判断是不是NaN最可靠的值就是利用NaN不等同于自身这一点

```JavaScript
function myIsNaN(value) {
  return value !== value;
}
```



### 1.8 Symbol类型

#### a.symbol简介



`Symbol()`是原始函数,所以typeof返回结果依旧是 Symbol

```JavaScript
let sym = Symbol();
// 返回 symbol 
console.log(typeof (sym));
```



symbol()类型,相当于独自的id一样,每一个symbol类型都不会相等

```JavaScript
let sym1 = Symbol();
let sym2 = Symbol();

// 两个都是false
console.log(sym1 === sym2);
console.log(sym1 == sym2);
```



声明`symbo类型的时候,可以传入一个参数作为对符号的描述.但是这个字符串和定义标识符而安全无关,具体看如下代码

```JavaScript
let sym1 = Symbol('foo');
let sym2 = Symbol('foo');

// 两个都是false
console.log(sym1 === sym2);
console.log(sym1 == sym2);
```



#### b.symbol.for()

原理:

如果运行时的不同部分需要共享和重用符号实例，那么可以用一个字符串作为键，在全局符号注册表中创建并重用符号。

为此，需要使用Symbol.for()方法:

Symbol.for()对每个字符串键都执行幂等操作。第一次使用某个字符串调用时，它会检查全局运行时注册表，发现不存在对应的符号，于是就会生成一个新符号实例并添加到注册表中。后续使用相同字符串的调用同样会检查注册表，发现存在与该字符串对应的符号，然后就会返回该符号实例。



```JavaScript
/*
symbol本来不会相等
但是有需求用到时,想要他相等的时候
可以使用symbol.for()
*/


let sym1 = Symbol.for('foo');
let sym2 = Symbol.for('foo');

// 两个都是symbol类型
console.log(typeof (sym1));
console.log(typeof (sym2));

// true
console.log(sym1 === sym2);

// true
console.log(sym1 == sym2);
```





#### c . Symbol.keyFor()

用来查询**全局注册表** , 这个方法接收符号,返回全局符号对应的字符串键.

**如果查询的不是全局符号,则返回undefined**

```JavaScript

let sym1 = Symbol.for();
let sym2 = Symbol.for('foo');
let sym3 = Symbol('bar');

// undefined
console.log(Symbol.keyFor(sym1));
// undefined
console.log(Symbol.keyFor(sym2));
// undefined
console.log(Symbol.keyFor(sym3));
```



**如果`Symbol.keyFor()`中,传入的不是字符串,则会抛出TypeError错误**



## 2. 字符串

### 2.1 字符串多行显示



字符串太长,可以进行多行书写,需要用到反斜杠配合.

**注意，反斜杠的后面必须是换行符，而不能有其他字符（比如空格），否则会报错。**

注意这个反斜杠后面的回车符号还只能是一个,否则也会报错.

说明白点就是反斜杠后面只能且必须有一个回车符号.

```JavaScript
var longString = 'Long \
long \
long \
string';
```





或者使用链接符号( + )来多行输出

```JavaScript
var longString = 'Long '
  + 'long '
  + 'long '
  + 'string';
```



### 2.2   转义



下列字符都需要用到转义字符.

- `\0` ：null（`\u0000`）
- `\b` ：后退键（`\u0008`）
- `\f` ：换页符（`\u000C`）
- `\n` ：换行符（`\u000A`）
- `\r` ：回车键（`\u000D`）
- `\t` ：制表符（`\u0009`）
- `\v` ：垂直制表符（`\u000B`）
- `\'` ：单引号（`\u0027`）
- `\"` ：双引号（`\u0022`）
- `\\` ：反斜杠（`\u005C`）





反斜杠还有三种特殊用法。

（1）`\HHH`

反斜杠后面紧跟三个八进制数（`000`到`377`），代表一个字符。`HHH`对应该字符的 Unicode 码点，比如`\251`表示版权符号。显然，这种方法只能输出256种字符。

（2）`\xHH`

`\x`后面紧跟两个十六进制数（`00`到`FF`），代表一个字符。`HH`对应该字符的 Unicode 码点，比如`\xA9`表示版权符号。这种方法也只能输出256种字符。

（3）`\uXXXX`

`\u`后面紧跟四个十六进制数（`0000`到`FFFF`），代表一个字符。`XXXX`对应该字符的 Unicode 码点，比如`\u00A9`表示版权符号。





如果在正常的字符前面使用反斜杠,这个反斜杠则会被忽略.



### 2.3 字符串与数组

字符串某种意义上来说就可以被当作字符数组.

也就是说在JavaScript中,你可以用数组下面来使用字符串中的字符.

```JavaScript
var str = 'helloworld';
console.log(str[5]);
console.log('helloworld'[5]);
```

如果使用的下标超过字符串长度,则返回undefined.



### 2.4 length属性

```JavaScript
var str = 'helloworld';

// 输出字符串长度,有几个字母就有多长.
console.log(str.length);
```



### 2.5 字符集

JavaScript 内部使用的是 unicode字符集, 可以类比ASCII表 , 就是各种字符的另一种形式的写法.

举例几个Unicode形式的字符

```JavaScript
// 字母 O
console.log('\u006F泡果奶,我要\u006F泡,我要\u006F泡');
// 结果: o泡果奶,我要o泡,我要o泡
```



除了这样书写,还可以用来命名.

```JavaScript
var f\u006F\u006Ft = 'foot是脚的意思.';
```



放心,JavaScript会自动识别Unicode形式和字面形式,不管何种形式,最后输出都是以字面形式输出的.



### 【重点】

>UTF-16 有两种长度：
>
>对于码点在`U+0000`到`U+FFFF`之间的字符，长度为16位（即2个字节）
>
>对于码点在`U+10000`到`U+10FFFF`之间的字符，长度为32位（即4个字节）,而且前两个字节在`0xD800`到`0xDBFF`之间，后两个字节在`0xDC00`到`0xDFFF`之间。
>
>JavaScript 对 UTF-16 的支持是不完整的，由于历史原因，只支持两字节的字符，不支持四字节的字符。这是因为 JavaScript 第一版发布的时候，Unicode 的码点只编到`U+FFFF`，因此两字节足够表示了。后来，Unicode 纳入的字符越来越多，出现了四字节的编码。但是，JavaScript 的标准此时已经定型了，统一将字符长度限制在两字节，导致无法识别四字节的字符。上一节的那个四字节字符`𝌆`，浏览器会正确识别这是一个字符，但是 JavaScript 无法识别，会认为这是两个字符。
>
>```
>'𝌆'.length // 2
>```
>
>上面代码中，JavaScript 认为`𝌆`的长度为2，而不是1。
>
>总结一下，对于码点在`U+10000`到`U+10FFFF`之间的字符，JavaScript 总是认为它们是两个字符（`length`属性为2）。所以处理的时候，必须把这一点考虑在内，也就是说，JavaScript 返回的字符串长度可能是不正确的。

我觉得我看不太明白具体的原理,但是我好像清楚就是对于拥有四字节的字符的字符串,返回值不一定准确.



### 2.6 Base转码

比如ASCII中0-31的符号无法打印,就可以用到Base转码,或者以文本格式传递二进制数据.

>所谓 Base64 就是一种编码方法，可以将任意值转成 0～9、A～Z、a-z、`+`和`/`这64个字符组成的可打印字符。使用它的主要目的，不是为了加密，而是为了不出现特殊字符，简化程序的处理。



JavaScript 原生提供两个 Base64 相关的方法。

- `btoa()`：任意值转为 Base64 编码
- `atob()`：Base64 编码转为原来的值

使用Base转码如下

```JavaScript
var str_1 = 'hello world!!!';
// 把str_1转化成Base编码格式
var str_1_ma = btoa(str_1);

// str_1对应的编码格式
//  aGVsbG8gd29ybGQhISE=
console.log(str_1_ma);

var str_1_wen = atob('aGVsbG8gd29ybGQhISE=');
// 输出了 hello world!!!
console.log(str_1_wen);
```



如果转码内容不是ASCII码表中的内容(比如中文),那么得先转码.

1. 先将encodeURIComponent()方法把中文文本进行 URI 编码
2. 然后用btoa()方法将URI编码转化成Base64编码
3. 用atob()方法转回原来得 URI 编码
4. 然后用 decodeURIComponent() 对 encodeURIComponent()得 URI 的编码进行解码



- encodeURIComponent( uri )
   - 可以把字符串作为 URI 组件进行编码
   - 该方法不会对ASCII字母和数字进行编码,也不会对ASCII得标点符号进行编码.
- decodeURIComponent (URIstring)
   - 用于对 URI 码进行解析(还原)





~~~JavaScript
function b64Encode(str) {
   return btoa(encodeURIComponent(str));
}

function b64Decode(str) {
   return decodeURIComponent(atob(str));
}

var a = b64Encode('你真的傻')
console.log(a);
var a = b64Decode('JUU0JUJEJUEwJUU3JTlDJTlGJUU3JTlBJTg0JUU1JTgyJUJC')
console.log(a);
~~~



### 2.7 操作字符串方法

#### 2.7.1  concat()方法

*将一个或多个字符拼接成一个新字符串.*

```JavaScript
let str_one = "hello";
let result = str_one.concat("world");
// helloworld
console.log(result);
// hello
console.log(str_one);
```



从上面可知,并不会对原字符串`str_one`有什么影响.

我们还可以多个字符串连续拼接,但是多数情况下,使用`+`号更加便捷.

```JavaScript
let str_one = "hello";
let result = str_one.concat("world", ",", '我是刘英俊');
// helloworld
console.log(result);
// hello
console.log(str_one);

```





#### 2.7.2 提取字符串

提供了三个提取字符串的方法.

slice() , substr() , substring()

传入的参数是正数,这三个返回的结果没啥区别,直接去第三个字符串的前面部分.

```JavaScript
let str = "helloworld!!!";

// 下面三个都是 oworld!!!
// 说明字符串中第一个字母算 0
console.log(str.slice(4));
console.log(str.substr(4));
console.log(str.substring(4));
```



如果都传入 0 ,最后结果都是将字符串整个输出.

```JavaScript
let str = "helloworld!!!";

// helloworld!!!
console.log(str.slice(0));
console.log(str.substr(0));
console.log(str.substring(0));
```





**当参数是负数的时候比较不一样**

`slice()` 第一个参数为负的时候,是将总长度加上这个负数

```JavaScript
let str = "helloworld!!!";
// 13
console.log(str.length);
// 13+(-5)=8,从0开始数到第八个开始截取
// ld!!!
console.log(str.slice(-5));

//从第五位截取到第八位
console.log(str.slice(5, -5));
```



substr()方法将第一个负参数值当成字符串长度加上该值，将第二个负参数值转换为0

```JavaScript
// 说白了就是第一个参数和slice()一样,长度加这个负数
// 但是当第一个参数为负数,第二个只要不为正整数,都转成0

let str = "helloworld!!!";
// 13
console.log(str.length);

// 空的 什么都不输出
console.log(str.substr(-5, -2));
// 空的 什么都不输出
console.log(str.substr(-5, 0));

// 从第八个字符开始截取两个字符
console.log(str.substr(-5, 2));
```





`substring()`这个方法就比较极端,将所有负数都转化成0

```JavaScript
let str = "helloworld!!!";
// 13
console.log(str.length);

// 都是从0 截取 到第五位之前
console.log(str.substring(0, 5));
console.log(str.substring(-5, 5));

// 空的 啥都不输出
console.log(str.substring(0, -5));

/* 
等价于
str.substring(5, 0)
等价于
str.substring(5)
*/
console.log(str.substring(5, -5));

```



#### 2.7.3 字符串位置

indexOf() 和 lastindexOf()

**前者默认是从开头搜索字符串,后者默认是从结尾搜索**

*如果找到就立即返回位置不再寻找*
*如果没有找到就返回`-1`*

```JavaScript
let str = "helloworld";
// 4
console.log(str.indexOf("o"));
// 6
console.log(str.lastIndexOf("o"));
```



第二个参数就是自己设置找字符串的七点从哪里开始

```JavaScript
let str = "helloworld";
// 6
console.log(str.indexOf("o", 5));
// 4
console.log(str.lastIndexOf("o", 5));
```





#### 2.7.4 字符串包含方法

以下三个方法用来判断一个字符串中是否包含其他方法.

```JavaScript
// startsWith()检查开始于索引0的匹配项
startsWith()

// endsWith()检查开始于索引(string.length - substring.length)的匹配项
// 说白了就是看结尾处字符串是不是和你要找的字符串一样
endsWith() 

//检查整个字符串
includes()
```



startsWith()

```JavaScript
let str = "animalbeartigerlionsnake";
// 从两个字符串的开头进行匹配
console.log(str.startsWith("bear"));  // false
console.log(str.startsWith("animal")); //true

/* 提供参数 自己设定查找位置 */
// 从提供位置的地方向字符串后面查找
console.log(str.startsWith("bear",6));  // true
```



endsWith() 

```JavaScript
let str = "animalbeartigerlionsnake";
// 匹配结尾最后一点和参数相不相同
console.log(str.endsWith("snake")); //true
console.log(str.endsWith("nak"));   //false

/* 提供参数 自己设定查找位置 */
// 把提供的参数当作字符串尾部
console.log(str.endsWith("snake", str.length - 5)); //false
console.log(str.endsWith("lion", str.length - 5));   //true
```



includes()

```JavaScript
let str = "animalbeartigerlionsnake";
// 对字符串整个进行查找
console.log(str.endsWith("tiger")); //true
console.log(str.endsWith("squirrel"));   //false

/* 提供参数 自己设定查找位置 */
// 从提供位置的地方向字符串后面查找
console.log(str.endsWith("tiger",5)); //true

```



#### 2.7.5 trim()方法

作用

```
这个方法会创建字符串的一个副本，删除前、后所有空格符，再返回结果
```



```JavaScript
let str = "    animal bear tiger lion  snake      ";
console.log(str);
let aaa = str.trim();
// 只能删除双引号距离字符串中间的空格,字符串内本身的空格不能删除.
console.log(aaa);

```





- trimLeft()
   - 清理字符串和左边双引号中间的空格
- trimRight()
   - 清理字符串和右边双引号之间的空格





#### 2.7.6 repeat()方法

将这个字符串重复多遍(具体多少遍由你来决定),然后拼接.

```JavaScript
let str = " very ";
// I am  very  very  very    pretty
console.log("I am " + str.repeat(3) + "   pretty");
```





#### 2.7.7 复制字符串



`padStart()` 

```JavaScript
let str = "helloworld";

// 指定长度小于要复制的字符串长度
// 就会无视指定长度,直接复制整个字符串
// 输出 helloworld
console.log(str.padStart(5));

// 指定长度大于字符串长度
// 那么就在开头默认填充空格
// 输出                helloworld 
console.log(str.padStart(35));


/* 可以指定填充符号 */
//**********helloworld
console.log(str.padStart(20),"*");
```



`padEnd()`

```JavaScript
let str = "helloworld";

// 指定长度小于要复制的字符串长度
// 就会无视指定长度,直接复制整个字符串
// 输出 helloworld
console.log(str.padEnd(5));

// 指定长度大于字符串长度
// 那么就在结尾默认填充空格
// 输出helloworld                 
console.log(str.padEnd(35));


/* 可以指定填充符号 */
// helloworld**********
console.log(str.padEnd(20, "*"));
```



#### 2.7.8 字符串大小写

包括4个方法：

toLowerCase()、toLocaleLowerCase()、toUpperCase()和toLocaleUpperCase()。

toLowerCase() 和 toUpperCase()方法是原来就有的方法，与java.lang.String中的方法同名。

toLocaleLowerCase()和toLocaleUpperCase()方法旨在基于特定地区实现。

在很多地区，地区特定的方法与通用的方法是一样的。但在少数语言中（如土耳其语）,Unicode大小写转换需应用特殊规则，要使用地区特定的方法才能实现正确转换

通常，如果不知道代码涉及什么语言，则最好使用地区特定的转换方法



```JavaScript
let message = "aBc";
// abc
console.log(message.toLowerCase());
// abc
console.log(message.toLocaleLowerCase());

// ABC
console.log(message.toUpperCase());
// ABC
console.log(message.toLocaleUpperCase());
```







## 3. 对象

### 3.1 对象语法



我觉得对象有点点像C语言的结构体.

对象的创建:

成员(**键值**)之间逗号隔开,最后结尾不用逗号.

**所有成员名(也就是键名)书写时尽量符合标识符命名规则.**
如果不符合,比如 `11a` ,那么久必须用单引号包括起来才不会报错

```JavaScript
var this_is_me = {
    weight: 168.00,
    height: 166.00,
    name: '中国第一丑男',
    salary: 0,
    '11a':10
}
```



所有的键名都是字符串,哪怕你写数值都会转化成字符串.

每一个键值除了时单纯的值之外,还可以是函数

```JavaScript
var obj = {
  p: function (x) {
    return 2 * x;
  }
};

obj.p(1) // 2
```



**除了是函数外,还可以是另一个对象,这样就形成了链式引用**

```JavaScript
var obj_1 = {
};
var obj_2 = {
   bar: 'hello',
   p: 100
};

// 动态创建属性,不必再对象中声明
obj_1.foo_1 = obj_2;
// 输出指向的对象成员 {bar: "hello", p: 100}
console.log(obj_1.foo_1);

obj_1.foo_2 = obj_2.bar;
// 输出指向的obj_2中bar的值 hello
console.log(obj_1.foo_2);
```



### 3.2 对象的引用

看下面代码,可以了解到如下知识点.

- 不同变量名指向同一个对象,其中任何一个变量名修改对象成员的值,另一个对象都会被影响.
- 不同比变量名指向同一对象,其中一个取消对原对象的引用,不会影响到另一对象对原对象的引用.

```JavaScript
var obj_1 = {
   name: 'helloworld',
   age: 18,
};
var obj_2 = {
};

// {name: "helloworld", age: 18}
console.log(obj_1);
// {}
console.log(obj_2);

// 我们将obj_2指向obj_1
obj_2 = obj_1;

// {name: "helloworld", age: 18}
console.log(obj_1);
// {name: "helloworld", age: 18}
console.log(obj_2);
/*--------------分割线--------------*/
/* 
obj_1和obj_2都指向同意地址,这时任何一个对象修改其值,
都会影响到另一个对象.
*/
obj_1.age = 20;
// 输出 20
console.log(obj_2.age);

/*
   此时,取消一个变量对原对象的引用
   则不会影响到另一个值
 */

var obj_3 = {};
obj_1 = obj_3;
// {}
console.log(obj_1);
// {name: "helloworld", age: 18}
console.log(obj_2);
```



### 3.3  JavaScript区分对象的表达式和语句

比如有下面代码

```JavaScript
{foo : 233}
```

那么JavaScript如何知道这是一个带有大括号的语句还是对象的表达式呢?

所以**JavaScript中像这种情况,它会一律视为带有代码块语句**.

有时候我们想这么写,又想被JavaScript识别成对象的表达式,那我们怎么办?

我们想到一个 `()` ,原因很简单,**小括号中只能是表达式**.

```JavaScript
({foo: 233})  //正确
```



### 3.4 属性的读取

- 对象键名引用的两种方法
- 数值键名不能用小数点引用
- 符合标识符规范的键名,用方括号引用的时候需要加单引号,否则会被视为变量名使用.

```javascript
var hehe = 'bar';

var obg = {
   111: 100,
   0.7: 700,
   hehe: 10,
   bar: 20,
}

// 引用既可以用小数点也可以用方括号
console.log(obg.hehe);  //10 
console.log(obg[111]);  //100

/* 
符合标识符的键名,用方括号时,需要打单引号
否则将会被视为变量来使用
*/
console.log(obg[hehe]);       // 20
console.log(obg['hehe']);      // 10

/*
数值的键名使用方括号的时候可以不打单引号
但是数值的键名不能使用小数点引用
原因是数值会自动转化成字符串
 */

// console.log(obg.111);  >>>  报错
console.log(obg[111]);      // 10
```



**使用小数点和方括号运算符,不仅仅可以用来读取数值,还可以用来赋值**

```JavaScript
var hehe = 'bar';

var obg = {
   111: 100,
   0.7: 700,
   hehe: 10,
   bar: 20,
}
// {111: 100, 0.7: 700, hehe: 10, bar: 20}
console.log(obg);

obg.foo1 = 'hello';
// {111: 100, 0.7: 700, hehe: 10, bar: 20, foo1: "hello"}
console.log(obg);


obg['foo2'] = 'world';
// {111: 100, 0.7: 700, hehe: 10, bar: 20, foo1: "hello", foo2: "world"}
console.log(obg);
```



### 3.5 属性的操作



#### 数据属性



**属性默认的四个值如下**

❑ Configurable：表示属性是否可以通过delete删除并重新定义，是否可以修改它的特性，以及是否可以把它改为访问器属性。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。

❑ Enumerable：表示属性是否可以通过for-in循环返回。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。

❑ Writable：表示属性的值是否可以被修改。默认情况下，所有直接定义在对象上的属性的这个特性都是true，如前面的例子所示。

❑ Value：包含属性实际的值。这就是前面提到的那个读取和写入属性值的位置。这个特性的默认值为undefined。



比如我们将一个对象的属性的值设置成不可修改,

我们现在创建一个object对象
就拿里面的name举例,在没有复制的时候,name这个属性的Value是默认的undefined,
但是当我们将那么赋值 "liuyaogui" 之后,这个Value的值就是"liuyaogui"为不是undefined

```JavaScript
let person = {
   name: "liuyaogui",
   age: 21,
   sex:"男"
}
```



比如我们现在修改姓名这个属性的值

```JavaScript
let person = {
   name: "liuyaogui",
   age: 21,
   sex: "男"
}
// liuyaogui
console.log(person.name);

person.name = "liuyingjun";
// liuyingjun
console.log(person.name);

```



就是因为对象属性的`Writable`值默认是true,所以可以被修改.
那么我们如何修改对象属性的值呢来达到一些效果呢?

修改属性的值必须要用到 `Object.defineProperty()`方法

```JavaScript
let person = {
   name: "liuyaogui",
   age: 21,
   sex: "男"
}
// liuyaogui
console.log(person.name);

person.name = "liuyingjun";
// liuyingjun
console.log(person.name);


Object.defineProperty(person, "sex", {
   writable: false,
   value: "男"
});

person.sex = "女";
// 输出 男,并没有别改成女
console.log(person.sex);

```



**但是在严格属性下,操作writable的值,回报错.**

```JavaScript
"use strict";
```



同样,更改其他属性的默认值
比如Configurable改成false,就不能够在非严格模式下受用delete命令删除.

#### 访问器属性

访问器属性同样有四个特征描述

❑ [[Configurable]]：表示属性是否可以通过delete删除并重新定义，是否可以修改它的特性，以及是否可以把它改为数据属性。默认情况下，所有直接定义在对象上的属性的这个特性都是true。

❑ [[Enumerable]]：表示属性是否可以通过for-in循环返回。默认情况下，所有直接定义在对象上的属性的这个特性都是true。

❑ [[Get]]：获取函数，在读取属性时调用。默认值为undefined。

❑ [[Set]]：设置函数，在写入属性时调用。默认值为undefined。



**这是访问器属性的典型使用场景，即设置一个属性值会导致一些其他变化发生。**
下面的`defineProperty`方法中的参数并没有使用`year_ `
但是set()函数最终缺还是改变了`year_`的值,

```JavaScript
let book = {
   // year_ 后面的下划线一般表示不希望被访问.
   year_: 2021,
   edition: 1,
   author: "刘英俊001"
}

Object.defineProperty(book, "year", {
   get() {
      return this.year_;
   },
   set(newValue) {
      if (newValue > 2021) {
         // 仔细看,defineProperty方法中的参数并不是year_
         this.year_ = newValue;
         // 一年增加一个版本.
         this.edition += newValue - 2021;
      }
   }
});

book.year = 2025;
// 输出 5 
console.log(book.edition);

```



`get()`方法在严格模式下回返回**undefined**
`set()`方法在严格模式下会抛出**错误**



`get()`方法设置了固定的返回值,不管要访问的属性原本是什么,
最后输出的只会是你再`get()`方法中的值.

```JavaScript
let book = {
   // year_ 后面的下划线一般表示不希望被访问.
   heheda: 2021,
   edition: 1,
   author: "刘英俊001"
}

Object.defineProperty(book, "author", {
   get() {
      return "你不配知道作者神圣之名";
   },
   // set(newValue) {
   //    if (newValue > 2021) {
   //       // 仔细看,defineProperty方法中的参数并不是year_
   //       this.heheda = newValue;
   //       // 一年增加一个版本.
   //       this.edition += newValue - 2021;
   //    }
   // }
});

//你不配知道作者神圣之名
console.log(book.author);

book.author = "最帅之人";

//你不配知道作者神圣之名
console.log(book.author);

```









#### 1. 属性的查看



使用 `Object.keys()`方法可以查看一个对象的所有键名

```JavaScript
var obg = {
   111: 100,
   0.7: 700,
   hehe: 10,
   bar: 20,
}
// (4) ["111", "0.7", "hehe", "bar"]
console.log(Object.keys(obg));
```





#### 2. 属性的删除

删除直接名delete命令,就可以删除,

使用delete命令删除成功后返回true

**删除成功后再访问被删除的属性,就会返回undefined**

```JavaScript
var obg = {
   111: 100,
   0.7: 700,
   hehe: 10,
   bar: 20,
}
// (4) ["111", "0.7", "hehe", "bar"]
console.log(Object.keys(obg));
// true
console.log(delete obg.hehe);
// (4) ["111", "0.7", "bar"]
console.log(Object.keys(obg));
//访问被删除的属性返回undefined
console.log(obg.hehe);
```



**注意删除一个不存在的属性,delete不报错,同样返回true**

```JavaScript
var obg = {
   111: 100,
   0.7: 700,
   hehe: 10,
   bar: 20,
}

// 删除不存在属性同样返回true
console.log(delete obg.aaa);
```



**只有当删除某条属性时,这条属性不可被删除,则会返回false.**

delete命令只能删除属于当前对象或者数组的的属性,该属性的子类等等不属于被删除的对象或者数组的属性是不可以删除的.

同样,有时候特殊情况delete返回true,被删除的属性值依旧可以被调用.



#### 3. 属性是否存在

使用 `in运算符` 可以勘察对象中是否包含某一键名.

语法格式

```JavaScript
'键名' in 对象名
/*
	如果包含就返回true
	如果不包含就返回false
*/
```



但是`in运算符`有个问题,不能识别该属性时属于该对象的属性,还是该对象的属性的子属性.

```javascript
var obg = {
   111: 100,
   0.7: 700,
   hehe: 10,
   bar: 20,
}

// 返回 true
console.log('toString' in obg);
```

`toString` 这个方法,是属于默认继承object对象,但是我们创建的obg对象本身并没有创建`toString`这个对象属性.

这个时候可以使用`hasOwnProperty`方法判断

```JavaScript
if ('toString' in obg) {
   // false
   console.log(obg.hasOwnProperty('toString'));
}
```



当我们遍历一个对象时,for循环除了遍历该对象的属性,该对象属性的子属性再**一些情况**下也会遍历出来,我们可以搭配`hasOwnProperty`这个方法遍历出只属于该对象的属性

```javascript
for (var key in obg) {
   if (obg.hasOwnProperty(key)) {
      console.log(key);
   }
}
```



#### 4.with语句

with语句是操作同一个对象的多个属性提供便捷的写法

```
with(对象){
	语句;
}
```

看如下使用例子

```JavaScript
// 例一
var obj = {
  p1: 1,
  p2: 2,
};
with (obj) {
  p1 = 4;
  p2 = 5;
}
// 等同于
obj.p1 = 4;
obj.p2 = 5;

// 例二
with (document.links[0]){
  console.log(href);
  console.log(title);
  console.log(style);
}
// 等同于
console.log(document.links[0].href);
console.log(document.links[0].title);
console.log(document.links[0].style);
```



**注意,使用with区块内部进行变量的赋值操作,必须是已经存在的对象属性,否则with会创建一个全局变量.**

```JavaScript
var obg = {
   targe: 10,
   bear: 20
};

with (obg) {
   p1 = 10;
   heheda = 'hello';
}
//undefined
console.log(obg.p1);
//  10
console.log(p1);

// undefined
console.log(obg['heheda']);
// hello
console.log(heheda);
```









## 4. 函数



### 4.1 函数介绍

JavaScript中函数只能返回一个值,如果返回多个值,是返回一个对象

在JavaScript中,函数就是一个变量
既我们可以在使用变量的所有地方也可以用到函数.

函数语法

```javascript
function fun_name(parameter...){
    balabala...
    retune 返回值
}
```



**函数多次声明**

当同意函数被多次声明,后面声明的函数会覆盖掉前面声明的函数.

```JavaScript
function fun_one(){
    console.log('我是第一函数');
}

function fun_two(){
    console.log('我是第二函数');
}
```



**第一等公民**

JavaScript中将函数视作一种值而已,它和数值,字符串,布尔值地位效率沟通,也正是这样,像下文就有用变量声明函数,像对象里面可以有函数,像把函数作为参数传到另一个函数...等等

比如将函数作为参数.

```JavaScript
function fun_one(x, y) {
   return x + y;
}

function fun_two(result) {
   return result;
}
// 将函数作为参数,并将返回值赋值给一个变量
var print_result = fun_two(fun_one)(5, 20);

// 输出 25 
console.log(print_result);
```





**return语句**

当函数运行到return语句的时候,便是返回,哪怕后面还有语句也将不会再执行.

```JavaScript
function fun_two(){
    console.log('我再return之前');
    return 0;
    console.log('我再return之后');
}
```



### 4.2 变量声明函数



如果使用变量声明函数,则该函数后面一般不带函数名,因为带了也不能使用该函数名而调用函数,倒是可以使用变量名来使用函数.

如下例fun_name就不能直接调用,但是它可以再函数中使用,代指的就是该函数本身.

注意,使用变量声明函数,结尾最好用分号结束.

```JavaScript
var printf = function fun_name() {
   console.log('hello world');
};

// 使用这个函数名调用报错.
// fun_name();

// 但是使用方法名却可以输出hello world
printf();
```





### 4.3  Function构造函数

第三种声明函数的方式是`Function`构造函数。



```JavaScript
var add = new Function(
  'x',
  'y',
  'return x + y'
);

// 等同于
function add(x, y) {
  return x + y;
}
```



上面代码中，`Function`构造函数接受三个参数，除了最后一个参数是`add`函数的“函数体”，其他参数都是`add`函数的参数。

**你可以传递任意数量的参数给`Function`构造函数，只有最后一个参数会被当做函数体，如果只有一个参数，该参数就是函数体。**



```javascript
var foo = new Function(
  'return "hello world";'
);

// 等同于
function foo() {
  return 'hello world';
}
```

`Function`构造函数可以不使用`new`命令，返回结果完全一样。

总的来说，这种声明函数的方式非常不直观，几乎无人使用。



### 4.4 函数名提升

之前我们是又学到过变量名提升这一知识点,同样函数名和声明变量名一样会被提升.

以下代码不会报错,哪怕再函数声明前使用函数

```JavaScript
var print_result = fun_one(5, 20);
console.log(print_result);

function fun_one(x, y) {
   return x + y;
}
```

但是在变量函数声明前使用该函数,则会报错

```
f();
var f = function () {
  console.log('hello');
}
```







**变量函数声明和函数声明同时声明,将采用变量函数声明.**

```JavaScript
var f = function () {
  console.log('hello');
}

function f() {
  console.log('world');
}

f() // hello
```







### 4.5 函数属性和方法

#### 1. name属性

用来防护函数名的属性

```JavaScript
function fun_name1() { }
console.log(fun_name1.name);

var fun_name2 = function () { };
console.log(fun_name2.name);

```



特殊一点

以下情况虽然返回fake_name,但实际情况fun_name3才是这个函数的实际名字,使用时依旧是书写fun_name3这一函数名

```JavaScript
var fun_name3 = function fake_name() { };
console.log(fun_name2.name);
```





#### 2. length属性

用来返回函数参数个数

```JavaScript
function fun(a,b,c){};
// 3个参数
fun.length;
```





#### 3. toString()

返回一个字符串,内容是函数的源码,包括函数内部的注释和换行符.

```
function fun(x, y) {
   /* 
      这是让两个数相加的函数
   */
   return x + y;
};

console.log(fun.toString());
```





### 4.6 函数作用域



- 全部作用域
   - 全局作用域
   - 函数作用域
   - ES6新增的块级作用域



在函数域中声明一个变量,外部访问不了.

所以局部变量一般是再函数累声明,我们前面学到了的,再块中用var声明量一律都是全局变量

```JavaScript
var c = 100;

function fun() {
   var c = 10;
   return c;
};
var b = fun();

// 输出100
console.log(c);
// 输出 10
console.log(b);
```



函数域内部依旧是拥有变量提升

```JavaScript
function foo(x) {
  if (x > 100) {
    var tmp = x - 100;
  }
}

// 等同于
function foo(x) {
  var tmp;
  if (x > 100) {
    tmp = x - 100;
  };
}
```



同样下面例子证明函数域内部和外部一样,有着变量提升.

```JavaScript
console.log(a);  //undefined
var a = 100;
console.log(a);  //100

function fun_b() {
   console.log(b);  //undefined
   var b = 200;
   console.log(b);  //200
}

fun_b();
```



###  4.7 函数参数

#### 1. 函数参数简介

JavaScript中函数明明规定了形参,但是使用时没有传入参数并不会报错.

**JavaScript中函数可以省略参数,没有写的参数子自动编程undefined.**

但是函数的length属性和实际传入的参数无关

```JavaScript
function fun(a , b , c) {
    console.log(a);  
    console.log(b);
    console.log(c);
}

// 输出 1 2 undefined
function(1,2);
```



如果我们实在是想省略前面的参数,而传入后面的参数呢?

只能将前面的参数手动传入undefined,

```JavaScript
function fun(a , b , c) {
    console.log(a);  
    console.log(b);
    console.log(c);
}

// 输出 undefined 1 2 
function(undefined,1,2);
```



#### 2. 函数参数传递方式



**如果是数值,字符串,布尔值这三个原始类型**,那么传递方式就是**传值传递**
表示着再函数内部修改这个值的数据不会影响到外部的值.

```JavaScript
var a = 100;

function fun(a) {
   a = a - 80;
   console.log(a);
}
// 输出 20
fun(a);
// 输出 100
console.log(a);
```





**如果函数的参数是符合类型的值(对象 函数 数组)**

那么传递的方式就是**传址传递**,就是直接指向其地址,正如C语言中我们就可以知道,如果直接指向其地址进行修改,修改的就是这个值的本身数据.



**当(对象 函数 数组)作为参数,针对其某一属性进行修改的时候会改变其值**

```JavaScript
var a = [1, 2, 3];
// 输出 object
console.log(typeof a);
// 输出(3)[1,2,3]
console.log(a);

function fun(a) {
   a[0] = 10;
   console.log(a);
}
// 输出 (3) [10, 2, 3]
fun(a);
// 输出 (3) [10, 2, 3]
console.log(a);
```





**但是将这个参数(对象 函数 数组)整个替换掉时,这个时候就不影响原地址的值**

```JavaScript
var a = [1, 2, 3];
// 输出 object
console.log(typeof a);
// 输出(3)[1,2,3]
console.log(a);

function fun(a) {
   a = [10, 11, 12];
   console.log(a);
}
// 输出 (3) [10, 11, 12]
fun(a);
// 输出 (3) [1, 2, 3]
console.log(a);
```



#### 3. 同名函数参数

当一个函数参数中出现同名参数,那么就会选择**后面**的一个运行.

```JavaScript
function fun(a, a, c) {
   var result = 0;
   result = a + c;
   console.log(result);
}

// 输出 110
fun(10, 100, 10);
```



这里有个有趣的现象,同名的两个参数,传给前面一个值,后面一个不传值(也就是undefined)

实际运算起来依旧按照后面那个形参来.

```JavaScript
function fun(a, a) {
   console.log(a);
}

// 输出 undefined
fun(10);
```

上面代码,明明给前面的a穿了值10,但是实际代码运行的时候依旧输出了a为undefined.

这个时候如果想获取第一个a 的值运行,那就可以**使用arguments对象**

```JavaScript
function f(a, a) {
  console.log(arguments[0]);
}

f(1) // 输出 1
```



### 4.8 arguments 对象

**arguments对象 可以再函数内部读取多有参数**

也就是说arguments包含一个函数运行时的所有参数,arguments[0]就时第一个参数,arguments[1]则是第二个参数,以此类推.

```JavaScript
function f(a, a, b, b) {
   console.log(arguments[0]); // 10
   console.log(arguments[1]); // 11
   console.log(arguments[2]); // 12
   console.log(arguments[3]); // 13
}

f(10, 11, 12, 13);
```



再调用arguments这个对象时,可以再运行时修改其值,但是开启**严格模式**后对于实际的参数值(可以理解为实际arguments地址上的值)不会有任何改变

```JavaScript
function fun(a, b) {
   arguments[0] = 1;
   arguments[1] = 2;
   return a + b;

}

// 输出 3 是因为没有开启严格模式
console.log(fun(10, 11));

//------------------开启严格模式-----------//
var f = function (a, b) {
   'use strict'; // 开启严格模式
   arguments[0] = 3;
   arguments[1] = 2;
   return a + b;
}
// 这个时候输出 2
console.log(f(1, 1));
```



一般可以对arguments对象使用length属性,来判断到底有多少参数.

```JavaScript
function f() {
  return arguments.length;
}
```



### 4.9 闭包[难点!]

首先我们得知道基本知识.

函数的内部可以访问外面得全局变量,但是外部访问不到函数内部得变量

```JavaScript
var parameter = 200;

function fun() {
   var fun_parameter = 100;
   // 内部可以访问外部
   console.log(parameter);
}
// 但是外部不能够访问内部
// console.log(fun_parameter); 报错
```



但是我们就是想访问函数内部的变量怎么办?

再函数内部再创建一个函数,把这个函数作为返回值,这样就可以访问某一函数内部的变量,

```JavaScript

var parameter = 200;

function fun() {
   var fun_parameter = 100;
   // 内部可以访问外部
   console.log(parameter);

   function fun_son() {
      console.log(fun_parameter);
   }
   // 将内部函数作为返回值 返回
   return fun_son;
}

var visit = fun();
// 这样就可以得到fun_parameter的数据了
visit();

```

在上面这一段代码中,闭包的就是fun_son这一函数.

本质上闭包就是将一个函数内部和函数外部链接起来的一个桥梁.

闭包最大的用处

1. 可以从外部读取一个函数内部的变量.
2. 让这些变量始终保存在内存中.

这个始终保持在内存中可以看如下代码

```JavaScript
function fun(start) {
   return function fun_son() {
      return start++;
   };
}

var visit = fun(10);

console.log(visit()); // 10
console.log(visit()); // 11
console.log(visit()); // 12
console.log(visit()); // 13
console.log(visit()); // 14
```



***封装对象私有属性.***

```JavaScript
function Person(name) {
   var _age;
   function setAge(n) {
      _age = n;
   }
   function getAge() {
      return _age;
   }

   return {
      name: name,
      getAge: getAge,
      setAge: setAge
   };
}

var p1 = Person('张三');
p1.setAge(25);
// 输出 25
console.log(p1);
// {name: "张三", getAge: ƒ, setAge: ƒ}
console.log(p1.getAge());
```



### 4-1.0 函数知识补充

#### a.箭头函数

```JavaScript
let function_one = (a,b) =>{
  return a+b;  
};
// 等价于
let function_one = function(a,b){
    return a + b;
}
```



箭头函数非常适合一些语句中需要写函数的场景,用来简洁代码.

```JavaScript
console.log(ints.map(function(i) {return i+1}));
// 像只有一个参数的情况下,可以不用小括号.
console.log(ints.map(i=>{return i+1}));
```

以下几种的写法都有效

```JavaScript
let double = (x) => {return 2*x};
let triple = (x) => 3*x;
let Quadruple = x => 4*x;
console.log(double(10)); //20
console.log(triple(10)); //30
console.log(Quadruple(10)); //40
```



使用箭头函数给对象添加属性值

```JavaScript
let mun = {};
let num = x => x.name = "刘英俊";
num(mun);
console.log(mun.name); //刘英俊
```



**箭头函数的缺点**

1. 不能使用 `arguments` `super` `new.target`
2. 也不能作为构造函数使用
3. 同样箭头函数也没有`prototype`属性



#### b. 函数名

所有函数创建之后,都会暴露出一个可读的属性`name`,然而这个`name`属性大多数形况下都是保存着函数的函数名.

```JavaScript
function fun_one(){};
let fun_two = ()=>{};
let fun_three = function(){};
console.log(fun_one.name); // fun_one
console.log(fun_two.name); // fun_two
console.log(fun_three.name); // fun_three
// 没有函数名的时候,输出空
console.log( ( ()=>{} ).name );
// new Function()创建则输出anonymous
console.log( (new Function()).name )
```



创建完函数后立即调用函数的表达式

我们一般调用函数都是在函数创建完后,然后函数名+()进行调用

```JavaScript
function fun(name) {
   console.log('你好啊' + name);
}
// 形成调用
fun();
// 形成调用
var a = fun();
```



**上面代码第二个之所以能够调用,是因为JavaScript中function出现在行首才会被视为函数,如果不是在行首,就会被视为表达式.**

所以作为**表达式**的时候,可以直接**末尾添加圆括号调用**

```JavaScript
var f = function f() {
   var a = 100;
   var b = 200;
   // 输出表明这时候直接调用
   console.log('helloworld');
   return a + b;
}();

console.log(f);
```



同样基于上面的理解,只要函数被理解成表达式,那么就可以末尾加圆括号直接调用.

**那么不正好有圆括号里面一般只能放表达式嘛**

```
(function f() {
   // 输出helloworld
   console.log('helloworld');
}())
```

除了使用圆括号不让function被理解成函数,还可以用以下方法

```JavaScript
var i = function(){ return 10; }();
true && function(){ /* code */ }();
0, function(){ /* code */ }();


!function () { /* code */ }();
~function () { /* code */ }();
-function () { /* code */ }();
+function () { /* code */ }();
```



一般情况下支队匿名函数使用这种**立即调用的方法**

```JavaScript
// 写法一
var tmp = newData;
processData(tmp);
storeData(tmp);

// 写法二 避免污染全局变量
(function () {
  var tmp = newData;
  processData(tmp);
  storeData(tmp);
}());
```



#### c.函数参数



JavaScript根本不管你函数参数传多少,也不管你有没有传过来.

他本质是传过来的一个数组,不管是多还是少,数组里面的元素(函数的参数)有或者没有,并不会影响到这个数组的本身.这也就是为啥我们可以使用`arguments`进行计算传过来的参数有多少个.

```JavaScript
function  text(one , two , three , four ,five) {
    console.log(arguments.length);
    return arguments[0] + two;
}
/* 我传入的参数和我设定的参数可以毫不相干 */
text(); // 0
text(1,2,3); //3
text(1,2,3,4,5,6,7,8,9); //9

let result = text(10,20); //30
console.log(result);
```



修改`argumen[i]`达到修改对应的参数的效果,并不意味着他们就是访问同一内存地址,它们再内存中依旧是分开的,只不过JavaScript会将这两个数字的内容一般保持同步

所以改动`argument[i]`第 i 个参数也会跟着改变,反之修改第 i 个参数,argument[i]同理改变.



**箭头函数中使用`argument`**

正常情况下,箭头函数是使用不了`argument`的,但是我们可以在箭头函数的外面提添加一个包装函数.

```JavaScript
function foo(){
    let bar = () => {console.log(arguments[0])};
    bar(); 
}
foo(5);  // 5
```



感觉带着那么点点闭包的思想在里面 :)

#### d.没有重载

在 Java语言中,只要参数的类型和数量不同,便可以实现方法的重载,但是JavaScript中你只要方法名相同,那么后面的函数就会覆盖掉前面的函数.

下方代码就表明,并不会像Java中那样根据参数去选择函数执行,而是统一执行第二个函数.

```javascript
function aa(x) {
    return x + 2;
}

function aa(x,y) {
    return x + y;
}

console.log(aa(10));  //NaN
console.log(aa(10,20)); // 30
```



#### e.给未定义参数设置默认值

在之前,判断一个参数有没有被传过来,就是判断这个参数是否等于`undefined`,如果是的就给这个参数赋值一个默认值.

```JavaScript
function fun_name(value){
    value = (value !== undefined) ? value:"默认值";
}
```



但是在`ECMASript 6`之后就不用这么麻烦,直接在参数后加`=`和`默认值`

```javascript
function hello(value = 'world') {
    console.log(value);
}
hello(); // world
hello("hello"); // hello
```



####  f. 扩展和收集

****

扩展思想

扩展符号`(...)` 即`spread` ，方便的操作集合数据或者组合集合数据。

**个人理解 : 扩展符号就是能够将数组进行元素序列化.**

假使现在我想要一下两个数组合并

~~~JavaScript
let arr1 = [1,2,3];  
let arr2 = [4,5,6];
let arr3 = arr1.concat(arr2);
let arr33 = [...arr1,...arr2];
 // [1,2,3,4,5,6]
console.log(arr3);
 // [1,2,3,4,5,6]
console.log(arr33);

console.log(...[1, 2, 3])
// 1 2 3
console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

~~~

以前的时候则需要用到其他的方法,如`concat()` `splice()`
有了扩展符号之后,针对数组的操作能够简便很多.

同样这种将数组元素序列化的方法,同样可以用到函数的传参上.

```JavaScript
function sum_number1(){
    let sum = 0;
    for(let i = 0 ; i < arguments.length ; ++i){
        sum += arguments[i];
    }
    return sum;
}
console.log(sum_number1(...arr));
```



****

收集思想

上面一般是将一个数组进行累加或者合并等等,下面同样是通过扩展符号,但是实现了收集多个参数进行集中按照某一函数执行.

```JavaScript
function getsum(...value) {
    // 这个0是指当前元素
    return value.reduce((x,y)=>x+y,0);
}
console.log(getsum(1,2,3,4)); //10
```



`reduce()`方法的语法

MDN中比较难理解,我就简单粗鄙的介绍一下.

reduce()在下方使用的时候,第一个参数是你的函数代码,下面的四种情况调用函数都可以使用,那个 0 就是起始开始加的数组.

```JavaScript
var sum1 = [0, 1, 2, 3].reduce(function (accumulator, currentValue) {
    return accumulator + currentValue;
}, 0);
console.log(sum1);

var sum2 = [0, 1, 2, 3].reduce((x,y)=>x+y, 0);
console.log(sum2);

let reducer = function reducer(accumulator, currentValue) {
    return accumulator + currentValue;
}
var sum3 = [0, 1, 2, 3].reduce(reducer, 0);
console.log(sum3);

function aaa(accumulator, currentValue) {
    return accumulator + currentValue;
}
var sum4 = [0, 1, 2, 3].reduce(aaa, 0);
console.log(sum4);
```



#### G. 函数内部

在以前的ECMAScript 5 中,函数只存在两个特殊的对象
`arguments` `this`

然后再ECMAScript 6 中,新增了 `new.target`





**arguments**

还是先来回顾一下我们的老朋友 `arguments`

`arguments`对象有一个`callee`属性,这个`callee`属性,是一个指向`arguments`对象所在函数的指针.

通常正确调用函数名才能够执行和函数名对应的函数代码,因为内存中这个函数名和这个函数本身是紧密耦合的,但是我们可以使用`arguments.callee`让函数和函数名`解耦`

```JavaScript
// 阶层函数
function foo(num){
    if(num<1){
        return 1;
    }  
    else{
        return num * foo(num-1);
    }
}
console.log(foo(5)); // 120
// 使用arguments.callee解耦
function foo2(num){
    if(num<1){
        return 1;
    }  
    else{
        return num * arguments.callee(num-1);
    }
}

let test01 = foo;
console.log(test01(5)); //120
foo = function(){};
console.log(test01(5)); //NaN
console.log(foo(5)); //undefined



let test02 = foo2;
console.log(foo2(5)); //120
console.log(test02(5)) //120
foo2 = function(){};
console.log(foo2(5)); //undefined
console.log(test02(5)) //120
```



#### H. this [重点]

*****

`this`关键字默认指向的是全局上下文,以为就是`window`.

箭头函数会保留定义该函数时的上下文

所以在回调函数或者定时函数中,用箭头函数可以防止this又默认指向`window`

```JavaScript
window.name = "刘英俊";
console.log(this.name); // 刘英俊
// 函数并没有改变this 的指向
function fun(){
    let name = "刘帅气";
    console.log(this.name); //刘英俊
}
fun();
// 对象却可以改变this的指向
let obj_name = {
    name : "刘潇洒",
    sayName:function (){
        console.log(this.name); // 刘潇洒
    }
}
obj_name.sayName();
/*
当在回调函数或者定时函数中的另一个函数里使用this
this依旧会变回默认指向window
*/
let obj_name2 = {
    name : "刘潇洒",
    sayName:function (){
        setTimeout(function(){
            console.log(this.name);
        }, 1000);
    }
}
obj_name2.sayName();  // 刘英俊

// 回调函数或者定时函数中使用箭头函数
let obj_name3 = {
    name : "刘小小",
    sayName:function (){
        setTimeout(()=>{
            console.log(this.name);
        }, 1000);
    }
}
obj_name3.sayName();  //刘潇洒 
```



#### I . new.target

`new.target` 这个属性可以判断函数是被正常调用还是被`new`关键字调用.

```JavaScript
function King(){
    if(new.target){throw "King 是new关键字调用 "}
    console.log("King 是正常得调用");
}
King();
new King();
```



其实`new`关键字调用函数和正常调用函数有什么不同
这其实是一个值得深思得问题.



#### k. 函数的属性和方法

##### lenght属性

函数默认会有两个属性,分别是`lenght` 和 `prototype`属性

这里的`lenght`属性非常好理解,就是这个函数再书写的时候,有多少个参数就表示这个函数的`lenght`属性等于多少

```JavaScript
function sum(num1,num2,num3) {
    return 0;
}
function callsum() {
    return 0;
}
function callsum2(num1,num2) {
    return 0;
}
console.log(sum.length) // 3
console.log(callsum.length) // 0
console.log(callsum2.length)// 2
```



##### +++prototype属性

##### +++call() 和 apply() 方法

函数同样默认会有这两个方法





*****



### 构造函数

构造函数比较有用的就是它的`this`会指向函数内部而不是window



1. 构造函数的函数名首字母要大写
2. 构造函数不需要`return`就可以返回结果
3. 我们调用构造函数,必须使用new
4. 函数里面需要使用 `this` 关键字

```JavaScript
function Star(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.sing = function(string sang){
        console.log(sang);
    }
}
// 返回一个对象给 zs 这个变量
let zs = new Star('张三',15,'男');
console.log(zs.name);
console.log(zs['sex']);
console.log(zs.age);
console.log(zs.'七里香'); // 打印歌名
```



同样再已经存在的构造函数不能直接外部添加属性或者方法,只能在构造函数中去添加属性和方法.

```JavaScript
function Star(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.sing = function(string sang){
        console.log(sang);
    }
}

Star.nationality = "English"; // 添加失败
```



但是使用`prototype`方法可以给构造器函数添加新的属性或者方法

```JavaScript
Star.prototype.nationality = "English";
```

或者添加新的函数

```JavaScript
Person.prototype.figure = function(a,b) {
  return a+b;
};
```



### eval命令

`eval`命令接受一个字符串作为参数，并将这个字符串当作语句执行。

`eval()` 解析的变量和函数都不会提升,因为他们本身是放在一个字符串中的,

```JavaScript
eval('var a = 100;');
// 输出 100
console.log(a);

// 如果不能作为语句执行就会报错
// eval('ssa4654');// 报错


// 如果参数不是字符串,原样返回
var b = eval(100000);
// 输出 100000
console.log(b);


// eval没有自己作用域,就是在当前作用域运行
// 所以可以修改当前作用域变量的值.
var c = 10;
eval('c = 100;');
// 输出 100
console.log(c);
```



可以在一个函数域中使用严格模式,这样eval修改的值,就不会影响到外面.

```JavaScript
var foo = 100;

function fun() {
   // 使用严格模式
   'use strict';
   eval('var foo = 123');
   // 输出 100
   console.log(foo);
}

fun();
```







```JavaScript
var m = eval;
m('var x = 1');
x // 1
```

上面代码中，变量`m`是`eval`的别名。静态代码分析阶段，引擎分辨不出`m('var x = 1')`执行的是`eval`命令。

为了保证`eval`的别名不影响代码优化，JavaScript 的标准规定，凡是使用别名执行`eval`，`eval`内部一律是全局作用域。

```JavaScript
var a = 1;

function f() {
  var a = 2;
  var e = eval;
  e('console.log(a)');
}

f() // 1
```

上面代码中，`eval`是别名调用，所以即使它是在函数中，它的作用域还是全局作用域，因此输出的`a`为全局变量。这样的话，引擎就能确认`e()`不会对当前的函数作用域产生影响，优化的时候就可以把这一行排除掉。

`eval`的别名调用的形式五花八门，只要不是直接调用，都属于别名调用，因为引擎只能分辨`eval()`这一种形式是直接调用。





## 5. 数组(array)



### 5.0 检测数组



当只有一个全局执行上下文.

```
if (value instanceof Array){
	// balabala...
}
```



网页中有多个框架的时候,可能有两个不用全局执行的上下文,这个时候可以用到如下方法确定一个值是否为数组.

```JavaScript
if(Array.isArray(value)){
    // balabala...
}
```





创建数组并赋值

```JavaScript
var arr = [];
arr[0] = 1;
arr[1] = 2;
arr[2] = 3;
// 输出 3 
console.log(arr.length);
```

**如果我直接在那个中括号中写数组长度是没有用的.**

```JavaScript
var arr = [5];
arr[0] = 1;
arr[1] = 2;
arr[2] = 3;
// 数组长度依旧是 3 
console.log(arr.length);

```



**数组中可以时任何类型的数据**

```JavaScript
var arr = [
  {a: 1},
  [1, 2, 3],
  function() {return true;}
];

arr[0] // Object {a: 1}
arr[1] // [1, 2, 3]
arr[2] // function (){return true;}
```



**如果数组元素依旧是数组,就形成多维数组.**

```JavaScript
var a = [[1, 2], [3, 4]];
a[0][1] // 2
a[1][1] // 4
```



### 5.1 数组的本质

**数组的本质其实是一个特殊的对象.**

```JavaScript
var arr = [];
arr[0] = 1;
arr[1] = 2;
arr[2] = 3;
// 返回object
console.log(typeof (arr));
```



说明数组具有对象所有的特性,只不过数组的键名是固定的数字(0,1,2...).

```JavaScript
var arr = [];
arr[0] = 1;
// 依旧会转换字符串,所以可以.
arr[1.00] = 2;
// 直接打引号注明字符串
arr['2'] = 3;
// 输出成功 (3) [1, 2, 3]
console.log(arr);

```



同样可以使用针对对象的 `Object.keys`方法来返回键名.来证明键名是固定的数字.
所以创建数组这个特殊对象的时候不用为数组创建每一个键名

```JavaScript
var arr = ['a', 'b', 'c'];

Object.keys(arr)
// ["0", "1", "2"]
```



正因为数组是特殊对象,键名都是数字,所以如果使用`arr.0`的写法是错误的,所以只能够使用`arr[0]`带方括号的写法.



### 5.2 length属性



和Java还有C语言一样,数组的长度总是比最大的键名的那个值大一.

```JavaScript
var arr = [1, 2, 3, 4, 5];
// 输出数组长度 5
console.log(arr.length);
```



数组是动态的,可以不断添加元素

```JavaScript
var arr = [1, 2, 3, 4, 5];
// 输出数组长度 5
console.log(arr.length);

arr[5] = 6;
// 输出数组长度为 6
console.log(arr.length);
```



同样我们可以定死length长度;

定死长度后,超出数组长度的数据就自动被删除了.

如果设定数组长度大于本身数组,那么多出来的数字下标对应的值就是undefined

```JavaScript
var arr = [1, 2, 3, 4, 5];
// 输出数组长度 5
console.log(arr.length);

arr[5] = 6;
// 输出数组长度为 6
console.log(arr.length);

arr.length = 3;
// 只有 [1, 2, 3]
console.log(arr);


arr.length = 10;
// 控制台输出 (10) [1, 2, 3, empty × 7]
console.log(arr);
// 输出undefined
console.log(arr[9]);
```



如果我们将length设置不适合的值,就会报错.

```JavaScript
// 设置负值
[].length = -1
// RangeError: Invalid array length

// 数组元素个数大于等于2的32次方
[].length = Math.pow(2, 32)
// RangeError: Invalid array length

// 设置字符串
[].length = 'abc'
// RangeError: Invalid array length
```





**我们如果想快速清空一个数组里面的数据,只用将数组长度定位0即可**





再次因为数组其实是对象,所以可以使用对象添加键名的方法来添加属性,但是添加的属性如果不是正整数是不会影响到数组length的值的.

见如下代码

```JavaScript
var arr = [1, 2, 3, 4, 5];
// 输出数组长度 5
console.log(arr.length);

arr['pp'] = 100;
// 输出数组长度 5
console.log(arr.length);

arr[2.1] = 200;
// 输出数组长度 5
console.log(arr.length);

/*
但是如果打印,会发现实际数据是添加进去了的
(5) [1, 2, 3, 4, 5, pp: 100, 2.1: 200]
*/
console.log(arr);

```



同样,添加的键名不合法,会被视为字符串被length忽视.
但是使用这些不是数字的键名调用依旧可以调出数据,充分证明数组下标在使用的时候是先转化成字符串的.

```JavaScript
var arr = [1, 2, 3, 4, 5];
// 输出数组长度 5
console.log(arr.length);

arr[-1] = 100;
// 输出数组长度 5
console.log(arr.length);

arr[Math.pow(2, 32)] = 200;
// 输出数组长度 5
console.log(arr.length);

/*
但是如果打印,会发现实际数据是添加进去了的
(5) [1, 2, 3, 4, 5, -1: 100, 4294967296: 200]
*/
// 输出 100
console.log(arr[-1]);
// 输出 200
console.log(arr[Math.pow(2, 32)]);
```



### 5.3   in运算符



检查某个键名是否存在的运算符`in`，适用于对象，也适用于数组。

```javascript
var arr = [ 'a', 'b', 'c' ];
2 in arr  // true
'2' in arr // true
4 in arr // false
```

上面代码表明，数组存在键名为`2`的键。由于键名都是字符串，所以数值`2`会自动转成字符串。

注意，如果数组的某个位置是空位，`in`运算符返回`false`。

```javascript
var arr = [];
arr[100] = 'a';

100 in arr // true
1 in arr // false
```

上面代码中，数组`arr`只有一个成员`arr[100]`，其他位置的键名都会返回`false`。



### 5.4 遍历数组



**下面是遍历数组三种简单写法.**



```JavaScript
var a = [1, 2, 3];

// for循环
for(var i = 0; i < a.length; i++) {
  console.log(a[i]);
}



// for循环配合 in运算符
var a = [1, 2, 3];
a.foo = true;
// 使用 in遍历还会遍历出键名是字符串的成员.
for (var key in a) {
  console.log(key);
}



// while循环
var i = 0;
while (i < a.length) {
  console.log(a[i]);
  i++;
}

// 逆向遍历
var l = a.length;
while (l--) {
  console.log(a[l]);
}
```





### 5.5 数组的空位

数组中间的某一位置可以空出来,这叫做数组的空位

那么最后一个元素后面加一个逗号,会不会就是把最后一个位置空着在呢?
答案是 >> **最后一个元素后面有逗号不影响数组长度**

```JavaScript
// 末尾加逗号
var arr1 = [1, 2, , 4,];
// 末尾不加逗号
var arr2 = [1, 2, , 4];

// 下面两个都是输出长度为 4 
console.log(arr1.length);
console.log(arr2.length);
```



数组的空位是可以读取的,结果就是undefined

```JavaScript
var arr2 = [1, 2, , 4];
// 输出undefined
console.log(arr2[2]);
```



使用delete命令删除一个数组元素会形成空位,但是不影响lengt的值
也就是说一个长度为3的数组,使用delete命令删除一个成员之后,形成空位,它的长度依旧是3



```JavaScript
var arr2 = [1, 2, 3, 4];
delete arr2[0];
// 空位 输出undefined
console.log(arr2[0]);
// 依旧输出长度为 4
console.log(arr2.length);
```





**正因为length属性不会过滤掉空位,所以使用length属性遍历数组的时候一定小心**

一个数组的空位调用时候是undefined,一个数组的元素的值是undefined,这两个虽说都是undefined,但是实际运用中是不一样的,尤其是在遍历一个数组的时候.

**遍历时空位会被跳过,但是数值是undefined则不会被跳过.**

举个例子,见如下代码

```JavaScript
var a = [, , ,];

// 不会输出结果,跳过空位
for (var i in a) {
   console.log(i);
}
console.log(Object.keys(a));
```



**但是如果值为undefined,则不会跳过**

```JavaScript
var a = [undefined, undefined, undefined];

// 输出 0 1 2 (下标)
for (var i in a) {
   console.log(i);
}
console.log(Object.keys(a));
```





### 5.6类似数组的对象

既然数组本质上其实是一个特殊的对象
那么一个对象如果键名都是正整数或者0,那么是否表示这个对象就是数组?
答 : **这个类似数组的对象并不是数组,因为它没有数组的一些特有的方法,比如push方法,数组调用就不会报错,但是对象调用就会报错.**

正因为它不能是数组,像这类的对象就称为**类似数组的对象**.



“类似数组的对象”的根本特征，就是具有`length`属性。只要有`length`属性，就可以认为这个对象类似于数组。但是有一个问题，这种`length`属性不是动态值，不会随着成员的变化而变化。

```JavaScript
var obj = {
  length: 0
};
obj[3] = 'd';
obj.length // 0
```



数组的`slice`方法可以将“类似数组的对象”变成真正的数组。

```JavaScript
var arr = Array.prototype.slice.call(arrayLike);
```





如果想这个类似数组的对象使用数组特有的方法,除了上面先转为数组然后使用数组的方法,我们还可以使用`call()`把数组的方法放到对象上.

```JavaScript
function print(value, index) {
  console.log(index + ' : ' + value);
}

Array.prototype.forEach.call(arrayLike, print);
```



上面代码中，`arrayLike`代表一个类似数组的对象，本来是不可以使用数组的`forEach()`方法的，但是通过`call()`，可以把`forEach()`嫁接到`arrayLike`上面调用。

下面的例子就是通过这种方法，在`arguments`对象上面调用`forEach`方法。

```JavaScript
// forEach 方法
function logArgs() {
  Array.prototype.forEach.call(arguments, function (elem, i) {
    console.log(i + '. ' + elem);
  });
}

// 等同于 for 循环
function logArgs() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(i + '. ' + arguments[i]);
  }
}
```



字符串也是类似数组的对象，所以也可以用`Array.prototype.forEach.call`遍历。

```JavaScript
Array.prototype.forEach.call('abc', function (chr) {
  console.log(chr);
});
// a
// b
// c
```





注意，这种方法比直接使用数组原生的`forEach`要慢，所以最好还是先将“类似数组的对象”转为真正的数组，然后再直接调用数组的`forEach`方法。

```JavaScript
var arr = Array.prototype.slice.call('abc');
arr.forEach(function (chr) {
  console.log(chr);
});
// a
// b
// c
```



### 5.7数组的复制和填充

ES6新增两个方法,分别是`copyWithin()` 和 `fill()`

#### 5.7.1 fill()方法

fill()使用的方法具体如下

我个人觉得`fill()`更像是覆盖,见如下代码:

```JavaScript
fill(填充的东西,覆盖开始的下标,覆盖结束的下标);
```



比如我使用数字和符号覆盖数组中的元素

```JavaScript
let arr = new Array();
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
// 我们结束3元素是没有被覆盖的
// 使用字符串是需要打上引号的
arr.fill('*', 0, 3);
arr.fill(0, 9);
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

//输出 [*,*,*,4,5,6,7,8,9,0]
```



如果 fill() 后面不设定开始和结束的元素下标,那么就是默认覆盖全部数组

```JavaScript
const zeros = [0,0,0,0,0];

// [5,5,5,5,5]
zeros.fill(5);
```



然后就是`fill()`方法输下标不符合规范的的情况

```JavaScript
const zeros = [0,0,0,0,0];
// [5,5,5,5,5]
zeros.fill(5);

//索引过低,忽略 
zeros.fill('*',-10,-5);
//索引过高忽略
zeros.fill('*',6,10);
//索引反向,忽略
zeros.fill('*',4,2);
//如果索引只有部分可用,就之填充可用部分
//[0,0,0,5,5]
zeros.fill('*',3,10);
```



#### 5.7.2 copyWithin()

感觉`fill()`是用单个的符号去复制,这个`copyWithin()`则可以使用一段一段的去覆盖.

和fill()一样,都有起始和结束.读取也是一样,开始的下标会被算进去,结束的下标则不会.

```JavaScript
arr.copyWithin(插入索引, 复制的开始索引, 复制的结束索引);
```



具体例子见如下

```JavaScript
let arr = new Array();
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
//复制0-5下标的内容,从下标7插入
// [1,2,3,4,5,6,7,1,2,3]
arr.copyWithin(7, 0, 5);
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

```



`copyWithin()`和`fill()`最大的不同就是支持负索引

```JavaScript
//这个负索引是从数组结尾开始算的
arr.copyWithin(-4, -7, -5);
```



同样`copywithin()`方法遇见`索引过高`,`索引过低`,`索引反向`,都会被忽略为不做任何行为,索引部分可用也同样是复制填充可用部分.

```JavaScript
let arr = new Array();
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

arr.copyWithin(4, 8, 11);
// 1,2,3,4,9,10,7,8,9,10
alert(arr);

```



### 5.8转换方法

说白了就是把数组进行字符串的返回

因为数组就是一个特殊的对象,所有的对象都有`toLocalString()` , `toSting()`,`valueOf()`方法,

valueOf()返回的还是数组本身。而toString()返回由数组中每个值的等效字符串拼接而成的一个逗号分隔的字符串。也就是说，对数组的每个值都会调用其toString()方法，以得到最终的字符串

```JavaScript
let arr = new Array();
arr = ["green", "red", 100];
//三个都显示 green,red,100
alert(arr.toString());
//同样调用toString方法
alert(arr.valueOf());
//直接输出就会后台嗲用toString方法
alert(arr)
```



想默认后台调用的 toString 返回不用都好风格,就可以使用`join()`方法

```JavaScript
let arr = new Array();
arr = ["green", "red", 100];
//green,red,100
alert(arr);
// green*red*100
alert(arr.join("*"));
```





### 数组模拟栈的方法

> ECMAScript给数组提供几个方法，让它看起来像是另外一种数据结构。数组对象可以像栈一样，也就是一种限制插入和删除项的数据结构
>
> 推入 push   弹出 pop
>
> pop(弹出) 和 push(推入)都是数组默认的方法



就是使用push()方法就默认再数组最后以为添加元素,使用pop方法,调用的就是数组的最后一位元素,模仿栈的先进后出.

```JavaScript
let arr = new Array();

arr = ['10', '20'];

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

arr.push("end");

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

//调用最上面的一个元素
let item = arr.pop();
console.log(item);
```



### 数组模拟队列的方法

> 队列以先进先出（FIFO, First-In-First-Out）形式限制访问。队列在列表末尾添加数据，但从列表开头获取数据。
>
> 因为有了在数据末尾添加数据的push()方法，所以要模拟队列就差一个从数组开头取得数据的方法了。这个数组方法叫shift()，它会删除数组的第一项并返回它，然后数组长度减1。使用shift()和push()，可以把数组当成队列来使用

使用shift()方法

```JavaScript
let arr = new Array();

arr = ['10', '20'];

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

arr.push("end");

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
//调用最上面的一个元素
let item = arr.shift();
console.log(item);

// 输出20 , end 10别调用出去之后长度减一
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

```



那有开头使用数据他妈就把他删除了?
那肯定还得搞一个开头添加数据得啥

这个就是主角 unshift() 了 

```JavaScript
let arr = new Array();

arr = ['10', '20'];

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

arr.push("end");

for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
//调用最上面的一个元素
let item = arr.shift();
console.log(item);

// 输出20 , end 10别调用出去之后长度减一
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

arr.unshift("frist");
// frist 20 end
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

```



### 数组得排序方法

>reverse()   将数组反转
>
>sort() 转化成字符串,再使用字符串比较数组元素,将数组元素进行从小到大得顺序排列,但是得主义的是,排序的方法是按照字符串比较得方法.

**一下两个方法都是再原数组上面进行排序的,不会生成副本**



#### reverse()

```JavaScript
let arr = new Array();

arr = [10, 15, 20, 25, 30];

arr.reverse();
//   [30,25,20,15,10]
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

```



这个方法很简单粗暴,但是不够灵活

#### sort()

这个方法有点蛋疼,它虽然可以把数组按照从小到大得方式进行排序,但是从小到大是按照字符串得比较大小进行的.

```JavaScript
let arr = new Array();

arr = [0, 1, 3, 5, 15, 20];

arr.sort();
// 输出[0,1,15,20,3,5]
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
```



比较函数接收两个参数，如果第一个参数应该排在第二个参数前面，就返回负值；如果两个参数相等，就返回0；如果第一个参数应该排在第二个参数后面，就返回正值。

```JavaScript
let arr = new Array();

arr = [0, 1, 3, 5, 15, 20];

arr.sort();
// 输出[0,1,15,20,3,5]
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}

function compare(value1, value2) {
   if (value1 < value2)
      return -1;
   else if (value1 > value2)
      return 1
   else
      return 0;
}


arr.sort(compare);
// 输出[0,1,15,20,3,5]
for (let i = 0; i < arr.length; i++) {
   console.log(arr[i]);
}
```



**如果数组元素都是数字**,sort()的比较函数还可以更精简一点

```JavaScript
var points = [40,100,1,5,25,10];
// 升序
points.sort(function(a,b){return a-b});
// 降序
points.sort(function(a,b){return b-a});
```



### 数组的操作方法

#### concat()

> concat()方法可以在现有数组全部元素基础上创建一个新数组。它首先会创建一个当前数组的副本，然后再把它的参数添加到副本末尾，最后返回这个新构建的数组。如果传入一个或多个数组，则concat()会把这些数组的每一项都添加到结果数组。如果参数不是数组，则直接把它们添加到结果数组末尾

原始数组arr保持不变,因为创建的是arr的一个副本进行的添加.

```JavaScript
let arr = new Array();

arr = ["one", "two", "three"];

let new_arr = arr.concat("four", ["five", 'six', 'senve']);
// ["one", "two", "three","four","five", 'six', 'senve']
for (let i = 0; i < new_arr.length; i++) {
   console.log(new_arr[i]);
}

```



**防止假如得数组被打平**

将 `Symbol.isConcatSpreadable` 设置成false就是签字不打平数组.

```JavaScript
let arr_one = new Array();
let arr_two = new Array();

arr_one = ["one", "two", "three"];
arr_two = [4, 5, 6, 7];

// 如果使用正常得concat方法进行合并
let new_arr = arr_one.concat(arr_two);
// ['one', 'two', 'three', 4, 5, 6, 7]
console.log(new_arr);

//防止arr_two这个数组被打平
arr_two[Symbol.isConcatSpreadable] = false;
let new_arr_2 = arr_one.concat(arr_two);
// ['one', 'two', 'three', Array(4)]
console.log(new_arr_2);

```



concat方法终究是将一个数组的全部和另一个数组的副本组合,创建一个新的数组,但是如果我想只要原来数组的一部分元素呢?

提供了一个slice()方法,它可以寄接收两个参数,分别是开始索引和结束索引,但是谨记,结束索引和上面方法一样,是不会被复制的.
如果只有一个参数,就会被认为是开始索引,直接复制到最后一个元素.

```JavaScript
let arr = new Array();
arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
let arr_1 = arr.slice(5);
 // [5, 6, 7, 8, 9]
console.log(arr_1);

let arr_2 = arr.slice(5, 8);
// [5, 6, 7] 注意,没有包括第8下标的元素
console.log(arr_2);
```



#### slice()



**slice()的下标依旧支持负数,如果下标错误,就是返回空数组.**

```JavaScript
let arr = new Array();
arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
/*
let arr_1 = arr.slice(5);
 // [5, 6, 7, 8, 9]
console.log(arr_1);

let arr_2 = arr.slice(5, 8);
// [5, 6, 7] 注意,没有包括第8下标的元素
console.log(arr_2);
*/

// 下标反向的时候
let arr_3 = arr.slice(8, 5);
// 下标错误,输出空数组
console.log(arr_3);

// 支持负数的下标
let arr_4 = arr.slice(-5);
// [5, 6, 7, 8, 9]
console.log(arr_4);

```



#### splice()方法

> 或许最强大的数组方法就属splice()了，使用它的方式可以有很多种。
>
> splice()的主要目的是在数组中间插入元素，但有3种不同的方式使用这个方法。
>
> 插入  删除  替换



基本使用介绍

```JavaScript
// 使用删除功能 splice(0, 2)
arr.splice(开始下标,结束下标);

// 插入功能需要三个参数
// 插入功能 splice(2, 0,"red", "green",...可以添加多个元素)
arr.splice(5,0,10,20,30)从下标5开始,删除0个元素,插入10,20,30

// 替换同样需要三个元素 开始位置,删除元素个数,插入的元素
//会在位置2删除一个元素
splice(2, 1, "red","green") 
```



`splice()`始终返回这样一个数组,它包含从数组中删除的元素.
**如果splice()没有删除元素则会返回一个空数组.**



### 数组的搜索和位置方法



#### 1.严格相等



javascript提供三个严格相等的方法.

- indexOf()
  - 所有版本都可用
- lastIndexOf()
  - 所有版本都可用
- includes()
  - ECS7增加的



上面三个方法都是接受两个参数,
一个是要查找的元素,一个是可选的查找起始位置.



**如果没有找到元素，都会返回－１**
**三个方法 查找元素都是使用的严格相等符号进行 比较** 

使用这三个 方法 如果输入负数的时候需要注意一点数组的基本知识
*一个数组元素最后算作-1,依次向前数则依次递减*

**一些方法的 开始下标总是包含运算之中但是结束下标一般不包括.**

```
arr[0,1,2]
// 2就是-1 1是-2 0是-3
```





indexOf() 和 includes()都是从头开始找元素,lastIndex()则是从后面开始找元素.



#####　１.indexOf()

见下面的ｉｎｄｅｘＯｆ（）的基本用法．

```javascript
let arr = new Array();
arr = [0, 1, 2, 3, 7, 5, 6, 7, 8, 9];
// 输出下标4
let num_1 = arr.indexOf(7);
console.log(num_1);
// 输出下标7
let num_2 = arr.indexOf(7, 5);
console.log(num_2);
// 同样可以使用负数作为参数
let num_3 = arr.indexOf(7, -4);
console.log(num_3);
let num_4 = arr.indexOf(7, -6);
console.log(num_4);
```



又到了我们故意输错下标的时间



这里indexOf()有点意思,下标正整数超过最大值 ,不会别找到,但是负数超过很多依旧可以找到 
**只能说 indexOf()应该是按照同一段 地址往后找的.**

~~~javascript
let arr = new Array();
arr = [0, 1, 2, 3, 7, 5, 6, 7, 8, 9];
//我们负数超过数组却可以找到 下标4
let num_1 = arr.indexOf(7, -100);
console.log(num_1);
// 正数超过 最大值,返回-1
let num_2 = arr.indexOf(7, 16);
console.log(num_2);
~~~



同样根据上面的严格相等 符号比较的原理,我试了试把下标4的7改成字符串

这个时候找的就不是原来的 下标4的元素7,找到的 是 下标7 的元素7

```JavaScript
let arr = new Array();
arr = [0, 1, 2, 3, '7', 5, 6, 7, 8, 9];
let num_1 = arr.indexOf(7, -100);
//找到下标7
console.log(num_1);
```





##### 2.  lastIndexOf()

基本使用见如下代码

同样和indexOf()一样,如果超出太多只有符合自己往后查找的方向相反的才会能够查到

```JavaScript
let arr = new Array();
arr = [0, 1, 2, 3, '7', 5, 6, 7, 8, 7];
//查到下标7
let mun_1 = arr.lastIndexOf(7);
console.log(mun_1);
// 因为绝对相等,所以下标4的字符串7找不到 返回-1
let mun_2 = arr.lastIndexOf(7, 5);
console.log(mun_2);
// 返回-1
let mun_3 = arr.lastIndexOf(7, -100);
console.log(mun_3);
// 查到下标 9
let mun_4 = arr.lastIndexOf(7, 100);
console.log(mun_4);
```



##### 3.includes()

这个方法和上面两个方法不同的是includes()他找元素只返回**布尔值**.

看下面代码可知,同样支持负数的参数.

```JavaScript
let arr = new Array();
arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
// 找到返回ture
let mun_1 = arr.includes(7);
console.log(mun_1);
// 从下标8开始找,找不到返回false
let mun_2 = arr.includes(7, -2);
console.log(mun_2);
// 返回数组下标 7
let mun_3 = arr.indexOf(7);
console.log(mun_3);
```







#### 数组元素的迭代方法



> ECMAScript为数组定义了5个迭代方法。
>
> 每个方法接收两个参数：以每一项为参数运行的函数，以及可选的作为函数运行上下文的作用域对象（影响函数中this的值）。
>
> 传给每个方法的函数接收3个参数：数组元素、元素索引和数组本身。
>
> **因具体方法而异，这个函数的执行结果可能会也可能不会影响方法的返回值**。



##### 1.forEach（）

**forEach() 对于空数组是不会执行回调函数的**

这个方法就是将元素的每一个都按照传入的函数执行一遍。

forEach（）方法会改变原数组，并且函数里面不支持continue和break

```JavaScript
let arr = Array();
arr = [0,1,2,3,4,5,6,7,8,9];

arr.forEach(mufunction);

function myfunction(item,index,arr){
    console.log(item);
}
```



forEach本身不支持continue 和 break
但是可以用其他方法实现其效果



比如使用return代替continue效果,跳过输出元素3

```JavaScript
var arr = [1, 2, 3, 4, 5];

arr.forEach(function (item) {
    if (item === 3) {
        return;
    }
    console.log(item);
});
```



使用return代替break的写法

```JavaScript
var arr = [1, 2, 3, 4, 5];

arr.every(function (item) {
        console.log(item);
        return item !== 3;
});
```





根据菜鸟教程forEach方法地下的评论如下:

**forEach改变原数组情况**





##### every() and some()



every()方法和some()这两个方法是最接近的两个方法.

**every() 数组所有元素都执行传入的方法,所有元素都符合则返回true,否则返回false**
**some()数组所有元素都执行传入的方法,只要有一个元素符合就返回true,否则返回false**



```JavaScript
let arr = Array();
arr = [0,1,2,3,4,5,6,7,8,9];


let everyresult_1 = arr.every(myfunction_1);
let everyresult_2 = arr.every(myfunction_2);
// true false
console.log("everyresult_1="+everyresult_1+"   everyresult_2="+everyresult_2);

let someresult_1 = arr.some(myfunction_1);
let someresult_2 = arr.some(myfunction_2);
//都是true
console.log("someresult_1="+someresult_1+"    someresult_2="+someresult_2);

function myfunction_1(item){
    return item > -1;
}

function myfunction_2(item){
    return item > 8;
}
```





##### filter()

这个方法非常适合从数组中筛选满足给定条件的元素;

这些方法看似是返回满足条件的方法,更不如说就是那个元素是方法返回true,这个方法则返回这个数组元素.

```javascript
let arr = Array();
arr = [0,1,2,3,4,5,6,7,8,9];

let result = arr.filter(myfunction);

// 输出  0,2,4,6,8
alert(result);


function myfunction(item,index,arr){
	if(item%2===0)
		return true
	else
		return false
}

```







##### map()

这个方法肯filter（）一样，返回的是数组元素。

这个会修改元素组，执行一些吧数组所有元素都乘以2等操作



```JavaScript
let arr = Array();
arr = [0,1,2,3,4,5,6,7,8,9];

let result = arr.map(myfunction);

// 0,2,4,6,8,10,12,,14,16,18
alert(result);


function myfunction(item,index,arr){
	return item*2;
}

```





#### 数组的归并



究竟是使用reduce()还是reduceRight()，只取决于遍历数组元素的方向。除此之外，这两个方法没什么区别。



```JavaScript
let arr = Array();
arr = [0,1,2,3,4,5,6,7,8,9];

let result = arr.reduce(myfunction);

// 45
alert(result);


function myfunction(item_1,item_2){
	return item_1+item_2;
}

```



### +++定型数组+++

typed array() 定型数组

目的是提升向原生库传输数据的效率

#### +++ArrayBuffer+++



ArrayBufer()是一个普通的JavaScript构造函数，可用于在内存中分配特定数量的字节空间。



**创建一个ArrayBuffer**

ArrayBuffer类型得数组,可以自己分配字节.

```JavaScript
// 分配16个字节
let arr = new ArrayBuffer(16);
```



创建的定性数组
能够看字节长度,看数组长度的时候就显示undefined

```JavaScript
// 分配16个字节
let arr = new ArrayBuffer(16);

for (let i = 0; i < 20; i++) { arr[i] = i; }

// 16
console.log(arr.byteLength);
// undefined
console.log(arr.lenght);

// 确确实实能够输出所有的元素 0-19
for (let i = 0; i < 20; i++) { console.log(arr[i]); }
```



就像是创建一个自定义的内存空间,这个创建的内存缓冲区可以被其他东西使用.

因为一个 int 占有四个字节嘛,所以16/4=4,所以这个数组长度为4

```JavaScript
// 分配一个12字节的缓冲
const buf = new ArrayBuffer(16);

// 创建一个引用该缓冲的Int32Array
const ints = new Int32Array(buf);
// 16
console.log(ints.byteLength);
// 4
console.log(ints.length);

```



还有如下几个类型

```JavaScript
// 分配一个12字节的缓冲
const buf = new ArrayBuffer(16);

// 创建一个引用该缓冲的Int32Array
const ints_1 = new Int32Array(buf);
const ints_2 = new Int16Array(buf);
const ints_3 = new Int8Array(buf);

// 4
console.log(ints_1.length);
// 8
console.log(ints_2.length);
// 16
console.log(ints_3.length);


// 31位的float一个就是4字节
const floats_1 = new Float32Array(buf);
// 64位的float一个就是8字节
const floats_2 = new Float64Array(buf);

// 4
console.log(floats_1.length);
// 2
console.log(floats_2.length);

```



贴一下ArrayBuffer 和 C语言中的 malloc()的区别.

ArrayBuffer某种程度上类似于C++的malloc()，但也有几个明显的区别。

❑ malloc()在分配失败时会返回一个null指针。ArrayBuffer在分配失败时会抛出错误。

❑ malloc()可以利用虚拟内存，因此最大可分配尺寸只受可寻址系统内存限制。ArrayBuffer分配的内存不能超过Number.MAX_SAFE_INTEGER（253-1）字节。

❑ malloc()调用成功不会初始化实际的地址。声明ArrayBuffer则会将所有二进制位初始化为0。

❑ 通过malloc()分配的堆内存除非调用free()或程序退出，否则系统不能再使用。

而通过声明ArrayBuffer分配的堆内存可以被当成垃圾回收，不用手动释放。不能仅通过对ArrayBuffer的引用就读取或写入其内容。要读取或写入ArrayBuffer，就必须通过视图。视图有不同的类型，但引用的都是ArrayBuffer中存储的二进制数据。



#### +++DataView+++

必须在对已有的ArrayBuffer读取或写入时才能创建DataView实例。

语法如下:

```JavaScript
new DataView(buffer [, byteOffset [, byteLength]])
```





> MDN解释如下
>
> **`DataView`** 视图是一个可以从 二进制[`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 对象中读写多种数值类型的底层接口，使用它时，不用考虑不同平台的[字节序](https://developer.mozilla.org/zh-CN/docs/Glossary/Endianness)问题。



代码如下

```JavaScript
// create an ArrayBuffer with a size in bytes
const buffer = new ArrayBuffer(16);

// Create a couple of views
const view1 = new DataView(buffer);
const view2 = new DataView(buffer, 12, 4); //from byte 12 for the next 4 bytes
view1.setInt8(12, 42); // put 42 in slot 12

console.log(view2.getInt8(0));
// expected output: 42

```





## 6. 运算符

**JavaScript基本运算符如下**

- **加法运算符**：`x + y`
- **减法运算符**： `x - y`
- **乘法运算符**： `x * y`
- **除法运算符**：`x / y`
- **指数运算符**：`x ** y`
- **余数运算符**：`x % y`
- **自增运算符**：`++x` 或者 `x++`
- **自减运算符**：`--x` 或者 `x--`
- **数值运算符**： `+x`
- **负数值运算符**：`-x`



### 6.1  布尔值参与运算

*false >> 表示 0  true >> 表示 1*

**当运算中有布尔值的时候,布尔值会先自动转成数值.**

```javascript
// 输出 4
console.log(2 * (true + true));

// 输出 0
console.log(2 * false);
```



### 6.2 字符串相加

**当有字符串参与相加的时候,加号会被理解成链接符号**

```JavaScript
// ab
console.log('a' + 'b');
// a1
console.log('a' + 1);
// flasea
console.log(false + 'a');
// 1.22a
console.log(1.22 + 'a');
```



以上这种现象称为 ''重载''(overload) , 由于**只有加法存在这种现象**,所以有时候你不知道它倒是是执行那种运算方法,

**比如会根据运算成员类型位置的不同而产生不同的结果.**

```JavaScript
// a55
console.log('a' + 5 + 5);
// 10a
console.log(5 + 5 + 'a');
```



其他运算符则不存在这种现象,因为他们的规则是所有参与运算的成员一律转化成数值之后再运算.

遇见纯字符串不能转数值的,转化成NaN,然后进行运算.

```JavaScript
// NaN
console.log('a' * 1);
// NaN
console.log(100 - 'a');
// NaN
console.log(100 / 'a');
```



**遇见可以转为数值的,直接转为数值进行运算**

```JavaScript
// 7.5
console.log(10 - '2.5');
// 25
console.log(10 * '2.5');
// 4
console.log(10 / '2.5');
```



### 6.3 余数运算符

运算符的正负由第一个数字的符号决定

但是我有个疑虑,正常来说一个正数除以一个负数,或者一个负数除以一个正数,他们之间有余数这个概念嘛.....所以我还去百度了下

>其实从数学角度看,a=x*b+r (x为整数, 0=<r<b) 则 a%b=r
>3=2*1+1 所以 3 % 2 = 1
>-3=2*(-1)-1 所以-3 % 2 = -1 这里当然 也可以 -3=2*(-2)+1 也可以说-3 % 2 = 1 其实在 模 2 上,-1 可以认为是 +1 ,等效
>3= -2*(-1)+1 所以 3 % -2 = 1
>-3=-2*1-1 或者-3=-2*2+1 所以-3 % -2 = -1 或者-3 % -2 = 1
>-2=3*(-1)+1 所以 -2%3=1 即3除-2的余数是 1
>-2=-3*1+1 所以-2%-3=1 即-3除-2的余数是 1

其实上面答案我也看不太懂,但是我觉得知道这个机制就行,开发中应该不常见.

```JavaScript
// 2
console.log(10 % -8);
// -2
console.log(-10 % 8);
```



我们可以使用`Math.asb()`方法来得到绝对值.

```JavaScript
// 2
console.log(10 % -8);
// 使用绝对值方法输出 2
console.log(Math.abs(-10 % 8));
```



**余数运算符还可以用来计算浮点数,但是不精确**

```JavaScript
6.5 % 2.1
// 0.19999999999999973
```





### 6.4  数值运算符,负值运算符

#### 1. 数值运算符

数值运算符同样是一个加号( + ) ,但它是一元运算符(只需要一个操作数),而加法运算符是二元运算符,

**数值运算符的作用是可以将任何值转成数值(与Number函数作用相同).**

```JavaScript
+true // 1
+[] // 0
+{} // NaN
```



#### 2. 负值运算符



负值运算符的作用是将任何数值变成与它自身相反的符号,也就是说如果连续使用两个负值运算符那么就等同于数值运算符.

```JavaScript
var x = 1;
-x // -1
-(-x) // 1
```



### 6.5 指数运算符

指数运算符（`**`）完成指数运算，前一个运算子是底数，后一个运算子是指数。

```JavaScript
2 ** 4 // 16
```

注意，**指数运算符是右结合，而不是左结合**。即多个指数运算符连用时，先进行最右边的计算。

```JavaScript
// 相当于 2 ** (3 ** 2)
2 ** 3 ** 2
// 512
```

上面代码中，由于指数运算符是右结合，所以先计算第二个指数运算符，而不是第一个。





### 6.6 比较运算符



- `>` 大于运算符
- `<` 小于运算符
- `<=` 小于或等于运算符
- `>=` 大于或等于运算符
- `==` 相等运算符
- `===` 严格相等运算符
- `!=` 不相等运算符
- `!==` 严格不相等运算符



#### 1.讲一讲字符串的比较

JavaScript 引擎内部首先比较首字符的 Unicode 码点。如果相等，再比较第二个字符的 Unicode 码点，以此类推。

```JavaScript
'cat' > 'dog' // false
'cat' > 'catalog' // false


/*
小写的c的 Unicode 码点（99）大于大写的C的 Unicode 码点（67），所以返回true。
*/
'cat' > 'Cat' // true'
```

正因为比较的是Unicode码,所以汉字也是可以比较的.

```JavaScript
'大' > '小' // false
```



#### 2. 原始类型值比较

字符串还有布尔值类型进行比较的时候,都会优先转化成数值(Number)然后再进行比较.

```JavaScript
// 输出 false
console.log(5 > 'a');
// 输出 true
console.log(true > false);
// 输出 true
console.log(-1 < false);
```



如果是这种不能转化成一般字符的字符串`Number('a15')` 那么转化成NaN,然后和NaN进行比较.

上文中我有写到,NaN做布尔值的时候是false,我还以为NaN会被当做false然后在被当作0来进行比较,最后结果不是,**实际是任何数和NaN比较都会返回false**

```JavaScript
// 下面和NaN作比较全是 false
console.log(5 < 'a15');
console.log(5 > 'a15');
console.log(5 == 'a15');
console.log(5 === 'a15');
```



**同样哪怕是NaN和NaN做比较也不行,因为NaN不等同于它本身.**



#### 3. 对象的比较

如果运算子是对象，会转为原始类型的值，再进行比较。

对象转换成原始类型的值，算法是先调用`valueOf`方法；如果返回的还是对象，再接着调用`toString`方法.

```JavaScript
var x = [2];
x > '11' // true
// 等同于 [2].valueOf().toString() > '11'
// 即 '2' > '11'

x.valueOf = function () { return '1' };
x > '11' // false
// 等同于 [2].valueOf() > '11'
// 即 '1' > '11'
```



两个对象之间的比较也是如此。

```JavaScript
[2] > [1] // true
// 等同于 [2].valueOf().toString() > [1].valueOf().toString()
// 即 '2' > '1' 

[2] > [11] // true
// 等同于 [2].valueOf().toString() > [11].valueOf().toString()
// 即 '2' > '11'

{ x: 2 } >= { x: 1 } // true
// 等同于 { x: 2 }.valueOf().toString() >= { x: 1 }.valueOf().toString()
// 即 '[object Object]' >= '[object Object]'
```



### 6.7 相等和严格相等

`==` 和 `===`的区别

>它们的区别是相等运算符（`==`）比较两个值是否相等，严格相等运算符（`===`）比较它们是否为“同一个值”。如果两个值不是同一类型，严格相等运算符（`===`）直接返回`false`，而相等运算符（`==`）会将它们转换成同一个类型，再用严格相等运算符进行比较。



```JavaScript
// true
console.log(5 == '5');
// false
console.log(5 === '5');
// true
console.log('1' == true);
// false
console.log('1' == 'true');
// false
console.log(1 == 'true');
// false
console.log(1 === true);
```



值得注意的一点是 `+0` 等于 `-0` 

```JavaScript
// true
console.log(+0 === -0);

```



空字符串同样使用一般相等运算符比较是等于 0 的

**原始类型的值会转换成数值再进行比较。**

```JavaScript
'' == 0 // true
// 等同于 Number('') === 0
// 等同于 0 === 0

'' == false  // true
// 等同于 Number('') === Number(false)
// 等同于 0 === 0

'\n  123  \t' == 123 // true
// 因为字符串转为数字时，省略前置和后置的空格
```





**复合类型值使用严格等于符号比较**

两个复合类型（对象、数组、函数）的数据比较时，不是比较它们的值是否相等，而是比较它们是否指向同一个地址。

```JavaScript
{} === {} // false
[] === [] // false
(function () {} === function () {}) // false
```



上面代码分别比较两个空对象、两个空数组、两个空函数，结果都是不相等。原因是对于复合类型的值，严格相等运算比较的是，它们是否引用同一个内存地址，而运算符两边的空对象、空数组、空函数的值，都存放在不同的内存地址，结果当然是`false`。

如果两个变量引用同一个对象，则它们相等。

```JavaScript
var v1 = {};
var v2 = v1;
v1 === v2 // true
```

注意，对于两个对象的比较，严格相等运算符比较的是地址，而大于或小于运算符比较的是值。

```JavaScript
var obj1 = {};
var obj2 = {};

obj1 > obj2 // false
obj1 < obj2 // false
obj1 === obj2 // false
```

上面的三个比较，前两个比较的是值，最后一个比较的是地址，所以都返回`false`。





**undefined and null**

`undefined`和`null`与自身严格相等。

```JavaScript
undefined === undefined // true
null === null // true
```

由于变量声明后默认值是`undefined`，因此两个只声明未赋值的变量是相等的。

```JavaScript
var v1;
var v2;
v1 === v2 // true
```



`undefined`和`null`只有与自身比较，或者互相比较时，才会返回`true`；与其他类型的值比较时，结果都为`false`。

```JavaScript
undefined == undefined // true
null == null // true
undefined == null // true

false == null // false
false == undefined // false

0 == null // false
0 == undefined // false
```





### 6.8 严格不相等运算符

严格相等运算符有一个对应的“严格不相等运算符”（`!==`），它的算法就是先求严格相等运算符的结果，然后返回相反值。

```JavaScript
1 !== '1' // true
// 等同于
!(1 === '1')
```

上面代码中，感叹号`!`是求出后面表达式的相反值。



### 6.9 一般不相等运算符

相等运算符有一个对应的“不相等运算符”（`!=`），它的算法就是先求相等运算符的结果，然后返回相反值。

```JavaScript
1 != '1' // false

// 等同于
!(1 == '1')
```





## 7. 布尔运算符



布尔运算符用于将表达式转为布尔值，一共包含四个运算符。

- 取反运算符：`!`
- 且运算符：`&&`
- 或运算符：`||`
- 三元运算符：`?:`



### 1. 取反运算符（!）



取反运算符是一个感叹号，用于将布尔值变为相反值，即`true`变成`false`，`false`变成`true`。

```
!true // false
!false // true
```

对于非布尔值，取反运算符会将其转为布尔值。可以这样记忆，以下六个值取反后为`true`，其他值都为`false`。

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- 空字符串（`''`）

```JavaScript
!undefined // true
!null // true
!0 // true
!NaN // true
!"" // true

!54 // false
!'hello' // false
![] // false
!{} // false
```

上面代码中，不管什么类型的值，经过取反运算后，都变成了布尔值。

如果对一个值连续做两次取反运算，等于将其转为对应的布尔值，与`Boolean`函数的作用相同。这是一种常用的类型转换的写法。

```JavaScript
!!x
// 等同于
Boolean(x)
```

上面代码中，不管`x`是什么类型的值，经过两次取反运算后，变成了与`Boolean`函数结果相同的布尔值。所以，两次取反就是将一个值转为布尔值的简便写法。



### 2.且运算符(&&)

**用于返回多个表达式的求值.**

*a.当只有两个表达式的时候*

```
表达式1 && 表达式2
```

如果表达式1 为真(true),**则返回表达式2的值,而不是返回布尔值**,

如果表达式1 为假(false),**则直接返回 表达式1 的值,并且不对表达式2进行求值**

```JavaScript
// 输出 20
console.log((5 + 5) && (10 + 10));
// 输出 0
console.log(0 && (10 + 10));
```



表达式1为真则计算表达式2,如果表达式1为假则不计算表达式2

**这种跳过第二个表达式的计算称为短路**

```JavaScript
var a, b;
a = 10;
b = 1;

// 输出 9
console.log(b && (b = a - 1));
// 这时 变量b确实是 9 
console.log(b);

b = 1;

// 输出 0
console.log(0 && (b = a - 5));
// 这时 变量b依旧是1没变说明表达式2没计算
console.log(b);
```



有时候可以用它来代替if判断

```JavaScript
var a = 0;

if (a === 0) {
   // 输出了 helloworld
   console.log('helloworld');
}

// 等价于
// 输出 helloworld
(a === 0) && console.log('helloworld');
```



**且运算符多个连用的时候**

```JavaScript
/*且运算符可以多个连用，这时返回第一个布尔值为false的表达式的值。如果所有表达式的布尔值都为true，则返回最后一个表达式的值。*/

true && 'foo' && '' && 4 && 'foo' && true
// ''

1 && 2 && 3
// 3
/*上面代码中，例一里面，第一个布尔值为false的表达式为第三个表达式，所以得到一个空字符串。例二里面，所有表达式的布尔值都是true，所以返回最后一个表达式的值3。*/
```



### 3. 或运算符 ( || )

符号使用如下:

```
表达式1 || 表达式2
```

如果第一个表达式1为真(true) , 直接返回表达式1的值,不对表达式2做任何计算.

如果表达式1为假(false) , 则返回第二个表达式的值.

同样具备短路

```JavaScript
var x = 1;
true || (x = 2) // true
x // 1
```



**多个或运算符连用**

这时返回**第一个布尔值为`true`的表达式的值**。

**如果所有表达式都为`false`，则返回最后一个表达式的值。**

```JavaScript
false || 0 || '' || 4 || 'foo' || true
// 4

false || 0 || ''
// ''
```

上面代码中，例一里面，第一个布尔值为`true`的表达式是第四个表达式，所以得到数值4。例二里面，所有表达式的布尔值都为`false`，所以返回最后一个表达式的值。



### 4. 三元运算符

总算有个布尔运算符和C语言中的一样了.(狗头)

```
表达式1 ? 表达式2 : 表达式3 ; 
```



表达式1为真,则返回表达式2的值
表达式1为假,则返回表达式3的值.

```JavaScript
var a = 0;
// 输出a为5,说明表达式3没有计算
console.log(1 ? a = a + 5 : a = a - 5);

var a = 0;
// 输出a为-5,说明表达式2没有计算
console.log(0 ? a = a + 5 : a = a - 5);
```





## 8.基本引用类型



### 8.1 Date

创建一个日期对象,就是用new操作嗲用Date构造函数.

```JavaScript
let now = new Date();
```



#### 8.1.1 Date.parse

比如创建一个表示 "2000年10月2号的日期对象"

```JavaScript
// Mon Oct 02 2000 00:00:00 GMT+0800 (中国标准时间)
let someDate = new Date(Date.parse("10/2/2000"));
console.log(someDate);

/*书写格式
1. --- "10/2/2000"
2. --- "Oct 2,2000"
3. --- "Mon Oct 2 2000 00:00:00 GMT-0700 "
.....(还有其他,但这上面三种够用了)

*/
```



如果传入的不是日期,Date.parse() 方法会返回NaN



#### 8.1.2 Date.UTC()



这个方法同样是返回一个参数,表示时间,但是返回的参数和Date.parse()方法格式不一样而已.

```JavaScript
//Sat Jan 01 2000 08:00:00 GMT+0800 (中国标准时间)
let mytime_one = new Date(Date.UTC(2000, 0));
console.log(mytime_one);

//Fri May 05 2000 08:55:55 GMT+0800 (中国标准时间)
//Date.UTC(年, 月, 日, 小时, 分钟, 秒数)
let mytime_two = new Date(Date.UTC(2000, 4, 5, 0, 55, 55));
console.log(mytime_two);
```



这里我发现一个谷歌浏览器有意思的地方,使用`Date.UTC()`输入的时间,有两个地方需要注意,一个是月份,一个是小时.

月份是从0开始(0表示一月,1表示二月...)

小时是可以使用的是24小时制  **但是** 我们这个谷歌浏览器小时是默认中国八点,所以如果小时写1,那么输出的小时就是就是九点(8+1=9)



#### 8.1.3 Date类继承的方法



- toLocaleDateString()
   - 返回表示时间的字符串
- tostring()
   - 返回表示时间的字符串
- valueOf()
   - 返回日期的毫秒表示



```JavaScript
let someDate = new Date();
// 2021/8/6
console.log(someDate.toLocaleDateString());
// Fri Aug 06 2021 14:59:58 GMT+0800 (中国标准时间)
console.log(someDate.toString());
```



偏心讲讲`valueOf` 
这个函数返回的是一串数字,日期约大,这串数字就越大
可以利用这个做日期得大小比较

```JavaScript
let time_one = new Date(2019, 1, 0);
let time_two = new Date(2020, 1, 0);

// 1548864000000
console.log(time_one.valueOf());
// 1580400000000
console.log(time_two.valueOf());
// true
console.log(time_two > time_one);
```



#### 8.1.4 格式化日期



以下这些方法的输出与toLocaleString()和toString()一样，会因浏览器而异。因此不能用于在用户界面上一致地显示日期。

- toDateString
- toTimeString
- toLocaleDateString
- toUTCString



说白了下面方法就是显示时间得格式不一样而已.

```JavaScript
let time_one = new Date(2020, 8, 6);

// Sun Sep 06 2020
console.log(time_one.toDateString());
// 00:00:00 GMT+0800 (中国标准时间)
console.log(time_one.toTimeString());
// 2020/9/6
console.log(time_one.toLocaleDateString());
// Sat, 05 Sep 2020 16:00:00 GMT
console.log(time_one.toUTCString());

```





### 8.2 RegExp

创建正则表达式

```JavaScript
var re = /ab+c/;  // 字面量形式
var re = new RegRxp("ab+c");
```



正则表达式的特殊符号作用,请移步MDN观看.



#### a.正则表达式

-  g：全局模式
   -  表示查找字符串的全部内容，而不是找到第一个匹配的内容就结束。
-  i：不区分大小写
   -  表示在查找匹配时忽略pattern和字符串的大小写。
-  m：多行模式
   -  表示查找到一行文本末尾时会继续查找。
-  y：粘附模式
   -  表示只查找从lastIndex开始及之后的字符串。
-  u: Unicode模式
   -  启用Unicode匹配。
-  s:dotAll模式
   -  表示元字符．匹配任何字符（包括\n或\r）。



**RegExp支持正则表达式,配合上面标记的使用,可以达成许多搜索条件.**

语法

下面两个写法等价,**只不多一个使用字面量定义,一个使用构造函数.**

```JavaScript
let expression = /pattern(样式)/flags(标识);
// 等价于⬇
let expression = new RegExp("[bc]at","i");
```



元字符再模式中必须转义,包括下面字符

**一定要转义,切记,很重要**

```
( [ { \ ^ $ | ? * + . } ] ) 
```



**例子**

```JavaScript
//匹配字符串中的所有"at"
let pattern1 = /at/g;

//匹配第一个"bat"或"cat"，忽略大小写
let pattern2=/[bc]at/i;

//匹配所有以"at"结尾的三字符组合，忽略大小写
let pattern3 = /.at/gi ;

```



**选择性修改标记**

```JavaScript
const re1 = /cat/g;
// 输出 /cat/g
console.log(re1);

const re2 = new RegExp(re1);
// 输出 /cat/g
console.log(re2);

// 这里我们标识就被修改了
const re3 = new RegExp(re1, "i");
// 输出 /cat/i
console.log(re3);
```





#### b.RegExp实例属性



- global：布尔值，表示是否设置了g标记。
- ignoreCase：布尔值，表示是否设置了i标记。
- unicode：布尔值，表示是否设置了u标记。
- sticky：布尔值，表示是否设置了y标记。
- lastIndex：整数，表示在源字符串中下一次搜索的开始位置，始终从0开始。
- multiline：布尔值，表示是否设置了m标记。
- dotAll：布尔值，表示是否设置了s标记。
- source：正则表达式的字面量字符串（不是传给构造函数的模式字符串），没有开头和结尾的斜杠。
- flags：正则表达式的标记字符串。始终以字面量而非传入构造函数的字符串模式形式返回（没有前后斜杠）。





#### 8.3 原始值包装类型

扩展:

```
substring(start,stop)  //提取字符串函数
start 起始位置
stop  结束位置
```



##### a.简介



下面代码中`str_one`是原始值,原始值不是对象,是没有方法的
但是下列代码依旧是成功运行,将`str_one`中的值用substring()方法给保存到`str_two`中

```JavaScript
let str_one = 'helloworld';
let str_two = str_one.substring(2);
// lloworld
console.log(str_two);
// helloworld
console.log(str_one);


let str_one = 'helloworld';
let str_two = str_one.substring(2);

// 上面两行代码实际理解为下面三行,具体看下文文字理解
let str_one = new String ("some text");
let str_two = str_one.substring(2);
str_ome = null;
```



*我对上面代码理解如下:*

**原本 原始值 和 原始值包装类型的对象  是不一样的,**
**但是我们像上面代码那样直接用 原始值 使用 原始值包装类型的对象 才能用的方法的时候,后台就直接创建一个和这个原始值(str_one)相对应的原始包装类型的对象(暴露出各种方法),导致我们使用原始值直接调用原始包装类型的对象才拥有的方法也可以执行**



（1）创建一个String类型的实例；

（2）调用实例上的特定方法；

（3）销毁实例。



**这种行为,让原始值拥有对象的行为,同样 布尔值和数值都会像string一样,再后台发生.**





我们上面代码之所以能够执行时通过new关键字,new关键字实例化引用类型后,得到的实例摘离开作用域时被销毁,所以我们上面的实例可以使用方法.

而自动创建的原始值包装对象则只存在于访问它的那行代码执行期间。这意味着不能在运行时给原始值添加属性和方法。比如下面的例子：

```JavaScript
let some = "some text";
some.color = "red";
// undefined
console.log(some.color);
```

因为当第三行代码运行的时候,`some.color`这个属性就被销毁了.



##### b.object类型包装

object对象,你输入哪一种类型的值,返回也返回同一类型.

```JavaScript
let obj1 = new Object("some string");
// true
console.log(obj1 instanceof String);

let obj2 = new Object(1);
console.log(obj2 instanceof Number);

let obj3 = new Object(true);
console.log(obj3 instanceof Boolean);
let obj4 = new Object(1);
// 输出false
console.log(obj4 instanceof Boolean);
```



但是我换成typeof就都返回的是object对象

`typeof()` 判断任何引用类型返回的都是object

```JavaScript
// 都是输出object
let obj1 = new Object("some string");
console.log(typeof (obj1));

let obj2 = new Object(1);
console.log(typeof (obj2));

let obj3 = new Object(true);
console.log(typeof (obj3));
let obj4 = new Object(1);
console.log(typeof (obj4));
```



##### c Number类型包装

Number中`toString()` `valueof()` `toLocaleString()` 都被重写过

value() 返回Number对象的原始数值,另外两个重写得方法返回数值字符串.

```JavaScript
let mun = 10;
// 默认按照十进制输出
console.log(mun.toString());
// 二进制输出
console.log(mun.toString(2));
// 八进制输出
console.log(mun.toString(8));
// 16进制
console.log(mun.toString(16));
// 10进制
console.log(mun.toString(10));

let mun2 = 10;
// 返回 10
console.log(mun2.valueOf());
```



**idinteger()方法和安全整数**

**isinteger()方法,用于辨别的一个数值是否位整数.**

**在阔括号中是运算的表达式也是可以的**

```JavaScript
// true
console.log(Number.isInteger(1));
// true
console.log(Number.isInteger(1.00));
// false
console.log(Number.isInteger(1.01));
// false
console.log(Number.isInteger(10 * 3 - 5 * 0.3));


let num = 1.2;
// console.log(num.isInteger());  使用报错
let mun = new Number(1.2);
// console.log(mun.isInteger()); 使用报错
```





**toFixed()返回包含小数点,括号传入位数**

如果这个数值本身的小数位多于传入的参数,那么多出来的将进行**四舍五入**

```JavaScript
let num = 10.26635;
// 输出10.27
console.log(num.toFixed(2));
```



再次提醒,浮点数的计算并不准确,

```
let num = 0.1 + 0.2;
// 输出0.30000000000000004
console.log(num);
```



同下文中的布尔值一样,**Number对象是Number类型的实例，而原始数值不是**



##### d. Boolean类型包装

**我们重点区分一下,布尔类型的对象和布尔原始值是有区别的!!!**

```JavaScript
let bealoon_object = new Boolean(false);
let result_one = bealoon_object && true;
// 输出true
console.log(result_one);

let bealoon_value = false;
let result_two = bealoon_value && true;
// 输出 false
console.log(result_two);
```



我们看上文的布尔运算符中就可知,`&&` 是属于  ""有假必要假"" , 所以我们第一个`bealoon_object` 属于布尔对象和布尔原始值`bealoon_value` 是有区别的,布尔类型对象,**你把他值设置成假,但是它本身依旧表示真.**



我们使用`typeof` 对于原始值(boolean值)返回原始类型的的数据(Boolean),但是对于引用类型,也就是`bealoon_object` 属于布尔类型的实例,则返回的是object

同样，Boolean对象是Boolean类型的实例，在使用instaceof操作符时返回true，但对原始值则返回false. (因为instanceof一个作用是用来判断对象的具体类型.)



```JavaScript
let bealoon_object = new Boolean(false);
let result_one = bealoon_object && true;
// 输出true
console.log(result_one);

let bealoon_value = false;
let result_two = bealoon_value && true;
// 输出 false
console.log(result_two);

// 输出的是object类型
console.log(typeof bealoon_object);
// 输出的是bealoon类型
console.log(typeof bealoon_value);

// 输出的是true
console.log(bealoon_object instanceof Boolean);
// 输出的是false
console.log(bealoon_value instanceof Boolean);
```









##  9. 同步 和 异步

*****



### a. 同步

同步的概念我们比较好理解

在`JavaScript`中,它是按照单线程进行执行的代码
正如网上所说`JavaScript`是解释型语言,一行一行的执行代码.

在下面代码中,`console.log()`如果想要输出`x`

那么就需要x赋值,又等完`x`计算之后才可以使用.

```JavaScript
let x = 3;
x = x + 7;
console.log(x); //10
```



而最基础最能体现异步的就是`setTimeout` 函数和 `setInterval`函数

```JavaScript
let x = 3;
setTimeout(() => {
    x = x + 70; 
    console.log(x); //80 
}, 0);
x = x + 7;
console.log(x); //10

输出结果:
10
80
```

我们会发现`setTimeout`函数是在`console.log`之后执行的,这种直接改变程序执行顺序的操作就是`JavaScript`中的**异步操作**

其原因就是在JavaScript中有一个主线,还有另一个任务队列,当JavaScript觉得这个函数或者程序需要消耗一等的时间会让其他程序等待,那么它会把这个程序放进任务队列,继续执行主线,等主线执行完了后,再来执行它所觉得耗时的任务队列.(实际我们的setTimeout设置时间为0 并不会占用时间,但是JavaScript它认为setTimeout会是个耗时的程序.)

为了让后续代码能够使用x，异步执行的函数需要在更新x的值以后通知其他代码。如果程序不需要这个值，那么就只管继续执行，不必等待这个结果了。



### b.异步[难点]

`JavaScript引擎`运行到异步代码之后,会将异步代码展示放到一个"暂存区".

继续执行同步代码,同步代码执行完成之后在来按顺序执行异步代码.



同样的异步代码,但是并不一定就是先进去的先执行.

下面两个`setTimeout` 由于下面的一个等待时间比上面一个小,所以下面的`setTimeout`先执行

```JavaScript
var a = 10;
var b = 20;
setTimeout(()=>{
    console.log("在代码中是第一个异步代码");
},1000)
setTimeout(()=>{
    console.log("在代码中是第二个异步代码");
},500)
```



当一个异步代码A要获取另一个异步代码B的数据时

我们必须要让这个异步代码A 在 B 之后执行.

```JavaScript
var a = 0;

setTimeout(()=>{
    a = 1
},1000);

setTimeout(()=>{
    console.log(a);
},2000);
```



虽然`JavaScript`是单线程执行代码

但是浏览器实际是以多个线程协助操作来实现按线程异步模型.



1. GUI渲染线程
2. JavaScript引擎线程
3. 事件触发线程
4. 定时器触发线程
5. http请求线程
6. 其他线程



上面的线程会被面试的时候归类为下面两种线程

主线程

用来执行页面渲染,JavaScript代码运行,时间的出发等等

工作线程

在幕后工作,用来处理异步任务的执行来实现非阻塞的运行模式.

![image-20220214204821769](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220214204821769.png)



当函数有嵌套的时候,这个时候执行栈中就回有堆积.

当函数嵌套到足够的多的时候,就会触发栈溢出,
也就是这个函数栈已经存放不下这么多函数的栈帧.





宏任务和微任务

`JavaScript`中有两种异步方式,分别是`宏任务`和`微任务`.

宏任务执行前优先清空本次的微任务,再执行下一次的宏任务

<img src="https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220214213952087.png" alt="image-20220214213952087" style="zoom:200%;" />



Promise.then  catch finally  MutationObserver  微任务

I/O setTimeout  setInterval  requestAnimationFrame[^1] 宏任务

[1]: requestAnimationFrame是浏览器中的一个自动刷新函数,大约每60秒左右刷新一次.





补充一下:

Promise内部是同步代码,后面的`.then` 和 `.catch`中才是异步执行.

```JavaScript
let pro = new Promise((resolve,reject)=>{
    console.log("我是promise中的同步代码");
    resolve("成功");
    setTimeout(()=>{
        console.log("我是promise中的宏任务! setTimeout");
    },0);
})
pro.then((res)=>{
    console.log("我是then 001,微任务!!")
})
.then((res)=>{
    console.log("我是then 002,微任务!!")
})
setTimeout(()=>{
    console.log("我是promise外的宏任务! setTimeout");
},0);
console.log("我是最外面的同步代码");
```



输出结果:

![image-20220226101047061](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220226101047061.png)



异步函数中,有一部分是我们主动触发的,有一部分一直是自动在运行.



#### Promise

先来看`promise` 的基本用法

```JavaScript
let pro = new Promise((resolve,reject)=>{
    // resolve('成功');
    reject('失败');
});
pro.then(()=>{
    console.log("执行成功");
})
pro.catch(()=>{
    console.log("执行失败,错误");
})
pro.finally(()=>{
    console.log("我是最后执行的finally");
})

```



首先`promise`是有三种状态的,默认的状态是`pending`.
当`promise`从pending改变成其余的两种中的一种的时候,就确定下来不会改变了.

而导致`promise`状态改变的就是`promise`中的两个参数`resolve`和`reject`.

```
resolve --> 实现(fulfilled)  reject --> 拒绝(rejected)
```



当 promise 中执行的是`resolve`函数,那么promise就回转变成实现的状态
并且触发下面的`then()`方法中的异步代码.

当 promise 中执行的是`reject`函数,那么promise就回转变成拒绝的状态

并且触发下面的`catch()`方法中的异步代码.

`finally` 就和其他语言中一样,表示最后都会执行的部分代码.



##### promise的链式调用

显然我们书写代码的时候,一个then并不能解决我们的问题

我们要处理多个异步问题的时候,我就可以用到链式调用.

此时,异步代码就是从上往下依次执行.

```JavaScript
let pro = new Promise((resolve,reject)=>{
    resolve('成功');
    //reject('失败');
});
pro.then(()=>{
    console.log("我是链式调用001");
})
.then(()=>{
    console.log("我是链式调用002");
})
.then(()=>{
    console.log("我是链式调用003");
})
.then(()=>{
    console.log("我是链式调用004");
})
.then(()=>{
    console.log("我是链式调用005");
})
```

原因是因为这有个调用链

我们现在想中断一个promise的调用链接,有下面两种方法

一个是 throw  一个是 return Promise.reject

```JavaScript
let pro = new Promise((resolve,reject)=>{
    resolve('成功');
    //reject('失败');
});
pro.then(()=>{
    console.log("我是链式调用001");
})
.then(()=>{
    console.log("我是链式调用002");
})
.then(()=>{
    console.log("我是链式调用003");
    //     throw(Error);
    return Promise.reject();
})
.then(()=>{
    console.log("我是链式调用004");
})
.then(()=>{
    console.log("我是链式调用005");
})
```

能中断的原因很简单,因为then()是将上面视为一个整体的promise.

来判断当前的then()方法能不能执行.

![image-20220226091910586](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220226091910586.png)



上面为个人理解,以下为视频中,老师的代码讲解:

链式调用能中断的原因,途中返回的是pending状态的promise

一样达到中断的结果,该代码主要是理解promise中断的原理.

![image-20220215211405505](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220215211405505.png)



##### Promise.all

Promise.all 中,所有结果都是resolve 则等待最慢的接口时间完成后,触发then

如果all中,哪怕有一个是reject 

那么终止时间就是执行到第一个reject程序就结束了

并且不会触发then  而出发了catch 

![image-20220215212005558](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220215212005558.png)



Promise.race  

和结果没有关系,这个只看速度 **天下武功 唯快不破**

在速度相同的情况下就是那个代码在前那个先执行

同样,返回resolve则then被执行,reject则不执行.

```JavaScript
let p1 = new Promise((resolve,reject)=>{
    setTimeout(resolve,100,"one");
})

let p2 = new Promise((resolve,reject)=>{
    setTimeout(resolve,500,"two");
})

let p3 = new Promise((resolve,reject)=>{
    setTimeout(reject,100,"three");
})

let p4 = new Promise((resolve,reject)=>{
    setTimeout(reject,100,"four");
})

Promise.race([p1 , p2]).then((res)=>{
    console.log(res); //输出 one 因为它执行更快
})

Promise.race([p3 , p1]).then((res)=>{
    console.log(res); //输出 one 同样速度,p1代码在上,先执行.
})

Promise.race([p3 , p4]).then((res)=>{
    console.log(res); //不执行
})
```









##### 异步代码同步化

##### Generator

异步函数在执行的过程中,没有遇见return语句,默认`return undefined`

ES6  用于向下兼容过度期的浏览器

![image-20220215213928330](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220215213928330.png)





##### async

`async/await` 被提出来 , 就是为了解决异步代码的同步执行顺序问题.

async 可以放在 函数前,函数表达式前,箭头函数前 和 方法前 

await 让异步函数任然具有异步特性,但是是同步求值



await 接受的不一定就一定要是resolve或者reject这两个值.

同异步函数一样,在函数中抛出错误(throw),会返回一个拒绝的状态

只是说这个 async 函数中抛出的错误不会被catch捕获到

```JavaScript
async function foo(){
    console.log(1);
    Promise.reject(3);
}
foo().catch(console.log("Error"));
console.log(2);
```



具体的`async/await`见 MDN 网址

```JavaScript
var resolveAfter2Seconds = function() {
    console.log("starting slow promise");
    return new Promise(resolve => {
      setTimeout(function() {
        resolve("slow");
        console.log("slow promise is done");
      }, 5000);
    });
  };
  
var resolveAfter1Second = function() {
    console.log("starting fast promise");
    return new Promise(resolve => {
      setTimeout(function() {
        resolve("fast");
        console.log("fast promise is done");
      }, 3000);
    });
  };
  
var sequentialStart = async function() {
    console.log('==SEQUENTIAL START==');
  
    // 1. Execution gets here almost instantly
    const slow = await resolveAfter2Seconds();
    console.log(slow); // 2. this runs 2 seconds after 1.
  
    const fast = await resolveAfter1Second();
    console.log(fast); // 3. this runs 3 seconds after 1.
  }

sequentialStart();
```





Babel 可以将一些新格式的js代码,翻译成旧格式的代码

但是Babel它也有局限性的



## 10. BOM

浏览器对象模型(BOM--Browser Object Model)

BOM主要是提供了与网页无关的浏览器功能对象

### 10.1 window对象

*****

1. ECMAScript中的 Golbal对象
2. 浏览器窗口的JavaScript接口



window全局对象

你可以理解在全局作用域中定义,就好像是在一个叫window的对象大括号里面写属性.

这个比喻不是很恰当,但是帮助你理解如下代码

```JavaScript
var a = 100;

function print(vaule){
  console.log(vaule);
}

console.log(window.a);
window.print("hello world");

let b = 200;
let c = function (vaule){console.log(vaule);}

const d = 300;
console.log(window.b); //undefined
console.log(window.c); //undefined
window.print("hello world");
```

在全局定义的变量 a 函数 还有用变量定义的函数c 
都可以被window对象运用`.`给使用出来

但是`let` 和 `const`定义的变量不会在window的全局作用域中
这两个则是另外在一个叫做 `Script`的作用域中
所有window对象不能将`b` 与 `d` 给点出来



不得不提到`this`关键字是默认指向window对象的

同样我们可以使用`this`来调用window对象中的属性

```JavaScript
var a = 100;
console.log(this.a);
```



BOM只是浏览器提供的API[^api]的统称

[^api]: 即应用程序编程接口,代之那些已经封装好的某些功能的函数.

然而这些`api`都放在`BOM`的`window`对象中

代表当前浏览器窗口

后面很重要的DOM也属于BOM中的一部分

![image-20220226145952647](JavaScript%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0.assets/image-20220226145952647.png)



BOM中常见的`API`
下面只是一部分呢常见,还有很多的BOM的API

具体请查阅 MDN

```
window.alter()  //弹窗
window.prompt() //确认弹窗
window.location 
	--> location.herf     
	--> location.hostname  //网址
	--> location.pathname  //网址路径
	--> location.reload()  //刷新
	
window.navigation   //浏览器用户相关信息

window.screen   //用户屏幕相关的属性
	-->screen.height
	-->screen.width
	-->screen.orientation
innerHeight  innerWidth //页面的宽高属性
open() close() //打开或关闭浏览器窗口
```



#####  top

返回最顶层的窗口对象引用(window)

```
var topWindow = window.top;
```

##### parent



```
var parentWindow = window.parent;
```

如果只有一层,或者两层

那么parent==top==window

```
if (window.parent != window.top) {
  // 至少有三层窗口
}
```



##### window.devicePixelRatio

在不同设备的分辨率是不一样的
而CSS中的像素是一个统一的单位,为了让写好的像素单位在不同的分辨率的设备上能够良好的显示出来,window.devicePixelRatio就会自动帮我们设配.



##### 窗口大小获取

```
innerWidth、innerHeight、outerWidth outerHeight
```



所有浏览器都支持上面这四个属性

`outerWidth`  , `outerHeight` 返回浏览器窗口大小

`innerWidth`、`innerHeight` 返回浏览器中视窗大小(不包括工具栏和任务栏)



下面两个属性返回视窗的高度和宽度

`document.documentElement.clientWidth`

`document.documentElement.clientHeight`







## 11.DOM

Document Object Model  >>>>> 文档对象类型



JavaScript中一般有三种对象

1. 用户定义对象  >>  自己创建的数据集合
2. 内建对象  >>  Array Date Math
3. 宿主对象 >> 像浏览器提供的一些可以使用的对象

***

### 11.1 节点介绍



节点  node

1.元素节点(element node)

```
<p></p>

<ul>
	<li></li>
</ul>
```



2.文本节点(text node)

```
<p>文字类容</p>
// p 标签中的文本类容就是文本节点
```



3.属性节点

```
<p title = "good">文字类容</p>
// p 标签中的title就是属性节点
```



4.注释节点



然后获取上面的元素节点获取,一般有三种方式

```JavaScript
//用Id获取,eleNode是个对象
var eleNode = doucument.getElementsById()  
//用标签名获取,获取的是一个节点对象的集合
var eleNode = doucument.getElementsByTagName()  
//用class获取,获取的是一个节点对象的集合
var eleNode = doucument.getElementsByClassName()  
```



因为本身获取的是一个对象,或者对象的集合.
所以使用的时候可以使用对象的`[]`,然后对象也可使用`.`调用属于这个对象的数据.

```
// 获取页面中的第一个p标签
var eleNode = doucument.getElementsByTagName('p')[0]
eleNode.XXX(属于这个eleNode元素的属性之类的....)
```

***



常见的就是如下三种:

- `nodeName`(节点名称)  是只读
     - 元素节点的nodeName和它的标签名相同
     - 属性节点的nodeName和它的属性名相同
     - 文本节点的nodeName永远都是#text
     - 文档节点的nodeName永远都是#document
          - 文档节点代表整个HTML节点,使用document就可访问.
- `nodeVaule`(节点的值) 
     - 元素节点的vaule是null或者undefined
     - 文本节点的vaule是文本滋生
     - 属性节点的vaule是属性的值
- `nodeType`(节点类型)
     - 就是表明当前的节点是属于哪一种节点类型,是只读



所有节点都继承Node类型,所有共享基本的属性和方法.

>每个节点都有nodeType属性，表示该节点的类型。
>
>节点类型由定义在Node类型上的12个数值常量表示：
>
>❑ Node.ELEMENT_NODE（1） -- 元素节点
>
>❑ Node.ATTRIBUTE_NODE（2） -- 属性节点
>
>❑ Node.TEXT_NODE（3）-- 文档节点
>
>❑ Node.CDATA_SECTION_NODE（4）
>
>❑ Node.ENTITY_REFERENCE_NODE（5）
>
>❑ Node.ENTITY_NODE（6）
>
>❑ Node.PROCESSING_INSTRUCTION_NODE（7）
>
>❑ Node.COMMENT_NODE（8） -- 注释节点
>
>❑ Node.DOCUMENT_NODE（9）
>
>❑ Node.DOCUMENT_TYPE_NODE（10）
>
>❑ Node.DOCUMENT_FRAGMENT_NODE（11）
>
>❑ Node.NOTATION_NODE（12）

***

**获取元素节点打印出三个属性值**

比如有如下的一个`div`

~~~html
<div id="box" title="我是div属性"></div>
~~~

我们可以通过`id`获取这个元素标签,然后再输出他的这三个常用属性看看

```JavaScript
let box = document.getElementById("box");
console.log(box.nodeName +' | '+ box.nodeValue+' | '+box.nodeType);

// 输出 : DIV | null | 1
// 对应上面的,这个1确实就是表示div就是元素节点.
```



**获取属性节点打印出三个属性值**

获取一个元素节点的属性节点使用`attributes`
我们还是通过上面的`div`来举例

因为div有两个属性节点,所以这个集合长度为2,可以使用下标0,1来获取对应的元素节点.

```JavaScript
console.log(box.attributes[0]); //输出 id = "box"
console.log(box.attributes[1]); //输出 title="我是div属性"
```



同样输出三个node属性看一看

```JavaScript
let arrNode = box.attributes[0];
// 输出 id | box | 2
console.log(arrNode.nodeName +' | '+ arrNode.nodeValue+' | '+arrNode.nodeType);
```





**获取文本节点打印出三个属性值**

现在在上面的div中添加一些文本作为文本节点.

看上面的node类型我们能知道注释其实也是注释节点,所以也添加上去顺便讲讲.

```html
    <div id="box" title="我是div属性">
        balabalabala....
        <!-- Emm... -->
        <a> 我是a标签的文本 </a>
    </div>
```



同样获取文本节点的同样需要另外一个方法,`childNodes`

这个方法不光是单独获取文本,就是这个标签内的文本注释同时获取都被获取了.

*提一嘴,文本中空格也会被视为文本内容被获取*

```JavaScript
let textNode = box.childNodes[0];
console.log(textNode.nodeName +' | '+ textNode.nodeValue+' | '+textNode.nodeType);

let commentNode = box.childNodes[1];
console.log(commentNode.nodeName +' | '+ commentNode.nodeValue+' | '+commentNode.nodeType);

/* 输出结果如下:
#text | 
        balabalabala....
         | 3  
         
#comment |  Emm...  | 8
*/
```



这是正常获取,但是还有低下 a 标签啊

如果算上a标签,应该是元素有三个,我们看看a标签有没有被获取到.

接着来试试看看输出什么

```JavaScript
let test1Node = box.childNodes[2];
console.log(test1Node.nodeName +' | '+ test1Node.nodeValue+' | '+test1Node.nodeType);

let test2Node = box.childNodes[3];
console.log(test2Node.nodeName +' | '+ test2Node.nodeValue+' | '+test2Node.nodeType);

let test3Node = box.childNodes[4];
console.log(test3Node.nodeName +' | '+ test3Node.nodeValue+' | '+test3Node.nodeType);

/*
#text | 
         | 3
         
 A | null | 1
 
 #text | 
         | 3
*/
```


a标签同样是被获取到了,并且能够正常输出.

使用不符合实际的下标的时候,输出的就是`#text | 空白 | 3`
至于为啥,这个我也不知道,我就是试试...emm....



### 11.2 节点常用属性

#### a . childNodes

`childNodes`这个属性就使用得比较多.

就有`fistchild` 和 `lastchild`,这两个好理解

```JavaScript
fistchild  等价于  childNodes[0]
lastchild 等价于   childNode[lenght - 1]
```



#### b. parentNode

用来调用父级节点

#### c. nextSibling and previousSibling

用来调用当前节点的下一行的兄弟节点.

这个我试了一下,比较有点意思

先看代码一

```html
    <ul title = "ul 标签属性">
        <li title = "li标签属性"></li>
        <li></li>
        <li></li>
    </ul><div id="box" title="我是div属性">
        balabalabala....
        <!-- Emm... -->
        <a> 我是a标签的文本 </a>
    </div>
```

再看代码二

```html
    <ul title = "ul 标签属性">
        <li title = "li标签属性"></li>
        <li></li>
        <li></li>
    </ul>
	<div id="box" title="我是div属性">
        balabalabala....
        <!-- Emm... -->
        <a> 我是a标签的文本 </a>
    </div>
```



这两者看起来没啥区别,别忘了
在html中 , 空格也算作是文本内容.

```JavaScript
let ulNode = document.getElementsByTagName("ul")[0];
console.log(ulNode.nodeName);
console.log(ulNode.nextSibling.nodeName);
```

所以在代码一中,输出结果是

```
UL
#text
```

在代码二中,输出结果是

```
UL
DIV
```



当然既然`nextSibling`是下一个节点
`previousSibling`就是上一个节点了



#### d.节点获取然后使用的简单处理

就像上面那样,我们些代码为了可读性,不可能不使用回车和空格啊

但是回车和空格都会被获取到,所以得有一个办法去除掉那些的回车和空格.

有如下的一个div

```html
    <div class = "previous">我是上面的div</div>

    <div id="box1">
        <p>this is frist p</p>
        <p>this is second p</p>
    </div>
    <div class="box2">
        <p>this is frist p</p>
        <p>this is second p</p>
    </div>

    <div class = "sibling">我是下面的div</div>
```

***

*小提一嘴*

这里我获取的时候发现`getElementByClassName`和`getElementById`有些不一样

使用`getElementsByClassName`获取的对象,需要添加 [下标] 才可以常常使用

因为`getElementsByClassName`和`getElementsByTagName`都是返回一个集合

```JavaScript
let useNode1 = document.getElementById("box1");
console.log(useNode1.childNodes);

let useNode2 = document.getElementsByClassName("box2");
console.log(useNode2.childNodes);

let useNode3 = document.getElementsByClassName("box2");
console.log(useNode3[0].childNodes);

/* 输出结果
NodeList(5) [text, p, text, p, text]
undefined
NodeList(5) [text, p, text, p, text]
*/
```

***



回到正题 , 就拿box1举例,我们使用一个方法,把这个获取到的集合过滤一下.

```JavaScript
let box_nodes = document.getElementById("box1");
console.log(box_nodes.childNodes);

function screening(obj_nodes){
    let nodes = obj_nodes.childNodes;
    let arr = [];  //保存需要的
    for(let i=0;i<nodes.length;i++){
        if(nodes[i].nodeType === 1 ){
            arr.push(nodes[i]);
        }
    }
    return arr;
}
let result = screening(box_nodes);
console.log(result);

```



同样的我们使用`nextSibling`也会获取到空格文本
所以一样的思路,过滤掉找到的空格文本,知道找到一个原属标签.

```JavaScript
function get_next(param){
    let x = param.nextSibling;
    while(x && x.nodeType!== 1){
        x = x.nextSibling;
    }
    return x;
}
let result_2 = get_next(box_nodes);
console.log(result_2);

/*  输出结果:
    <div class="box2">
        <p>this is frist p</p>
        <p>this is second p</p>
    </div>

获取下一个标签,是直接把下个标签包含的标签也获取过来了.
*/
```



#### e.节点的增删改查

**创建节点**

```javascript
createElement()
```



插入节点

```JavaScript
appendChild()
insertBefore(newNode,node)
```



删除一个子节点,返回这个子节点的引用.

```JavaScript
removeChild()
```



**替换节点**

```JavaScript
replaceChild(newNode,node)
```



**创建文本节点**

```JavaScript
createTextNode()
```



这边提两个属性 `innerHTML`  和 `innerText`

`innerHTML` 不经可以显示插入的文本,还可以选软插入的标签

而`innerText`只能够将类容以字符串的格式显示出来

创建--插入--设置样式 的基本格式

```JavaScript
// 先获取一个节点,表示我们要在这里插入
let target = document.getElementsByClassName("box2")[0];
// 在DOM中创建一个节点,并表明元素标签是 p
let new_node = document.createElement('p');
// 插入目标标签的里面去了
target.appendChild(new_node);
// setAttribute可以设置元素标签属性,可以通过属性设置样式.
new_node.setAttribute("class","new_p");

// 创建文本节点,插入p标签中
// let textnode = document.createTextNode("我就是我,不一样的烟火");
// new_node.appendChild(textnode);
// 使用innerHTML简化
// new_node.innerHTML = "我就是我,不一样的烟火";
//再次插入会覆盖点前面的文本内容
// new_node.innerHTML = "Emm..";
// 文本和标签都可以渲染出来
new_node.innerHTML = '你就是<a href="#">我的温柔</a>';

// 我们设置p标签文字的颜色
new_node.style.color = "#990033";

// 页面中已经再使用了,但是内存中依旧保存着这个new_node
// 将这个 new_node 等于 null 就是在内存中释放掉.
// 释放对象应该放在最后
new_node = null;
```



使用 `insertBefore` 会和上面的添加方式有点不一样

比如我们需要再A节点的前方插入一个节点B
要先获取A节点的父元素节点BigA,然后`BigA.insertBefore(A,B)`;

```JavaScript
let newNodeOne = document.createElement('span');
let newNodeTwo = document.createElement('span');


let ObjOne = document.getElementsByClassName('box2')[0];
newNodeOne.setAttribute('class','one')
newNodeOne.innerHTML = '<a herf = "#">arcane.con</a>';
ObjOne.appendChild(newNodeOne);

let ObjTwo = document.getElementById('box1');
let parent_box = ObjTwo.parentNode;
newNodeTwo.innerHTML = "我就是我,颜色不一样的花火";
parent_box.insertBefore(newNodeTwo,ObjTwo);
```



**删除节点**

知道父节点的情况下,定位父元素然后删除节点

```JavaScript
let p1 = ObjOne.getElementsByTagName('p')[0];
let guilai = ObjOne.removeChild(p1);
```



不知道父节点的情况加,获取父级元素然后再删除自身

```JavaScript
let p1 = document.getElementsByTagName('p')[0];
let guilai = p1.parentNode.removeChild(p1);
```



移除一个元素的所有节点

```JavaScript
// ObjTwo为上文html中box1的对象.
while(ObjTwo.firstChild){
    ObjTwo.removeChild(ObjTwo.firstChild);
}
```



替换一个节点

```JavaScript
ObjOne.replaceChild(newNodeOne,ObjOne.getElementsByTagName('p')[0]);
```



总结:

1. 后面带有`child`的`api`基本都是要获取父级节点,然后父级节点调用.
2. 使用`insertHTML`添加内容更加便捷一点





### 11.3 style 属性

每个标签属性都有一个`style`的一个属性.

```JavaScript
let op = document.getElementById('box1')
console.log(op.style);
```

如果你输出一下这个`style`会发现输出的是一个样式属性的集合,里面包含了`style`中所有的`行内样式`。



使用方法也很简单
下面这种获取到的方式添加样式是直接加入标签的行内。

优先级会比使用`style`或者外部链接`css文件`中使用类名调用的这种方法的优先级要更高一些.

```JavaScript
let op = document.getElementById('box1')
console.log(op.style);
op.style.color = 'white';
op.style.backgroundColor = 'black';
op.style.width = '300px';
op.style.height = '300px';
```



### 11.4 事件

JavaScript 常用的事件

![image-20220311085242600](https://arcane-yaogui.oss-cn-beijing.aliyuncs.com/PHOTOS/image-20220311085242600.png)





**onclick事件**

1.直接在标签中使用`onclick`

```JavaScript
<div id="box1" onclick="add()">  </div>

function add(){  alert("触发事件"); }
```



2.获取这个标签然后添加事件

```JavaScript
let op = document.getElementById('box1')
op.onclick = function(){ alert("触发事件"); }
```



**onmouseover**  and **onmouseout**

下面这个简答你都案例可以知道这两个事件的作用.

```JavaScript
let pram= document.getElementsByClassName('previous')[0];
pram.style.width = '300px';
pram.style.height  = '300px';
pram.style.backgroundColor = 'black';

pram.onmouseover = function () {
    this.style.backgroundColor = "red";
}

pram.onmouseout = function (){
    this.style.backgroundColor = "green";
}
```



**onselect**   **onchange**   **oninput**

简单写一个表单,用来试试这三个事件

```html
<form action="">
        <p>
            <label>用户账号:</label>
            <input type="text" name="user" id="user">
        </p>

        <p>
            <label>用户密码:</label>
            <input type="password" name="pwd" id="pwd">
        </p>

        <textarea cols="30" rows="10">balabalabala...</textarea>

        <br/>

        <button>提交</button>
    </form>
```





```JavaScript
let username = document.getElementById('user');
let newNode = document.createElement('span');

// 光标聚焦
username.onfocus = ()=>{
    newNode.innerHTML = "请输入用户名";
    newNode.setAttribute('class','span_text')
    newNode.style.color = 'red';
    newNode.style.fontSize = '15px';
    username.parentNode.appendChild(newNode);
}

// 光标失焦
username.onblur = ()=>{
    username.parentNode.removeChild(newNode);
}

let textArea = document.getElementsByTagName('textarea')[0];

textArea.onselect = ()=>{
    alert("请不要复制类容!!!");
}
textArea.onchange = ()=>{
    console.log("textArea内容被改变了");
    alert("请不要改变类容");
}
textArea.oninput = ()=>{
    console.log("textArea内容被修改中");
    // 实时获取被修改的值
    console.log(textArea.value); 
}
```





##### window对象中的窗口加载事件

有时候`script`标签放在`head`标签里面
但是如果获取某个标签,但是那个标签还没被执行,也就是js脚本再前面执行就回报错.

`window`中有个`onload`方法可以等待静态资源加载完成之后再执行脚本.

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <script>
        window.onload = function(){
            let p_value = document.getElementsByTagName('p')[0];
            p_value.onclick = function(){
                this.innerHTML = "不一样的烟火";
            }
        }
    </script>
    
</head>

<body>
    <p>我就是我</p>
</body>
```





但是window.onload有一个覆盖现象
下面的`window.onload`会覆盖掉上面的`window.onload`;

```javascript
window.onload = function(){
            let p_value = document.getElementsByTagName('p')[0];
            p_value.onclick = function(){
                this.innerHTML = "不一样的烟火";
            }
        }

window.onload = function(){
            let p_value = document.getElementsByTagName('p')[0];
            p_value.onclick = function(){
                this.innerHTML = "我是咸鱼";
            }
        }
```

