## 讲解正则表达式详细的用法


## 题目1： \d,\w,\s,[a-zA-Z0-9],\b,.,*,+,?,x{3},^,$分别是什么?

\d     匹配数字
\w    匹配**字母**或**数字**或**下划线**或**汉字**
\s     匹配任意的空白符
[a-zA-Z0-9]      匹配a-z，A-Z，0-9
\b     匹配单词的开始或结束
.       匹配除换行符以外的任意字符
\*      重复零次或更多次
\+     重复一次或更多次
?     重复零次或一次
x{3}   x重复3次
^      匹配字符串的开始
$	匹配字符串的结束




## 题目2： 写一个函数trim(str)，去除字符串两边的空白字符

```
function trim(str){
    return str.replace(/^\s+|\s+$/g, '');
}

var str=' 12 34 ';
trim(str);//输出"12 34"
```





## 题目3： 写一个函数isEmail(str)，判断用户输入的是不是邮箱
```
function isEmail(str){
    if(/^\w+@[\w.-]+$/.test(str)) return true;
    return false;
   }

var str='3hjknn738@qq.ocm';
isEmail(str);//输出true
```





## 题目4： 写一个函数isPhoneNum(str)，判断用户输入的是不是手机号
```
function isPhoneNum(str){
    if(/^1[356789]\d{9}$/.test(str)) return true;
    return false;  
}

var str='14589073690';
isPhoneNum(str);//输出false,因为是14开头
```





## 题目5： 写一个函数isValidUsername(str)，判断用户输入的是不是合法的用户名（长度6-20个字符，只能包括字母、数字、下划线）
```
function isValidUsername(str){
    if(/^\w{6,20}$/.test(str)){
        return true;
    }
    else{
        return false;
    }
}

var str='167895468.';
isValidUsername(str);//因为有.输出false
```





## 题目6： 写一个函数isValidPassword(str), 判断用户输入的是不是合法密码（长度6-20个字符，只包括大写字母、小写字母、数字、下划线，且至少至少包括两种）

```
function isValidPassword(str){
    if(/\W/.test(str)||str.length<6||str.length>20) return false;
    if(/^[A-Z]+$/.test(str)) return false;
    if(/^[0-9]+$/.test(str)) return false;
    if(/^[a-z]+$/.test(str)) return false;
    if(/^_+$/.test(str)) return false;
    return true;
   
}
var str='167';
isValidPassword(str);//输出false
```




## 题目7： 写一个正则表达式，得到如下字符串里所有的颜色
```
var re = /#[A-Fa-f0-9]{6}/g;
var subj = "color: #121212; background-color: #AA00ef; width: 12px; bad-colors: f#fddee "
console.log( subj.match(re) )  // ['#121212', '#AA00ef']
```





## 题目8： 下面代码输出什么? 为什么? 改写代码，让其输出[""hunger"", ""world""].
```
var str = 'hello  "hunger" , hello "world"';
var pat =  /".*"/g;//匹配""里面除了回车符和换行符之外的所有字符，将" , hello "也匹配上了。
str.match(pat);//输出[""hunger" , hello "world""]


改为：
var str = 'hello  "hunger" , hello "world"';
var pat =  /".*?"/g;
str.match(pat);

```
