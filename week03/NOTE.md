# 第3周 重学JavaScript

## 一、 作用域/作用域链

### 理解
- 作用域：一套查找变量的规则
- 作用域链：从当前作用域开始查找，一层一层的向上查找，找到最外层即为全局作用域，如果还未找到就将停止。
```
function fn(a) {
  console.log(a + b)
}
var b = 2 // 变量提升了
fn(3)
```
>分析以上代码，执行函数fn时，js引擎会fn函数内查找b的变量，但是并未找到，就向上一层作用域查找，在全局作用域下找到了b的值，这种一层层的向上查找变量的规则，即为作用域链。
- 词法作用域：是定义在词法阶段的作用域
词法作用域意味着作用域是由书写代码时的函数位置来决定的，编译的词法分析阶段基本上能够知道全部标志符（函数，变量）在哪里以及是如何声明的，从而能够预测在执行过程中如何对它们进行查找。
  - '欺骗' 词法作用域
eval 与 with可以在运行时修改此词法作用域。但是工作中尽量不用，因为会有性能问题。
- 函数作用域：
如何区分函数申明和函数表达式的最直接方法看function这个词的位置，如果是第一个词那么就是函数申明，否则为函数表达式。
```
function fn(){ // 函数申明
};
fn();
// ----
(function IIFE(global){ // 立即执行函数
 
})(windown)
setTimeout(function(){ // 匿名函数
},1000)
var a = 100
(function fn(def){
  def(this)
})(function def(){
  console.log(this.a)
})
```
fn函数被绑定在所在的作用域中。可以通过fn()来调用，而IIFE被绑定在函数表达式自身的函数中而不是作用域中。
- 块作用域
1. let 可以创建块作用域
2. const
3. 闭包
4. ES3 开始 try/catch结构在catch分句中也具有块作用域
## 二、this
### 1. 理解
> 处决于调用的位置

### 2. call apply bind
> 三者共同点都是改变this的指向

- call
有多个参数，第一个参数是this

```
function fn(){
    console.log(this.name)
}
var obj = {
    name: 'husanfeng'
}
var name = 'hello word'
fn.call(obj)
```
- apply
有两个参数，第一个参数是this，第二个参数是一个数组

```
function fn(){
    console.log(this.name)
}
var obj = {
    name: 'husanfeng'
}
fn.apply(obj)
```
- bind
传参与call类似，但是bind不能立即执行，返回的是一个函数，需要手动执行
```
function fn(){
    console.log(this.name)
}
var obj = {
    name: 'husanfeng'
}
var func = fn.bind(obj)
func();
```

## 三、 闭包

### 1. 理解
一个可以访问另一个函数的作用域的函数
函数不在它本身的词法作用域以外执行
函数在定义的词法作用域以外的地方被调用。闭包使得函数可以继续访问定义时的词法作用域

### 2. 代码应用

目前发现有两种闭包现象
- 将一个函数作为另一个函数的参数传递
- 将函数作为return 的返回值

## 四、原型/原型链

### 1. 原型

每个函数都有一个属性prototype，即原型。
prototype：每一个对象都一个prototype属性

__proto__：对象的(隐式)原型

函数的显式原型等于对象的隐式原型
每个对象都有一个隐式__proto__，指向创建这个对象的函数的显式原型prototype。

```
function fn(){}
var Fn = new fn()
fn.prototype === Fn.__proto__ // true
```

因为obj = {}，也是通过Object函数创建的，因此obj.__proto__=== Object.prototype
var obj = {}
obj.__proto__ === Object.prototype // true

### 2. 原型链

>访问一个对象的属性，首先在这个对象的基本属性上查找，如果没有，就沿着这个对象的__proto__原型上查找。
