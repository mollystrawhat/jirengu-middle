## 讲解了 DOM 的元素选取、增删改查、属性的操作


## 题目1： dom对象的innerText和innerHTML有什么区别？
 - innerText是一个可写属性，返回元素内包含的文本内容，在多层次的时候会按照元素由浅到深的顺序**拼接其内容**
```
<div>
    <p>
        123
        <span>456</span>
    </p>
</div>
//外层div的innerText返回内容是 "123456"
```
 - innerHTML属性作用和innerText类似，但是不是返回元素的文本内容，而是返回元素的**HTML结构**，在写入的时候也会自动构建DOM
```
<div>
    <p>
        123
        <span>456</span>
    </p>
</div>
//外层div的innerHTML返回内容是 "<p>123<span>456</span></p>"
```


## 题目2： elem.children和elem.childNodes的区别？
elem.children会忽略空白的文本节点，但elem.childNodes会将空白的文本节点也视为对象





## 题目3：查询元素有几种常见的方法？ES5的元素选择方法是什么?

 - document.getElementsByTagName('')
 - document.getElementsByName('')
 - document.getElementsById('')
 - document.getElementsByClassName('')

ES5的元素选择方法
 - document.querySelector('')
 - document.querySelectorAll('')




## 题目4：如何创建一个元素？如何给元素设置属性？如何删除属性
 - 生成HTML元素节点
createElement()  
```
var newH1 = document.createElement("h1");
```

 - 给元素设置属性
setAttribute()
```
var node = document.getElementById("header");
node.setAttribute("属性名", "属性值");
```
 - 删除属性
removeAttribute()
```
node.removeAttribute('class')//删除类名
```

## 题目5：如何给页面元素添加子元素？如何删除页面元素下的子元素?


 - appendChild()在元素末尾添加元素
```
var newDiv=document.createElement('div');//创建一个div元素
var newSpan=document.createElement('span');//创建一个span元素
newDiv.appendChild(newSpan);//将span元素添加到div元素的末尾
```
 - insertBefore()在某个元素之前插入元素
```
var newDiv=document.createElement('div');//创建一个div元素
var newSpan=document.createElement('span');//创建一个span元素
newDiv.insertBefore(newSpan,newDiv.firstChild);//将span元素添加到div元素中，并成为div中的第一个元素
```
 - removeChild()删除子元素
```
parentNode.removeChild(childNode);
```

## 题目6： element.classList有哪些方法？如何判断一个元素的 class 列表中是否包含某个 class？如何添加一个class？如何删除一个class?
```
element.classList.contains(class)//判断指定的类名是否存在
element.classList.add('class1', 'class2', 'class3', ...)//添加一个或多个不存在的类名
element.classList.remove(class1, class2, ...)//删除元素中一个或多个类名。删除不存在的类名，不会报错。
element.classList.item(index)//返回索引值对应的元素类名，在区间范围外则返回 null。
element.classList.toggle(class, true|false)//在元素中切换类名。第一个参数为要在元素中删除的类名，删除后返回 false。 如果该类名不存在则会在元素中添加类名，并返回 true。第二个是可选参数，用于设置是否强制添加或删除，不管该类名是否存在。

```




## 题目7： 如何选中如下代码所有的li元素？ 如何选中btn元素？
```
<div class="mod-tabs">
   <ul>
       <li>list1</li>
       <li>list2</li>
       <li>list3</li>
   </ul>
   <button class="btn">点我</button>
</div>
```


```
选中所有的li元素
document.getelementsByTagName('li')
document.querySelectorAll('.mod-tabs ul li')

选中btn元素
document.getelementsByClassName('btn')
```
