> {{  }}, 返回表达式结果  
> {%  %}, 执行语句  
> {#  #}, 注释  
> |filter, |filter(args...), 过滤器, 支持链式调用  
> is test, is test(args...), 测试  
> {%- a/r -%}, 去除返回左边和/或右边的空白  
> {% raw %} {% endraw %}, 转义块中内容  
> # 行语句, 括号内代码可换行  
> ## 行注释  
> {% block name %} {% endblock [name] %}, 定义块或扩展块  
> {% extends basefile %}, 继承  
> {{ self.block_name() }}, 多次调用块  
> {{ super() }}, 渲染父块内容  
> {% block name scoped %} {{ outer_varibles }} {% endblock %}  
> {% for item in iter %} {% endfor %}  
> loop.index		当前循环迭代的次数（从 1 开始）  
> loop.index0		当前循环迭代的次数（从 0 开始）  
> loop.revindex		到循环结束需要迭代的次数（从 1 开始）  
> loop.revindex0	到循环结束需要迭代的次数（从 0 开始）  
> loop.first		如果是第一次迭代，为 True 。  
> loop.last		如果是最后一次迭代，为 True 。  
> loop.length		序列中的项目数。  
> loop.cycle		在一串序列间期取值的辅助函数。见下面的解释。  
> {% for item in iter if condition %} {% endfor %}, 过滤项目  
> {% for item in iter %} {% else %} {% endfor %}, else 分支  
> {% for item in sitemap recursive %} {% if item.children %} {{ loop(item.children) }} {% endif %} {% endfor %}, 递归子项目  
> {% if condition %} {% endif %}, 简单分支  
> {% if condition %} {% elif condition %} {% else %} {% endif %}, 多重分支  
> {% macro name(args..., kargs...) -%} {%- endmacro %}, 宏定义  
> {{ macro_name(args...) }}, 宏调用  
> varargs: 位置参数列表, kwargs: 关键字参数列表, caller: 通过 call 调用宏的调用者, 宏内部特殊变量  
> name: 宏名, arguments: 参数名元组, defaults: 默认值元组, catch_kwargs: 是否接受额外的关键字参数, catch_varargs: 是否接受额外的位置参数, caller: 内部变量 caller 是否有效  
> 名称以下划线开始的宏不是导出的且不能被导入  
> {% filter name %} {% endfilter %}, 过滤  
> {% set key, value = call_something() %}, 变量赋值  
> {% include template_name %}, 包含模板内容  
> {% include template_name ignore missing [with|without context] %}, 忽略模板丢失错误  
> {% include [template_name1, template_name2] %}, 包含模板列表, 返回最先找到的那个  

### 表达式  
> 'string'/"string", 12/12.345, [‘list’, ‘of’, ‘objects’], (‘tuple’, ‘of’, ‘values’), {‘dict’: ‘of’, ‘key’: ‘and’, ‘value’: ‘pairs’}, true/false, 字面量  
> + - / // % * **, 算术  
> == != > >= < <=, 比较  
> and or not (expr): 表达式组, 逻辑  
> in: 包含检查, is: 测试, |: 过滤器, ~: 字符串连接, (): 函数调用, ./[]: 对象属性, 其他  
> <do something> if <something is true> else <do something else>, if 表达式  
