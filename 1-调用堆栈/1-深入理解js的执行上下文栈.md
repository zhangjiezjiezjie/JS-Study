 ## 执行栈
     执行栈，也叫调用栈，具有LIFO(后进先出)结构，用于存储在代码执行期间创建的所有执行上下文。
    
     首次运行JS代码时，会创建一个全局执行上下文并Push到当前的执行栈中；每当发生函数调用，引擎都会为该函数创建一个新的函数执行上下文并Push到当前执行栈的栈顶。
    
     根据执行栈LIFO规则，当栈顶函数运行完成后，其对应的函数执行上下文将会从执行栈中Pop出，上下文控制权将移到当前执行栈的下一个执行上下文。
    
     当JavaScript初始化的时候会向执行上下文栈压入一个全局执行上下文，我们用globalContext表示它，并且只有当整个程序结束的时候，执行栈才会被清空，所以程序结束前，执行栈最底部永远有个globalContext.
    
     ECStack = [ //使用数组模拟栈
         globalContext
     ]
 ## 变量对象（VO）
     在写程序的时候会定义很多变量和函数，js解析器是如何找到这些变量和函数的？
     变量对象是与执行上下文对应的概念，在执行上下文创建的阶段，它依次存在着在上下文中定义的一些内容
     变量对象(VO)是规范上或者是JS引擎上实现的，并不能在JS环境中直接访问
 
 ## 全局上下文
   在global全局上下文中，变量对象（VO）也是全局对象自身
 ```js
    console.log(test)
    console.log(b)
    function test() {
      
    }
    var test = 123
    var b = 456

//执行上下文过程
    var test;
    var b;
    function test(){
    
    }
    OV:{
       test: undefined function test(){}
       b:undefined
    }
 ```
## 执行过程
    执行上下文的代码会分成两个阶段进行处理
     1、创建阶段（预编译阶段）
       1.找变量声明：作为变量对象的属性名，值为undefined
       2.找函数声明：如果变量对象已经存在相同名称的属性，则完全替换这个属性
     2、代码执行阶段
## 函数上下文
     在函数上下文中，用活动对象（activation object,AO)来表示变量对象
     
     当进入到执行上下文后，这个变量对象才会被激活，所以叫活动（AO），这时候活动对象上的各种属性才能被访问。
     调用函数时，会为其创建一个Argguments对象，并自动初始化局部变量arguments，指代该arguments对象，所有作为参数传入的之都会成为Arguments对象的数组元素。
 # 执行过程
    执行上下文的代码会分成两个阶段进行处理：
```
function fn(a,c) {
  console.log(a);//function a() { }
  var a = 123;
  console.log(a); // 123
  console.log(c); //function c() { }
  function a() { }
  if(false){
      var d = 678; //不执行
  }
  console.log(d); //undefined
  console.log(b); // undefined
  var b = function () { }
  console.log(b); //function () { }
  function c() { }
  console.log(c); // function c() { }
}
fn(1,2); // 实参和形参统一
```
    1、创建阶段（预编译阶段）
       找形参和变量声明:作为AO的属性名 值为undefined
       将实参和形参统一
       找函数声明(function开头的；var a = function(){ }叫函数表达式): 如果变量对象已经存在相同名称的属性，则完全替换这个属性
    2、代码执行

