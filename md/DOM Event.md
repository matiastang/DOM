<!--
 * @Descripttion: 
 * @version: 
 * @Author: matias tang
 * @Date: 2020-09-17 17:57:47
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-06-23 16:45:38
-->
# DOM Event(事件)

[DOM 事件](https://www.runoob.com/jsref/dom-obj-event.html)

[W3C](https://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture)
[MDN Events](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Events)

DOM3级事件草案（DOM Level 3 Events draft）。DOM处理事件流的三个阶段:
![事件流](./img/eventflow.svg)

有3种方法来为一个DOM元素注册事件回调：

* EventTarget.addEventListener(IE 6-8 不支持这一方法，但提供了类似的API即 EventTarget.attachEvent 用以替代。)
```js
// 假设 myButton 是一个按钮
myButton.addEventListener('click', greet, false);
function greet(event) {
    // 打印并查看event对象
    // 打印arguments，以防忽略了其他参数
    console.log('greet: ' + arguments);
    alert('Hello world');
} 
```
* HTML 属性
```html
<button onclick="alert('Hello world!')">
```
* DOM 元素属性
```js
// 假设 myButton 是一个按钮
myButton.onclick = function(event){alert('Hello world');};
```

IE的event和其他的标准DOM的Event是不一样的，不同的浏览器事件的冒泡机制也是有区别

IE：
window.event.cancelBubble = true;//停止冒泡
window.event.returnValue = false;//阻止事件的默认行为

Firefox：
event.preventDefault();// 取消事件的默认行为  
event.stopPropagation(); // 阻止事件的传播

其他的浏览器，可以自己试一下。。。

http://hi.baidu.com/trarck/blog/item/1a959acad2c1d583c91768fc.html
------------------------------------------------------------------

下面的内容可以看一下：

event代表事件的状态，专门负责对事件的处理，它的属性和方法能帮助我们完成很多和用户交互的操作;

一、Event对象的主要属性和方法
  
         1.type：事件的类型，就是HTML标签属性中，没有“on”前缀之后的字符串，例如“Click”就代表单击事件。

  2.srcElement：事件源，就是发生事件的元素。比如<a onclick="check()"></a> a这个链接是事件发生的源头，也就是该事件的srcElement。(非IE中用target)

  3.button：声明了被按下的鼠标键，是一个整数。0代表没有按键，1代表鼠标左键，2代表鼠标右键，4代表鼠标的中间键，如果按下了多个鼠标键，就把这些值加在一起，所以3就代表左右键同时按下。

  4.clientX/clientY：是指事件发生的时候，鼠标的横、纵坐标，返回的是整数，它们的值是相对于包容窗口的左上角生成的。

  5.offsetX/offsetY：鼠标指针相对于源元素的位置，可以确定单击Image对象的哪个象素。

  6.altKey，ctrlKey，shiftKey：顾名思义，这些属性是指鼠标事件发生的时候，是否同时按住了Alt、Ctrl或者Shift键，返回的是一个布尔值。

  7.keyCode：返回keydown和keyup事件发生的时候，按键的代码以及keypress事件的Unicode字符。比如event.keyCode=13代表按下了回车键；

  8.fromElement、toElement前者是指代mouseover事件移动过的文档元素，后者指代mouseout事件中鼠标移动到的文档元素。

  9.cancelBubble：一个布尔属性，把它设置为true的时候，将停止事件进一步起泡到包容层次的元素，它用于检测是否接受上层元素的事件的控制。true代表不被上层元素的事件控制，false代表允许被上层元素的事件控制。

  10.returnValue：一个布尔值属性，设置为false的时候可以阻止浏览器执行默认的事件动作，相当于<a href=”#” onclick=”ProcessMethod();return false;” />。

          11.attachEvent()和detachEvent()方法：为制定DOM对象事件类型注册多个事件处理函数的方法，它们有两个参数，第一个是事件类型，第二个是事件处理函数。在attachEvent()事件执行的时候，this关键字指向的是window对象，而不是发生事件的那个元素。

二、 IE Event对象的一些说明
  Event对象是一个全局属性
  在IE中，不能把Event对象作为参数传递给事件处理程序，只能用window.event或者event来引用Event对象。因为在IE中，Event是window的一个属性，也就是说event是一个全局变量，这个变量提供了事件的细节。

三、关于事件的起泡的概念

         IE中事件的起泡：IE中事件可以沿着包容层次一点点起泡到上层，也就是说，下层的DOM节点定义的事件处理函数，到了上层的节点如果还有和下层相同事件类型的事件处理函数，那么上层的事件处理函数也会执行。例如，<div>标签包含了<a>，如果这两个标签都有 onclick事件的处理函数，那么执行的情况就是先执行<a>标签的onclick事件处理函数，再执行<div>的事件处理函数。如果希望<a>的事件处理函数执行完毕之后，不希望执行上层的<div>的onclick的事件处理函数了，那么就把 cancelBubble设置为false即可。

四、W3C DOM标准中的Event
         和IE不同的是，W3C DOM中的Event对象并不是window全局对象下面的属性，换句话说，event不是全局变量。通常在DOM二级标准中，event作为发生事件的文档对象的属性。Event含有两个子接口，分别是UIEvent和MutationEvent，这两个子接口实现了Event的所有方法和属性，而 MouseEvent接口又是UIEvent的子接口，所以实现了UIEvent和Event的所有方法和属性。下面，我们就看看Event、 UIEvent和MouseEvent的主要属性和方法。
  1.Event
     type：事件类型，和IE类似，但是没有“on”前缀，例如单击事件只是“click”。
     target：发生事件的节点。
     currentTarget：发生当前正在处理的事件的节点，可能是Target属性所指向的节点，也可能由于捕捉或者起泡，指向Target所指节点的父节点。
     eventPhase：指定了事件传播的阶段。是一个数字。
     timeStamp：事件发生的时间。
     bubbles：指明该事件是否起泡。
     cancelable：指明该事件是否可以用preventDefault()方法来取消默认的动作。
     preventDefault()方法：取消事件的默认动作；
     stopPropagation()方法：停止事件传播。
  2.UIEvent
     view：发生事件的window对象。
     detail：提供事件的额外信息，对于单击事件、mousedown和mouseup事件都代表的是点击次数。
  3.MouseEvent
   button：一个数字，指明在mousedown、mouseup和单击事件中，鼠标键的状态，和IE中的button属性类似，但是数字代表的意义不一样，0代表左键，1代表中间键，2代表右键。
   altKey、ctrlKey、shiftKey、metaKey：和IE相同，但是IE没有最后一个。
clientX、clientY：和IE的含义相同，但是在DOM标准中，这两个属性值都不考虑文档的滚动情况，也就是说，无论文档滚动到哪里，只要事件发生在窗口左上角，clientX和clientY都是0，所以在IE中，要想得到事件发生的坐标相对于文档开头的位置，要加上 document.body.scrollLeft和document.body.scrollTop。
   screenX、screenY：鼠标指针相对于显示器左上角的位置，如果你想打开新的窗口，这两个属性很重要。
   relatedTarget：和IE中的fromElement、toElement类似，除了对于mouseover和mouseout有意义外，其他的事件没什么意义。