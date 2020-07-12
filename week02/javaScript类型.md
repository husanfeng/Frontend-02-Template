# JavaScript类型

### 一、值类型

1. Undefined

undefined是一个变量，非关键词，一般不会给一个变量赋值为undefined，因为这样容易混淆或者无法判断这个变量是否已经赋值过。
undefined与null的区别：如果一个变量为null，说明这个变量已经赋值为null了，而如果为undefined,说明没有给这个变量赋值过。
2. String

我们来看看字符串是否有最大长度。String 用于表示文本数据。String 有最大长度是 2^53 - 1，这在一般开发中都是够用的，但是有趣的是，这个所谓最大长度，并不完全是你理解中的字符数。因为 String 的意义并非“字符串”，而是字符串的 UTF16 编码，我们字符串的操作 charAt、charCodeAt、length 等方法针对的都是 UTF16 编码。所以，字符串的最大长度，实际上是受字符串的编码长度影响的。
3. Symbol
Symbol 可以具有字符串类型的描述，但是即使描述相同，Symbol 也不相等。
```
var a = Symbol(26)
var b = Symbol(26)
console.log(a === b) //false
```
4. Boolean

Boolean类型有两个值，true和false，表示逻辑上的真假，同样有两个关键字 true 和 false来表示。
5. Number

为什么在 JavaScript 中，0.1+0.2 不能 =0.3
number类型运算都要想将其转化为二进制，将二进制运算，运算的结果再转化为十进制，因为number是64位双精度，小数部分只有52位，但0.1转化成为二进制是无限循环的，所以四舍五入了，这里就发生了精度丢失，0.1的二进制和0.2的二进制相加需要保留有效数字，所以又发生了精度丢失，所以结果为0.300000000000004，所以为false，而0.2+0.3恰好两个转化成为二进制和相加的过程都不会发生精度丢失，所以为true

### 二、引用类型

1. Null

Null是一个关键字，如果一个变量值为null，说明该变量已经赋值过，并且值为null。
值得注意的是：typeof null 居然等于'object'，这也是JavaScript的一个bug。这也是为什么把null归纳为引用类型。
```
typeof null // 'object'
```

2. Object

* 为什么给对象添加的方法能用在基本类型上？
```
String.prototype.hello = () => console.log('hello word')
var a = String('husanfeng')
a.hello() // hello word
```
. 运算符提供了装箱操作，它会根据基础类型构造一个临时对象，使得我们能在基础类型上调用对应对象的方法。

* 判断一个类型是否为Object？

值类型可以用typeof，引用类型可以用instanceof。
* Object in JavaScript

对象是一个kv对，k可以是两种类型，Symbol和String。
String是一种可以猜出来的这样一种key。Symbol则不同，它只能通过变量去引用它，没有办法构造两个一模一样的Symbol对象。即使Symbol名字一样，它俩也不是相等的。
JavaScript用属性来统一抽象对象状态和行为。  一般来说，数据属性用于描述状态，访问器属性则用于描述行为数据属性中如果存储函数，也可以用于描述行为。 
当我们访问对象属性时，如果当前对象没有，则会沿着原型找原型对象是否有此名称的属性，而原型对象还可能有原型，因此，会有“原型链”  这一说法。Object这一算法保证了，每个对象只需要描述自己和原型的区别即可。 

* Object API/Grammar 

    * {} . [] Object.defineProperty  
它们提供了一个基本的对象机制，那么我们能够通过语法去创建对象，访问属性和定义新的属性以及去改变属性的特征值，这个是基本的面向对象能力。
    * Object.create / Object.setPrototypeOf /  Object.getPrototypeOf  
基于原型的描述对象的方法，那么我们可以通过Object.create在指定原型的前提下创建对象，而我们又可以
去修改一个对象的原型或者获取一个对象的原型。
    * new / class / extends  
基于分类的方式去描述对象，而这种基于分类的方式尽管它在运行时仍然会被转换成javascript的相关的访              问，但是我们从语法上来看，从他的抽象能力来看，它完全就是一个基于类的这样的面向对象的组织方式。
    * new / function / prototype 
使用prototype的属性去完成对象的抽象。不建议使用
    * Function Object 
JavaScript中还有一些特殊的对 象，比如函数对象， 除了一般对象的属性和原型，函数对象还有一个行为[[call]]。 我们用JavaScript中的function 关键字、箭头运算符或者Function构 造器创建的对象，会有[[call]]这个行为。 
    * Special Object 
Array  [[length]]  
数组对象它的长度会随着我们的增加新的数字型而改变，
Object.prototype  [[setPrototypeOf]] 
Function.prototype,所有对象的原型她是没有setPrototypeOf的方法
* Host Object 

    Object  
    [[call]]  
[[construct]] 

除了js自身的那么它还有一些Host Object，Host Object是js语言标准中没有去定义
而是由宿主环境去定义的，比如说在浏览器里我们可以访问到window,settimeout,
这些都和js原生没有任何关系。
Host Object 的它就可以实现一些js语言并不支持，但是js语法支持的一些特性，
语法是语法，运行时是运行时，他两不冲突，只要语法允许，那么运行时Host Object
理论上都是可以做这样的事情。

### 三、类型转换
因为 JS 是弱类型语言，所以类型转换发生非常频繁，大部分我们熟悉的运算都会先进行类型转换。大部分类型转换符合人类的直觉，但是如果我们不去理解类型转换的严格定义，很容易造成一些代码中的判断失误。其中最为臭名昭著的是 JavaScript 中
其中最为臭名昭著的是 JavaScript 中的“ == ”运算，因为试图实现跨类型的比较，它的规则复杂到几乎没人可以记住。这里我们当然也不打算讲解 == 的规则，它属于设计失误，并非语言中有价值的部分，很多实践中推荐禁止使用“ ==”，而要求程序员进行显式地类型转换后，用 === 比较。其它运算，如加减乘除大于小于，也都会涉及类型转换。幸好的是，实际上大部分类型转换规则是非常简单的，如下表所示：
![q]('./1.jpeg')

1. StringToNumber

parseInt() 函数可解析一个字符串，并返回一个整数。
parseInt(string, radix)
string
必需。要被解析的字符串。
radix
可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。
如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。
如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN。

在不传入第二个参数的情况下，parseInt 只支持 16 进制前缀“0x”，而且会忽略非数字字符，也不支持科学计数法。在一些古老的浏览器环境中，parseInt 还支持 0 开头的数字作为 8 进制前缀，这是很多错误的来源。所以在任何环境下，都建议传入 parseInt 的第二个参数，而 parseFloat 则直接把原字符串作为十进制来解析，它不会引入任何的其他进制。
多数情况下，Number 是比 parseInt 和 parseFloat 更好的选择。
```
parseInt('100.222',0)//100
parseInt('10.222',1) // NaN
parseInt('10.222',37) // NaN
```
2. NumberToString
在较小的范围内，数字到字符串的转换是完全符合你直觉的十进制表示。当 Number 绝对值较大或者较小时，字符串表示则是使用科学计数法表示的
```
String(122222222222222222222222222222222222222222222222222222222222222222222222)
"1.2222222222222222e+71"
```