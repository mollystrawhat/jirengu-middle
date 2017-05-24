>讲解了运算符、运算符优先级相关知识点


>JavaScript 定义了几种数据类型? 哪些是原始类型?哪些是复杂类型?原始类型和复杂类型的区别是什么?
typeof和instanceof的作用和区别?
如何判断一个变量是否是数字、字符串、布尔、函数
NaN是什么? 有什么特别之处?
如何把非数值转化为数值?
==与===有什么区别
break与continue有什么区别
void 0 和 undefined在使用场景上有什么区别

## 1. JavaScript 定义了几种数据类型? 哪些是原始类型?哪些是复杂类型?原始类型和复杂类型的区别是什么?
>6种类型
 - 数值 （number）：整数和小数
 - 字符串（string）：字符组成的文本，一般用单引号或双引号包裹（比如"Hello World"，或者"hello 'word' "）
 - 布尔值（boolean）：true（真）和false（假）两个特定值
 - undefined：表示“未定义”或不存在，即此处目前没有任何值
 - null：表示空缺，即此处应该有一个值，但目前为空
 - 对象（object）：各种值组成的集合。
　　包括狭义的对象（object）
　　数组（array）
　　函数（function）
　　正则表达式 (regexp)

原始类型：
数值、字符串、布尔值称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。

复杂类型（引用类型）:
将对象称为复杂类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。

#### 区别：
>基本类型变量存的是值，复杂类型的变量存的是内存地址。
基本类型在赋值的时候拷贝值，复杂类型在赋值的时候只拷贝地址，不拷贝值。

1)存储方式
栈存储
因为原始值占据空间固定，是简单的数据段，为了便于提升变量查询速度，将其存储在**栈(stack)**中

堆存储
由于复杂值的大小会改变，所以不能将其存放在栈中，否则会降低变量查询速度，因此其存储在**堆(heap)**中，存储在变量处的值是一个指针，指向存储对象的内存处。

2)访问方式
原始值是作为不可细化的值进行存储和操作的，引用它们会**转移其值**
复杂值是通过引用进行存储和操作的，而不是实际的值。创建一个包含复杂对象的变量时，**其值是内存中的一个引用地址**。引用一个复杂对象时，使用它的名称(即变量或对象属性)通过内存中的引用地址获取该对象值

3)比较方式
原始值采用**值比较**，而复杂值采用**引用比较**。复杂值只有在引用相同的对象(即有相同的地址)时才相等。*即使是包含相同对象的两个变量也彼此不相等*，因为它们并不指向同一个对象

4)动态属性
对于复杂值，可以为其添加属性和方法，也可以改变和删除其属性和方法；但简单值不可以添加属性和方法

5)包装类型??
原始值被当作构造函数创建的一个对象来使用时，Javascript会将其转换成一个对象，以便可以使用对象的特性和方法，而后抛弃对象性质，并将它变回到原始值

详细的解释：
[JavaScript中的原始值和复杂值](http://www.jb51.net/article/77631.htm)
[JS里基本类型（值）和复杂类型（引用）有什么区别？](https://zhuanlan.zhihu.com/p/22400319)

## 2. typeof和instanceof的作用和区别?
 typeof运算符可以返回一个值的数据类型
```
1.原始类型
typeof 100 // "number"
typeof 'hello' // "string"
typeof true // "boolean"

2.函数
function f() {}                
typeof f   // "function"

3.typeof可以用来检查一个没有声明的变量，而不报错。实际编程中，这个特点通常用在判断语句
// 错误的写法
if (v) { }  // ReferenceError: v is not defined
// 正确的写法
if (typeof v === "undefined") { }

4.undefined
typeof undefined  // "undefined"

5.除此以外，其他情况都返回object。
typeof window // "object"
typeof {} // "object"
typeof [] // "object"
typeof null // "object"
```
instanceof区分数组和对象。
而typeof的第5 项返回的都是对象，不能判断是否为数组。
```
[]1,2,3] instanceof  Array   //true
var obj={}
obj instanceof Array      //false
```

## 3. 如何判断一个变量是否是数字、字符串、布尔、函数
在console中使用typeof，参照第二题

## 4. NaN是什么? 有什么特别之处?
NaN的含义是：不是一个数字。
要检测一个值是否是NaN，可以使用全局函数isNaN()
```
isNaN(3)   //false
```
NaN和任何值都不相等，包括自己。因为
```
parseInt('abc')   //NaN
parseInt('def')   //NaN
但是'abc'并不等于'def'
```
```
NaN==NaN    //false```
## 5. 如何把非数值转化为数值?
参考
[阮一峰  Number](http://javascript.ruanyifeng.com/grammar/conversion.html)
[阮一峰 parseInt   parseFloat](http://javascript.ruanyifeng.com/grammar/number.html)
>Number()
parseInt()
parseFloat()

 - Number

Number()函数的转换规则如下：
如果是Boolean值，true和false将分别被转换为1和0。
如果是数字值，只是简单返回数值。
如果是null值，返回0。
如果是undefined，返回NaN。
```
Number(123) // 123
Number('000111') // 111
Number("hello word");//NaN
Number("");//0
Number(null);//0
Number("ture");//1
Number(undefined) // NaN
Number('42 cats') // NaN
```
 - parseInt
parseInt方法用于将字符串转为整数。
```
parseInt('123')      // 123
```
如果字符串头部有空格，空格会被自动去除。
```
parseInt('   123')   // 123
```
如果parseInt的参数不是字符串，则会先转为字符串再转换。相当于只取整数部分
```
parseInt(1.7) // 1
// 等同于
parseInt('1.7') // 1
```
字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分。
```
parseInt('8a') // 8
parseInt('12**') // 12
```
如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回NaN。
```
parseInt('abc') // NaN
(parseInt('.3') // NaN     ☆       
parseInt('') // NaN
parseInt('+') // NaN
parseInt('+1') // 1        ☆
```

## 6. ==与===有什么区别
参考：
[阮一峰  运算符4.3](http://javascript.ruanyifeng.com/grammar/operator.html#toc9)
简单说，它们的区别是相等运算符（==）比较两个值是否相等，严格相等运算符（===）比较它们是否为“同一个值”。如果两个值不是同一类型，严格相等运算符（===）直接返回false，而相等运算符（==）会将它们转化成同一个类型，再用严格相等运算符进行比较。

## 7. break与continue有什么区别
break是结束整个循环体，continue是结束本次循环


## 8. void 0 和 undefined在使用场景上有什么区别？
undefined
变量声明后未赋值，则变量会被自动赋值为undefined;
函数中定义了一些形参，如果传入的实参少于预定义的形参，那么有一些形参就会匹配不到实参，继而会被自动赋值为undefined;
没有返回值的函数，默认返回undefined;

void运算符
void 运算符后面接一个表达式，无论表达式的内容是什么，只要跟在void 之后都会被调用执行，执行完毕之后void操作符返回undefined;
使用void 0生成undefined，既减少了在原形链上查找window.undefined的时间,也避免了误用被修改过的undefined。
```
function fn(){
    var undefined=3;
    if(a===undefined){
        console.log('===')
     }
    else{
           console.log('!==')}    
 }                                     //!==

function fn(){
    var undefined=3;
    if(a===void 0){
        console.log('===')
     }
    else{
           console.log('!==')}    
 }                                     //===
```
参考
http://www.jianshu.com/p/4b2f32e3119e
## 9. 以下代码的输出结果是?为什么?
```
console.log(1+1);//2，两个数字相加
console.log("2"+"4");//'24'，两个字符串拼接
console.log(2+"4");//'24'，一个是数字一个是字符串，数字转化为字符串后拼接
console.log(+"4");//4，只有一个字符串会转换成数字输出
```

```
var a = 1;  
a+++a;  
typeof a+2;    

//"number2"
//因为++的优先级高于+，先算a++为1，此时的a已经是2，则a+++a,1+2=3；
//typeof的优先级高于+，先算typeof a得出"number",  "number"+2,字符串和数字结合，输出为字符串"number2"
```

```
var a = 1;
var b = 3;
console.log( a+++b );

//输出4
//因为++的优先级高于+，a++为1,1+b=1+3=4
```
 遍历数组，打印数组每一项的平方
```
 var arr = [3,4,5]
//for(i=0; i<arr.length;i++){
console.log(arr[i]*arr[i])
}

输出9，16，25
```
 遍历 JSON, 打印里面的值
```
var obj = {
 name: 'hunger', 
 sex: 'male', 
 age: 28 
}

for(var key in obj){
console.log(obj[key])

输出 hunger，male，28

```
 以下代码输出结果是? 为什么 （选做题目）
```
var a = 1, b = 2, c = 3;
var val = typeof a + b || c >0
console.log(val) 

//输出number2
//((typeof a) + b) || (c >0)
typeof优先级高于+，typeof a 为number，("number" + b) || (c >0)
("number2" ) || (c >0)    "number2"是非空数组，为true，||不再计算后面的，直接输出number2

//只要“||”前面为true，无论“||”后面是true还是false，结果都返回“||”前面的值。
```


```
var d = 5;
var data = d ==5 && console.log('bb')
console.log(data)
//输出bb
//data ==5 && console.log('bb')，又因为&&的左结合，所以得出bb
```
```
var data2 = d = 0 || console.log('haha')
console.log(data2)
//输出haha
//
```
``` 
var x = !!"Hello" + (!"world", !!"from here!!");
console.log(x)
//输出2，空字符串为false，非空则为true，
//var x = true+(false+true),true为1，false为0，1+1=2。
```
