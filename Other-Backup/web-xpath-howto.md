# XPath基础

## 1.1 什么是XPath？

XPath 是一门在 XML 文档中查找信息(节点)的语言。XPath 可用来在 XML 文档中对元素和属性进行遍历。


## 节点

节点是XPath提取XML文档信息的最小单位，一共有7种：

（1）元素节点（element）

（2）属性节点（attribute）

（3）文本节点（text）

（4）名称命名节点（namespace）

（5）处理命令节点（processing-instruction）

（6）注释节点（comment）

（7）根节点（root）

## 节点关系

（1）父节点（parent）：每个元素以及属性都有一个父节点。

（2）子节点（child）：元素节点可以有零个、一个或多个子节点。

（3）同胞节点（sibling）: 拥有相同的父的节点。

（4）前辈节点（ancestor）:某节点的父节点的父节点。

（5）后代（descendant）:某节点的子节点的子节点。

## XPath 基本用法

 基本语法：

（1）//（双斜杠）：定位根节点，会对全文进行扫描，在文档中选取所有符合条件的内容，以列表的形式返回。
（2）/（单斜杠）:寻找当前标签路径的下一层路径标签或者对当前路标签内容进行操作 。
（3） /text()：获取当前路径下的文本内容 。
（4）/@xxxx：提取当前路径下标签的属性值 。
（5） | 可选符：使用|可选取若干个路径 如//p | //div 即在当前路径下选取所有符合条件的p标签和div标签。
（6）. 点：用来选取当前节点 。
（7）..（双点）：选取当前节点的父节点 。
（8）“*”（通配符）：表示匹配任何元素节点。
（9）“@*”（通配符）：表示匹配任何属性值。
（10）“node（）”（通配符）：表示匹配任何类型的节点。

## example code

```
```
