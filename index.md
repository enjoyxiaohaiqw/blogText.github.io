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


## Header 2
### Header 3

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
