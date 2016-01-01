微专业Issue

参考：

https://github.com/AttackOnDobby/iOS-Core-Animation-Advanced-Techniques/blob/master/2-%E5%AF%84%E5%AE%BF%E5%9B%BE/%E5%AF%84%E5%AE%BF%E5%9B%BE.md

“现在你理解了CALayerDelegate，并知道怎么使用它。但是除非你创建了一个单独的图层，你几乎没有机会用到CALayerDelegate协议。因为当UIView创建了它的宿主图层时，它就会自动地把图层的delegate设置为它自己，并提供了一个-displayLayer:的实现，那所有的问题就都没了。

当使用寄宿了视图的图层的时候，你也不必实现-displayLayer:和-drawLayer:inContext:方法来绘制你的寄宿图。通常做法是实现UIView的-drawRect:方法，UIView就会帮你做完剩下的工作，包括在需要重绘的时候调用-display方法。”


我的理解：
如果一个layer是依附于view的，那么不可以将layer的delegate设置为view之外的其他对象，否则会有问题；例如原来的微专业Demo中的例子就会存在crash，因为将一个view的layer的delegate设置为了controller; 必须在dealloc的时候将layer.delegate设置为nil才可以。


那么必须按照参考链接里面的做法，单独创建一个layer并且加入到view的layer中，这个时候就可以将layer的delegate设置为controller了.





### 其他一些有用的参考

1 http://stackoverflow.com/questions/4979192/ios-using-uiviews-drawrect-vs-its-layers-delagate-drawlayerincontext

"Always use drawRect:, and never use a UIView as the drawing delegate for any CALayer."

"This is why drawRect: was never called when you implemented drawLayer:inContext:"

从调用堆栈中其实是可以看到，drawRect其实就是通过drawLayer:inContext来调用到的...

2 http://stackoverflow.com/questions/10656975/calayer-delegation-causes-zombie-crash-why#

我自己遇到的crash和上面是一样的；但其实答案里面给出来的solution虽然可以解决crash的问题，其实也是不对的。

现象当然还是pop view controller的时候会crash.

3 Because the view is the layer’s delegate, never make the view the delegate of another CALayer object. Additionally, never change the delegate of this layer object.

出处：
https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/index.html#//apple_ref/occ/instp/UIView/layer