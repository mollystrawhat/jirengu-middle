## 主要讲解了引用类型、对象深拷贝和浅拷贝


1.引用类型有哪些？非引用类型有哪些

引用类型值（对象、数组、函数、正则）：指的是那些保存在堆内存中的对象，变量中保存的实际上只是一个指针，这个指针执行内存中的另一个位置，由该位置保存对象

非引用类型,即基本类型值（数值、布尔值、null和undefined）：指的是保存在栈内存中的简单数据段；
2.如下代码输出什么？为什么
```
var obj1 = {a:1, b:2};
var obj2 = {a:1, b:2};
console.log(obj1 == obj2);//输出false，因为两者的存储路径不一样
console.log(obj1 = obj2);//输出Object  {a:1, b:2}，赋值以后就相当于引用路径，此时路径一致
console.log(obj1 == obj2);//输出true，经过赋值，两者的路径已经完全一致，因此输出true

```




3.如下代码输出什么? 为什么
```
var a = 1
var b = 2
var c = { name: '饥人谷', age: 2 }
var d = [a, b, c]

var aa = a
var bb = b
var cc = c
var dd = d

a = 11//非引用类型只引用值，a的值变为11，aa的值还是1
b = 22//非引用类型只引用值，b的值变为22，bb的值是2
c.name = 'hello'//引用类型，引用的是路径，c和cc都改变为{ name: 'hello', age: 2 }
d[2]['age'] = 3//引用类型，c和cc都改变为{ name: 'hello', age: 3}

console.log(aa)  //输出1
console.log(bb)  //输出2
console.log(cc)  //输出Object {name: "hello", age: 3}
console.log(dd)  //输出Array(3)[1, 2, Object]
```


4.如下代码输出什么? 为什么
```
var a = 1
var c = { name: 'jirengu', age: 2 }

function f1(n){         //添加var n=a=1
  ++n      //此时n=2，但是a的值并没有变，还是1
}         
function f2(obj){      //添加var obj=c
  ++obj.age     //c的age是2,2+1=3
}

f1(a) 
f2(c) 
f1(c.age) //这个时候的age还是3
console.log(a) //输出1
console.log(c) //输出object，{age:3；name:"jirengu"}

```





5.过滤如下数组，只保留正数，直接在原数组上操作
```
var arr = [3,1,0,-1,-3,2,-5]
function filter(arr){
    for(i=0; i<arr.length;i++){
        if(arr[i]<=0){
          arr.splice(i,1)
          filter(arr)
        }
    }
}
filter(arr)
console.log(arr) 
```





6.过滤如下数组，只保留正数，原数组不变，生成新数组
```
var arr = [3,1,0,-1,-3,2,-5]
function filter(arr){
}
var arr2 = filter(arr)
console.log(arr2) // [3,1,2]
console.log(arr)  // [3,1,0,-1,-2,2,-5]
```
```
var arr = [3,1,0,-1,-3,2,-5];
var arr2 = [3,1,0,-1,-3,2,-5];
function filter(arr2) {
    for(var i=0;i<arr2.length;i++) {
        if(arr2[i]<=0) {
            arr2.splice(i,1);
            filter(arr2);
        }
    }
}
        filter(arr2);
        console.log(arr);
        console.log(arr2);
//对arr什么都不做，对arr2保留正数
```


7.写一个深拷贝函数，用两种方式实现
```
法一：
function deepCopy(oldObj){
  var newObj = {};
  for(var key in oldObj){
    if(typeof oldObj[key] === 'number' || 
      typeof oldObj[key] === 'string' || 
      typeof oldObj[key] === 'boolen' || 
      oldObj[key] === null ||
      oldObj[key] === undefined){ 
      newObj[key] = oldObj[key];
      }
    else{
      newObj[key] = deepCopy(oldObj[key]);
      }
  }
  return newObj;
}

法二：
 function deepCopy(oldObj){
        var newObj = JSON.parse(JSON.stringify(oldObj));
        return newObj;
 }
```
