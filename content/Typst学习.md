---
title: Typst 学习
date: 2024-05-18T00:13
tags:
  - Typst
---
> [!tip] 学习资料:
> - [Typst中文教程(小蓝书)](https://github.com/typst-doc-cn/tutorial?tab=readme-ov-file)
## 「set」语法
Typst 允许你为元素的「具名参数」设置新的「默认值」，这个特性由「set」语法实现。
例如，你可以这样设置文本字体：
```
#set text(fill: red)
```

## 「show」语法

「set」语法是「show set」语法的简写。因此显然，相比set，「show」语法可以更强大。
```
#show: set text(fill: blue)
```
我们可以看到「show」语法由两部分组成，由冒号分隔。

show 的左半部分是选择器，表示选择文档的一部分以作修改。它作用于「作用域」内的后续所有被选
择器选中的内容。
如果选择器为空，则默认选择后续所有内容。

第三方包在`C:\Users\<user>\AppData\Local\typst\packages\preview\`目录下