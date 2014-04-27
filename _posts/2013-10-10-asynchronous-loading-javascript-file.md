---
layout: post
title: "几种常见的异步加载javascript"
description: ""
category: 
tags: [javascript]
---

## 几种常见的异步加载javascript

### document.write

浏览器都支持这一写法。

但是，使用场景受限。 具体表现是当页面存在多个 script 节点时，包`document.write`的 script 节点会阻止后续 script 节点中 javascript 的解析，这个，需要确认一下结合情况考虑是否是想要的。

关于 document.write 的一些讨论: [Why is document.write considered a “bad practice”?](http://stackoverflow.com/questions/802854/why-is-document-write-considered-a-bad-practice)

由于当页面加载完毕之后，document.write
可能会重写页面，所以在不确定因素下，尽可能避免使用该方法.

### async 

优点: html5中标准，也就是支持标准的都支持，或即将支持. (具体见[这里](http://caniuse.com/#feat=script-async))

缺点: ie9以下以及ios 上低版本的 safari 不支持。这意味着什么。

要注意的一点，因为 async 是**下载完就执行** 所以实际情况下，有可能后面的 js 先下载完成，并且在依赖前面的 js 文件时，这种情况可能会出现异常。

### defer

ie 私有属性。但 Firefox 也支持较早。其他 A 级主流浏览器是从哪个版本号开始也给予了支持我没做详细测试。

优点： 连 ie 都支持。另外，相比较 async，较好得遵从了 dom 原本顺序来执行。

缺点： 是 ie 私有属性。

### 创建 dom 方式

优点： 最佳实践。

注意 由于 ie 的内存泄露比较严重，所以需要回收废弃节点上的资源占用。

[讨论1](http://www.iteye.com/topic/459090)

EOF
