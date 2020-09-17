<!--
 * @Descripttion: 
 * @version: 
 * @Author: matias tang
 * @Date: 2020-09-17 17:49:25
 * @LastEditors: matias tang
 * @LastEditTime: 2020-09-17 17:52:08
-->
# DOM选择器

[DOM选择器](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Locating_DOM_elements_using_selectors)

## 介绍

Selectors API提供了通过与一组选择器匹配来快速轻松地从DOM检索  Element节点的方法。这比以前的技术要快得多，其中有必要使用JavaScript代码中的循环来定位您需要查找的特定项目。

## NodeSelector 接口

此规范向实现  Document, DocumentFragment,  或 Element 接口的任何对象添加了两种新方法：

* querySelector
返回节点子树内与之相匹配的第一个 Element 节点。如果没有匹配的节点，则返回null。
* querySelectorAll
返回一个NodeList  包含节点子树内所有与之相匹配的Element节点，如果没有相匹配的，则返回一个空节点列表。
**注意**：由 querySelectorAll()返回的节点列表不是动态实时的。这和其他DOM查询方法返回动态实时节点列表不一样。

## Selectors
选择器方法接受一个或多个逗号分隔的选择器来确定应该返回哪些元素。

例如，要选择文档中所有CSS的类(class)是warning或者note的段落(p)元素,可以这样写：

var special = document.querySelectorAll( "p.warning, p.note" );
也可以通过ID来查询，例如：

var el = document.querySelector( "#main, #basic, #exclamation" );
执行上面的代码后，el就包含了文档中元素的ID是main，basic或exclamation的所有元素中的第一个元素。

querySelector() and querySelectorAll() 里可以使用任何CSS选择器。