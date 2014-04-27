---
layout: post
title: "Javascript Async"
description: "简单对比几种 Javascript Asnyc 模式的区别."
category: 
tags: [javascript]
---

## 简单对比几种 Javascript Asnyc 模式的区别.


### Callback

优点: 简单, 无依赖. 如果程序简单, 可以选择之.

缺点: 简单则不适合复杂项目. 容易造成高耦合. 只能指定一个回调, 不够灵活. 

### Event Emitter

优点: 和 DOM 绑定事件较为类似. 较好理解, 容易掌握, 对多个事件的绑定也能良好得支持. 

缺点: 多模块通讯是个问题. 或者更确切得说, 这是该方式不适合的一个场景. 逻辑稍微复杂就容易嵌套过深, 可以回避. 适合模块内通讯.

### Subscribe & Publish

与 **Event Emitter** 很类似. 

优点: 低耦合. 感觉该模式 是 **Event Emitter** 更为完善的版本, 适合 **Event Emitter** 的场景, 肯定 **Sub & Pub** 可以替代之, 反之未必.

缺点: 还没看到.

### Promise 模式

优点: 潮流的链式写法, 加之任务流中增加了 `reject` 的处理结果, 都使得程序逻辑如流水般变得清晰. 

缺点: 相对前三者稍微复杂了一些. 不适合模块间通讯.

## 总结

不得不提, 往往会碰到这样一个实际场景: 

    条件 I 已经满足, 程序才执行到`如果 I 满足 则 执行 T` 的逻辑. 

这种情景下依然希望 T 能执行而不是通过让程序再次手动触发一次 I
事件(实际中这也未必可控). 这种情况下, 前两种方式不得不退出舞台了.

最后来个总结, 引用一下.

    Pub Sub is more flexible for cross-component events.
    Deferred and Promises give a powerful way to handle callbacks.

[via](http://otaqui.com/blog/1374/event-emitter-pub-sub-or-deferred-promises-which-should-you-choose/)

各有各的适用场景, 则其适者而用之.

EOF

