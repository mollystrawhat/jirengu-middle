### 讲解函数声明、函数表达式、声明前置、作用域、作用域链相关概念


>1. 函数声明和函数表达式有什么区别
2. 什么是变量的声明前置？什么是函数的声明前置
3. arguments 是什么
4. 函数的"重载"怎样实现
5. 立即执行函数表达式是什么？有什么作用
6. 求n!，用递归来实现
7. 以下代码输出什么？

## 1. 函数声明和函数表达式有什么区别
 - 解析过程的区别
1) 声明总是在作用域开始时先行解析；也就是会声明前置。
因此声明不必放到调用的前面，函数表达式声明必须放到调用的前面
2) 表达式在遇到时候才运算。

```
alert(fn()); //输出Helloworld!   
 
function fn() {
return 'Helloworld!';
}
//函数 fn 是在 alert 后面声明的。但是，在alert 执行的时候，fn已经有定义了
```
 - 函数声明 **必须始终带有一个标识符（Identifier）**，也就是我们所说的函数名，而函数表达式则可以省略。

```
function Identifier ( FormalParameterList opt){ FunctionBody }
 //函数声明
function Identifier opt( FormalParameterList opt){ FunctionBody }  
//具名函数表达式
function Identifier ( FormalParameterList opt){ FunctionBody }  
//匿名函数表达式
```
 - ECMAScript是通过上下文来区分这两者的：假如 function foo(){} 是一个赋值表达式的一部分，则认为它是一个函数表达式。而如果 function foo(){} 被包含在一个函数体内，或者位于程序（的最上层）中，则将它作为一个函数声明来解析。

```
function foo(){}; // 声明，因为它是程序的一部分
 
var bar = function foo(){}; // 表达式，因为它是赋值表达（AssignmentExpression）的一部分
 
new function bar(){}; // 表达式，因为它是New表达式（NewExpression）的一部分
 
(function(){
    function bar(){}; // 声明，因为它是函数体（FunctionBody）的一部分
})();
 
(function foo(){}); // 函数表达式：注意它被包含在分组操作符中,而分组操作符只能包含表达式
 
try {
(var x = 5); // 分组操作符只能包含表达式，不能包含语句（这里的var就是语句）
}
catch(err) {
// SyntaxError（因为“var x = 5”是一个语句，而不是表达式——对表达式求值必须返回值，但对语句求值则未必返回值。——译
}
```
详细请参考：
[JavaScript中的函数声明和函数表达式区别浅析](http://www.jb51.net/article/62980.htm)






## 2. 什么是变量的声明前置？什么是函数的声明前置
 - 变量的声明前置
所有的变量声明语句，都会被提升到代码的头部，然后给他初始值undefined，然后才逐句执行程序，这就叫做“变量提升”，也即“变量的声明前置”。

```
var a = 1;
function main() {
    console.log(a);
    var a = 2;
}
main()//输出undefined
```

解析如下：
```
var a = 1;
function main() {
    var a;        //这时的a是undefined
    console.log(a);
    a = 2;
}
```
 - 函数的声明前置

```
console.log(fn());   //虽然函数fn()写在后面，但是由于函数的声明前置，所以在调用fn()的时候函数是已经被解析的。
function fn(){
    console.log('hello')
}
//输出hello
```



## 3. arguments 是什么
Arguments是个类似数组但不是数组的对象，说他类似数组是因为其具备数组相同的**访问性质及方式**，能够由arguments[n]来**访问**对应的单个参数的值，并拥有数组长度属性**length**。还有就是arguments对象存储的是实际 传递给函数的参数，而不局限于函数声明所定义的参数列表，而且不能显式创建 arguments 对象。

```
function howManyArgs() {
  console.log(arguments.length);
}
howManyArgs("string", 45);
howManyArgs();
howManyArgs(12);
//依次显示2,0,1
```



## 4. 函数的"重载"怎样实现
C++允许在同一范围中声明几个功能类似的同名函数，但是这些同名函数的形式参数（指参数的个数、类型或者顺序）必须不同，也就是说用同一个运算符完成不同的运算功能。这就是重载函数。

但是JS是不允许重载的，同名函数会覆盖。只能通过一些判断来模拟重载。
```
function doAdd() {
  if(arguments.length == 1) {
    console.log(arguments[0] + 5);
  } else if(arguments.length == 2) {
   console.log(arguments[0] + arguments[1]);
  }
}
doAdd(10);//输出 15
doAdd(10,20);//输出 30
```



## 5. 立即执行函数表达式是什么？有什么作用
立即执行函数就是
声明一个匿名函数，并马上调用这个匿名函数

表达式
```
[function fn(){var a=3}]()
,function fn(){var a=3}()
!function fn(){var a=3}()
```
作用：将全局变量与局部变量分隔开，保证全局变量不受污染。


```
(function fn(){var a=3})
var a=5;
```
详细请看：
[什么是立即执行函数？有什么作用？](http://www.cnblogs.com/mafeifan/p/5881408.html)





## 6. 求n!，用递归来实现
```
function fn(n){
    if(n===1){
          return 1
}
    else{
          return n*fn(n-1)
}
}

fn(4)//输出24
```





## 7. 以下代码输出什么？
```	
function getInfo(name, age, sex){
		console.log('name:',name);
		console.log('age:', age);
		console.log('sex:', sex);
		console.log(arguments);
		arguments[0] = 'valley';
		console.log('name', name);
	}
```
```
getInfo('饥人谷', 2, '男');
>//输出结果
 name: 饥人谷
 age: 2
 sex: 男
 ["饥人谷", 2, "男", callee: function, Symbol(Symbol.iterator): function]
name valley
```

```
getInfo('小谷', 3);
//
name: 小谷
 age: 3
 sex: undefined
 ["小谷", 3, callee: function, Symbol(Symbol.iterator): function]
 name valley
```

```
getInfo('男');
name: 男
age: undefined
sex: undefined
 ["男", callee: function, Symbol(Symbol.iterator): function]

```

## 8. 写一个函数，返回参数的平方和？

```

function sumOfSquares() {
	var result = 0;
	for(var i=0; i<arguments.length; i++){
	  result = result + arguments[i]*arguments[i]
	}
	return result;
}
var result = sumOfSquares(2,3,4)
var result2 = sumOfSquares(1,3)
console.log(result) 
console.log(result2) 
```



## 9. 如下代码的输出？为什么
```
	console.log(a);
	var a = 1;
	console.log(b);  //输出undefined，同时报错：b is not defined。因为变量声明会前置，并赋值undefined
                    即var a=undefined
                        console.log(a);
                        console.log(b);
                        a=1
```



## 10. 如下代码的输出？为什么
```
    sayName('world');
	sayAge(10);
	function sayName(name){
		console.log('hello ', name);
	}
	var sayAge = function(age){
		console.log(age);
	};//输出hello  world，同时报错sayAge is not a function。因为这是一个函数表达式，声明必须放到调用的前面，而这里声明放在了后面。
```
## 11. 如下代码输出什么? 写出作用域链查找过程伪代码
```
var x = 10
bar() 
function foo() {
  console.log(x)  //输出10
}
function bar(){ 
  var x = 30
  foo()           //此时barContext: Ao中没有foo，转去bar.scope即globalContext中发现有foo，因此还是输出10
}//输出10
```
```
globalContext:{
  Ao{ x:10;
      foo:function;
      bar:function;
      }
}
  foo[[scope]]=globalContext.Ao
  bar[[scope]]=globalContext.Ao

fooContext:{
  Ao:{}
scope:globalContext.Ao
}

barContext:{
  Ao:{x:30}
scope:globalContext.Ao
}


```

## 12. 如下代码输出什么? 写出作用域链查找过程伪代码

```
var x = 10;
bar()             //依旧为30
function bar(){
  var x = 30;
  function foo(){
    console.log(x) //输出30，fooContext.Ao为空，转去scope即barContext.Ao，有x:30,yinci shuchu 30
  }
  foo();  //调用foo，因此还是30
}//输出30
```	

```
globalContext:{
  Ao{ x:10;
      bar:function;
      }
}
  bar[[scope]]=globalContext.Ao


barContext:{
   Ao:{x:30
      foo:function
}
foo[[scope]]=barContext.Ao 
}

fooContext:{
  Ao:{}
scope:barlContext.Ao
}
```




## 13.以下代码输出什么? 写出作用域链的查找过程伪代码
```
var x = 10;
bar() 
function bar(){
  var x = 30;
  (function (){
    console.log(x)
  })()//这是立即执行函数表达式，外部的var x = 10，并不会影响里面的执行。输出30
}//输出30
```

```
globalContext:{
  Ao{ x:10;
      bar:function;
      }
}
  bar[[scope]]=globalContext.Ao


barContext:{
   Ao:{x:30}
foo[[scope]]=barContext.Ao 
}
```







## 14.以下代码输出什么？ 写出作用域链查找过程伪代码
```
var a = 1;
function fn(){
  console.log(a)//输出undefined
  var a = 5
  console.log(a)//输出5
  a++
  var a
  fn3()//调用fn3函数，最后输出1
  fn2()//调用fn2函数，最后输出20
  console.log(a)//输出20

  function fn2(){
    console.log(a)
    a = 20
  }//因上方调用调用fn2函数，输出20
}

function fn3(){
  console.log(a)
  a = 200
}//因上方调用调用fn3函数，输出1

fn()
console.log(a)//输出200


依次输出undefined，5，1，6，2，200
```
```
globalContext:{
  Ao:{a:1-->200
    fn:function
    fn3:function
}
}
fn[[scope]]=globalContext.Ao
fn3[[scope]]=globalContext.Ao

fnContext:{
    Ao:{
    a:undefined-->5-->6-->20
    fn2:function
}
scope:globalContext.Ao
}

fn3Context{
Ao:{}
scope:globalContext.Ao
}

fn2Context{
Ao:{}
scope:fnContext.Ao
}
```
