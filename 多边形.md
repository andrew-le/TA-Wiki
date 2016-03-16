> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[几何]] ▸ **多边形**

* 如发现翻译不当或有其他问题可以通过以下方式联系译者:
* 邮箱：zhang_tianxu@sina.com
* QQ群：[D3数据可视化](http://jq.qq.com/?_wv=1027&k=ZGcqYF)205076374，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)436442115

<a name="polygon" href="Polygon-Geom#polygon">#</a> d3.geom.<b>polygon</b>(<i>vertices</i>)

返回顶点的输入数组，并且附有一些其他方法，如下面所描述

<a name="area" href="Polygon-Geom#area">#</a> polygon.<b>area</b>()

返回此多边形的标定区域。如果顶点是逆时针顺序，面积为正，否则为负。

<a name="centroid" href="Polygon-Geom#centroid">#</a> polygon.<b>centroid</b>()

返回一个表示此多边形的质心的两元素数组。

<a name="clip" href="Polygon-Geom#clip">#</a> polygon.<b>clip</b>(<i>subject</i>)

对这个多边形剪切主题多边形 *subject* 。换句话说，返回一个多边形表示这个多边形和主题多边形的交集。假定剪切的多边形是逆时针方向以及凸多边形。

* 谁浮T20141125
* guluP20141208 2014年12月8日 21:07:33

