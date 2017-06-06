## 事件模型、事件冒泡、事件捕获、事件代理、阻止默认事件、事件兼容等

## 题目1： DOM0 事件和DOM2级在事件监听使用方式上有什么区别？
 - 添加多个事件处理程序区别：
Dom2级：可以添加多个事件处理程序
Dom0级：为一个事件添加多个事件处理程序时，后面的程序会覆盖前面的。
 - 是否可选事件模型
Dom2级：可以选择是在捕获阶段（true）和冒泡阶段（false）
Dom0级：只能在冒泡阶段
 - 删除绑定在元素上的事件处理程序



Dom2级：removeEventListener()
```
var btn=document.querySelector("#btn");
var handler=function(){
	alert(this.id);
}

btn.addEventListener("click",handler,false);// 指定事件处理程序
btn.removeEventListener("click",handler,false);// 删除事件处理程序
```

Dom0级：将事件处理程序设置为null
```
var btn=document.querySelector("#btn");
btn.onclick=function () {
	alert(this.id);
}// 添加事件处理程序

btn.onclick=null;// 删除事件处理程序
```







## 题目2： attachEvent与addEventListener的区别？
 - **参数个数不相同**
addEventListener有三个参数，attachEvent只有两个
attachEvent添加的事件处理程序只能发生在冒泡阶段，addEventListener第三个参数可以决定添加的事件处理程序是在捕获阶段还是冒泡阶段处理（我们一般为了浏览器兼容性都设置为冒泡阶段）

 - **第一个参数意义不同**
addEventListener第一个参数是事件类型（比如click，load），而attachEvent第一个参数指明的是事件处理函数名称（onclick，onload）

 - **事件处理程序的作用域不相同**
addEventListener的作用域是元素本身，this是指的触发元素，而attachEvent事件处理程序会在全局变量内运行，this是window，所以刚才例子才会返回undefined，而不是元素id

 - **为一个事件添加多个事件处理程序时，执行顺序不同**
addEventListener添加会按照添加顺序执行，而attachEvent添加多个事件处理程序时顺序无规律(添加的方法少的时候大多是按添加顺序的反顺序执行的，但是添加的多了就无规律了)，所以添加多个的时候，不依赖执行顺序的还好，若是依赖于函数执行顺序，最好自己处理，不要指望浏览器







## 题目3： 解释IE事件冒泡和DOM2事件传播机制？
![](http://upload-images.jianshu.io/upload_images/5804931-65cbe419a8dbebe5?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/5804931-192ce32b4c1c33be?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
IE事件冒泡：事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的元素，如上图一中所示，如果是一个点击事件，当点击div时，是一层一层的向父级元素传递

DOM2级事件规定事件流包括三个阶段，**事件捕获阶段**，**处于目标阶段**，**事件冒泡阶段**，首先发生的是事件捕获，为截取事件提供机会，然后是实际目标接收事件，最后是冒泡阶段





## 题目4： 如何阻止事件冒泡？ 如何阻止默认事件？
 - 支持DOM2浏览器
阻止冒泡e.stopPropagation();
阻止默认事件event.preventDefault()

 - IE浏览器
阻止冒泡e.cancelBubble = true;
阻止默认事件event.returnValue = false;

```
阻止事件冒泡
function stopPropagation(event){
    if(event.stopPropagation){
        event.stopPropagation()
    }
    else{
        event.cancelBubble = true;
    }

}


阻止默认事件
function  preventDefault(event){
    if(event.preventDefault){
        event.preventDefault()
    }
    else{
        e.returnValue = false;
    }
}

```








## 题目5： 有如下代码，要求当点击每一个元素li时控制台展示该元素的文本内容。不考虑兼容
```
<ul class="ct">
    <li>这里是</li>
    <li>饥人谷</li>
    <li>前端6班</li>
</ul>
<script>
var ct=document.querySelector('.ct');
ct.addEventListener('click',showText);//将事件监听放在父级元素
function showText(event){
    console.log(event.target.innerText);
}
</script> 
```
## 题目6： 补全代码，要求：
```
当点击按钮开头添加时在<li>这里是</li>元素前添加一个新元素，内容为用户输入的非空字符串；当点击结尾添加时在最后一个 li 元素后添加用户输入的非空字符串.
当点击每一个元素li时控制台展示该元素的文本内容。
<ul class="ct">
    <li>这里是</li>
    <li>饥人谷</li>
    <li>任务班</li>
</ul>
<input class="ipt-add-content" placeholder="添加内容"/>
<button id="btn-add-start">开头添加</button>
<button id="btn-add-end">结尾添加</button>
<script>
var ct=document.querySelector('.ct');
var ipt=document.querySelector('.ipt-add-content');
var addStart=document.querySelector('#btn-add-start');
var addEnd=document.querySelector('#btn-add-end');

ct.addEventListener('click',showText);
addStart.addEventListener('click',addBefore);
addEnd.addEventListener('click',addAfter);

function showText(event){
    console.log(event.target.innerText);
}
function addBefore(){
    if(!ipt.value){
        alert('Please fill in the contents in the input box');
        return;
    };
    var li=document.createElement('li');
    li.innerText=ipt.value;
    ct.insertBefore(li,ct.firstChild);
}
function addAfter(){
    if(!ipt.value){
        alert('Please fill in the contents in the input box');
        return;
    };
    var li=document.createElement('li');
    li.innerText=ipt.value;
    ct.appendChild(li);
}

</script>  
```
## 题目7： 补全代码，要求：当鼠标放置在li元素上，会在img-preview里展示当前li元素的data-img对应的图片。
```
<ul class="ct">
    <li data-img="http://a.hiphotos.baidu.com/zhidao/pic/item/1b4c510fd9f9d72aa05bac6cd22a2834349bbb80.jpg">鼠标放置查看图片1</li>
    <li data-img="http://www.qqleju.com/uploads/allimg/140326/26-045728_826.jpg">鼠标放置查看图片2</li>
    <li data-img="http://img1.3lian.com/2015/w2/12/d/83.jpg">鼠标放置查看图片3</li>
</ul>
<div class="img-preview"></div>
<script>

var ct = document.querySelector('.ct');
var preview = document.querySelector('.img-preview');

ct.addEventListener('mouseover',eventOver);
ct.addEventListener('mouseout',eventOut);
  
function eventOver(e){
    var img = e.target.getAttribute('data-img');
    preview.innerHTML =  '<img src = "' + img + '">';
}
function eventOut(e){
     preview.innerHTML = '';
}
</script>
```

题目8： 在 github 上创建个人项目，把视频里事件兼容的函数写法放入项目，在 Readme.md里描述项目(选做题目)
```
<script>
//绑定事件
    function  bindEvent(node,type,handler){
        if(node.addEventListener){
            node.addEventListener(type,handler);
        }
        else{
            node.attachEvent('on'+type,handler);
        }
    }
//解除事件
    function removeEvent(node,type,handler){
        if(node.removeEventListener){
            node.removeEventListener(type,handler);
        }
        else{
            node.detachEvent('on'+type,handler);
        }
    }
//获取target
    function getTarget(e){
        return e.target || e.srcElement;
    }

</script>
```
