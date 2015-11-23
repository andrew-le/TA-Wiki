> [Wiki](Home) ▸ [[API--中文手册]] ▸ [[几何]] ▸ **赫尔**

* 如发现翻译不当或有其他问题可以通过以下方式联系译者:
* 邮箱：zhang_tianxu@sina.com
* QQ群：[D3数据可视化](http://jq.qq.com/?_wv=1027&k=ZGcqYF)205076374，[大数据可视化](http://jq.qq.com/?_wv=1027&k=S8wGMe)436442115

# d3.geom.hull()
 使用默认的x和y访问器创建一个新的hull布局。
# hull(vertices)

返回指定顶点数组的凸包，使用当前x和y坐标访问器。返回的凸包被表示为包含输入顶点的子集的数组，排列成逆时针顺序（与polygon.clip一致）。
Assumes the vertices array is greater than three in length. If vertices is of length <= 3, returns [].
假设顶点数组vertices 的长度大于3。如果顶点vertices 是长度< = 3 ，则返回[] 。
# hull.x([x])

如果指定的x ，则设置X坐标访问器。如果没有指定X是返回当前x坐标访问，默认为：
function(d){returnd[0];}
# hull.y([y])

如果指定的y，则设置y坐标访问器。如果没有指定y是返回当前y坐标访问，默认为：
function(d){returnd[1];}

* 谁浮T20141125
* guluP 2014年12月8日 21:01:53
