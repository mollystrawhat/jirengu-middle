## 讲解了数组、Math 对象、日期函数的用法，包含大量常见使用场景

# Math任务

## 1、写一个函数，返回从min到max之间的 随机整数，包括min不包括max 
```
//获取[15,20)之间随机整数
var num=15+Math.floor(Math.random()*5)
```
## 2、写一个函数，返回从min都max之间的 随机整数，包括min包括max 
```
获取[15,20]之间随机整数
var num=15+Math.floor(Math.random()*6)
```


## 3、写一个函数，生成一个长度为 n 的随机字符串，字符串字符的取值范围包括0到9，a到 z，A到Z。
```
function getRandStr(len){
    var dic='abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
    var idx,str='';//同时声明两个变量，等同于var idx；var str='';
    for(var i=0;i<len;i++){
        idx=Math.floor(Math.random()*62);
        str+=dic[idx]
    }
    return str;
}
var str = getRandStr(20);//长度为几就填几，此处长度n=20
```
## 4、写一个函数，生成一个随机 IP 地址，一个合法的 IP 地址为 0.0.0.0~255.255.255.255
```
function getRandIP(){
    var address='';
    for(var i=0;i<4;i++){
        var num =Math.floor(Math.random()*256);
        address=address+num+'.'
    }
    address=address.substr(0,address.length-1);
    return address;
}
var ip = getRandIP()
console.log(ip)
```
## 5、写一个函数，生成一个随机颜色字符串，合法的颜色为#000000~ #ffffff
```
function getRandColor(){
    var dic='0123456789abcdef'
    var idx,arr=[];
     for(var i=0;i<6;i++){
        idx=Math.floor(Math.random()*16);
        arr+=dic[idx]
    }
    arr="#"+arr
    return arr;
}
var color = getRandColor()
console.log(color)
```


# 数组任务
## 1、数组方法里push、pop、shift、unshift、join、splice分别是什么作用？用 splice函数分别实现push、pop、shift、unshift方法
push：在末尾添加
pop：在末尾删除
```
var a = new Array(1,2,3);
a.push(20);
console.log(a);//[1, 2, 3, 20]
a.pop()
console.log(a);//[1, 2, 3]
```

unshift：在头部添加
shift：在头部删除
```
var a = new Array(13,52,3);
a.unshift(20);
console.log(a);//[20,13,52,3]
a.shift()
console.log(a);//[13,52,3]
```
join：用什么连接
```
var a = new Array(13,52,3);
a.join('-')
console.log(a);//"13-52-3"
```
splice：一次性解决数组添加、删除（这两种方法一结合就可以达到替换效果）

```
第1个位置的数字是从下标为几的开始
第2个位置的数字是从当前取几个
从第3个位置开始是添加进去的东西


var a = new Array(13,52,3);
a.splice(a.length,0,20);   //push

var a = new Array(13,52,3);
a.splice(a.length-1,1);    //pop

var a = new Array(13,52,3);
a.splice(0,0,20);          // unshift

var a = new Array(13,52,3);
a.splice(0,1);             //shift

```






## 2、写一个函数，操作数组，数组中的每一项变为原来的平方，在原数组上操作
```
function squareArr(arr){
    var length = length1 = arr.length;
    for(var i=0; i<length; i++){
        arr.splice(length1, 0, arr[i]*arr[i])
        length1++;
    }
    return arr.splice(0,3)
}
var arr = [2, 4, 6]
squareArr(arr)
console.log(arr)//输出[4, 16, 36]

法二：
function squareArr(arr) {
    arr.forEach(function(element, index){
        arr[index] = element * element;
    });
}
var arr = [2, 4, 6]
squareArr(arr)
console.log(arr)//输出[4, 16, 36]
```

## 3、写一个函数，操作数组，返回一个新数组，新数组中只包含正数，原数组不变
```
function filterPositive(arr){
  var positiveArr = [];
  for(var i = 0;i < arr.length;i++){
    if(typeof arr[i] === "number" && arr[i] > 0){
      positiveArr.push(arr[i]);
    }
  }
  return positiveArr;
}
var arr = [3, -1,  2,  '饥人谷', true]
var newArr = filterPositive(arr)
console.log(newArr) //[3, 2]
console.log(arr) //[3, -1,  2,  '饥人谷', true]
```

# Date 任务
## 1、 写一个函数getChIntv，获取从当前时间到指定日期的间隔时间
```
function getChIntv(timeStr){
    var timeStart = new Date().getTime();
    var timeEnd = new Date(timeStr).getTime();
    var interval = timeEnd - timeStart;

    var days = parseInt(interval / (1000*60*60*24));
    var hours = parseInt((interval % (1000*60*60*24)) /(1000*60*60))
    var minutes = parseInt(interval % (1000*60*60) / (1000*60) )
    var seconds=parseInt(interval % (1000*60) / 1000 )

    return '距离除夕还有'+days+'天'+hours+'小时'+minutes+'分'+seconds+'秒'
}
var str = getChIntv('2018-02-15');
console.log(str);
```
## 2、把hh-mm-dd格式数字日期改成中文日期
```
function getChsDate(str){
    var dict=["零","一","二","三","四","五","六","七","八","九","十","十一","十二","十三","十四","十五","十六","十七","十八","十九","二十","二十一","二十二","二十三","二十四","二十五","二十六","二十七","二十八","二十九","三十","三十一"]
    var dateArr = str.split('-'),
        yearStr = dateArr[0],
        monthStr = dateArr[1],
        dayStr = dateArr[2];

    var chYearStr = dict[parseInt(yearStr[0])] + dict[parseInt(yearStr[1])] + dict[parseInt(yearStr[2])] + dict[parseInt(yearStr[3])];
    var chMonthStr = dict[parseInt(monthStr) + ''];
    var chDayStr = dict[parseInt(dayStr) + ''];

    return chYearStr + '年' + chMonthStr + '月' + chDayStr + '日'
}

var chStr = getChsDate('2015-01-08');
```
## 3、写一个函数，参数为时间对象毫秒数的字符串格式，返回值为字符串。假设参数为时间对象毫秒数t，根据t的时间分别返回如下字符串:

刚刚（ t 距当前时间不到1分钟时间间隔）
3分钟前 (t距当前时间大于等于1分钟，小于1小时)
8小时前 (t 距离当前时间大于等于1小时，小于24小时)
3天前 (t 距离当前时间大于等于24小时，小于30天)
2个月前 (t 距离当前时间大于等于30天小于12个月)
8年前 (t 距离当前时间大于等于12个月)
```
function friendlyDate(time){
  var now = new Date().getTime();
  if((now - time) < 60*1000){
    return "刚刚";
  }
  else if((now - time) < 60*60*1000){
    return "3分钟前";
  }
  else if((now - time) < 24*60*60*1000){
    return "8小时前";
  }
  else if((now - time) < 30*24*60*60*1000){
    return "3天前";
  }
  else if((now - time) < 12*30*24*60*60*1000){
    return "2个月前";
  }
  else if{
    return "8年前";
  }
}
var str = friendlyDate( '1485584391984' ) //  1分钟前
console.log(str);
var str2 = friendlyDate('1405504991984') //4天前
console.log(str2);
```
