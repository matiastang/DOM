<!--
 * @Author: tangdaoyong
 * @Date: 2021-05-18 10:18:21
 * @LastEditors: tangdaoyong
 * @LastEditTime: 2021-05-18 10:23:04
 * @Description: DOM宽高说明
-->
# DOM宽高说明

## window

`window.innerWidth`返回窗口的文档显示区的宽度。
`window.innerHeight`返回窗口的文档显示区的高度。
`window.outerWidth`设置或返回一个窗口的外部高度，包括所有界面元素（如工具栏/滚动条）。
`window.outerHeight`设置或返回窗口的外部宽度，包括所有的界面元素（如工具栏/滚动）。

## body

`body.clientWidth`网页可见区域宽。
`body.clientHeight`网页可见区域高。
`body.scrollWidth`网页正文全文宽。
`body.scrollHeight`网页正文全文高。

## obj

`obj.offsetWidth`对象盒子的宽度,是对象的可见宽度，包滚动条等边线，会随窗口的显示大小改变。
`obj.offsetHeight`对象盒子的高度。
`obj.clientWidth`是对象可见的宽度，不包滚动条等边线，会随窗口的显示大小改变。
`obj.clientHeight`是对象可见的高度。
`obj.scrollWidth`是对象的实际内容的宽，不包边线宽度，会随对象中内容的多少改变（内容多了可能会改变对象的实际宽度）。
`obj.scrollHeight`是对象的实际内容的高。
`obj.scrollTop`返回或设置匹配元素的滚动条的垂直位置。scroll top offset 指的是滚动条相对于其顶部的偏移。
`obj.scrollLeft`返回或设置匹配元素的滚动条的水平位置。
`obj.offsetTop` 指 obj 距离上方或上层控件的位置，整型，单位像素。
`obj.offsetLeft` 指 obj 距离左方或上层控件的位置，整型，单位像素。
重点：一般情况下，html和body的宽高都是相等的，除非是body的margin的影响,其宽高不包括滚动条。而innerHeight和innerWidth代表的永远是窗口的大小，窗口变大，他们的值就会变大，窗口变小，他们的值也就会变小，而且它的值包括滚动条的宽度，有可能比body和html的值大，也可能小.完全在于body中的元素的尺寸。
`offsetWidth = border-left + border-right + padding-left+padding-right+元素本身的宽度`
`offsetHeight = border-top + border-bottom + padding-top+padding-bottom+元素本身的高度`
`scrollTop``scrollLeft`
这两个属性是相对于滚动条,垂直位置，当滚动条不存在的时候，`obj.scrollLeft` 和 `obj.scrollTop`的值为0，滚动条存在的时候， 不同位置值是不同的。