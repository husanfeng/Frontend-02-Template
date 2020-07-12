# JavaScript语言通识

### 一、语言按语法分类
* 非形式语言
     * 中文，英文
* 形式语言（乔姆斯基谱系）
    * 0型 无限制文法
    * 1型 上下文相关文法
    * 2型 上下文无关文法
    * 3型 正则文法

### 二、产生式（BNF）

>定义：巴斯科-诺尔范式 简称叫BNF
程序设计语言的语法成分，如标识符、表达式、句子等，大多可以用BNF的产生规则加以描述。 

* 用尖括号括起来的名称来表示语法结构名  
* 语法结构分成基础结构和需要用其他语法结构定义的复合结构  
    * 基础结构称终结符  
    * 复合结构称非终结符 
* 引号和中间的字符表示终结符  
* 可以有括号  
* * 表示重复多次  
* | 表示或  
* + 表示至少一次 
以四则运算为例深度理解产生式
四则运算：  
* 1 + 2 * 3  终结符： 
* Number  * + - * /  非终结符： 
* MultiplicativeExpression  
* AddtiveExpression
```
<MultiplicativeExpression>::=<Number>|  
    <MultiplicativeExpression>"*"<Number>|  
    <MultiplicativeExpression>"/"<Number>|  
<AddtiveExpression>::=< MultiplicativeExpression>|  
    <AddtiveExpression>"+"<MultiplicativeExpression>|  
    <AddtiveExpression>"-"<MultiplicativeExpression>| 
```
如果四则远算带括号我们应该如何去定义产生式：
```
<MultiplicativeExpression>::=<Number>|  
    <MultiplicativeExpression>"*"<Number>|  
    <MultiplicativeExpression>"/"<Number>|  
<AddtiveExpression>::=< MultiplicativeExpression>|  
    <AddtiveExpression>"+"<MultiplicativeExpression>|  
    <AddtiveExpression>"-"<MultiplicativeExpression>| 
<BracketsExpression>::="("<AddtiveExpression>")" |
    <BracketsExpression> "+" "(" <AddtiveExpression> ")" |
    <BracketsExpression> "-" "(" <AddtiveExpression> ")" |
    <BracketsExpression> "*" "(" <AddtiveExpression> ")" |
    <BracketsExpression> "/" "(" <AddtiveExpression> ")" 
```
通过产生式理解乔姆斯基谱系 
* 0型 无限制文法  
     ?::=? 
* 1型 上下文相关文法  
     ?<A>?::=?<B>?  
* 2型 上下文无关文法 
     <A>::=?  
* 3型 正则文法  
     <A>::=<A>? 
### 三、现代语言的特例 
* C++中，* 可能表示乘号或者指针，具体是哪个，取决于星号前  面的标识符是否被声明为类型  
* VB中，< 可能是小于号，也可能是XML直接量的开始，取决于  当前位置是否可以接受XML直接量  
* Python中，行首的tab符和空格会根据上一行的行首空白以一定  规则被处理成虚拟终结符indent或者dedent  
* JavaScript中，/ 可能是除号，也可能是正则表达式开头，处理  方式类似于VB，字符串模板中也需要特殊处理 }，还有自动插入 分号规则 

### 四、语言的分类 
* 形式语言—用途  
    * 数据描述语言  
    * 编程语言 
JSON, HTML, XAML, SQL, CSS  
C, C++, Java, C#, Python, Ruby,  Perl,  Lisp, T-SQL, Clojure, Haskell,  JavaScript 
* 形式语言—表达方式  
    * 声明式语言  
    * 命令型语言 
JSON, HTML, XAML, SQL, CSS,  Lisp, Clojure, Haskell 
C, C++, Java, C#, Python, Ruby,  Perl, JavaScript 
### 五、图灵完备性 
* 图灵完备性  
    * 命令式——图灵机  
        * goto 
        * if和while 
 * 声明式——lambda 
        * 递归 
### 六、动态与静态 
* 动态：  
    * 在用户的设备/在线服务器上  
    * 产品实际运行时  
    * Runtime  
* 静态：  
    * 在程序员的设备上  
    * 产品开发时  
    * Compiletime 
### 七、类型系统 
* 动态类型系统与静态类型系统  
* 强类型与弱类型  
    * String + Number  
    * String == Boolean  
* 复合类型  
    * 结构体  
    * 函数签名  
* 子类型  
* 泛型  
    * 逆变/协变 
### 八、计算机语言的分类

 1. 面向对象型和面向过程型

* 面向对象型：java，c++
* 面向过程型：c，fortran

面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了。面向对象是把构成问题事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为。

 2. 高级语言和低级语言

* 低级语言有：机器码、汇编语言，masm
* 高级语言：c，c++，java，python，PHP，c#，Ruby，go，kotlin，swift

高级语言与低级语言的区别：高级语言大部分不能直接更硬件打交道，这使得相对来的程序运行速度降低，总之一句话来说那种语言更接近人性化的语言就更高级。

 3. 动态类型和静态类型

* 动态类型：python，Ruby，Perl
* 静态类型：c，c++，Java、Delphi、C#

动态性语言是指在程序运行期间才给变量指定数据的类型，而静态类型语言则恰好相反，在写程序代码的时候就要指定变量的类型

 4. 编译型，解释型，半编译半解释
* 编译型语言：c，c++
* 解释型语言：python，JavaScript，Perl，shell
* 半编译半解释型语言：java

编译型语言在执行程序中会将源文件一次性的转化为机器码，而解释型语言是边编译边解释；编译型语言是离不开解释程序的，这也导致了解释性语言对于运行时候的速度比价慢，解释型语言只要有解释器，移植起来比较方便，而编译型语言则要对于不同的系统进行编译，是的工作繁琐，且在调试程序的时候比较慢。

 5. 强制类型和弱类型
* 强制类型：c，c++
* 弱类型：python
强制类型更严谨，更不容易出现错误，但弱类型的语言写起来更优雅，更舒畅
 