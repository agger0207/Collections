# 专题阅读 之 Core Animation相关

=========================================================================================================

## 一 Core Animation 之 iOS-Core-Animation-Advanced-Techniques

链接：https://github.com/AttackOnDobby/iOS-Core-Animation-Advanced-Techniques

对应的gitbook排版:
https://www.gitbook.com/book/zsisme/ios-/details

内容：主要是对iOS Core Animation: Advanced Techniques的翻译, 中文名就是iOS 核心动画高级技巧

### 读书心得与笔记：

第一章 图层树

可以帮助理解三棵树的关系，即Model Tree(模型树), Presentation Tree（呈现树）以及Rendering Tree（渲染树）.
以及理解View和Layer 的对应关系；

Model Tree: 我们修改的CALayer, 属于CALayer的Model层；通常我们是通过修改Model Tree的属性来使得显示生效；
Presentation Tree: 展示的CALayer的Tree; 那么主要是可以获取到渲染时的属性，做动画的时候可以在动画的不同阶段获取到当前显示的界面的属性；
Rendering Tree: 渲染所用，私有，应用开发过程中不可操作。

第十二章 性能调优
介绍了影响渲染性能的主要因素（离屏渲染和组合）；介绍如何使用Instrument Core Animation来检测帧率，检测性能瓶颈，检测离屏渲染和组合，检测是否使用缓存；从而优化性能。

给出了示例如何通过开启光栅化合理的通过Cache来避免过多的离屏渲染从而达到性能优化的目的。

从这一章，我们可以了解到为什么之前一些性能优化的文章说，需要利用opaque属性来提高性能，因为可以避免组合(Blending); 为什么设置圆角、阴影会影响性能（因为会带来离屏渲染，更好的办法是使用shadowPath设置阴影或者开启光栅化shouldRasterize); 以及为何有时候开启shouldRasterize反而会降低性能。

同时，也能够对在什么时候使用Core Graphics绘制view有一个认识: 如果视图简单，那么应该尽量使用UIKit，性能更好；只有当视图非常复杂的时候，才去尝试自定义绘制；最理想的方法，应该是将绘制的过程放在另一个线程中，在主线程中应该是只获取到绘制后的最后的图片；这样性能更佳。


## 二 Core Animation 的Session

## 三 iOS-Core-Animation-Advanced-Terchiniques 读书笔记与总结

### 1 英文笔记1

https://gist.github.com/JeOam/94e833bcefd738d805cc

主要内容："iOS-Core-Animation-Advanced-Terchiniques"前六章；不过没仔细看是原文还是摘抄还是理解；里面关于The Backing Image的内容可以看一下，这样也能够理解CA里面的一些术语。


