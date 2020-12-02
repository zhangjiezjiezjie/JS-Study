
# 执行栈
执行栈，也叫调用栈，具有 LIFO（后进先出）结构，用于存储在代码执行期间创建的所有执行上下文。

首次运行JS代码时，会创建一个全局执行上下文并Push到当前的执行栈中。每当发生函数调用，引擎都会为该函数创建一个新的函数执行上下文并Push到当前执行栈的栈顶。

根据执行栈LIFO规则，当栈顶函数运行完成后，其对应的函数执行上下文将会从执行栈中Pop出，上下文控制权将移到当前执行栈的下一个执行上下文。



当 JavaScript 初始化的时候会向执行上下文栈压入一个全局执行上下文，我们用 globalContext 表示它，并且只有当整个应用程序结束的时候，执行栈才会被清空，所以程序结束之前， 执行栈最底部永远有个 globalContext。

ECStack = [		// 使用数组模拟栈
    globalContext
];

# 找不同
有如下两段代码，执行的结果是一样的，但是两段代码究竟有什么不同？
```js
var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f();
}
checkscope();

ECStack.push(<checkscope> functionContext)
ECStack.push(<f> functionContext)
ECStack.pop()
ECStack.pop()



var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f;
}
checkscope()();

ECStack.push(<checkscope> functionContext)
ECStack.pop()
ECStack.push(<f> functionContext)
ECStack.pop()

```


# 变量对象VO
在写程序的时候会定义很多变量和函数，那js解析器是如何找到这些变量和函数的？
变量对象是与执行上下文对应的概念，在执行上下文的创建阶段，它依次存储着在上下文中定义的一些内容
变量对象（VO）是规范上或者是JS引擎上实现的，并不能在JS环境中直接访问

# 全局上下文
在global全局上下文中，变量对象（VO）也是全局对象自身

```js
    console.log(test) 
    console.log(b) 
    function test() {
 
    }
    var test = 123
    var b = 456

```
# 执行过程
执行上下文的代码会分成两个阶段进行处理

1、创建阶段（预编译阶段）
  1. 找变量声明 作为VO的属性名 值为undefined
  2. 找函数声明：如果变量对象已经存在相同名称的属性，则完全替换这个属性。
2、代码执行


# 函数上下文
在函数上下文中，用活动对象(activation object, AO)来表示变量对象。

当进入到一个执行上下文后，这个变量对象才会被激活，所以叫活动对象（AO），这时候活动对象上的各种属性才能被访问。
调用函数时，会为其创建一个Arguments对象，并自动初始化局部变量arguments，指代该Arguments对象。所有作为参数传入的值都会成为Arguments对象的数组元素。

# 执行过程
执行上下文的代码会分成两个阶段进行处理
```js
    function fn(a, c) {
      console.log(a) 
      var a = 123
      console.log(a) 
      console.log(c)  
      function a() { }
      if (false) {
        var d = 678
      }
      console.log(d) 
      console.log(b) 
      var b = function () { }
      console.log(b) 
      function c() { }
      console.log(c) 
    }
    fn(1, 2)
```
1、创建阶段（预编译阶段）
  1. 找形参和变量声明 作为AO的属性名 值为undefined
  2. 将实参和形参相统一
  3. 找函数声明：如果变量对象已经存在相同名称的属性，则完全替换这个属性。
2、代码执行



# 代码执行




## 预编译习题讲解

```js
console.log(b)
console.log(test)
function test(a){
  console.log(c)
  var a = b = 345
  c = 9
  if(false){
    var c = 789
  }
  console.log(a)
  console.log(c)
}
test(234)
console.log(b)
console.log(test)
var test = 123
var b = 456



```


## 前端东西多 杂 
- 杂 不精 
- 养成解决问题的思维 
- 你要知道你自己在干什么 时时刻刻记住自己的目标 
  - 百度 
  - 
