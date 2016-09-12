> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[SVG函数]] ▸ **SVG 轴**

-------------

+ 本文档由[VisualCrew小组](https://github.com/VisualCrew)耗时两年翻译，并保持与[最新版](https://github.com/mbostock/d3/wiki/API-Reference)同步。
+ 如发现翻译不当或有其他问题可以通过以下方式联系译者:
    - 邮箱：zhang_tianxu@sina.com
    - QQ群：[D3.js](http://jq.qq.com/?_wv=1027&k=239rjew):437278817，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)：436442115
+ API使用方法可参考：https://github.com/tianxuzhang/d3-api-demo

-------------

D3的轴组件([axis component](http://bl.ocks.org/mbostock/1166403))自动展示比例尺参照的线。这使得你可以专注于展示数据，而轴组件需要关心绘制坐标轴和刻度标记的繁琐任务。

[![Axis Component](http://bl.ocks.org/mbostock/raw/1166403/thumbnail.png)](http://bl.ocks.org/mbostock/1166403)
[![6186172](http://bl.ocks.org/mbostock/raw/6186172/thumbnail.png)](http://bl.ocks.org/mbostock/6186172)
[![5537697](http://bl.ocks.org/mbostock/raw/5537697/thumbnail.png)](http://bl.ocks.org/mbostock/5537697)
[![4573883](http://bl.ocks.org/mbostock/raw/4573883/thumbnail.png)](http://bl.ocks.org/mbostock/4573883)
[![4403522](http://bl.ocks.org/mbostock/raw/4403522/thumbnail.png)](http://bl.ocks.org/mbostock/4403522)
[![4349486](http://bl.ocks.org/mbostock/raw/4349486/thumbnail.png)](http://bl.ocks.org/mbostock/4349486)
[![3892919](http://bl.ocks.org/mbostock/raw/3892919/thumbnail.png)](http://bl.ocks.org/mbostock/3892919)
[![3371592](http://bl.ocks.org/mbostock/raw/3371592/thumbnail.png)](http://bl.ocks.org/mbostock/3371592)
[![3259783](http://bl.ocks.org/mbostock/raw/3259783/thumbnail.png)](http://bl.ocks.org/mbostock/3259783)
[![3212294](http://bl.ocks.org/mbostock/raw/3212294/thumbnail.png)](http://bl.ocks.org/mbostock/3212294)
[![2983699](http://bl.ocks.org/mbostock/raw/2983699/thumbnail.png)](http://bl.ocks.org/mbostock/2983699)
[![2996766](http://bl.ocks.org/mbostock/raw/2996766/thumbnail.png)](http://bl.ocks.org/mbostock/2996766)
[![2996785](http://bl.ocks.org/mbostock/raw/2996785/thumbnail.png)](http://bl.ocks.org/mbostock/2996785)
[![1849162](http://bl.ocks.org/mbostock/raw/1849162/thumbnail.png)](http://bl.ocks.org/mbostock/1849162)
[![4323929](http://bl.ocks.org/mbostock/raw/4323929/thumbnail.png)](http://bl.ocks.org/mbostock/4323929)

## Axis

轴组件设计来和D3的定量([quantitative](数值比例尺))，时间([time](时间比例尺))和序数比例尺([ordinal](序数比例尺))一起使用。

<a name="axis" href="SVG-Axes#axis">#</a> d3.svg.<b>axis</b>()

创建一个默认的轴。

<a name="_axis" href="SVG-Axes#_axis">#</a> <b>axis</b>(<i>selection</i>)

将轴应用到[选择器](选择器)和[过渡](过渡)上。选择必须包含`svg`或者`g`元素。例如：

```js
d3.select("body").append("svg")
    .attr("class", "axis")
    .attr("width", 1440)
    .attr("height", 30)
  .append("g")
    .attr("transform", "translate(0,30)")
    .call(axis);
```

<a name="scale" href="#scale">#</a> axis.<b>scale</b>([<i>scale</i>])

如果指定了 *scale* 参数则设置刻度尺，并返回轴。如果未指定 *scale* 参数，将返回当前的刻度尺，默认为线性刻度。

<a name="orient" href="#orient">#</a> axis.<b>orient</b>([<i>orientation</i>])

如果指定了方向 *orientation* 参数则设置方向 ，并返回轴。如果未指定 *orientation* 参数，将返回当前的刻度尺，默认为`"bottom"`。支持下面几种方向：

* `"top"` -刻度位于横轴域路径上面
* `"bottom"` -刻度位于横轴域路径下面
* `"left"` -刻度位于纵轴域路径左边
* `"right"` -刻度位于纵轴域路径右边

如果指定的方向是不支持的值之一，该轴将恢复为默认的方向。改变方向将影响刻度和它们的标签相对于轴路径的的位置，但不改变该轴本身的位置; 为了改变轴相对于基址图的位置，可以指定`g`元素上的 [transform](http://www.w3.org/TR/SVG/coords.html#TransformAttribute) 变换属性。

<a name="ticks" href="#ticks">#</a> axis.<b>ticks</b>([<i>arguments…</i>])

如果指定了 *arguments* 参数，存储指定的参数为之后来用生成刻度并返回轴。参数之后会传递给[scale.ticks](数值比例尺#linear_ticks)生成刻度值(除非刻度值通过明确地指定[axis.tickValues](#tickValues))。参数将传递给比例尺的tickFormat方法用来生成默认的刻度格式。如果没有指定参数，返回当前的刻度参数，默认是[10]。

合适的参数取决于关联的比例尺：对于[线性比例尺](数值比例尺)，你可以指定刻度数为`axis.ticks(20)`；对于[对数比例尺](数值比例尺#log_tickFormat)你可以指定数量和刻度格式；对于[时间比例尺](时间比例尺#ticks)，时间间隔例如`axis.ticks(d3.time.minutes, 15)`可能更合适。

<a name="tickValues" href="#tickValues">#</a> axis.<b>tickValues</b>([<i>values</i>])

如果指定了 *values* 数组，指定的数值 将用于刻度，而不是使用使用比例尺的自动刻度生成器。如果 *values* 是`null`，清空任何预先设定的明确的刻度值，回到原来比例尺的生成器。如果没有指定 *values* ，返回当前设定的刻度值，默认是`null`。例如，为了生成刻度为指定的值：

```js
var xAxis = d3.svg.axis()
    .scale(x)
    .tickValues([1, 2, 3, 5, 8, 13, 21]);
```

明确地刻度值优先于通过使用 [axis.ticks](#ticks) 设置刻度参数。但是，任何的参数都仍然传递给比例尺的 [tickFormat](#tickFormat) 函数，如果一个刻度格式也没设置；这样，它可以有效的设置axis.ticks和axis.tickValues。

<a name="tickSize" href="#tickSize">#</a> axis.<b>tickSize</b>([<i>inner, outer</i>])

如果指定了 *inner* 和 *outer* ，设置内部和外部刻度尺寸为指定的值并返回轴。如果 *inner* 和 *outer* 没有指定，返回当前的内部刻度尺寸，默认是6。

<a name="innerTickSize" href="#innerTickSize">#</a> axis.<b>innerTickSize</b>([<i>size</i>])

如果指定了 *size* ，设置内部刻度尺寸为指定的值并返回轴。如果没有指定 *size* ，返回当前的内部刻度尺寸，默认是6。内部刻度尺寸控制刻度线的长度，从轴的原生位置偏移。

<a name="outerTickSize" href="#outerTickSize">#</a> axis.<b>outerTickSize</b>([<i>size</i>])

如果指定了 *size* ，设置外部刻度尺寸为指定的值，并返回轴。如果没有指定 *size* ，返回当前的外部刻度尺寸，默认是6。外部刻度尺寸控制域路径末尾的平方长度，从轴的原生位置偏移。这样，因此，“外刻度”实际上不是刻度但是域路径的一部分，并且它们的位置由相关的比例尺的域范围来确定。这样，外刻度可能与第一个或最后内部刻度重叠。外刻度尺寸0的禁止域路径的平方端，而不是产生一条直线。

<a name="tickPadding" href="#tickPadding">#</a> axis.<b>tickPadding</b>([<i>padding</i>])

如果指定填充边距 *padding*，设置填充边距的指定值并返回对应的轴。如果没有指定填充边距 *padding*，返回当前默认填充边距（默认为3像素）。

<a name="tickFormat" href="#tickFormat">#</a> axis.<b>tickFormat</b>([<i>format</i>])

如果指定格式 *format*，格式设置为指定的函数并返回axis。如果没有指定格式 *format*，返回当前格式函数，默认为空。空格式表示应该使用比例尺的默认格式器，此格式通过调用[scale.tickFormat](数值比例尺#linear_tickFormat)产生。在这种情况下，[ticks](#ticks)指定的参数同样传递给scale.tickFormat方法。

查看[d3.format](格式化#d3_format)创建格式的帮助。例如,`axis.tickFormat(d3.format(.0f“))`将通过逗号分组千位显示一个整数。首先定义格式器：`var commasFormatter = d3.format(”,.0f”)` 可以让你把它作为你的数据的函数，例如,在comma-grouped整数前添加“$”符号：`.tickFormat(function(d) { return "$" + commasFormatter(d); })`。

注意:对于对数比例尺，刻度的数值不能自定义；然而，刻度的数值标签**可以**通过[ticks](#ticks)自定义。同样，对数比例尺刻度的格式器通常是通过ticks而不是tickFormat指定，以保持默认标签隐藏(label-hiding)行为。

------

|本文参与  |人员   |组织   |时间   |
|------   |------ |------|------|
|翻译(axis.scale、axis.orient)      |小屁孩|-|20140425 21:40:39| 
|翻译(axis.tickPadding、axis.tickFormat)      |[WeiFei365](https://github.com/WeiFei365)|[VisualCrew小组](https://github.com/VisualCrew)|2014-11-29 17:03:41| 
|翻译(其余)、校对 |[大傻](https://github.com/tianxuzhang)|[VisualCrew小组](https://github.com/VisualCrew)|2014-11-29 16:56:20 |
|校对/排版/案例补充         |[liang42hao](https://github.com/liang42hao)|[VisualCrew小组](https://github.com/VisualCrew)|2016-03-02T20:16:32Z|