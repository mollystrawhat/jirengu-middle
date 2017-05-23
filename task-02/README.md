>JavaScript �����˼�����������? ��Щ��ԭʼ����?��Щ�Ǹ�������?ԭʼ���ͺ͸������͵�������ʲô?
typeof��instanceof�����ú�����?
����ж�һ�������Ƿ������֡��ַ���������������
NaN��ʲô? ��ʲô�ر�֮��?
��ΰѷ���ֵת��Ϊ��ֵ?
==��===��ʲô����
break��continue��ʲô����
void 0 �� undefined��ʹ�ó�������ʲô����

## 1. JavaScript �����˼�����������? ��Щ��ԭʼ����?��Щ�Ǹ�������?ԭʼ���ͺ͸������͵�������ʲô?
>6������
 - ��ֵ ��number����������С��
 - �ַ�����string�����ַ���ɵ��ı���һ���õ����Ż�˫���Ű���������"Hello World"������"hello 'word' "��
 - ����ֵ��boolean����true���棩��false���٣������ض�ֵ
 - undefined����ʾ��δ���塱�򲻴��ڣ����˴�Ŀǰû���κ�ֵ
 - null����ʾ��ȱ�����˴�Ӧ����һ��ֵ����ĿǰΪ��
 - ����object��������ֵ��ɵļ��ϡ�
������������Ķ���object��
�������飨array��
����������function��
����������ʽ (regexp)

ԭʼ���ͣ�
��ֵ���ַ���������ֵ��Ϊԭʼ���ͣ�primitive type����ֵ������������������������ͣ�������ϸ���ˡ�

�������ͣ��������ͣ�:
�������Ϊ�������ͣ�complex type����ֵ����Ϊһ�����������Ƕ��ԭʼ���͵�ֵ�ĺϳɣ����Կ�����һ����Ÿ���ֵ��������

#### ����
>�������ͱ��������ֵ���������͵ı���������ڴ��ַ��
���������ڸ�ֵ��ʱ�򿽱�ֵ�����������ڸ�ֵ��ʱ��ֻ������ַ��������ֵ��

1)�洢��ʽ
ջ�洢
��Ϊԭʼֵռ�ݿռ�̶����Ǽ򵥵����ݶΣ�Ϊ�˱�������������ѯ�ٶȣ�����洢��**ջ(stack)**��

�Ѵ洢
���ڸ���ֵ�Ĵ�С��ı䣬���Բ��ܽ�������ջ�У�����ή�ͱ�����ѯ�ٶȣ������洢��**��(heap)**�У��洢�ڱ�������ֵ��һ��ָ�룬ָ��洢������ڴ洦��

2)���ʷ�ʽ
ԭʼֵ����Ϊ����ϸ����ֵ���д洢�Ͳ����ģ��������ǻ�**ת����ֵ**
����ֵ��ͨ�����ý��д洢�Ͳ����ģ�������ʵ�ʵ�ֵ������һ���������Ӷ���ı���ʱ��**��ֵ���ڴ��е�һ�����õ�ַ**������һ�����Ӷ���ʱ��ʹ����������(���������������)ͨ���ڴ��е����õ�ַ��ȡ�ö���ֵ

3)�ȽϷ�ʽ
ԭʼֵ����**ֵ�Ƚ�**��������ֵ����**���ñȽ�**������ֵֻ����������ͬ�Ķ���(������ͬ�ĵ�ַ)ʱ����ȡ�*��ʹ�ǰ�����ͬ�������������Ҳ�˴˲����*����Ϊ���ǲ���ָ��ͬһ������

4)��̬����
���ڸ���ֵ������Ϊ��������Ժͷ�����Ҳ���Ըı��ɾ�������Ժͷ���������ֵ������������Ժͷ���

5)��װ����??
ԭʼֵ���������캯��������һ��������ʹ��ʱ��Javascript�Ὣ��ת����һ�������Ա����ʹ�ö�������Ժͷ��������������������ʣ���������ص�ԭʼֵ

��ϸ�Ľ��ͣ�
[JavaScript�е�ԭʼֵ�͸���ֵ](http://www.jb51.net/article/77631.htm)
[JS��������ͣ�ֵ���͸������ͣ����ã���ʲô����](https://zhuanlan.zhihu.com/p/22400319)

## 2. typeof��instanceof�����ú�����?
 typeof��������Է���һ��ֵ����������
```
1.ԭʼ����
typeof 100 // "number"
typeof 'hello' // "string"
typeof true // "boolean"

2.����
function f() {}                
typeof f   // "function"

3.typeof�����������һ��û�������ı�������������ʵ�ʱ���У�����ص�ͨ�������ж����
// �����д��
if (v) { }  // ReferenceError: v is not defined
// ��ȷ��д��
if (typeof v === "undefined") { }

4.undefined
typeof undefined  // "undefined"

5.�������⣬�������������object��
typeof window // "object"
typeof {} // "object"
typeof [] // "object"
typeof null // "object"
```
instanceof��������Ͷ���
��typeof�ĵ�5 ��صĶ��Ƕ��󣬲����ж��Ƿ�Ϊ���顣
```
[]1,2,3] instanceof  Array   //true
var obj={}
obj instanceof Array      //false
```

## 3. ����ж�һ�������Ƿ������֡��ַ���������������
��console��ʹ��typeof�����յڶ���

## 4. NaN��ʲô? ��ʲô�ر�֮��?
NaN�ĺ����ǣ�����һ�����֡�
Ҫ���һ��ֵ�Ƿ���NaN������ʹ��ȫ�ֺ���isNaN()
```
isNaN(3)   //false
```
NaN���κ�ֵ������ȣ������Լ�����Ϊ
```
parseInt('abc')   //NaN
parseInt('def')   //NaN
����'abc'��������'def'
```
```
NaN==NaN    //false```
## 5. ��ΰѷ���ֵת��Ϊ��ֵ?
�ο�
[��һ��  Number](http://javascript.ruanyifeng.com/grammar/conversion.html)
[��һ�� parseInt   parseFloat](http://javascript.ruanyifeng.com/grammar/number.html)
>Number()
parseInt()
parseFloat()

 - Number

Number()������ת���������£�
�����Booleanֵ��true��false���ֱ�ת��Ϊ1��0��
���������ֵ��ֻ�Ǽ򵥷�����ֵ��
�����nullֵ������0��
�����undefined������NaN��
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
parseInt�������ڽ��ַ���תΪ������
```
parseInt('123')      // 123
```
����ַ���ͷ���пո񣬿ո�ᱻ�Զ�ȥ����
```
parseInt('   123')   // 123
```
���parseInt�Ĳ��������ַ����������תΪ�ַ�����ת�����൱��ֻȡ��������
```
parseInt(1.7) // 1
// ��ͬ��
parseInt('1.7') // 1
```
�ַ���תΪ������ʱ����һ�����ַ�����ת���������������תΪ���ֵ��ַ����Ͳ��ٽ�����ȥ�������Ѿ�ת�õĲ��֡�
```
parseInt('8a') // 8
parseInt('12**') // 12
```
����ַ����ĵ�һ���ַ�����ת��Ϊ���֣�����������ֵ������ų��⣩������NaN��
```
parseInt('abc') // NaN
(parseInt('.3') // NaN     ��       
parseInt('') // NaN
parseInt('+') // NaN
parseInt('+1') // 1        ��
```

## 6. ==��===��ʲô����
�ο���
[��һ��  �����4.3](http://javascript.ruanyifeng.com/grammar/operator.html#toc9)
��˵�����ǵ�����������������==���Ƚ�����ֵ�Ƿ���ȣ��ϸ�����������===���Ƚ������Ƿ�Ϊ��ͬһ��ֵ�����������ֵ����ͬһ���ͣ��ϸ�����������===��ֱ�ӷ���false��������������==���Ὣ����ת����ͬһ�����ͣ������ϸ������������бȽϡ�

## 7. break��continue��ʲô����
break�ǽ�������ѭ���壬continue�ǽ�������ѭ��


## 8. void 0 �� undefined��ʹ�ó�������ʲô����
undefined
����������δ��ֵ��������ᱻ�Զ���ֵΪundefined;
�����ж�����һЩ�βΣ���������ʵ������Ԥ������βΣ���ô��һЩ�βξͻ�ƥ�䲻��ʵ�Σ��̶��ᱻ�Զ���ֵΪundefined;
û�з���ֵ�ĺ�����Ĭ�Ϸ���undefined;

void�����
void ����������һ�����ʽ�����۱��ʽ��������ʲô��ֻҪ����void ֮�󶼻ᱻ����ִ�У�ִ�����֮��void����������undefined;
ʹ��void 0����undefined���ȼ�������ԭ�����ϲ���window.undefined��ʱ��,Ҳ���������ñ��޸Ĺ���undefined��
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
�ο�
http://www.jianshu.com/p/4b2f32e3119e
## 9. ���´������������?Ϊʲô?
```
console.log(1+1);//2�������������
console.log("2"+"4");//'24'�������ַ���ƴ��
console.log(2+"4");//'24'��һ��������һ�����ַ���������ת��Ϊ�ַ�����ƴ��
console.log(+"4");//4��ֻ��һ���ַ�����ת�����������
```

```
var a = 1;  
a+++a;  
typeof a+2;    

//"number2"
//��Ϊ++�����ȼ�����+������a++Ϊ1����ʱ��a�Ѿ���2����a+++a,1+2=3��
//typeof�����ȼ�����+������typeof a�ó�"number",  "number"+2,�ַ��������ֽ�ϣ����Ϊ�ַ���"number2"
```

```
var a = 1;
var b = 3;
console.log( a+++b );

//���4
//��Ϊ++�����ȼ�����+��a++Ϊ1,1+b=1+3=4
```
 �������飬��ӡ����ÿһ���ƽ��
```
 var arr = [3,4,5]
//for(i=0; i<arr.length;i++){
console.log(arr[i]*arr[i])
}

���9��16��25
```
 ���� JSON, ��ӡ�����ֵ
```
var obj = {
 name: 'hunger', 
 sex: 'male', 
 age: 28 
}

for(var key in obj){
console.log(obj[key])

��� hunger��male��28

```
 ���´�����������? Ϊʲô ��ѡ����Ŀ��
```
var a = 1, b = 2, c = 3;
var val = typeof a + b || c >0
console.log(val) 

//���number2
//((typeof a) + b) || (c >0)
typeof���ȼ�����+��typeof a Ϊnumber��("number" + b) || (c >0)
("number2" ) || (c >0)    "number2"�Ƿǿ����飬Ϊtrue��||���ټ������ģ�ֱ�����number2

//ֻҪ��||��ǰ��Ϊtrue�����ۡ�||��������true����false����������ء�||��ǰ���ֵ��
```


```
var d = 5;
var data = d ==5 && console.log('bb')
console.log(data)
//���bb
//data ==5 && console.log('bb')������Ϊ&&�����ϣ����Եó�bb
```
```
var data2 = d = 0 || console.log('haha')
console.log(data2)
//���haha
//
```
``` 
var x = !!"Hello" + (!"world", !!"from here!!");
console.log(x)
//���2�����ַ���Ϊfalse���ǿ���Ϊtrue��
//var x = true+(false+true),trueΪ1��falseΪ0��1+1=2��
```