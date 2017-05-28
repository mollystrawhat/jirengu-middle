## 讲解了字符串的详细使用方法，JSON 对象的相关概念

## 1、使用数组拼接出如下字符串
```
var prod = {
    name: '女装',
    styles: ['短款', '冬季', '春装']
};
function getTplStr(data){
        var dt = '<dt>' + data.name + '</dt>'
        var dd = ''
        for (var i=0;i<data.styles.length;i++)
        var dd = dd + '<dd>' + data.styles[i] +'</dd>' 
    return '<dl class="product">' + dt + dd + '</dl>'
};
var result = getTplStr(prod);  //result为下面的字符串

<dl class="product">
    <dt>女装</dt>
    <dd>短款</dd>
    <dd>冬季</dd>
    <dd>春装</dd>
</dl>
```




## 2、写出两种以上声明多行字符串的方法

```
法一：使用\，注意：\后不能有空格也不能有其他的字符。如果报错，不容易检查出来
var str = 'happy\
every\
day'


法二：多行注释
(function () { /*
line 1
line 2
line 3
*/}).toString().split('\n').slice(1,-1).join('\n')
如果没有.join('\n')输出["line 1", "line 2", "line 3"]
如果有，\n的作用是换行，输出
"line 1
line 2
line 3"


法三：使用+
var str = 'happy'
+'every'
+'day'


```



## 3、补全如下代码,让输出结果为字符串: hello\\饥人谷
```
var str = "hello\\\\饥人谷"
console.log(str)
```





## 4、以下代码输出什么?为什么
```
var str = 'jirengu\nruoyu'
console.log(str.length)
//输出13，\n是转义符，相当于一个字符
```






## 5、写一个函数，判断一个字符串是回文字符串，如 abcdcba是回文字符串, abcdcbb不是
```
法一：
var str="abcdcba"
str==str.split('').reverse().join('')//输出true
var str1="abcdcbb"
str1==str1.split('').reverse().join('')//输出false
```
```
法二：
function palindrome(str){
    for (var i = 0; i < str.length/2; i++) {
        if (str[i] == str[str.length-1-i]) {
        }
        else{
            return false;
        }
    return true;
    }
 }
palindrome('abcdcba');
palindrome('abcdcbb')
```



## 6、写一个函数，统计字符串里出现频率最多的字符
```
var str="skajdblljbckjsgf7eghbjjbcgf"
var dict={}
for(var i=0;i<str.length;i++){
    if(dict[str[i]]){
        ++dict[str[i]]
    }
    else{
        dict[str[i]]=1
    }
}

var count=0
var maxValue
for(key in dict){
    if(dict[key]>count){
        maxValue=key
        count=dict[key]
    }
}

console.log(count,maxValue)
```





## 7、写一个camelize函数，把my-short-string形式的字符串转化成myShortString形式的字符串，如
```
camelize("background-color") == 'backgroundColor'
camelize("list-style-image") == 'listStyleImage'
```
```
upperCase("my-short-string")
function upperCase(str) {
  var array = str.toLowerCase().split("-");//声明一个数组，是原始字符串把-去掉以后每个单词组成的
  for (var i = 0; i < array.length; i++){
    array[i] = array[i][0].toUpperCase() + array[i].substring(1, array[i].length);//数组的第i个单词是此单词的第0个字母变为大写加上剩下的，此处运用了sunstring截取
  }
  var string = array.join("");//遍历结束以后变量声明，用""连接每个单词

  console.log(string);
}

```



## 8、写一个 ucFirst函数，返回第一个字母为大写的字符 （***）
```
function ucFirst(str){
  var newstr = str[0].toUpperCase()+str.substring(1,str.length);
  return newstr;
}
ucFirst("hunger");
```
## 9、写一个函数truncate(str, maxlength), 如果str的长度大于maxlength，会把str截断到maxlength长，并加上...，如
```
function truncate(str,maxlength){
    if(str.length > maxlength){
        return str.slice(0,maxlength)+"..."
    }
    else{
        return str;
    }
}
truncate("hello, this is hunger valley", 10);
truncate("hello world", 20);
```
## 10、什么是 json？什么是 json 语言？JSON 语言如何表示对象？window.JSON 是什么？
 - 什么是 json？
JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。它基于JavaScript（Standard ECMA-262 3rd Edition - December 1999）的一个子集。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C, C++, C#, Java, JavaScript, Perl, Python等）。这些特性使JSON成为理想的数据交换语言。 **易于人阅读和编写，同时也易于机器解析和生成(网络传输速度)**。

 - JSON 语言如何表示对象？
在 JS 语言中，一切都是对象。因此，任何支持的类型都可以通过 JSON 来表示，例如字符串、数字、对象、数组、布尔值、null等。但是对象和数组是比较特殊且常用的两种类型：

对象表示为键值对   
数据由逗号分隔    
花括号保存对象     
方括号保存数组 
```
var json={"name":"xiaoming","age","20"}
var json1 = [
    {"name":"xiaoming","age":"20"}, 
    {"name": "xiaohua","age": "25"}
]
```

 - window.JSON 是什么？
window.JSON 用于判断浏览器是否兼容JSON。IE8以上兼容



## 11、如何把JSON 格式的字符串转换为 JS 对象？如何把 JS对象转换为 JSON 格式的字符串?
```
var str='{"name": "hello","age":"30"}'
var obj=JSON.parse(str)//把JSON 格式的字符串转换为 JS 对象

var obj = {
    "name":"hello",
    "age":30
}
var str=JSON.stringify(obj)//把 JS对象转换为 JSON 格式的字符
console.log(JSON.stringify(obj))


eval,一般不用，但需要了解
var json_str='{ "name": "hello", "age":"30"}'
var json=eval('('+json_str+')')//把JSON 格式的字符串转换为 JS 对象

```
