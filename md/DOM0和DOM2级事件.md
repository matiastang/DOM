# DOM0和DOM2级事件

[参考-JS基础知识（十一）DOM0和DOM2级事件](https://blog.csdn.net/qq_23389687/article/details/80166843)

## 事件的传播机制

### 事件传播有三个阶段
Event.prototype
```
- 0  NONE:默认值，不代表任何意思
- 1  `CAPTURING_PHASE  捕获阶段`
- 2 ` AT_TARGET  目标阶段（当前事件源）`
- 3  `BUBBLING _PHASE :冒泡阶段`
```
* 当前元素的某个事件行为被触发，它的所有的祖先元素（一直到document）的相关事件行为也会被触发执行（由里向外），我们把这种传播机制叫做冒泡传播

mouseover和mouseenter事件的区别
mouseover：鼠标滑到元素上：存在事件的冒泡传播机制 mouseenter：鼠标进入元素里；浏览器阻止了它的冒泡传播机制； 不同点
区别	mouseover	mouseenter
区别 1	存在冒泡传播机制	冒泡传播机制被浏览器阻止
区别 2	当鼠标从父元素进入到子元素时，首先会触发父元素的mouseout事件，再触发子元素的mouseover事件，由于冒泡传播机制，导致父元素的mouseover事件也被触发	当鼠标从父元素进入到子元素时,并不会触发父元素的mouseout事件，但是触发了子元素的mouseenter事件，由于浏览器阻止了它的冒泡传播，所以父元素的该事件不会被触发

### 事件委托（very important）
`原理`：利用事件的冒泡传播机制完成（mouseenter不存在冒泡传播）
当一个容器内的很多元素都要为同一事件绑定方法，那么我们只需要给外层容器的该事件绑定方法，当里层元素的事件被出发时，会通过冒泡传播机制传到最外层容器那里，触发外层容器绑定的方法执行，在方法执行时，我们只需要根据判断事件源的不同而做不同的事情。（利用事件委托可提高50%左右的性能）

### DOM2事件绑定
```
//=>标准浏览器
oBox.addEventLister('click',function(e){
    //this:obx
},false)
//false=>让事件在冒泡传播时执行
//true=>让事件在捕获阶段执行（非常少见）
//=>IE6-8浏览器
oBox.attachEvent('onclick',function(e){
//e:事件对象，不同于DOM0级事件，浏览器会默认将事件对象传递进来，与window.event的值相同，因此对于：pageX/pageY/target...等依旧存在兼容；
})
//=>绑定的方法都是在冒泡传播阶段执行
```

## DOM0于DOM2事件绑定的区别

### DOM0事件绑定的原理
给当前元素的某一私有属性（onXXX）赋值的过程；（之前属性默认值是null，如果我们赋值了一个函数，就相当于绑定了一个方法）
当我们赋值成功（赋值一个函数），此时浏览器会把DOM元素和赋值的的函数建立关联，以及建立DOM元素的行为监听，当某一行为被用户触发，浏览器会把赋值的函数执行；
### DOM0事件绑定的特点：
只有DOM元素天生拥有这个私有属性（onxxx事件私有属性），我们赋值的方法才叫事件绑定，否则属于设置自定义属性
移除事件绑定的时候，我们只需要赋值为null；
在DOM0事件绑定中，只能给当前元素的某一个事件行为绑定一个方法，绑定多个方法，最后一次的绑定的会替换前面绑定的
## DOM2事件绑定的原理
DOM2事件绑定使用的 addEventListener/attachEvent方法都是在eventTarget这个内置类的原型上定义的，我们调用的时候，首先要通过原型链找到这个方法，然后执行完成事件绑定的效果
浏览器会给当前元素的某个事件行为开辟一个事件池（事件队列）【浏览器有一个统一的事件池，每个元素绑定的行为都放在这里，通过相关标志区分】，当我们通过 addEventListener/attachEvent进行事件绑定的时候，会把绑定的方法放在事件池中；
当元素的某一行为被触发，浏览器回到对应事件池中，把当前放在事件池的所有方法按序依次执行

特点

所有DOM0支持的行为，DOM2都可以用，DOM2还支持DOM0没有的事件行为（这样说比较笼统）
（核心）【浏览器会把一些常用事件挂载到元素对象的私有属性上，让我们可以实现DOM0事件绑定，DOM2：凡是浏览器给元素天生设置的事件在DOM2中都可以使用】
例如：onDOMContentLoaded（所有的DOM0和IE6-8的DOM2都不支持）

onDOMContentLoaded//当前浏览器中的DOM结构加载完成，就会触发这个事件

DOM2中可以给当前元素的某一事件行为绑定多个不同方法（因为绑定的所有方法都放在事件池中）；

事件的移除:事件类型、绑定的方法、传播阶段三个完全一致，才可以完成移除(因此在绑定方法时，尽量不要用匿名函数，否则不好移除)
```
//=>ON:给当前元素的某个事件绑定某个方法
   var on = function (curEle, type, fn) {
   if (document.addEventListener) {
       //=>标准浏览器
        curEle.addEventListener(type, fn, false);
       return;
   }
  //=>IE6~8
  curEle.attachEvent('on' + type, fn);
};
//=>OFF:移除当前元素某个事件绑定的某个方法
var off = function (curEle, type, fn) {
    if (document.removeEventListener) {
        curEle.removeEventListener(type, fn, false);
        return;
    }
    //=>IE6~8
    curEle.detachEvent('on' + type, fn);
};
```
xxx.removeEventLister('click',function(){},false)

*DOM0和DOM2绑定的方法是毫无联系的（因为是两套完全不同的机制），即使绑定的方法相同，也是执行两次，谁先绑定，就先执行谁*

## window.onload&&$(document).ready()的区别
window.onload:当浏览器中的所有资源（DOM结构、文本内容、图片）都加载完成，触发load事件；
- 它是基于DOM0的事件绑定机制完成的，所以在同一页面中只能为他绑定一个方法，绑定多个，以最后一个为主；
- 如果想在一个页面中使用多次，应该是基于DOM2绑定的；
```
function fn1(){
}
function fn2(){
}
window.addEventListener('load',fn1,false);
window.addEventListener('load',fn2,false);
```
$(function(){})或者$(document).ready(function(){});
当文档中的DOM结构加载完成，就会触发执行，在一个页面中可以使用多次
- JQ中提供的方法，JQ是基于onDOMContentLoaded这个事件完成操作的
- JQ中的事件绑定都是基于DOM2事件绑定的
- onDOMContentLoaded在IE6-8下attachEvent也是不支持的，JQ在IE6-8下使用readystatechange来完成