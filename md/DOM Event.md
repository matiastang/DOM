<!--
 * @Descripttion: 
 * @version: 
 * @Author: matias tang
 * @Date: 2020-09-17 17:57:47
 * @LastEditors: matias tang
 * @LastEditTime: 2020-09-17 18:06:15
-->
# DOM Event(事件)

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