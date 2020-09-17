<!--
 * @Descripttion: 
 * @version: 
 * @Author: matias tang
 * @Date: 2020-09-17 17:42:12
 * @LastEditors: matias tang
 * @LastEditTime: 2020-09-17 18:29:20
-->
# DOM操作

[DOM操作](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents)

* Document.getElementsByTagName()，返回页面中包含的所有已知类型元素的数组

getElementByTagName是文档接口（Document interface）和元素接口（Element interface）的中的方法，所以不管是根文档对象还是所有的元素对象都含有方法getElementByTagName。用来通过它们的标签名称（tag name）来获得某些元素的一系列子元素。你可以使用的方法是：element.getElementsByTagName(tagname)。

## 使用document.createTextNode(..)创建文本节点

## 使用appendChild(..)插入元素

## 使用文档对象和createElement(..)方法创建新的元素

## 使用removeChild(..)方法移除节点

## childNodes

使用childNodes属性来获得mycel的孩子节点列表。childNodes列表包括所有的孩子节点，无论它们的名称或类型是什么。

## getAttribute

对象上调用了setAttribute方法来获得一个属性的值

* Document.getElementById()，选择一个id属性值已知的元素

* Node.cloneNode() 

## node.previousSibling

返回当前节点的前一个兄弟节点,没有则返回null.

## node.parentNode

parentNode是指定节点的父节点.一个元素节点的父节点可能是一个元素(Element )节点,也可能是一个文档(Document )节点,或者是个文档碎片(DocumentFragment)节点.

## 操作样式

使用 Document.stylesheets返回CSSStyleSheet数组，获取绑定到文档的所有样式表的序列。然后添加/删除想要的样式。然而，我们并不想扩展这些特性，因此它们在操作样式方面有点陈旧和困难，而现在有了更容易的方法。

第一种方法是直接在想要动态设置样式的元素内部添加内联样式。这是用HTMLElement.style属性来实现。这个属性包含了文档中每个元素的内联样式信息。你可以设置这个对象的属性直接修改元素样式。

第二种方式:Element.setAttribute()
```js
<style>
.highlight {
  color: white;
  background-color: black;
  padding: 10px;
  width: 250px;
  text-align: center;
}
</style>
para.setAttribute('class', 'highlight');
```

两种方式各有优缺点，选择哪种取决于你自己。第一种方式无需安装，适合简单应用，第二种方式更加正统（没有CSS和JavaScript的混合，没有内联样式，而这些被认为是不好的体验）。当你开始构建更大更具吸引力的应用时，你可能会更多地使用第二种方法，但这完全取决于你自己。

在这一点上，我们还没有做任何有用的事！使用JavaScript创建静态内容是毫无意义的 — 最好将其写入HTML，而不使用JavaScript。用JavaScript创建内容也有其他问题（如不能被搜索引擎读取），比HTML复杂得多。