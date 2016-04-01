> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[布局]] ▸ **直方图布局**

* 如发现翻译不当或有其他问题可以通过以下方式联系译者:
* 邮箱：zhang_tianxu@sina.com
* QQ群：[D3数据可视化](http://jq.qq.com/?_wv=1027&k=ZGcqYF)205076374，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)436442115

**直方图布局(histogram layout)**可以用来表示数据分布，通过将离散数据点分组归纳到箱子里。使用实例详见 [bl.ock 3048450](http://bl.ocks.org/mbostock/3048450)。

<a name="histogram" href="Histogram-Layout#histogram">#</a> d3.layout.**histogram**()

使用默认值访问器、范围函数和箱函数，构建新的直方图函数。默认条件下，直方图函数返回值为频率。返回布局对象既是一个对象，也是一个函数。即: 可以像调用其他函数一样调用该布局，并且布局有额外的方法改变自身行为。和D3中的其他类一样，布局遵循方法链模式，在该模式下setter方法返回布局本身，允许使用简单语句调用多个setter。

<a name="_histogram" href="Histogram-Layout#_histogram">#</a> **histogram**(*values*[, *index*])

在指定的*values*数组上计算直方图。可以指定一个可选参数*index*, 传递给范围函数和箱函数。返回值为数组的数组：外部数组的每个元素表示一个容器，每个容器包含输入*values*的相关元素。此外，每个容器有三个属性：

* *x* -箱的下界（包含）。
* *dx* -箱的宽度；x + dx为上界（不包含）。
* *y* - 计数（如果[frequency](#frequency)为`true`），或概率（如果frequency为`false`）。

请注意，在频率方式上，y属性和长度属性相同。

<a name="value" href="#value">#</a> histogram.**value**([*accessor*])

指定从关联数据中提取值的方法；*accessor*是一个函数，每当输入值传递到[histogram](#_histogram)时，都需要调用该函数，即等于在计算直方图之前调用values.map(accessor)。默认值函数为内置[Number](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Number)，与恒等函数类似。如果未指定*accessor*，则返回当前值访问器。

<a name="range" href="#range">#</a> histogram.**range**([*range*])

指定直方图范围。忽略在指定范围之外的值。可以通过二元数组指定range，数组表示范围的最大值和最小值；或者将range指定为一个函数，该函数返回values数组和传递到histogram的当前索引。默认范围为值的长度([minimum](数组#d3_min) 和 [maximum](数组#d3_max))。如果未指定range，则返回当前范围函数。

<a name="bins" href="#bins">#</a> histogram.**bins**()
<br><a name="bins" href="#bins">#</a> histogram.**bins**(*count*)
<br><a name="bins" href="#bins">#</a> histogram.**bins**(*thresholds*)
<br><a name="bins" href="#bins">#</a> histogram.**bins**(*function*)

详细说明如何将值归类到直方图中。如果没有指定参数，则返回当前箱函数，默认值为[Sturges' formula](http://en.wikipedia.org/wiki/Histogram)的一个实现，Sturges' formula使用等间隔的值将值划分到不同的箱当中。如果已经指定*count*值，则将 [range](#range)的值均匀分布到指定数量的箱中。

如果已指定*thresholds*数组，则它定义了箱的极限值，从最左边的值（最小值）开始到最右边的值（最大值）。*n* + 1 *thresholds*指定了*n*个箱。任何小于*thresholds[1]*的值都将被放在第一个箱中；同理，任何大于或等于*thresholds[thresholds.length - 2]*的值将被放在最后一个箱中。因此，虽然第一个和最后一个极值并未分配到箱中，但他们对于定义第一个箱的*x*属性和最后一个箱的dx属性还是有必要存在的。

最后，如果已经指定箱*function*，该函数会在布局传递数据时调用，传递当前[range](#range)，值得数列和当前索引传递到[histogram](#_histogram)。该函数必须返回上文所述的*thresholds*数列。

<a name="frequency" href="#frequency">#</a> histogram.**frequency**([*frequency*])

**<此段需更新>**
指定直方图的*y*值是否是一个计数（频率）或概率（密度）；默认值为频率。如果没有指定频数，则返回当前频率的布尔值。
**<此段需更新>**

**此段现为**
```
Specifies the meaning of the generated bins’ *y*-values. If *frequency* is true, which is the default, the *y*-value represents the count of elements in the bin. If false, it represents the probability of a random element in the sample population being in that bin. Note that this is a *probability*, not a *probability density*, and so for [irregular histograms](http://bl.ocks.org/mbostock/1624660), you must normalize the *y*-value by the bin width (`bin.y / bin.dx`) for the area of the displayed bar to be proportional to the probability. If *frequency* is not specified, returns the current frequency boolean.
```

----
* 张烁译 20140430 
* 咕噜校对 2014-11-30 10:42:08
