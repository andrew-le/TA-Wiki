> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[SVG函数]] ▸ **SVG 轴**

* 本文档是D3官方文档中文翻译，并保持与[最新版](https://github.com/mbostock/d3/wiki/API-Reference)同步。
* 如发现翻译不当或有其他问题可以通过以下方式联系译者:
* 邮箱：zhang_tianxu@sina.com
* QQ群：[D3数据可视化](http://jq.qq.com/?_wv=1027&k=ZGcqYF)205076374，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)436442115

D3的轴组件自动展示比例尺参照的线。这使得你可以专注于展示数据，而轴组件需要关心绘制坐标轴和刻度标记的繁琐任务。
                             
Axis
轴组件设计来和D3的定量，时间和序数比例尺一起使用。
# d3.svg.axis()

创建一个默认的轴。
# axis(selection)
将轴应用到选择和过渡上。选择必须包含svg或者g元素。例如：
d3.select("body").append("svg")
    .attr("class", "axis")
    .attr("width", 1440)
    .attr("height", 30)
  .append("g")
    .attr("transform", "translate(0,30)")
    .call(axis);
# axis.scale([scale])

如果指定了scale 参数则设置刻度尺，并返回轴。如果未指定scale参数，将返回当前的刻度尺，默认为线性刻度。

# axis.orient([orientation])

如果指定了方向orientation 参数则设置orientation ，并返回轴。如果未指定orientation参数，将返回当前的刻度尺，默认为“bottom”。支持下面几种方向：
•	top -刻度位于横轴域路径上面
•	bottom -刻度位于横轴域路径下面
•	left -刻度位于纵轴域路径左边
•	right -刻度位于纵轴域路径右边
如果指定的方向是不支持的值之一，该轴将恢复为默认的方向。改变方向将影响刻度和它们的标签相对于轴路径的的位置，但不改变该轴本身的位置; 为了改变轴相对于基址图的位置，可以指定g元素上的transform 变换属性。


# axis.ticks([arguments…])

如果指定了arguments 参数，存储指定的参数为之后来用生成刻度并返回轴。参数之后会传递给scale.ticks生成刻度值（除非刻度值通过明确地指定axis.tickValues）。参数将传递给比例尺的tickFormat方法用来生成默认的刻度格式。如果没有指定参数，返回当前的刻度参数，默认是[10]。

合适的参数取决于关联的比例尺：对于线性比例尺，你可以指定刻度数为axis.ticks(20)；对于对数比例尺你可以指定数量和刻度格式；对于时间比例尺，时间间隔例如axis.ticks(d3.time.minutes, 15)可能更合适。
# axis.tickValues([values])

如果指定了values 数组，指定的values 将用于刻度，而不是使用使用比例尺的自动刻度生成器。如果values 是null，清空任何预先设定的明确的刻度值，回到原来比例尺的生成器。如果没有指定values ，返回当前设定的刻度值，默认是null。例如，为了生成刻度为指定的values ：
var xAxis = d3.svg.axis()
    .scale(x)
    .tickValues([1, 2, 3, 5, 8, 13, 21]);

明确地刻度值优先于通过使用axis.ticks设置刻度参数。但是，任何的参数都仍然传递给比例尺的tickFormat 函数，如果一个刻度格式也没设置；这样，设置axis.ticks和axis.tickValues它可能有效。
# axis.tickSize([inner, outer])
如果指定了inner和outer，设置内部和外部刻度尺寸为指定的值并返回轴。如果inner和outer没有指定，返回当前的内部刻度尺寸，默认是6。
# axis.innerTickSize([size])

如果指定了size ，设置内部刻度尺寸为指定的值并返回轴。如果没有指定size ，返回当前的内部刻度尺寸，默认是6。内部刻度尺寸控制刻度线的长度，从轴的原生位置偏移。
# axis.outerTickSize([size])

如果指定了size ，设置外部刻度尺寸为指定的值，并返回轴。如果没有指定size ，返回当前的外部刻度尺寸，默认是6。外部刻度尺寸控制域路径末尾的平方长度，从轴的原生位置偏移。这样，因此，“外刻度”实际上不是刻度但是域路径的一部分，并且它们的位置由相关的比例尺的域范围来确定。这样，外刻度可能与第一个或最后内部刻度重叠。外刻度尺寸0的禁止域路径的平方端，而不是产生一条直线。
# axis.tickPadding([padding])

如果指定填充边距，设置填充边距的指定值并返回对应的axis。如果没有指定填充边距，返回当前默认填充边距（默认为3像素）。

# axis.tickFormat([format])

如果指定格式，格式设置为指定的函数并返回axis。如果没有指定格式，返回当前格式函数，默认为空。空格式表示应该使用比例尺的默认格式器，此格式通过调用scale.tickFormat产生。在这种情况下，指定的参数同样传递给scale.tickFormat方法。
查看d3.format创建格式的帮助。例如,axis.tickFormat(d3.format(.0f“))将通过逗号分组千位显示一个整数。首先定义格式器：var commasFormatter = d3.format(”,.0f”) 可以让你把它作为你的数据的函数，例如,在comma-grouped整数前添加“$”符号：.tickFormat(function(d) { return "$" + commasFormatter(d); })。
注意:对于对数比例尺，刻度的数值不能自定义；然而，刻度的数值标签可以通过ticks自定义。同样，对数比例尺刻度的格式器通常是通过ticks而不是tickFormat指定，以保持默认label-hiding行为。

* axis.scale  axis.orient小屁孩翻译，咕噜校正20140425 21:40:39
* axis.tickPadding  axis.tickFormat魏飞20140427译 咕噜校对 2014-11-29 17:03:41
* 其余 咕噜译 2014-11-29 16:56:20
