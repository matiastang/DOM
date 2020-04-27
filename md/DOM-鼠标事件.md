# DOM-鼠标事件

[参考](https://www.cnblogs.com/xiaohuochai/p/5867195.html)
* 类型
鼠标事件共10类，包括click、contextmenu、dblclick、mousedown、mouseup、mousemove、mouseover、mouseout、mouseenter和mouseleave
```
click         当用户按下并释放鼠标按键或其他方式“激活”元素时触发
contextmenu   可以取消的事件，当上下文菜单即将出现时触发。当前浏览器在鼠标右击时显示上下文菜单
dblclick      当用户双击鼠标时触发
mousedown     当用户按下鼠标按键时触发
mouseup       当用户释放鼠标按键时触发
mousemove     当用户移动鼠标时触发
mouseover     当鼠标进入元素时触发。relatedTarget(在IE中是fromElement)指的是鼠标来自的元素
mouseout      当鼠标离开元素时触发。relatedTarget(在IE中是toElement)指的是鼠标要去往的元素
mouseenter    类似mouseover，但不冒泡。IE将其引入，HTML5将其标准化，但尚未广泛实现
mouseleave    类似mouseout，但不冒泡。IE将其引入，HTML5将其标准化，但尚未广泛实现
```
* 冒泡

页面上的所有元素都支持鼠标事件，除了mouseenter和mouseleave事件外，所有的鼠标事件都会冒泡
[注意]safari浏览器不支持mouseenter和mouseleave事件

* 事件顺序

1. 鼠标移入时，触发mouseover、mouseenter和mousemove事件

IE浏览器会先触发一次mousemove事件，再触发mouseover和mouseenter事件，再触发多次mousemove事件
而其他浏览器都是先触发mouseover和mouseenter事件，再触发多次mousemove事件

2. 鼠标移出时，触发mousemove、mouseleave和mouseout事件
所有浏览器的顺序都是(1)mousemove、(2)mouseout和(3)mouseleave事件

3. 双击鼠标时，触发mousedown、mouseup、click、dblclick事件

　　一般地，浏览器的顺序是(1)mousedown、(2)mouseup、(3)click、(4)mousedown、(5)mouseup、(6)click、(7)dblclick

　　但IE8-浏览器有一个小bug，在双击事件中，它会跳过第二个mousedown和click事件，顺序为(1)mousedown、(2)mouseup、(3)click、(4)mouseup、(5)dblclick

4. 点击鼠标右键时，触发mousedown、mouseup、contextmenu事件

　　一般地，浏览器的顺序是(1)mousedown、(2)mouseup、(3)contextmenu

　　但safari浏览器有一个小bug，它不触发mouseup事件，顺序为(1)mousedown、(2)contextmenu

5. 嵌套元素的移入移出时，触发mouseover、mouseenter、mouseleave、mouseout事件

　　从父级元素进入子级元素时，顺序为:(1)父级元素的mouseout、(2)子级元素的mouseover、(3)父级元素的mouseover、(4)子级元素的mouseenter

　　从子级元素进入父级元素时，顺序为:(1)子级元素的mouseout、(2)父级元素的mouseout、(3)子级元素的mouseleave、(4)父级元素的mouseover

*注意*
从上面的结果可以看出mouseover、mouseout和mouseleave、mouseenter事件的区别

1、mouseover、mouseout是冒泡的，而mouseleave和mouseenter是不冒泡的
2、从父级元素进入子级元素时，不会触发父级元素的mouseleave事件
3、从子级元素进入父级元素时，不会触发父级元素的mouseenter事件

## 事件对象

### 坐标位置

关于坐标位置，事件对象提供了`clientX/Y`、`pageX/Y`、`screenX/Y`、`x/y`、`offsetX/Y`、`layerX/Y`这6对信息。

#### clientX/Y与x/y

　　clientX/Y表示鼠标指针在可视区域中的水平和垂直坐标

　　x/y与clientX/Y相同，但有兼容问题。firefox浏览器不支持x/y，且IE7-浏览器把视口的左上角坐标设置为(2,2)，其他浏览器则将(0,0)作为起点坐标，所以存在(2,2)的差距

#### screenX/Y

　　screenX/Y表示鼠标指针相对于屏幕的水平和垂直坐标

#### pageX/Y与layerX/Y

　　pageX/Y表示相对于页面的水平和垂直坐标，它与clientX/clientY的区别是不随滚动条的位置变化

　　layerX/Y与pageX/Y相同
[注意]IE8-浏览器不支持pageX/Y和layerX/Y，不过可以根据scrollTop/Left和clientX/Y计算出来

#### offsetX/Y

　　offsetX/Y表示相对于定位父级的水平和垂直坐标

　　当页面无定位元素时，body是元素的定位父级。由于body的默认margin是8px，所以offsetX/Y与clientX/Y差(8,8)

### 修改键
　　虽然鼠标事件主要是使用鼠标来触发的，但在按下鼠标时键盘上的某些键的状态也可以影响到所要采取的操作

　　这些修改键就是Shift、Ctrl、Alt和Meta(在Windows键盘中是Windows键，在苹果机中是Cmd键)，它们经常被用来修改鼠标事件的行为

　　DOM为此规定了4个属性，表示这些修改键的状态：shiftKey、ctrlKey、altKey和metaKey。这些属性中包含的都是布尔值，如果相应的键被按下了，则值为true；否则值为false

　　[注意]IE8-浏览器不支持metaKey属性

### 相关元素
　　relatedTarget属性返回事件的次要相关节点。对于那些没有次要相关节点的事件，该属性返回null

　　对mouseover事件而言，事件的主目标target是获得光标的元素，而相关元素relatedTarget就是那个失去光标的元素

　　下表列出不同事件的target属性和relatedTarget属性含义

```
事件名称    　　target属性       relatedTarget属性
focusin       接受焦点的节点    丧失焦点的节点
focusout    　丧失焦点的节点    接受焦点的节点
mouseenter    将要进入的节点    将要离开的节点
mouseleave    将要离开的节点    将要进入的节点
mouseout      将要离开的节点    将要进入的节点
mouseover     将要进入的节点    将要离开的节点
dragenter     将要进入的节点    将要离开的节点
dragexit      将要离开的节点    将要进入的节点
```
IE8-浏览器不支持target和relatedTarget属性

兼容

　　target可以用srcElement属性替代，relatedTarget可以用toElement属性替代　

　　[注意]firefox浏览器不支持srcElement和toElement属性

### 鼠标按键
　　button和buttons属性返回事件鼠标按键信息

#### button

　　button属性返回一个数值，表示按下了鼠标哪个键

　　[注意]若不阻止右键默认行为，safari浏览器无法表示按下右键
```
-1     表示没有按下按键
0      表示按下左键
1      表示按下滚轮
2      表示按下右键
```

#### buttons

　　buttons属性返回一个3个比特位的值，表示同时按下了哪些键。它用来处理同时按下多个鼠标键的情况

　　[注意]safari浏览器不支持buttons属性
```
1     二进制为001，表示按下左键
2     二进制为010，表示按下右键
4     二进制为100，表示按下滚轮
```
所以，同时按下左键和右键，buttons的二进制为011，表示3；同时按下左键和滚轮，buttons的二进制为101，表示5；同时按下右键和滚轮，buttons的二进制为110，表示6

但，IE8-浏览器的button属性的值与标准的button属性有很大差异
```
0:表示没有按下按钮
1:表示按下了左键
2:表示按下了右键
3:表示同时按下了左、右键
4:表示按下了滚轮
5:表示同时按下了左键和滚轮
6:表示同时按下了右键和滚轮
7:表示同时按下了左键、右键和滚轮
```
兼容

　　此时，无法使用能力检测来确定差异，可以通过hasFeature()方法来检测，关于hasFeature()方法的详细信息[DOM一致性检测](https://www.cnblogs.com/xiaohuochai/p/4853121.html)

### 滚轮事件
　　对于滚轮事件，有类似的滚动事件scroll，但是滚动事件不兼容IE8-浏览器，详细情况[深入理解滚动scroll](https://www.cnblogs.com/xiaohuochai/p/5831640.html#anchor6)

　　滚轮事件与滚动事件不同，滚动事件必须有滚动条，才可以实现。而滚动事件是滚动鼠标滚轮触发的事件，与是否有滚动条无关

　　IE6首先实现了鼠标滚轮mousewheel事件，当用户通过滚动与页面交互、在垂直方向上滚动页面时，会触发mousewheel事件。最终会冒泡到document(IE8-)或window(标准)

　　[注意]这个事件可以在任何元素上触发

　　滚轮事件中有一个wheelDelta属性，当用户向前滚动鼠标滚轮时，wheelDelta是120的倍数；当用户向后滚动鼠标滚轮时，wheelDelta是-120的倍数

firefox浏览器不支持mousewheel事件，它支持DOMMouseScroll事件，而有关鼠标滚轮的信息则保存在detail属性中，当向前滚动鼠标滚轮时，这个属性的值是-3的倍数，当向后滚动鼠标滚轮时，这个属性的值是3的倍数

　　[注意]该事件仅支持DOM2级事件处理程序的写法

### 移动设备
　　由于移动设备没有鼠标，所以与电脑端有一些不同之处。移动设备尽量使用移动端事件，而不要使用鼠标事件

　　【1】不支持dblclick双击事件。在移动设备中双击浏览器窗口会放大画面

　　【2】单击元素会触发mousemove事件

　　【3】两个手指放在屏幕上且页面随手指移动而滚动时会触发mousewheel和scroll事件