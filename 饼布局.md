> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[布局]] ▸ **饼布局**

* 如发现翻译不当或有其他问题可以通过以下方式联系译者:
* 邮箱：zhang_tianxu@sina.com
* QQ群：[D3数据可视化](http://jq.qq.com/?_wv=1027&k=ZGcqYF)205076374，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)436442115

饼布局方便与计算组成饼图或圈图的弧的开始和结束的角度：
 
![pie](https://github.com/mbostock/d3/wiki/pie.png)

并*不一定*要用饼布局来画饼状图，如果你喜欢，你还可以直接弧形状([arc shape](SVG-形状#arc))。饼布局会简单的将一个数据数组（如字符串数据）转换成一个对象数据，这个对象数组中会包含开始角度和结束角度，这些角度的范围为0到2π，然后传给弧形生成器。

<a name="pie" href="#pie">#</a> d3.layout.**pie**()

构造一个新的饼图函数，使用默认的值访问器（数值）、进行比较排序（降序）、开始角度（0）、结束角度（2π）；返回的布局对象即是对象也是一个函数，这就意味着：你可以想调用方法一样调用该布局对象，布局还具有改变其行为的其他方法；就像D3的其他类型方法一样，饼布局也支持方法链模式，setter方法返回布局自身，允许在一个简单的申明中调用多个setter方法。

<a name="_pie" href="#_pie">#</a> **pie**(*values*[, *index*])

用指定的*values*数组计算饼函数。一个可选的*index* 参数会被传递给开始和结束的函数；返回值是一个数组，数组元素包含以下属性：

* value - 数据值，计算来自于*value* 生成器；
* startAngle - 弧的开始弧度，非角度；
* endAngle - 弧的结束弧度，非角度；
* data - 数据原生的值；

按照原生的排序返回元素，匹配*values*参数，即使排序([sort](#sort))顺序已经应用了；这保证了数组中每个元素原生的索引，这是非常好的，当你使用原生的值数组来匹配颜色分类时。

<a name="value" href="#value">#</a> pie.**value**([*accessor*])

指定如何从关联的数据提取值（如：给饼图绑定一个访问器函数）；*accessor* 是一个函数，会在每个输入值传给[pie](#_pie)时调用，原理相当于在计算饼布局前，先调用了`values.map(accessor)`；该函数可以传两个参数：当前的数据d和所在索引i；默认的值函数是内置的[Number](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Number)，类似于特征函数；如果未指定accessor ，则返回当前的访问器 。

<a name="sort" href="#sort">#</a> pie.**sort**([*comparator*])

如果指定比较函数*comparator*，则设置数据的排序方法为指定的；传入`null`来禁止排序；如果未指定*comparator*，则返回当前的比较函数 ；默认的排序方法是降序；排序会保留原生数据的索引，只会影响到角度；比较函数会在每对传给 [pie](#_pie) 的数据上调用；当然，该排序函数你可以使用 [d3.ascending](Arrays#d3_ascending) 或  [d3.descending](Arrays#d3_descending) 代替。

<a name="startAngle" href="#startAngle">#</a> pie.**startAngle**([*angle*])

如果指定*angle* ，则设置饼布局所有的起始弧度为指定值：如果未指定*angle* ，返回当前的值，默认为0；起始弧度可以被指定为常数或一个函数，如果是函数，当 [pie](#_pie)被调用时，会进行一次起始弧度的计算，被传递的参数有：当前数据d和索引i。

<a name="endAngle" href="#endAngle">#</a> pie.**endAngle**([*angle*])

如果指定*angle*，则设置饼布局所有的起始弧度为指定值：如果未指定angle ，返回当前的值，默认为2π；起始弧度可以被指定为常数或一个函数，如果是函数，当 [pie](#_pie)被调用时，会进行一次起始弧度的计算，被传递的参数有：当前数据`d`和索引`i`。
 
 <a name="padAngle" href="#padAngle">#</a> pie.**padAngle**([*angle*])

如果指定*angle*，将填充角(pad angle)设为给定的弧度. 相邻的弧将被填充角[分隔](http://bl.ocks.org/mbostock/f098d146315be4d1db52). 若*angle*未指定, 返回当前值, 默认为0. 填充角既可以是数值也可以是函数, 若其为函数, 则会在 [pie](#_pie) 函数被调用时带入当前的数据`d`和索引`i`求值

----
* 魏飞译 2014-07-16-19-25
* 咕噜校对 2014-11-30 21:19:34