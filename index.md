## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/enjoyxiaohaiqw/blogText/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1

## 教程

http://es6.ruanyifeng.com

在线工具：http://babeljs.cn/repl/

## 工具

npm install -g babel-cli
// 最新转码规则
npm install --save-dev babel-preset-latest

### 编写.babelrc
{
	"presets": [
	  "latest"
	],
	"plugins": []
}

### 命令行命令

// 转码结果输出到标准输出
babel example.js

// 转码结果写入一个文件
--out-file 或 -o 参数指定输出文件
babel example.js --out-file compiled.js
或者
babel example.js -o compiled.js

// 整个目录转码
--out-dir 或 -d 参数指定输出目录
babel src --out-dir lib
或者
babel src -d lib

-s 参数生成source map文件
babel src -d lib -s 

### babel-register

babel-register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用Babel进行转码。

npm install --save-dev babel-register

使用时，必须首先加载babel-register。

require("babel-register");
require("./index.js");


### api

如果某些代码需要调用 Babel 的 API 进行转码，就要使用babel-core模块。

npm install babel-core --save

	var babel = require('babel-core');
	// 字符串转码
	babel.transform('code();', options);
	// => { code, map, ast }
	// 文件转码（异步）
	babel.transformFile('filename.js', options, function(err, result) {
	  result; // => { code, map, ast }
	});
	// 文件转码（同步）
	babel.transformFileSync('filename.js', options);
	// => { code, map, ast }
	// Babel AST转码
	babel.transformFromAst(ast, code, options);
	// => { code, map, ast }



## ES6

### let & const

let 变量名 = 值 //声明一个变量

特点：

+ let声明的变量只在当前块内有效
+ 不允许重复声明
+ 在for循环里，声明的let i 只在本轮循环有效
+ 不存在变量提升（声明后再使用）
+ ES6明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。
+ 声明变量前使用 typeof 会报错

const 常量 = 值 // 声明一个常量

特点：

+ const 声明的常量，不允许重新复制（对象与数组元素可以）

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。
对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，
因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，
保存的只是一个指针，const只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。

#### 顶层对象属性

顶层对象，在浏览器环境指的是window对象，在Node指的是global对象。ES5之中，顶层对象的属性与全局变量是等价的。
ES6为了改变这一点，一方面规定，为了保持兼容性，var命令和function命令声明的全局变量，依旧是顶层对象的属性；
另一方面规定，let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性


### 变量的解构与赋值

#### 数组解构

匹配模式，未匹配上的会以undefined返回

let [vara, varb, varc, ...] = [1, 2, 3, ...]

默认值：

let [vara = 'default'] = []
let [vara = 'default'] = [null] // vara = null
注意，ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。

#### 对象解构

let {key1, key2, key3, ...} = {key1: 'xxx', key2: 'xxx', ...}

如果键不对应择返回undefined，如果需要指定值则：

let {name: username} = {name: 'xxxx'} //usernmae = 'xxx'

也可以设置默认值：

let {title='default'} = {} // title = 'default'

定义后再解构

let a
({a} = {a: 'x'})

#### 字符串解构

let [a,b,c,...] = 'hello'


### 字符串模板

var str = `this is tpl ${n}`


### 数值扩展

ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。
ES6 在Number对象上，新提供了Number.isFinite()和Number.isNaN()两个方法。

Math.trunc(num) //去除小数部分返回整数
Math.sign() //方法用来判断一个数到底是正数、负数、还是零。
	参数为正数，返回+1；
	参数为负数，返回-1；
	参数为0，返回0；
	参数为-0，返回-0;
	其他值，返回NaN。
ES2016 新增了一个指数运算符（**）。2**3 

### 函数扩展

函数默认参数
function fun(a, b = 12) {}

rest参数
function fun(a, ...args) {} //args为数组，接收剩余参数

箭头函数
var fun = args => args //同 var fun = function (args) {return args}
var fun = ({a,b}) => a + b

注：
	1、函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
	2、不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
	3、不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
	4、不可以使用yield命令，因此箭头函数不能用作 Generator 函数。


### 对象扩展

var attr = 'xxx'
var obj = {attr} //{attr: 'xxx'}

var obj = {
	fun () {

	},
	[funName] () {}//funName 是一个变量
}


扩展运算 

扩展运算符（...）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。
var obj = {a: 'a', b: 'b'}
var obj2 = {...obj} //{a: 'a', b: 'b'}


Object.assign()//合并对象，将源对象（source）的所有可枚举属性，复制到目标对象（target）用在合并对象或者对象默认值,浅拷贝
Object.getOwnPropertyDescriptor(obj, 'foo') //获取对象的可枚举信息
Object.setPrototypeOf()//设置对象__proto__
Object.getPrototypeOf()

注：方法实行的是浅拷贝，而不是深拷贝。


### Symbol

	
它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

Symbol 作为属性名，该属性不会出现在for...in、for...of循环中，也不会被Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回。


Object.getOwnPropertySymbols(obj) //方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。
Symbol.for('foo') //返回symbol 如果之前初始化过此字符串，则直接返回，否则新建



### Set & Map

#### Set

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

var s = new Set() //实例化一个set
s.add(el)// 增加一个元素，类似于push,Set 结构不会添加重复的值

Set.prototype.size 			//返回成员总数
Set.prototype.add(value)	//添加某个值，返回Set结构本身。
Set.prototype.delete(value)	//删除某个值，返回一个布尔值，表示删除是否成功。
Set.prototype.has(value)	//返回一个布尔值，表示该值是否为Set的成员。
Set.prototype.clear()		//清除所有成员，没有返回值。
Set.prototype.keys() 		//返回键名的遍历器
Set.prototype.values() 		//返回键值的遍历器
Set.prototype.entries() 	//返回键值对的遍历器
Set.prototype.forEach((value, key) => {}) 	//使用回调函数遍历每个成员


1、set内部判断两个值是 === 关系才会去重
2、Array.from方法可以把set转成数组,或者[...set]

set一些例子

// 并集
let union = new Set([...a, ...b]);
// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// 差集
let difference = new Set([...a].filter(x => !b.has(x)));

#### WeakSet

WeakSet 结构与 Set 类似，也是不重复的值的集合，不同的是WeakSet成员只能是对象。

WeakSet.prototype.add(value)	//向 WeakSet 实例添加一个新成员。
WeakSet.prototype.delete(value)	//清除 WeakSet 实例的指定成员。
WeakSet.prototype.has(value)	//返回一个布尔值，表示某个值是否在 

注：
	1、WeakSet 不能遍历，是因为成员都是弱引用，随时可能消失

#### Map

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

m = new Map()

Map.prototype.size //返回成员总数
Map.prototype.set(key, val)//添加成员
Map.prototype.get(key)
Map.prototype.has(key)
Map.prototype.delete(key)
Map.prototype.clear()
Map.prototype.keys()	//返回键名的遍历器。
Map.prototype.values()	//返回键值的遍历器。
Map.prototype.entries()	//返回所有成员的遍历器。
Map.prototype.forEach()	//遍历 Map 的所有成员。

#### WeakMap

WeakMap结构与Map结构类似，也是用于生成键值对的集合。
WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。


### Proxy

ES6 原生提供 Proxy 构造函数，用来生成 Proxy 实例。作用，用来拦截对象操作

proxy = new Proxy(target, handler) //代理一个对象target

handler是一个对象，可以拦截的动作如下：
	get(target, propKey, receiver)
	set(target, propKey, value, receiver)
	has(target, propKey)
	deleteProperty(target, propKey)
	ownKeys(target)
	getOwnPropertyDescriptor(target, propKey)
	defineProperty(target, propKey, propDesc)
	preventExtensions(target)
	getPrototypeOf(target)
	setPrototypeOf(target, proto)
	apply(target, object, args)
	construct(target, args)

例子：

new Proxy(target, {
	get (target, propKey, receiver) {}
})


### Reflect


Reflect.apply(target,thisArg,args)
Reflect.construct(target,args)
Reflect.get(target,name,receiver)
Reflect.set(target,name,value,receiver)
Reflect.defineProperty(target,name,desc)
Reflect.deleteProperty(target,name)
Reflect.has(target,name)
Reflect.ownKeys(target)
Reflect.isExtensible(target)
Reflect.preventExtensions(target)
Reflect.getOwnPropertyDescriptor(target, name)
Reflect.getPrototypeOf(target)
Reflect.setPrototypeOf(target, prototype)

### Promise


### iterator遍历器

凡是部署了Symbol.iterator属性的数据结构，就称为部署了遍历器接口。

原生具备 Iterator 接口的数据结构如下。
    Array
    Map
    Set
    String
    TypedArray
    函数的 arguments 对象
    NodeList 对象
 

遍历器方法

  next
  return
  throw


例子：

let arr = ['a', 'b', 'c'];
let iter = arr[Symbol.iterator]();

iter.next() // { value: 'a', done: false }
iter.next() // { value: 'b', done: false }
iter.next() // { value: 'c', done: false }
iter.next() // { value: undefined, done: true }


### Generator 

function *task () {
  yield run()
  yield say()
  return end()
}


调用 Generator 函数，返回一个iterator遍历器对象，代表 Generator 函数的内部指针。

yield表达式如果用在另一个表达式之中，必须放在圆括号里面。
yield表达式用作函数参数或放在赋值表达式的右边，可以不加括号。


### async

async function fun() {
  var result = await timeout()
  return 'result'
}
fun().then(val => console.log(val))// result

注：

	+ async函数返回一个 Promise 对象。
    + async函数中 throw new Error() 会导致返回的 Promise 对象变为reject状态。
	+ async函数内部return语句返回的值，会成为then方法回调函数的参数。
	+ await 后面跟的是一个Promise对象，Promise对象执行完才往下执行，如果不是，会被转成一个立即resolve
	+ await 后的Promise结果返回
	+ 只要一个await语句后面的 Promise 变为reject，那么整个async函数都会中断执行。
 	+ 如果await后面的异步操作出错，那么等同于async函数返回的 Promise 对象被reject。
 	+ await命令只能用在async函数之中，如果用在普通函数，就会报错。

    + await命令错误处理通过 try {} catch () {}


    // async/await延迟
    function sleep(t) {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve()
        }, t || 15)
      })
    } 

并发执行：getFoo和getBar都是同时触发，这样就会缩短程序的执行时间。
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;



### class

class Obj extends Parent {
  // 构造函数
  constructor() {
  	// super()
  	this.attr = ''
  }
  // 属性
  attr = ''
  // 静态属性
  static attr = ''
  // prototype 方法(不可枚举)
  fun () {}
  // Generator 函数
  * fun () {}
  // 静态方法
  static fun () {}
  // getter
  get attr () {}
  // setter
  set attr (val) {}
}
// 静态属性
Obj.staticAttr 

new.target //返回当前类，如果类不是通过new调用则值为undefined

if (new.target !== undefined) {
	this.name = name;
} else {
	throw new Error('必须使用new生成实例');
}

注：
1、类和模块的内部，默认就是严格模式
2、es6不提供类的私有方法，需要自己实现
3、静态方法不会被实例继承，父类的静态方法，可以被子类继承。
4、子类继承父类时，new.target返回子类


### Decorator

修饰器（Decorator）函数，用来修改类的行为。

function TestDecorator (data) {
    return function (target) {
        target.test = data
    }
}

@TestDecorator(true) //使用TestDecorator修饰器修饰MyTestableClass类
class MyTestableClass {}

注：
    + 修饰器对类的行为的改变，是代码编译时发生的，而不是在运行时
	+ 修饰器只能用于类和类的方法，不能用于函数，因为存在函数提升。

### Module 

ES6 模块与 CommonJS 模块的差异

CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用，只读，不能重新赋值。
CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

CommonJS 加载的是一个对象（即module.exports属性），该对象只有在脚本运行完才会生成。
而 ES6 模块不是对象，它的对外接口只是一种静态定义，在代码静态解析阶段就会生成。



module.exports = xxx 
同
export default xxx

import fs from 'fs'
import {default as fs} from 'fs'
import * as fs from 'fs'
import {readFile} from 'fs'
import {readFile as read} from 'fs'
import fs, {readFile} from 'fs'

export default obj  	 // import obj from '' 这种导出方式不能import解构，同export {obj as default}
export 修饰符 name = val // import * as obj form '' // import {name} from '' 
export {readFile, read}  // import * as obj form '' // import {name} from ''
export * from 'fs'


Object.defineProperty(obj, "prop", {
    configurable: false, // 当且仅当该属性的 configurable 键值为 true 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除。
    enumerable: false, // 当且仅当该属性的 enumerable 键值为 true 时，该属性才会出现在对象的枚举属性中。
    writable: false, // 表示是否可以修改属性的值。
    value: "", // 该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。
  });
  
  // 这样设置之后，prop属性就变成了不能删除、不可重新修改特性、不可枚举、不能修改的属性值的属性。


  function myFreeze(obj) {
    // 判断参数是否为Object类型
    if (obj instanceof Object) {
      for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
          Object.defineProperty(obj, key, {
            writable: false, // 设置只读
          });
          Object.seal(obj); // 封闭对象
        }
      }
    }
    return obj;
  }

  const obj = { name: "yd" };
Object.getOwnPropertyDescriptors(obj);
/* 
{
    name:{
        configurable: true
        enumerable: true
        value: "yd"
        writable: true
    }
}
*/

Object.seal(obj);
Object.getOwnPropertyDescriptors(obj);
/* 
{
    name:{
        configurable: false
        enumerable: true
        value: "yd"
        writable: true
    }
}
*/

// 这时如果再去配置就失效了
Object.defineProperty(obj, "name", {
  writable: false,
});
Object.getOwnPropertyDescriptors(obj);
/* 
{
    name:{
        configurable: false
        enumerable: true
        value: "yd"
        writable: true
    }
}
*/
// writable 已经不可以配置了


## Header 2


// 服务器代码
const WebSocket = require('ws');

// 模块 立即执行函数
;(function(WebSocket) {
  // 创建服务器 运行在8000端口
  const server = new WebSocket.Server({
    port: 8000
  });

  // 初始化
  const init = () => {
    bindEvent();
  };

  // 事件处理函数的绑定
  function bindEvent() {
    server.on('open', handleOpen);
    server.on('close', handleClose);
    server.on('error', handleError);
    server.on('connection', handleConnection);
  }

  function handleOpen() {
    console.log('backend: WebSocket server open');
  }

  function handleClose() {
    console.log('backend: WebSocket server close');
  }

  function handleError() {
    console.log('backend: WebSocket server error');
  }

  function handleConnection(ws) {
    console.log('backend: WebSocket server connection');
    
    // 监听用户发送消息的事件
    ws.on('message', handleIncomingMessage);
  }

  function handleIncomingMessage(incomingMessage) {
    console.log(server.clients.forEach(client => {
      client.send(incomingMessage);
    }));
  }

  init();
})(WebSocket);
### Header 3

<template>
  <div>
    <h1>首页</h1>
    <input type="text" v-model="message" />
    <button @click="sendMessage">发送消息</button>
    <ul v-if="messageList.length > 0">
      <li v-for="item in messageList" :key="item.id">
        <p>
          <span>{{ item.user }}</span> |
          <span>{{ new Date(item.dateTime) }}</span>
        </p>

        <p>消息：{{ item.message }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
// 检查是否有username 1
// 服务器运行的地址
// 协议 http(s) ws(s)
// WebSocket实例
const ws = new WebSocket('ws://localhost:8000');

export default {
  data() {
    return {
      // 登录后的用户名
      username: '',
      // 待发送的消息
      message: '',
      // 所有消息
      messageList: [],
    };
  },
  methods: {
    sendMessage() {
      const message = this.message;

      if (!message.trim().length) {
        return;
      }

      // 发送消息的格式
      // id
      // user     用户名
      // dataTime 发送的时间
      // message  消息
      const messageData = {
        id: Math.random(),
        user: this.username,
        dateTime: new Date().getTime(),
        message: this.message,
      };

      // 发送消息 WebSocket
      // 浏览器 <-> 服务器  格式  String？Object？Number？
      // JSON字符串 6
      ws.send(JSON.stringify(messageData));

      this.message = '';
    },
    handleWsOpen() {
      console.log('frontend: WebSocket open');
    },
    handleWsClose() {
      console.log('frontend: WebSocket close');
    },
    handleWsError() {
      console.log('frontend: WebSocket error');
    },
    handleWsMessage(e) {
      console.log('frontend: WebSocket message', e.data);
      const message = JSON.parse(e.data);
      console.log('message', message);
      this.messageList.push(message);
    },
  },
  mounted() {
    this.username = localStorage.getItem('username');

    if (!this.username) {
      // 如果没有登录，我们应该跳转到登录页面 login
      this.$router.push('/login');
      return;
    }

    ws.addEventListener('open', this.handleWsOpen.bind(this));
    ws.addEventListener('close', this.handleWsClose.bind(this));
    ws.addEventListener('error', this.handleWsError.bind(this));
    ws.addEventListener('message', this.handleWsMessage.bind(this));
  },
};
</script>

<style></style>

Array.prototype.reduce=function(fn,initialValue){
    let index = 0;
    if (!initialValue) {
        initialValue=this[0];
        index++
    }
    while (index<this.length) {
        initialValue=fn(initialValue,this[index],index,this)
        index++
    }
    return initialValue
}

HTML/CSS/JS：精通h5、css3、es3/es5/es6各项特性
TS：熟悉type、interface、访问修饰符、高阶泛型
Vue：熟悉Vue1/2/3底层实现原理，包括但不限于各API、生命周期函数、数据绑定与虚拟dom、模板编译及编译时优化
React：熟悉虚拟dom及其diff算法、fiber原理、hooks底层原理
Angular：熟悉脏值检查原理及rxjs
网络：熟悉网络协议模型及TCP/IP协议，包括TCP/IP协议报文、滑动窗口、拥塞控制、TCP慢启动、握手挥手过程及状态码，了解UDP原理，熟悉http1.0/1.1/2/3及其差异，熟悉https原理，熟悉http各状态码
浏览器：熟悉底层渲染原理，绘制与合成原理，ignition/turbofan编译器对js的优化原理，gc机制，了解v8对js底层数据结构的实现原理
缓存：熟悉强缓存与协商缓存原理
跨域：了解原理及常见处理手段，熟悉oAuth与jwtToken对登录的处理手段
Web安全：熟悉xss/csrf/sql注入原理，及前后端防御手段
Node：了解libuv架构，事件回调模型。熟悉express、koa、egg等框架，熟悉洋葱模型
工程化：熟悉webpack、rollup、vite、snowpack原理及优化手段，熟悉docker、k8s、jenkins，熟悉运维部署手段及监控报警方案
跨平台：熟悉electron、flutter、weex、react native、ionic等跨端框架，熟悉小程序及其实现原理，精通快应用原理并负责其引擎核心模块编写
性能优化：熟悉performance对应api及首屏检测方式，熟悉雅虎军规，了解端侧预渲染、SSR、snapshot、资源数据预缓存等方案及适用场景
流媒体：熟悉h264/h265视频格式及其编解码手段，熟悉ffmpeg、broadway、flv、videojs等音视频处理方案
图形学：熟悉webGL及three.js，熟悉OpenGL原理，包括bezier曲线曲面、b样条曲线曲面、phong光照模型及其数学公式
AI：熟悉机器学习及深度学习，熟悉SVM（包括linear SVM与kernel SVM）、卷积神经网络、空间金字塔池化等常见分类学习手段，并能通过数学手段对算法进行优化
数据库：熟悉sql基本语法、了解mongoDB、redis等nosql数据库、了解索引聚合等基础优化手段
计算机基础：熟悉数据结构、算法、编译原理、软件工程、设计模式、操作系统等相关知识
后台语言：熟悉C/C++，了解java/php/python
面向未来：了解webAssembly、serverless

/*
 * JS中的数据类型：
 *    + 原始值类型
 *      + number : NaN「不是一个有效数字」、Infinity「无穷大的值」
 *      + string : 基于 单引号/双引号/反引号「模板字符串」 包起来的都是字符串
 *      + boolean : true/false
 *      + null
 *      + undefined
 *      + symbol : 唯一值
 *      + bigint : 大数
 *    + 对象类型 
 *      + 标准普通对象 object
 *      + 标准特殊对象 Array/RegExp/Date/Error/Math/ArrayBuffer/DataView/Set/Map...
 *      + 非标准特殊对象 Number/String/Boolean/Symbol/BigInt... 基于构造函数「或者Object」创在出来的原始值对象类型的格式信息，类型属于对象类型
 *      + 可调用对象「实现了call方法」 function
 */

// 数据类型检测
//  + typeof 运算符
//  + instanceof 「本意：检测实例是否属于某个类」
//  + constructor「本意：获取构造函数」
//  + Object.prototype.toString.call([value]) 检测数据类型的
//  ------
//  + Array.isArray([value]) 检测值是否为数组
// =======
// typeof [value]
//   + 返回[value]所属类型的字符串，例如：'number'/'string'...
//   + 不能检测null   typeof null->'object'
//   + 除可调用对象「函数」会返回'function'「不论是箭头函数、还是构造函数、还是生成器函数、在以及普通函数等，都返回的'function'」，其余的对象数据值返回都是'object'；
//   + 检测一个未被声明的变量不会报错，返回'undefined'
//   -------
//   GetValue(val)「C++内部提供的方法」，按照值存储的二进制进行检测的
//     + 对象 000 -> 实现call，则返回‘function’，没实现call返回‘object’
//     + null 000000
//     + undefined  -2^30
//     + 数字 -> 整数1  浮点数010
//     + 字符串 100
//     + 布尔 110
//     + ......
//   -------
//   typeof 检测数据类型还是很快的，检测原始值类型『除了null』还是很准确的

/* 
// 字面量:原始值
let n = 10;
// 构造函数:对象值
let m = new Number(10);
let x = Object(10);
// new Symbol() Uncaught TypeError:Symbol is not a constructor
// new BigInt() Uncaught TypeError: BigInt is not a constructor 
*/

/* 
// 最大安全数字：9007199254740991，超过这个数字进行运算就不准确了
// console.log(Number.MAX_SAFE_INTEGER, Number.MIN_SAFE_INTEGER);
// 问题:服务器中有 longInt 长整型这种值，如果把这样的值返回给客户端，则客户端无法进行有效的处理「一般服务都是以字符串返回，但是字符串进行计算还是需要转换为数字才可以，还是不准确」
BigInt('9007199254740992134') -> 9007199254740992134n
9007199254740992134n + 1n
(9007199254740992133n).toString() -> "9007199254740992133" 
*/

/* 
let n = Symbol('AA');
let m = Symbol('AA');
console.log(n === m); //->false 

// 1.对象的唯一属性
let key = Symbol();
let obj = {
    [key]: 100
};
console.log(obj[key]);
let arr = Object.getOwnPropertySymbols(obj);
arr.forEach(item => {
    console.log(obj[item]);
});

// 2.宏观管理标识：保证标志唯一性（vuex/redux）

// 3.底层原理
//   Symbol.hasInstance
//   Symbol.iterator
//   Symbol.toPrimitive
//   Symbol.toStringTag
//   ......
*/

/* 
if (NaN === NaN) {
    // 不相等的：所以不能基于“是否等于NaN”来检测值是否为有效数字
    // isNaN([value])：不论[value]啥类型，默认隐式转换为数字类型「Number([value])」，再校验是否为有效数字，如果是有效数字，返回false，不是有效数字才返回true
    // Object.is(NaN,NaN)：true 「不兼容IE（Edge除外）」
} 
*/

/*
 * 把其它类型「原始值」转换为对象：Object([value])
 *  
 * 把其它类型转换为数字
 *   + Number([value])
 *     + 一般用于隐式转换「数学运算、isNaN、==比较...」
 *     + 字符串->数字  空字符串变为0  字符串中只要出现非有效数字字符结果就是NaN
 *     + 布尔->数字  true变为1  false变为0
 *     + null->0
 *     + undefined->NaN
 *     + Symbol->报错
 *     + BigInt->正常转换
 *     + 对象遵循 Symbol.toPrimitive/valueOf/toString/Number
 * 
 *   + parseInt/parseFloat([value])
 *     + 首先会把[value]变为字符串，从字符串左侧第一个字符开始查找，直到找到一个非有效数字字符为止，把找到的结果转换为数字，一个都没找到，结果就是NaN「parseFloat多识别一个小数点」
 *   + ...
 * 
 * 把其它类型转换为字符串
 *   规则：原始值转换是直接用引号包起来「bigint会去除n」；除对象转换为字符串是比较特殊的；
 *   + toString「排除Object.prototype.toString{检测数据类型}」
 *   + 字符串/模板字符串拼接「“+”在JS中除了数学运算还有字符串拼接{但是其它运算符一般都是数学运算}」
 *   + ...
 * 
 * 把其它类型转换为布尔
 *   规则：只有“0、NaN、null、undefined、空字符串”会变为false，其余都是转换为true
 *   + Boolean([value])
 *   + !![value]  
 *   + ![value] 转换为布尔类型取反
 *   + 条件判断  例如：if(1){}
 *   + A||B  A&&B
 *   + ...
 */

// console.log(1 + 1); //->2
// console.log(1 + '1'); //->'11'
// console.log(1 - '1'); //->0
// “+”左右两边，有一边出现了 字符串或者部分对象 则都是按照字符串拼接处理的


// CASE3:不是所有对象都是字符串拼接
//   规则：
//   + 先去调取对象的 Symbol.toPrimitive 属性值，如果没有这个属性
//   + 再去调取对象的 valueOf 获取原始值，如果不是原始值
//   + 再去调用对象的 toString 转换为字符串「如果是想转换为数字，则还会调用Number处理」
// console.log(10 + [10, 20]); //->"1010,20"
// console.log(10 + new Number(10)); //->20   new Number(10).valueOf()有原始值的
// console.log(+new Date()); //->1609941989208

/* let obj = {x: 10};
console.log(10 + obj); //->"10[object Object]" */

/* let obj = {
    x: 10,
    // obj[Symbol.toPrimitive] && valueOf && toString
    [Symbol.toPrimitive](hint) {
        // console.log(hint); //=>”default“、”string“、”number“
        return this.x;
    }
};
console.log(10 + obj); //->20 */


// CASE2:“+”有一边出现对象
// let n = 10;
// // {}+n -> 10  把左侧的{}当做代码块，不参与运算，运算的只有 +n
// // n+{} -> '10[object Object]' 字符串拼接

// CASE1:“+”只有一边
// let n = '10';
// console.log(+n); //10 ->转换为数字
// console.log(++n); //11 ->转换为数字然后累加1
// console.log(n++); //11 ->转换为数字然后累加1
// i++ 和 i=i+1 以及 i+=1  三个是否一样？
//   + i=i+1 & i+=1 是一样的
//   + i++一定返回的是数字 但是i+=1就不一定了，有可能是字符串拼接
// let i = 10;
// // console.log(5 + (++i)); //先i累加1，累加后的结果运算  16 i->11
// // console.log(5 + (i++)); //先运算 再累加1  15 i->11


// console.log(!![]); //->true
// console.log(!!-1); //->true

// src/utils/validates.js

/* 姓名校验 由2-10位汉字组成 */
exportfunction validateUsername(str) {
    const reg = /^[\u4e00-\u9fa5]{2,10}$/
    return reg.test(str)
}

/* 手机号校验 由以1开头的11位数字组成  */
exportfunction validateMobile(str) {
    const reg = /^1\d{10}$/
    return reg.test(str)
}

/* 邮箱校验 */
exportfunction validateEmail(str) {
    const reg = /^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/
    return reg.test(str)
}


前端
前端框架使用Vue+Element UI
1. 使用vue-cli3搭建环境
2. 安装Element UI
3.  main.js
import Vue from 'vue'
import App from './App.vue'
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
Vue.use(ElementUI);
Vue.config.productionTip = false
new Vue({
  render: h => h(App)
}).$mount('#app')
上传组件：
1. 上传、恢复、暂停暂停按钮
2. hash计算进度
3. 上传文件总进度
<template>
  <div id="app">
    <div>
      <input
        type="file"
        :disabled="status !== Status.wait"
        @change="handleFileChange"
      />
      <el-button @click="handleUpload" :disabled="uploadDisabled"
        >上传</el-button
      >
      <el-button @click="handleResume" v-if="status === Status.pause"
        >恢复</el-button
      >
      <el-button
        v-else
        :disabled="status !== Status.uploading || !container.hash"
        @click="handlePause"
        >暂停</el-button
      >
    </div>
    <div>
      <div>计算文件 hash</div>
      <el-progress :percentage="hashPercentage"></el-progress>
      <div>总进度</div>
      <el-progress :percentage="fakeUploadPercentage"></el-progress>
    </div>
    <el-table :data="data">
      <el-table-column
        prop="hash"
        label="切片hash"
        align="center"
      ></el-table-column>
      <el-table-column label="大小(KB)" align="center" width="120">
        <template v-slot="{ row }">
          {{ row.size | transformByte }}
        </template>
      </el-table-column>
      <el-table-column label="进度" align="center">
        <template v-slot="{ row }">
          <el-progress
            :percentage="row.percentage"
            color="#909399"
          ></el-progress>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
文件上传和断点续传逻辑
1. 核心是Blob.prototype.slice 方法，将源文件切成多个切片
2. 根据切片内容生成hash，此处用到的是spark-md5.js，因为解析切片内容比较耗时，所以开辟了WebWorker线程来处理hash的生成，在处理切片hash的时候，还与主线程进行通信返回进度。
3.  向服务器发请求，检验文件切片是否上传,返回是否需要继续上传和已上传列表（断点续传核心）。
4. 利用http 的可并发性，同时上传多个切片，减少上传时间
5. 切片上传完成，给服务器发送合并切片请求
• 常量和基础属性
<script>
 //单个切片大小
const SIZE = 10*1024*1024;//10MB
//状态常量
const Status = {
  wait: "wait",
  pause: "pause",
  uploading: "uploading"
};
export default {
   name: "App",
   filters: {
    transformByte(val) {
      return Number((val / 1024).toFixed(0));
    }
  },
    data() {
    return {
      Status,
      container: { //保存文件信息
        file: null,
        hash: "",//所有切片hash
        worker: null
      },
      hashPercentage:0,//hash进度百分比
      data: [],//保存所有切片信息
      requestList: [],//请求列表
      status: Status.wait,//状态，默认为等待
      fakeUploadPercentage: 0//文件上传总进度
    };
  },
}
</script>
• 计算属性、watch
computed: {
  //上传按钮不可用
    uploadDisabled() {
      return (
        !this.container.file ||
        [Status.pause, Status.uploading].includes(this.status)
      );
    },
      //下载进度百分比
    uploadPercentage() {
      if (!this.container.file || !this.data.length) return 0;
      const loaded = this.data
        .map(item => item.size * item.percentage)
        .reduce((acc, cur) => acc + cur);
      return parseInt((loaded / this.container.file.size).toFixed(2));
    }
  },
  watch: {
    //下载进度百分比
    uploadPercentage(now) {
      if (now > this.fakeUploadPercentage) {
        this.fakeUploadPercentage = now;
      }
    }
  },
• methods：三个按钮上面的方法定义
methods: {
  //中止处理函数
    handlePause() {
      this.status = Status.pause;
      this.resetData();
    },
    resetData() {
      //中止请求列表中的所有请求
      this.requestList.forEach(xhr => {
        if (xhr) {
          xhr.abort();
        }
      });
      this.requestList = [];
      if (this.container.worker) {
        this.container.worker.onmessage = null;
      }
    },
     //恢复处理函数
    async handleResume() {
      this.status = Status.uploading;
      //获取已经上传的文件名和hash
      const { uploadedList } = await this.verifyUpload(
        this.container.file.name,
        this.container.hash
      );
      await this.uploadChunks(unloadedList);
    },
    //file input change事件触发
    handleFileChange(e){
      const [file] = e.target.files;
      if(!file) return;
      this.resetData();
      Object.assign(this.$data,this.$options.data());
      this.container.file = file;
    }
}
• 核心：文件上传逻辑  切片=>hash=>校验=>批量上传
async handleUpload(){
      if(!this.container.file) return;
      this.status = Status.uploading;
      //生成文件切片
      const fileChunkList = this.createFileChunk(this.container.file);
      //根据切片列表计算切片hash
      this.container.hash = await this.calculateHash(fileChunkList);
      //检验文件切片是否上传,返回是否需要上传和已上传列表
      const { shouldUpload,uploadedList } = await this.verifyUpload(
        this.container.file.name,
        this.container.hash
      );
      //没有需要上传的文件切片
      if(!shouldUpload){
        this.$message.sucess('秒传：上传成功');
        this.status = Status.wait;
        return;
      }
      //根据文件列表生成每个切片的信息对象
      this.data = fileChunkList.map(({file},index)=>({
        fileHash : this.container.hash,
        index,
        hash: this.container.hash + '-'+index,
        chunk:file,
        size:file.size,
        percentage:uploadedList.includes(index)?100:0
      }));
      //上传文件切片
      await this.uploadChunks(uploadedList);
    },
• 文件核心逻辑实现：
生成文件切片：file.slice()
    // 生成文件切片 file.slice
    createFileChunk(file, size = SIZE) {
      const fileChunkList = [];
      let cur = 0;
      while (cur < file.size) {
        fileChunkList.push({ file: file.slice(cur, cur + size) });
        cur += size;
      }
      return fileChunkList;
    },
生成文件切片hash: webworker
    // 生成文件 hash（web-worker）
    calculateHash(fileChunkList) {
      return new Promise(resolve => {
        this.container.worker = new Worker("/hash.js");
        //与worker通信
        this.container.worker.postMessage({ fileChunkList });
        this.container.worker.onmessage = e => {
          const { percentage, hash } = e.data;
          this.hashPercentage = percentage;
          //返回总文件生成hash进度的百分比，如果切片hash全部生成，返回所有切片hash组成的对象
          if (hash) {
            resolve(hash);
          }
        };
      });
    },
hash.js：边计算边与主线程进行通信，返回hash计算进度
self.importScripts("/spark-md5.min.js"); // 导入脚本
// 生成文件 hash
self.onmessage = e => {
  const { fileChunkList } = e.data;
  const spark = new self.SparkMD5.ArrayBuffer();
  let percentage = 0;
  let count = 0;
  const loadNext = index => {
    const reader = new FileReader();//异步读取文件，在webworker中使用
    reader.readAsArrayBuffer(fileChunkList[index].file);//读取文件完成后，属性result保存着二进制数据对象
    //文件读取完成后触发
    reader.onload = e => {
      //递归计数器
      count++;
      spark.append(e.target.result);//append ArrayBuffer数据
      if (count === fileChunkList.length) {
        self.postMessage({
          percentage: 100,
          hash: spark.end()//完成hash
        });
        self.close();//关闭 Worker 线程。
      } else {
        percentage += 100 / fileChunkList.length;
        self.postMessage({
          percentage
        });
        loadNext(count);//递归继续
      }
    };
  };
  loadNext(0);
};
断点续传核心：文件切片完成之后，向服务器发请求检验文件切片是否已经上传
    async verifyUpload(filename,fileHash){
      const { data } = await this.request({
        url:'http://localhost:3000/verify',//验证接口
        headers:{
          'content-type':'application/json'
        },
        data:JSON.stringify({
          filename,
          fileHash
        })
      })
      //返回数据
      return JSON.parse(data);
    },
上传文件切片：过滤已经上传的文件+Promise.all并发请求
//上传文件切片，同时过滤已经上传的切片
    async uploadChunks(uploadedList = []){
      const requestList = this.data
        .filter(({hash})=>!uploadedList.includes(hash)) //过滤已经上传的chunks
        .map(({chunk,hash,index})=>{
          const formData = new FormData();
          formData.append('chunk',chunk);
          formData.append('hash',hash);
          formData.append("filename", this.container.file.name);
          formData.append("fileHash", this.container.hash);
          return { formData,index }
        })//创建表单数据
        .map(async ({formData,index})=>
          this.request({
            url:'http://localhost:3000',
            data:formData,
            onProgress : this.createProgressHandler(this.data[index]),
            requestList:this.requestList//将xhr push到请求列表
          })
        )//创建请求列表
        //并发上传
        await Promise.all(requestList);
        //已经上传切片数量+本次上传切片数量==所有切片数量时 
        //切片上传完成，给服务器发送合并切片请求
        if(uploadedList.length + requestList.length === this.data.length){
          await this.mergeRequest();
        } 
    }
合并切片：服务端发送请求
    // 通知服务端合并切片
    async mergeRequest() {
      await this.request({
        url: "http://localhost:3000/merge",
        headers: {
          "content-type": "application/json"
        },
        data: JSON.stringify({
          size: SIZE,
          fileHash: this.container.hash,
          filename: this.container.file.name
        })
      });
      this.$message.success("上传成功");
      this.status = Status.wait;
    },
用原生xhr进行封装http请求
// xhr
    request({
      url,
      method = "post",
      data,
      headers = {},
      onProgress = e => e,
      requestList
    }) {
      return new Promise(resolve => {
        const xhr = new XMLHttpRequest();
        xhr.upload.onprogress = onProgress;
        xhr.open(method, url);
        Object.keys(headers).forEach(key =>
          xhr.setRequestHeader(key, headers[key])
        );
        xhr.send(data);
        xhr.onload = e => {
          // 将请求成功的 xhr 从列表中删除
          if (requestList) {
            const xhrIndex = requestList.findIndex(item => item === xhr);
            requestList.splice(xhrIndex, 1);
          }
          resolve({
            data: e.target.response
          });
        };
        // 暴露当前 xhr 给外部
        requestList?.push(xhr);
      });
    }
服务端
开启服务：未使用node框架，原生利用http模块
const Controller = require("./controller");
const http = require("http");
const server = http.createServer();
const controller = new Controller();
server.on("request", async (req, res) => {
  //设置响应头，允许跨域
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Access-Control-Allow-Headers", "*");
  if (req.method === "OPTIONS") {
    res.status = 200;
    res.end();
    return;
  }
  //切片验证
  if (req.url === "/verify") {
    console.log(req);
    await controller.handleVerifyUpload(req, res);
    return;
  }
//切片合并
  if (req.url === "/merge") {
    await controller.handleMerge(req, res);
    return;
  }
//切片提交
  if (req.url === "/") {
    await controller.handleFormData(req, res);
  }
});
server.listen(3000, () => console.log("正在监听 3000 端口"));
controller.js
合并切片的方式：使用stream pipe方式，节省内存，边读边写入，占用内存更小，效率更高
const multiparty = require("multiparty");//解析文件上传
const path = require("path");
const fse = require("fs-extra");//fs模块拓展
const extractExt = filename =>
filename&&filename.slice(filename.lastIndexOf("."), filename.length); // 提取后缀名
const UPLOAD_DIR = path.resolve(__dirname, "..", "target"); // 大文件存储目录
//使用stream pipe方式，合并切片
const pipeStream = (path, writeStream) =>
  new Promise(resolve => {
    const readStream = fse.createReadStream(path);
    readStream.on("end", () => {
      fse.unlinkSync(path);
      resolve();
    });
    readStream.pipe(writeStream);
  });
// 合并切片
const mergeFileChunk = async (filePath, fileHash, size) => {
  const chunkDir = path.resolve(UPLOAD_DIR, fileHash);
  const chunkPaths = await fse.readdir(chunkDir);
  // 根据切片下标进行排序
  // 否则直接读取目录的获得的顺序可能会错乱
  chunkPaths.sort((a, b) => a.split("-")[1] - b.split("-")[1]);
  await Promise.all(
    chunkPaths.map((chunkPath, index) =>
      pipeStream(
        path.resolve(chunkDir, chunkPath),
        // 指定位置创建可写流
        fse.createWriteStream(filePath, {
          start: index * size,
          end: (index + 1) * size
        })
      )
    )
  );
  fse.rmdirSync(chunkDir); // 合并后删除保存切片的目录
};
const resolvePost = req =>
  new Promise(resolve => {
    let chunk = "";
    req.on("data", data => {
      chunk += data;
    });
    req.on("end", () => {
      resolve(JSON.parse(chunk));
    });
  });
// 返回已经上传切片名
const createUploadedList = async fileHash =>
  fse.existsSync(path.resolve(UPLOAD_DIR, fileHash))
    ? await fse.readdir(path.resolve(UPLOAD_DIR, fileHash))
    : [];
module.exports = class {
  // 合并切片
  async handleMerge(req, res) {
    const data = await resolvePost(req);
    const { fileHash, filename, size } = data;
    const ext = extractExt(filename);
    const filePath = path.resolve(UPLOAD_DIR, `${fileHash}${ext}`);
    await mergeFileChunk(filePath, fileHash, size);
    res.end(
      JSON.stringify({
        code: 0,
        message: "file merged success"
      })
    );
  }
  // 处理切片
  async handleFormData(req, res) {
    const multipart = new multiparty.Form();
    multipart.parse(req, async (err, fields, files) => {
      if (err) {
        console.error(err);
        res.status = 500;
        res.end("process file chunk failed");
        return;
      }
      const [chunk] = files.chunk;
      const [hash] = fields.hash;
      const [fileHash] = fields.fileHash;
      const [filename] = fields.filename;
      const filePath = path.resolve(
        UPLOAD_DIR,
        `${fileHash}${extractExt(filename)}`
      );
      const chunkDir = path.resolve(UPLOAD_DIR, fileHash);
      // 文件存在直接返回
      if (fse.existsSync(filePath)) {
        res.end("file exist");
        return;
      }
      // 切片目录不存在，创建切片目录
      if (!fse.existsSync(chunkDir)) {
        await fse.mkdirs(chunkDir);
      }
      await fse.move(chunk.path, path.resolve(chunkDir, hash));
      res.end("received file chunk");
    });
  }
  // 验证是否已上传/返回已上传切片下标
  async handleVerifyUpload(req, res) {
    const data = await resolvePost(req);
    console.log(data);
    const { fileHash, filename } = data;
    const ext = extractExt(filename);
    const filePath = path.resolve(UPLOAD_DIR, `${fileHash}${ext}`);
    if (fse.existsSync(filePath)) {
      res.end(
        JSON.stringify({
          shouldUpload: false
        })
      );
    } else {
      res.end(
        JSON.stringify({
          shouldUpload: true,
          uploadedList: await createUploadedList(fileHash)
        })
      );
    }
  }
};

高频面试题：
1. CSS：BFC容器、居中方式、flex布局
2. JS：原型链、函数执行栈、闭包、this
3. 手写JS代码：防抖/节流、Promise.all、快排/归并排序
4. vue：computed原理、数组绑定原理、nextTick原理、keep-alive原理、vue3新特性
5. react：fiber原理、hooks原理、diff算法原理
6. 网络：DNS解析流程、CDN原理、TCP/UDP协议、三次握手四次挥手过程、HTTP1.1/2区别、各状态码表达含义
7. 浏览器原理：从HTML到完整页面展
6. 网络：DNS解析流程、CDN原理、TCP/UDP协议、三次握手四次挥手过程、HTTP1.1/2区别、各状态码表达含义
7. 浏览器原理：从HTML到完整页面展示全流程
8.  v8：GC机制
9. 缓存：强缓存与协商缓存完整过程
10. 跨域：成因、注意事项及解决方案
11.  node：express/koa中间件原理，SSR原理
12. web安全：xss与csrf，原理及防范手段
13. 前端工程化：webpack优化策略，vite优点
14. 性能优化：常见性能瓶颈、优化手段，如何检测首屏时间并提升首屏速度
其它：TS、移动端适配、flutter/RN/weex等native开发方式


几乎100%必考题：
1. JS eventloop机制
2. 回流/重绘/合成
3. vue/react原理，virtual dom结构
4. https原理

高频面试题：
1. CSS：BFC容器、居中方式、flex布局
2. JS：原型链、函数执行栈、闭包、this
3. 手写JS代码：防抖/节流、Promise.all、快排/归并排序
4. vue：computed原理、数组绑定原理、nextTick原理、keep-alive原理、vue3新特性
5. react：fiber原理、hooks原理、diff算法原理
6. 网络：DNS解析流程、CDN原理、TCP/UDP协议、三次握手四次挥手过程、HTTP1.1/2区别、各状态码表达含义
7. 浏览器原理：从HTML到完整页面展示全流程
8.  v8：GC机制
9. 缓存：强缓存与协商缓存完整过程
10. 跨域：成因、注意事项及解决方案
11.  node：express/koa中间件原理，SSR原理
12. web安全：xss与csrf，原理及防范手段
13. 前端工程化：webpack优化策略，vite优点
14. 性能优化：常见性能瓶颈、优化手段，如何检测首屏时间并提升首屏速度

其它：TS、移动端适配、flutter/RN/weex等native开发方式

🔥flex-direction（决定主轴方向）：row | row-reverse | column | column-reverse;
row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿
🔥justify-content（项目在主轴上的对齐方式）：flex-start | flex-end | center | space-between | space-around;
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍
🔥align-items（项目在交叉轴上如何对齐）：flex-start | flex-end | center | baseline | stretch;
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度


面经：

字节跳动 飞书
一面
这一轮全是代码题，没问别的
1. css实现开关样式，要求只可使用一个dom元素
2. 实现sum函数，使得
sum(1,2,3).sumOf() //6
sum(2,3)(2).sumOf() //7
sum(1)(2)(3)(4).sumOf() //10
3. 求二叉树所有根到叶子路径组成的数字之和，二叉树每个节点的value范围是1-9
4. js实现一个带并发限制的异步调度器schedule，保证同时运行的任务最多有两个

二面
先聊了项目中遇到的一些困难点，再提问题
1. react更新原理，和angular/vue异同
2. angular脏值检查原理，为什么它不使用vue的数据绑定模式
3. 操作系统都做了哪些工作
4. LRU算法的原理和实现
5. AI图像识别的步骤及原理(因本人写过相关论文)
6. 性能优化的指标和常见优化手段
7. SSR的原理
8. 扫码登录的实现原理
9. 算法题：实现一个二进制加法
10. 算法题：合并两个number数组a，b并排序，如果有一个数出现多次，如a数组有1个5，b数组有2个5，合并出的数组应有2个5，即按次数多的保留

三面
这一轮主要会提供一些特定场景，让你进行方案设计。也包括一些软件工程相关的抽象概念。
1. native如何检测webview页面白屏/崩溃，纯js是否能实现类似功能
2. 代码实现一个需求，发送请求时如果5秒内没有响应，则重复执行当前的请求，请求发送次数总共不超过三次
3. 如果让你实现RN/weex/flutter之间的代码互相转换，你会怎么做设计
4. 一个持续进行的项目，如何从系统层面减少工作量

阿里 淘宝搜索推荐
算法机试
函数实现一个大位数乘法，可以计算出诸如1865459497823＊6349526719336的结果

一面
1. vue/react开发与jQuery开发有什么区别
2. vue/react的dom diff过程，二者有什么差异
3. react hooks的useState相对于有状态组件state区别
4. DNS解析流程
5. TCP/IP协议分层，三次握手四次挥手的状态码，服务端连接队列拥堵时怎么处理，客户端第四次挥手后为什么要等待2MSL时间才转换为close状态
6. 网络通信中引入滑动窗口的作用
7. http1.1/2/3差异，有做什么优化
8. https详细流程，为什么最后会使用对称加密，而不是全过程使用非对称加密
9. 服务器如何得知浏览器发送了http请求
10. 服务端高并发问题怎么解决
11. redis如何得知缓存失效
12. xss/csrf/SQL注入，在前端和后台分别要做什么安全防范工作
13. 从获得HTML到解析页面全流程，为什么栅格线程使用GPU计算而不是CPU计算
14. 影响首屏加载的因素有哪些，分别如何进行优化，performance有哪些相关的指标
15. js原型链/执行上下文/闭包/eventloop机制，class的继承和prototype是完全一样的吗，new操作符做了哪些事情
16. js常见几种异步代码编写的方式对比（promise/generator/async-await/rxjs）
17. js内存回收机制，如何避免内存泄漏
18. v8引擎解释执行js代码的详细流程
19. WebAssembly有听说过吗？它的优点是什么，使用时需要注意哪些问题
20. 项目中可以通过什么方法来避免出现错误

二面
前面主要在聊项目
1. 服务端如何得知客户端的http请求已发送完毕
2. 客户端如何得知服务器的数据已传输完毕
3. 请求在客户端报504gateway timeout时，在服务端看到的状态码是什么
4. 请求在客户端报413是什么错误，怎么解决
5. docker部署项目的完整流程
6. cookie、session storage、local storage差异
7. restful API的官方定义是什么

三面
这一轮主要聊项目和未来规划，问题考察不多
1. 项目中用到了哪些设计模式，具体怎么运用的
2. 现在让你实现一个web IDE，可以在网页上编写Java代码，并实时运行得到结果。你会怎么设计整套方案，中间流程大致是什么样的。

四面
交叉面环节，其它部门的面试官来进行交叉验证。
基本都在聊项目，问项目难点，解决方案等等，没考察实际问题

京东 凹凸实验室
一面
因为面试部门的业务和之前的项目业务高度重合，所以主要在聊项目这一块
1. 小程序、快应用、RN、原生安卓/iOS开发的区别
2. webview和iframe的区别
3. electron主进程和渲染进程怎么通信，渲染进程如何进行文件读写
4. 快应用的组件是如何转换为原生安卓组件进行渲染的，如何在浏览器端模拟实现list、stack组件
5. 在前端项目中实现IOC有哪些方式

二面
1. 手写es5组合寄生继承
2. 手写LRU算法，优化方式(使用双向链表)
3. vue 数组双向绑定原理，vue3如何处理数组
4. vue computed原理
5. vue nextTick原理
6. 浏览器和node处理宏任务微任务的差异
7. vue3 composition API
8. vite和webpack对比，为什么vite在dev模式下运行速度快很多
9. service worker和webworker差异，各自的缺陷是什么，service worker如何清除缓存
10. react hooks原理
11. react fiber原理
12. https详细流程
13. 强缓存和协商缓存
14. 浏览器解析html的过程
15. script标签async和defer区别
16. canvas/css如何旋转一张图片，原理是什么(答：矩阵旋转)追问：矩阵结构和参数应该是什么
17. css transform是如何处理动画效果并与GPU交互的
18. ts中pick、partial、record作用
19. canvas和svg同时画一万条直线，谁的效率更高
20. 图像识别的计算训练流程，如何提取特征，如何进行数据分类(本人写过AI相关的论文)

三面
简单问了下我想去哪个项目组，没怎么聊技术细节
1. webpack的打包优化方案有哪些
2. webpack的热模块更新是怎么实现的
3. 对大图片如何进行压缩

四面
主要聊项目问题和未来发展方向，问了对taro的了解，觉得其优缺点有哪些，未来发展方向(taro是他们搞出来的)

360数科(即原来的360金融)
一面
1. 函数柯里化的理解和运用
2. 防抖节流手写代码
3. zoom和scale区别，造成其差异的原因
4. js和node中eventloop机制分别是什么，其运行结果有什么差异
5. vue nextTick原理，为什么优先使用microtask处理
6. vue keep-alive原理，LRU缓存原理
7. 浏览器请求缓存机制
8. 浏览器状态码有哪些，301和302表现在客户端的区别，浏览器对301和302的处理有什么不同
9. 如何区分简单请求和复杂请求，options请求在什么场景下会出现，其作用是什么
10. 现在有一个能装5升水的桶和一个能装3升水的桶，问如何利用这两个桶装4升水
11. 算法题：洗牌算法
12. 算法题：在一个int型数组中，找出所有符合条件的三元组[a,b,c]，满足a+b+c=0。要求时间复杂度不得超过O(n^2)

二面
这一面主要聊项目，完成之后随便问了几个问题，最后让手写了两个leetcode hard算法题
1. 移动端h5适配方案，1px边框问题如何解决
2. 移动端点击一个按钮，一共会触发哪些事件，它们的触发先后顺序是怎样的
3. 首屏加载的性能指标有哪些，它们分别的意义是什么，如何优化首屏加载速度
4. 手写算法：鸡蛋掉落问题。
你有K个鸡蛋和一栋N层楼的建筑。你可以取一个鸡蛋从任意楼层扔下，查看鸡蛋是否会摔碎；若鸡蛋被摔碎，你就不能再扔它。现已知存在楼层F，小于等于F的楼层落下的鸡蛋都不会碎，大于F的楼层落下落下的鸡蛋都会碎。问找到这个F最少要扔多少次鸡蛋。(详情见leetcode 887题)
5. 手写算法：编辑距离。
给你两个单词word1和word2，计算将word1转为word2所使用的最少操作数。你可以对一个单词进行如下三种操作：插入一个字符、删除一个字符、替换一个字符(详情见leetcode 72题)

三面
1. flutter和原生安卓/iOS开发的区别，怎么看待flutter的前景，其缺陷是什么
2. jsBridge原理，webview如何实现和native通信
3. 已缓存未过期的文件，如何强制刷新
4. js的数组和对象，在v8中分别是如何处理的，异同点是什么
5. 数组有哪些内置属性
6. 前后台通信时，如何保证敏感数据不被第三方窃听获取。对加密算法有什么了解
7. oAuth2.0的登录详细流程
8. 对git flow了解吗，应该如何使用

腾讯音乐 QQ音乐商业化
一面
1. 对事件流的理解，如果addEventListener的第三个参数设置为true会发生什么
2. 浏览器GC机制
3. 对函数执行上下文的理解，执行上下文中存储了哪些内容
4. 浏览器和node对于事件循环的差异
5. react hooks解决了什么问题，其原理是什么(以useEffect为例)。useMemo和useCallback差别
6. 跨域问题有哪些常见的处理方式
7. http1.1和http2区别，https为什么会同时使用对称和非对称加密
8. 前端常见的安全问题有哪些，分别怎么处理
9. 前端性能指标及性能优化方案
10. SSR 同构原理
11. 移动端的点击事件为什么会有延迟
12. webpack常见优化手段，hash、chunkhash和contenthash区别
13. service worker缓存原理
14. cookie和session的区别
15. 强缓存与协商缓存的机制详解，命中缓存的返回状态码是什么
16. 如何实现一个无侵入sdk，用于上报当前页面的首屏加载速度
17. 如何实现一个无侵入sdk，用于捕获并上报当前页面中发生的错误异常

二面
先聊项目，问了下项目中的难点有哪些，工程化是如何处理的，接下来开始问问题
1. web和node有哪些方式启动多线程/多进程，其交互是如何进行的。进程之间的通信主要有哪些方式。
2. node如何保证服务的稳定性和延续性，保证其服务不宕机，服务挂掉之后能迅速恢复
3. 对canvas性能优化有什么样的方案，具体实践过程。对多线程原子锁是否有了解。
4. TCP和UDP差异，分别用于什么样的场景，为什么会有两套不同的方案
5. TCP握手与挥手过程，每个状态下的状态码。半连接和全连接遭受攻击分别如何解决。第四次挥手需要等待2MSL的原因。
6. HTTP2有哪些优化，多路复用为什么可以提高传输效率，其原理是什么，复用的到底是什么。
7. csrf攻击的本质是什么，csrf token是如何生成并校验的，其防范攻击的原理是什么
8. 如何通过js sdk获取网页首屏加载时间及可交互时间，对应如何进行性能优化
9. 数据结构中，哈希表的优点缺陷分别是什么，哈希冲突的解决方案。从硬件层面对比数组、链表和哈希表差异
10. JS遍历数组有哪些方式，各遍历方式的性能对比
11. react、vue和angular对比及差异，包括其设计核心思想，优化思想是什么
12. 对ts装饰器的理解和运用，ts高级类型与泛型

富途证券

一面
1. 两列布局，左侧200px，右侧自适应宽度，写出所有实现方式
2. 递归实现斐波那契数列，要求缓存中间的结果
3. 浏览器从输入URL到加载页面全过程，中间各个步骤如何做优化(包括DNS、网络连接、缓存、渲染流程等)
4. vue 数组是如何做双向绑定的
5. vue $nextTick实现
6. 首屏优化方案，懒加载、预加载原理
7. nuxt.js在服务端和客户端分别会触发什么生命周期函数，执行SSR后端推流时，如何在前台建立数据视图依赖关系
8. express中间件原理
9. xss/csrf攻击原理及预防手段，富文本编辑器如何防xss注入
10. 对js原型链的理解，super方法作用，不调用super会导致什么结果
11. js this指向问题，bind绑定this后还可以被call/apply吗
12. js eventloop机制，node中如何进行进程管理
13. get/post区别
14. options请求的出现场景，需要注意哪些问题

二面
这一面主要考察逻辑思维能力和算法题
1. 已知有8个球，其中7个球的重量是一样的，唯独有一个球的重量要比其他球轻点。现在给你一个天平，问最少测几次可以找到这个轻球
2. 有25个小朋友参加跑步比赛，已知一轮最多可同时让5个小朋友参赛。假设不考虑小朋友的体力，且小朋友每次跑步的速度都保持一致。问最少测几次能找到跑得最快的前三名小朋友。
3. 算法题：已知输入为'R'，'G'，'B'三个字符组成的字符串，代码实现将字符按R，G，B的顺序排序。如：输入RGGBGBRRBG，输出RRRGGGGBBB
4. 给定一个以()[]{}输入的字符串，写一个函数用于判断括号匹配关系是否完全闭合
5. 算法题，给定两个从小到大有序排列的int数组A B，写一个函数判断B是不是A的完全子集

三面
1. 死锁的定义，其四个必要条件分别是什么 ？造成死锁最少需要几个线程和几个资源
2. 一个线程可以同时属于多个进程吗？线程和协程之间是否存在一对多的关系
3. 一个进程十个线程，需要占据的堆内存和栈内存空间
4. 传输层协议除了TCP还有什么？网络层协议除了IP还有什么？TCP用哪些方式确保了它的可靠性

bigo 音视频sdk工程师

一面
这一轮主要考察基本知识
1. 事件捕获与事件冒泡的过程
2. react hooks中，useLayoutEffect作用
3. react fiber原理
4. 银行家算法有了解过吗，它是如何解决死锁问题的
5. 算法题，如何在O(1)时间内判断一个数是否是2的N次方（N & N-1）
6. 算法题，一个长度为n-1的数组中，所有数都是唯一的，并且每个数都在1 ~ n的范围内。在范围1 ~ n内的n个数中，有且只有一个数不在该数组中，请找出这个数
7. 算法题，接雨水（详情见leetcode 42题）

二面
这一轮考察音视频/流媒体核心知识，全部和这块相关
1. h264和h265区别
2. h264的I帧、P帧、B帧分别作用，SPS和PPS是做什么用的
3. flv.js有研究过吗，它的实现思路是怎么做的
4. YUV和RGB区别，各自有什么优点
5. 原生video标签不支持m3u8格式的视频，如何解决此问题（答：video.js）追问：video.js实现原理是什么，为什么能实现对m3u8的兼容
6. blob和ArrayBuffer区别
其实还有很多问题，但因为其中很多连题目都没听懂，概念也不知道，就没记录下来。

三面
这一面主要问一些实际场景的应用解决方案
1. 现在某主播正在直播一款游戏，如何获取主播当前电脑的图像/视频/音频数据并上传，这过程中需要注意什么问题（尤其是如何保证音频与视频的同步）
2. 如何从视频中提取某一时刻的图像，并作为封面展示出来

一面
1.实现一个tab组件，越详细越好
2.设置一个form表单组件，越详细越好
3.前端的性能优化，问的很深，各种指标，FP,FCP,FMP是什么，还有新版统计性能的指标有哪些，LCP,FID,TBT,CLS这些，怎么算白屏时间等等
各种工具问你了解没
4.webpack的优化，怎么去做打包的，怎么去优化构建速度等等
5.CDN原理
6.数据结构的hash有了解吗
7.webpack的contenthash值是怎么算出来的
8vue的双向数据响应原理
9.vue路由原理
10.项目中一些业务组件的封装

// 实现一个函数add(1)(2, 3)(4).getValue()
// function add(){
//     let sum = Array.from(arguments).reduce((a,b)=>{
//         return a +b
//     })
//     function fn(){
//         let result = Array.from(arguments).reduce((a,b)=>{
//             return a +b
//         })
//         sum += result;
//         return fn
//     }
//     fn.getValue = function (){
//         return sum;
//     }
//     return fn;
// }
// console.log(add(1).getValue())

// console.log(add(1)(2)(3).getValue())
// console.log(add(1)(2,5)(3).getValue())

function add(){
    let res = Array.from(arguments).reduce((a,b)=>{
        return a +b
    })
    function fn(...args){
        
        return  add.apply(null,[res,...args])
    }
    fn.getValue = function (){
        return res;
    }
    return fn;
}
console.log(add(1).getValue())

console.log(add(1)(2)(3).getValue())
console.log(add(1)(2,5)(3).getValue())

function get(arr) {
    // debugger
    for (let i = 0; i < arr.length; i++) {
        // debugger
        let result = arr[i].reduce((pre, cur) => pre +=cur)
        // console.log(result,'result')
        if (result>1) return false
        if (arr.reduce((pre, cur) => pre += cur[i], 0) > 1) {
            return false
        }
    
    }
    return true
} 
    let bool = get([
        [0, 0, 0, 0, 1, 0],
        [0, 0, 0, 0, 0, 0],
        [0, 1, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 1],
        [0, 0, 0, 0, 0, 0]
    ])
   
    let bool1 = get([
        [0, 0, 0, 0, 1, 0],
        [0, 0, 0, 0, 1, 0],
        [0, 1, 0, 0, 0, 0],
        [0, 1, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 1],
        [0, 0, 0, 0, 0, 1],
        [0, 0, 0, 0, 0, 1],
        [0, 0, 0, 0, 0, 1]
    ])


    console.log(bool, 'bool');
    console.log(bool1, 'bool');

    // let bool = get([
//     [0, 0, 0, 0, 1, 0],
//     [0, 0, 0, 0, 0, 0],
//     [0, 1, 0, 0, 0, 0],
//     [0, 0, 0, 0, 0, 0],
//     [0, 0, 0, 0, 0, 1],
//     [0, 0, 0, 0, 0, 0]
// ])

// let bool1 = get([
//     [0, 0, 0, 0, 1, 0],
//     [0, 0, 0, 0, 1, 0],
//     [0, 1, 0, 0, 0, 0],
//     [0, 1, 0, 0, 0, 0],
//     [0, 0, 0, 0, 0, 1],
//     [0, 0, 0, 0, 0, 1],
//     [0, 0, 0, 0, 0, 1],
//     [0, 0, 0, 0, 0, 1]
// ])


function valid(array) {
    let record = new Set();
    for (let i = 0; i <array.length; i++) {
        let row = array[i];
        // console.log(row,'row')
        let index = row.indexOf(1);
        if(index >0 ){
            if(index != row.lastIndexOf(1)){
                return false
            }
            if(record.has(index)){
                 return false
            }
            record.add(index)
        }
        
    }
    return true

}
let bool = valid([
    [0, 0, 0, 0, 1, 0,0,1],
    [0, 0, 0, 0, 0, 0,0,0],
    [0, 1, 0, 0, 0, 0,0,0],
    [0, 0, 0, 0, 0, 0,0,0],
    [0, 0, 0, 0, 0, 1,0,0],
    [0, 0, 0, 0, 0, 0,0,0],
    [0, 0, 0, 0, 0, 0,0,0]
    
])
console.log(bool)

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/enjoyxiaohaiqw/blogText/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
