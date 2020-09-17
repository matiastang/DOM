
[TOC]

# DOM

[什么是 DOM?](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction)
[文档](DOM：文档https://dom.spec.whatwg.org)

## 什么是 DOM？

* DOM 是 W3C（万维网联盟） 的推荐标准。
* DOM 定义了访问诸如 XML 和 XHTML 文档的标准。
> “W3C 文档对象模型（DOM）是一个使程序和脚本有能力动态地访问和更新文档的内容、结构以及样式的平台和语言中立的接口。”
* W3C DOM 被分为 3 个不同的部分/级别（parts / levels）：

1. 核心 DOM
> 用于任何结构化文档的标准模型

2. XML DOM
> 用于 XML 文档的标准模型

3. HTML DOM
> 用于 HTML 文档的标准模型

* DOM 定义了所有文档元素的对象和属性，以及访问它们的方法（接口）。

开始的时候，JavaScript和DOM是交织在一起的，但它们最终演变成了两个独立的实体。JavaScript可以访问和操作存储在DOM中的内容，因此我们可以写成这个近似的等式：

API (web 或 XML 页面) = DOM + JS (脚本语言)

DOM 被设计成与特定编程语言相独立，使文档的结构化表述可以通过单一，一致的API获得。尽管我们在本参考文档中会专注于使用JavaScript， 但DOM 也可以使用其他的语言来实现

在DOM编程时，通常使用的最多的就是 Document 和 window 对象。简单的说， window 对象表示浏览器中的内容，而 document 对象是文档本身的根节点。Element 继承了通用的 Node 接口,  将这两个接口结合后就提供了许多方法和属性可以供单个元素使用。

## 什么是 XML DOM?

[XML DOM](https://www.w3school.com.cn/xmldom/dom_intro.asp)

* XML DOM 是：

> * 用于 XML 的标准对象模型
> * 用于 XML 的标准编程接口
> * 中立于平台和语言
> * W3C 的标准

* XML DOM 定义了所有 XML 元素的对象和属性，以及访问它们的方法（接口）。

* 换句话说：
> XML DOM 是用于获取、更改、添加或删除 XML 元素的标准。

## 什么是 HTML DOM？

[HTML DOM](https://www.w3school.com.cn/htmldom/index.asp)

* HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法（接口）。