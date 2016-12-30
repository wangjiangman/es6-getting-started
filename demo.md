title: ES6入门
speaker: Fiona
url: https://github.com/ksky521/nodePPT
transition: slide3
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: moon
usemathjax: yes

[slide style="background-image:url('/img/bg1.png')"]
# ES6(ECMAScript 2015)简介
<small>演讲者：Fiona</small>

[slide]

[magic data-transition="earthquake"]
<img src="/paozhuan.jpg" alt="">
[/magic]
[slide style="background-image:url('/img/bg1.png')"]

## 主要内容
----
* ES6简介 {:&.rollIn} 
* ES6功能概览
* ES6数据遍历
* ES6的类和模块化

[slide]
## ES6简介
----
* **ECMAScript** {:&.rollIn} -> JavaScript语言的核心
* **ES6** -> ECMAScript于2015年6月发布的版本
* **JavaScript** -> ECMAScript的一种实现<img src="/javascript.gif" height="120">

[slide style="background-image:url('/img/bg1.png')"]

# ES6功能概览

[slide style="background-image:url('/img/bg1.png')"]
## ES6功能概览（一）
---
| ES5 | ES6
:-------|:------|:-------
变量声明方式 | var 和 function | ES6有六种申明变量的方法： var function let const import class(一种语法糖)
变量定义 | 普通一对一赋值方式 | 支持变量的解构赋值
基本数据类型 | 六种：<span class="text-success">Boolean、undefined、NULL，String、Number、Object</span> | 新增了<span class="text-danger">Symbol</span>基本数据类型，对字符串和数字的操作进行了扩展
基本引用类型 | | ES6在ES5的基础上对基本引用类型<span class="text-danger">RegExp Array Function</span>进行了扩展，且新增了<span class="text-danger">Map</span>和<span class="text-danger">Set</span>两种基本引用类型。
对象操作API | | 新增对象操作API：<span class="text-danger">Proxy</span>和<span class="text-danger">Reflect</span>

[slide style="background-image:url('/img/bg1.png')"]
## ES6功能概览（二）
---
| ES5 | ES6
:-------|:------|:-------
数据结构遍历机制 | | 新增对数据结构(原生的或者自定义的)的遍历机制<span class="text-danger">Iterator</span>，Iterator供for...of消费
异步编程解决方案 | | 新增异步编程解决方案 <span class="text-danger">Generator</span>函数、<span class="text-danger">Promise</span>对象
模块加载方案 | CommonJS：后台js模块加载方案,如NodeJS；AMD：web端js模块加载方案，如Require.js; CMD: 另一种web端js模块加载方案，如Sea.js | 使用<span class="text-danger">import</span>(加载外部模块)和<span class="text-danger">export</span>(定义对外接口)在语言标准的层面上，实现了模块功能。可以完全替代CommonJS和AMD，实现由<span class="text-danger">运行时加载</span>到<span class="text-danger">编译时加载</span>的转变。

[slide style="background-image:url('/img/bg1.png')"]
# ES6数据遍历

[slide style="background-image:url('/img/bg1.png')"]
## ES6数据遍历 — **for**
### 基本循环语句，常用于对数组进行遍历
----

<pre><code class="javascript">/* 基本循环语句，常用于对数组进行遍历 */
var a = []
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i)
  }
}

// a[6]() = ?
// 将var换成let后，a[6]() = ?
</code>
</pre>

[slide style="background-image:url('/img/bg1.png')"]
##ES6 6种遍历对象属性的方法
----
* 1.**for ... in** 循环遍历对象自身的和继承的可枚举属性(不含Symbol属性).检测给定的属性是否可枚举，可以使用对象实例的propertyIsEnumerable方法。 {:&.rollIn} 

* 2.**Obejct.keys(obj)**,返回一个数组,包括对象自身的(不含继承的)所有可枚举属性(不含Symbol属性).

* 3.**Object.getOwnPropertyNames(obj)**,返回一个数组,包含对象自身的所有属性(不含Symbol属性,但是包括不可枚举属性).

* 4.**Object.getOwnPropertySymbols(obj)**,返回一个数组,包含对象自身的所有Symbol属性.

* 5.**Reflect.ownKeys(obj)**,返回一个数组,包含对象自身的所有属性,不管属性名是Symbol或字符串,也不管是否可枚举.

* 6.**Reflect.enumerate(obj)**,返回一个Iterator对象,遍历对象自身的和继承的所有可枚举属性(不含Symbol属性),与for ... in 循环相同.

[slide style="background-image:url('/img/bg1.png')"]
## ES6数据遍历 — **for-of**
### 任何部署了Iterator接口的对象，都可以用for...of循环遍历
----

<pre><code class="javascript">/* 
 * for...of可以遍历数据结构包括：
 * 数组、Set和Map结构，类数组对象（arguments对象、DOM NodeList对象），
 * Generator对象和字符串。 
*/
// 自定义Iterator接口
let iterable = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3,
  [Symbol.iterator]: Array.prototype[Symbol.iterator]
};
for (let item of iterable) {
  console.log(item); // 'a', 'b', 'c'
}

// 自带Iterator接口
let generator = function* () {
  yield 1;
  yield* [2,3,4];
  yield 5;
};

var iterator = generator();
for (step of iterator) {console.log(step)} // 1, 2, 3, 4, 5
</code>
</pre>

[slide style="background-image:url('/img/bg1.png')"]
## **map** 和 **forEach**
----
* **map** 适用于数组，对数组的每一项执行给定的函数，返回每次函数调用的结果组成的数组 {:&.rollIn}<pre><code class="javascript">var members = [1, 2, 3]
var mapResult = members.map((member) => member*2)
console.log(mapResult)
// [2, 4, 6]
</code></pre>

* **forEach** 适用于数组、Set和Map，对数据结构的每一项执行给定的函数，没有返回值。<pre><code class="javascript">var members = [2,4,5,6,7]
var result = members.forEach((item, index, array) => {
    console.log(`item: ${item}, index is ${index}, array is ${array}`)
})
// item: 2, index is 0, array is 2,4,5,6,7
// item: 4, index is 1, array is 2,4,5,6,7
// item: 5, index is 2, array is 2,4,5,6,7
// item: 6, index is 3, array is 2,4,5,6,7
// item: 7, index is 4, array is 2,4,5,6,7
</code></pre>


[slide style="background-image:url('/img/bg1.png')"]

## ES6的类和模块化

[slide style="background-image:url('/img/bg1.png')"]
## 引入语法糖Class
### 借鉴传统面向对象语言(Java、C++)
    <pre><code class="javascript">/* ES5通过构造函数，定义并生成新对象。 */
    function Point(x, y) {
      this.x = x;
      this.y = y;
    }

    Point.prototype.toString = function () {
      return '(' + this.x + ', ' + this.y + ')';
    };

    var p = new Point(1, 2);
    </code></pre>
    <pre><code class="javascript">/* ES6定义类 */
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}</code></pre>

[slide style="background-image:url('/img/bg1.png')"]
## ES6的类，完全可以看作构造函数的另一种写法
----
* 类的数据类型是函数 {:&.rollIn}  <pre><code class="javascript">class Point {
  // ...
}
typeof Point // "function"
</code></pre>
* 类的所有方法都定义在**prototype**上，类的内部定义的所有方法都不可枚举
* 类有默认构造函数**constructor**，指向类本身，支持重写
* 类的实例化方法与ES5一样使用**new**命令<pre><code class="javascript">class B {}
let b = new B();
</code></pre>
* 类通过**extends**关键字实现继承

[slide style="background-image:url('/img/bg1.png')"]
## 引入import和export命令实现模块化


[slide style="background-image:url('/img/bg1.png')"]
## import和export解决了什么
----
* ES5中浏览器端模块化方案：AMD CMD {:&.rollIn} 
* ES5中浏服务器端模块化方案：CommonJS  <pre><code>// CommonJS模块
let { stat, exists, readFile } = require('fs');
// 等同于
let _fs = require('fs');
let stat = _fs.stat, exists = _fs.exists, readfile = _fs.readfile;</code></pre>

* 使用<span class="text-danger">import</span>(加载外部模块)和<span class="text-danger">export</span>(定义对外接口)在语言标准的层面上，实现了模块功能。可以完全替代CommonJS和AMD，实现由<span class="text-danger">运行时加载</span>到<span class="text-danger">编译时加载</span>的转变。<pre><code>// ES6模块
import { stat, exists, readFile } from 'fs';
export function multiply(x, y) {
  return x * y;
};</code></pre>
[slide style="background-image:url('/img/bg1.png')"]

## ES6代码转为ES5代码神奇：**Babel**
### 安装
----
* 1、配置.babelrc  {:&.rollIn}  <pre><code>{
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }</code></pre>
* 2、安装**babel-cli**，babel-cli工具自带一个babel-node命令，提供一个支持ES6的REPL环境。

[slide style="background-image:url('/img/bg1.png')"]

## 参考
---
http://es6.ruanyifeng.com/

http://www.ruanyifeng.com/blog/2016/01/babel.html

http://www.cnblogs.com/futai/p/5258349.html
