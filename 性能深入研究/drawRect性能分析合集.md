# drawRect性能分析合集


## 官方文章与文档：

### 1 iOS-Core-Animation-Advanced-Techniques

翻译可以参见：
https://github.com/AttackOnDobby/iOS-Core-Animation-Advanced-Techniques/blob/master/12-%E6%80%A7%E8%83%BD%E8%B0%83%E4%BC%98/%E6%80%A7%E8%83%BD%E8%B0%83%E4%BC%98.md

重点是第十二章，第十三章和十五章.

### 2 wwdc 2012 中 的session "session_238__ios_app_performance_graphics_and_animations.pdf"

When possible, use CALayer properties instead


### 官方观点总结：


## 著名文章与讨论:
### 1 深入的讨论
http://stackoverflow.com/questions/14659563/to-drawrect-or-not-to-drawrect-when-should-one-use-drawrect-core-graphics-vs-su

这里面作者提出的问题就是想知道为什么 一方面说CG性能差；但是使用CG却可以改善UITableViewCell的性能

### 2 后台绘制

http://onevcat.com/2014/03/common-background-practices/

这篇王巍写的文章中给出了下面两个链接专门讨论drawRect的性能问题.

这里面也谈到了后台执行绘制代码的问题

给出来的两个链接：
http://floriankugler.com/2013/05/24/layer-trees-vs-flat-drawing-graphics-performance-across-ios-device-generations/

https://lobste.rs/s/ckm4uw/a_performance-minded_take_on_ios_design/comments/itdkfh



### 经验性结论：

UITableViewCell中使用drawRect大幅提高性能；但据说只是在2013年之前的老设备中.