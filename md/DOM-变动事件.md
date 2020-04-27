# 变动事件

[参考](https://www.cnblogs.com/yhl-0822/articles/7818930.html)
变动(mutation)事件能在DOM中的某一部分发生变化时给出提示，这类事件非常有用，但都只能使用DOM2级事件处理程序，且由于浏览器兼容性不好

## 删除节点

删除节点时，涉及到`DOMNodeRemoved`、`DOMNodeRemovedFromDocument`和`DOMSubtreeModified`三个事件
* 删除节点时，事件触发的先后顺序是`DOMNodeRemoved`事件、`DOMNodeRemovedFromDocument`事件和`DOMSubtreeModified`事件

### DOMNodeRemoved

使用`removeChild()`或`replacechild()`从DOM中删除节点时，会触发`DOMNodeRemoved`事件。而`event.relatedNode`属性中包含着对目标节点父节点的引用。在这个事件触发时，节点尚未从其父节点删除，因此其`parentNode`属性仍然指向父节点。该事件会冒泡。

```html
```
[注意]IE8-浏览器不支持

### DOMNodeRemovedFromDocument

如果被移除的节点包含子节点，那么在其所有子节点以及这个被移除的节点上会相继触发`DOMNodeRemovedFromDocument`事件，这个事件不会冒泡，目标`target`指向被移除的节点

```html
```
[注意]该事件只有chrome/safari/opera浏览器支持

### DOMSubtreeModified

在DOM结构中发生任何变化时都会触发DOMSubtreeModified事件，该事件在其他任何事件触发后都会触发，该事件的目标是被移除节点的父节点。

```html
```
[注意]IE8-浏览器不支持

## 插入节点

插入节点时涉及到`DOMNodeInserted`事件、`DOMNodeInsertedIntoDocument`事件及`DOMSubtreeModified`事件。

* 插入节点时，事件触发的先后顺序是DOMNodeInserted事件、DOMNodeInsertedIntoDocument事件和DOMSubtreeModified事件　

### DOMNodeInserted

在使用`appendChild()`、`replaceChild()`或`insertBefore()`向DOM中插入节点时，首先触发`DOMNodeInserted`事件。这个事件的目标是被插入的节点，而`event.relatedNode`属性中包含一个对父节点的引用。在这个事件触发时，节点已经被插入到了新的父节点中。这个事件是冒泡的，因此可以在DOM的各个层次上处理它

[注意]IE8-浏览器不支持

### DOMNodeInsertedIntoDocument

在新插入的节点上面会触发`DOMNodeInsertedIntoDocument`事件。这个事件不冒泡，因此必须在插入节点之前为它添加这个事件处理程序。这个事件的目标是被插入的节点

[注意]该事件只有chrome/safari/opera浏览器支持

### DOMSubtreeModified

*同删除*

## 特性节点

### DOMAttrmodified

当特性被修改后，`DOMAttrmodified`事件被触发

[注意]该事件只有firefox和IE8+浏览器支持

## 文本节点

### DOMCharacterDataModified

当文本节点的值发生变化时，触发`DOMCharacterDataModified`事件

[注意]该方法只有chrome/safari/opera浏览器支持