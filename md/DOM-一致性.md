# DOM一致性

[DOM一致性](https://developer.mozilla.org/en-US/docs/Web/API/DOMImplementation/hasFeature)

> DOMImplementation.hasFeature()
> 返回一个Boolean指示是否支持给定功能。该函数不可靠，仅出于兼容性目的而保留：除了与SVG相关的查询外，它始终返回true。旧的浏览器的行为非常不一致。

由于DOM分为多个级别，也包含多个部分，因此检测浏览器实现了DOM的哪些部分就十分必要。document.implementation属性就是这些提供相应信息和功能的对象。与浏览器对DOM的实现直接对应。
DOM1级只为document.implementation规定了一个方法，即hasFeature()。这个方法接受两个参数:要检测的DOM功能的名称及版本号。如果浏览器支持给定名称和版本的功能，则该方法返回true。

> flage = document.implementation.hasFeature(feature，version);

feature:是DOMString代表功能名称。
version:是DOMString表示定义功能部件的规范版本。