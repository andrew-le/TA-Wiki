> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[行为]] ▸ **缩放**

* 如发现翻译不当或有其他问题可以通过以下方式联系译者:
* 邮箱：zhang_tianxu@sina.com
* QQ群：[D3数据可视化](http://jq.qq.com/?_wv=1027&k=ZGcqYF)205076374，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)436442115

[![Pan+Zoom](http://bl.ocks.org/mbostock/raw/3892919/thumbnail.png)](http://bl.ocks.org/mbostock/3892919)
[![Zoomable Area](http://bl.ocks.org/mbostock/raw/4015254/thumbnail.png)](http://bl.ocks.org/mbostock/4015254)
[![Geometric Zooming](http://bl.ocks.org/mbostock/raw/3680999/thumbnail.png)](http://bl.ocks.org/mbostock/3680999)
[![d3.geo.tile](http://bl.ocks.org/mbostock/raw/4132797/thumbnail.png)](http://bl.ocks.org/mbostock/4132797)
[![Raster & Vector Zoom](http://bl.ocks.org/mbostock/raw/5914438/thumbnail.png)](http://bl.ocks.org/mbostock/5914438)
[![Zoomable Geography](http://bl.ocks.org/mbostock/raw/2374239/thumbnail.png)](http://bl.ocks.org/mbostock/2374239)

该行为会自动在容器元素中创建事件监听器来处理元素的缩放和平移动作，可支持鼠标事件和触摸事件。

<a name="zoom" href="#zoom">#</a> d3.behavior.**zoom**()

构造一个新的缩放行为。构造之后，可以通过[selection.call()](选择器#call)将此行为应用于选择器：

```js
var zoom = d3.behavior.zoom();
selection.call(zoom);
```

所有注册的监听器都使用 "zoom" 命名空间, 故如下可以移除缩放行为:

```js
selection.on(".zoom", null);
```

<a name="_zoom" href="#_zoom">#</a> **zoom**(*selection*)

应用缩放行为到指定的选择器 *selection*，注册所需的事件监听器，支持缩放和拖拽行为。

<a name="translate" href="#translate">#</a> zoom.**translate**([*translate*])

指定当前的缩放平移向量为*translate*；如果未指定*translate*，返回当前平移向量，默认：`[0, 0]`。

<a name="scale" href="#scale">#</a> zoom.**scale**([*scale*])

指定当前的缩放比例，如果未指定*scale*，则返回当前的缩放比例，默认为`1`。

<a name="scaleExtent" href="#scaleExtent">#</a> zoom.**scaleExtent**([*extent*])

指定缩放比例的允许范围为一个包含两个数值元素的数组，[*minimum*, *maximum*]；如果未指定extent，则返回当前的比例范围，默认为：`[0, Infinity]`。

<a name="center" href="#center">#</a> zoom.**center**([*center*])

如果指定了 *center* ，为鼠标滚轮设置缩放的焦点([focal point](http://bl.ocks.org/mbostock/6226534)) [*x*, *y*] 为缩放中心 ，并返回当前的缩放行为；如果未指定 *center* ，则返回当前的缩放焦点，默认为`null`；一个为`null`的缩放焦点即：是以当前鼠标指针为缩放焦点。

<a name="size" href="#size">#</a> zoom.**size**([*size*])

如果指定了*size*，设置视窗大小为指定的尺寸([*width*, *height*])，并返回当前的缩放行为对象；如果未指定*size*，返回当前的视窗大小，默认为：[960, 500]；*size*是支持在过渡时平滑的进行缩放行为([smooth zooming](过渡#d3_interpolateZoom))。

<a name="x" href="#x">#</a> zoom.**x**([*x*])

指定*x*比例，并且它的定义域会在缩放时自动调整；如果未指定*x*，返回当前的x缩放，默认为`null`；如果缩放的定义域或范围是通过函数修改的，则这个函数应该被再次调用。设置x比例，并重置缩放比例为1，平移为[0, 0]。

<a name="y" href="#y">#</a> zoom.**y**([*y*])

指定*y*比例，并且它的定义域会在缩放时自动调整；如果未指定*y*，返回当前的y缩放，默认为`null`；如果缩放的定义域或范围是通过函数修改的，则这个函数应该被再次调用，设置y比例，并重置缩放比例为1，平移为[0, 0]。

<a name="on" href="#on">#</a> zoom.**on**(*type*, *listener*)

注册监听器*listener*来接收指定事件类型*type*的缩放行为；支持的事件类型有：

* *zoomstart* - 缩放开始时 (e.g., touchstart)；
* *zoom* - 缩放行为发生时 (e.g., touchmove)；
* *zoomend* - 缩放行为结束时 (e.g., touchend)；

如果相同的事件类型已经指定了监听器，则首先会移除老的监听器，在加入新的监听器；要给一个事件类型注册多个监听器，则可以使用事件类型加命名空间后缀的形式，如："zoom.foo" 和 "zoom.bar"；想要移除监听器，只需要传入`null`即可；

对于鼠标滚轮事件，针对浏览器而言是没有明确的结束和开始通知的，在50毫秒内的多个事件会被分组到单个缩放中；如果想要更好的处理该种滚轮类型，请参考您的浏览器厂商，来获得更好的支持.

事件发生时，d3.event中会包含以下属性：

* *scale* - 一个数值，即当前的比例；
* *translate* - 一个含有两个数值元素的数组，代表平移向量。

<a name="event" href="#event">#</a> zoom.**event**(*selection*)

如果*selection*是一个选择器，立刻给注册的监听器分派一个缩放动作，作为三个时间序列：*zoomstart*，*zoom* 和 *zoomend*；这可以在设置了平移([translate](#translate))或比例([scale](#scale))后立刻触发监听器；如果*selection*是一个平移（transition），注册适当补间，使得缩放行为在过渡的过程中分派事件：*zoomstart* 事件发生在此前设定的视图平移开始时，*zoom* 事件则时刻发生在平移transition中，*zoomend* 事件则发生在平移transition结束时；注意：如果用户开始一个新的缩放行为前，之前的缩放行为动画会被立刻中断([interrupted](选择器#interrupt))。

* 魏飞T20141125
* guluP20141208 2014-12-8 22:21:03
