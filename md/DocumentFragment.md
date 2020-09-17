<!--
 * @Descripttion: 
 * @version: 
 * @Author: matias tang
 * @Date: 2020-09-17 18:32:56
 * @LastEditors: matias tang
 * @LastEditTime: 2020-09-17 18:34:03
-->
# DocumentFragment

[DocumentFragment](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentFragment)

DocumentFragment，文档片段接口，一个没有父对象的最小文档对象。它被作为一个轻量版的 Document 使用，就像标准的document一样，存储由节点（nodes）组成的文档结构。与document相比，最大的区别是DocumentFragment 不是真实 DOM 树的一部分，它的变化不会触发 DOM 树的重新渲染，且不会导致性能等问题。

最常用的方法是使用文档片段作为参数（例如，任何 Node 接口类似 Node.appendChild 和 Node.insertBefore 的方法），这种情况下被添加（append）或被插入（inserted）的是片段的所有子节点, 而非片段本身。因为所有的节点会被一次插入到文档中，而这个操作仅发生一个重渲染的操作，而不是每个节点分别被插入到文档中，因为后者会发生多次重渲染的操作。

该接口在 Web 组件（Web components）中也非常有用：<template> 元素在其 HTMLTemplateElement.content 属性中包含了一个 DocumentFragment。

可以使用document.createDocumentFragment 方法或者构造函数来创建一个空的 DocumentFragment。

## 属性
该接口没有特殊的属性，其属性都继承自 Node ，并补充了 ParentNode 接口中的属性。

ParentNode.children 只读
返回一个实时（live） HTMLCollection ，包含所有属于 DocumentFragment 的元素类型的子对象。
ParentNode.firstElementChild 只读
返回 DocumentFragment 的第一个 Element 类型的子对象，如果没有则返回 null 。
ParentNode.lastElementChild 只读
返回 DocumentFragment 的最后一个 Element 类型的子对象，如果没有则返回 null 。
ParentNode.childElementCount 只读
返回一个 unsigned long 给出 DocumentFragment 拥有的子项数量。
## 构造函数
DocumentFragment() 
返回一个空的 DocumentFragment 对象。
## 方法
该接口继承 Node 的全部方法，并实现了 ParentNode 接口中的方法。

DocumentFragment.querySelector()
返回在DocumentFragment中以文档顺序排列的第一个符合指定选择器的Element节点。
DocumentFragment.querySelectorAll()
返回在DocumentFragment中所有的符合指定选择器的Element节点组成的NodeList数组。
DocumentFragment.getElementById()
返回在DocumentFragment中以文档顺序排列的第一个符合指定ID选择器的Element节点。与Document.getElementById()作用相同。