# SuperDemo说明

AnimationViewController中：关于animationType的类型问题

可以参考：
http://www.cnblogs.com/wyqfighting/p/3204844.html

3、本来没什么疑问，看到这个说明后，反而觉得奇怪，如果type只有这么几个类型，那cube、page等都是在哪实现的了？

  cube等效果都不是它公开的方法，而是它提供的私有类型。

复制代码
animation.type = @"cube" ;  //立方体翻转
animation.type = @"suckEffect";   //收缩效果，如一块布被抽走  
animation.type = @"oglFlip";//上下翻转效果,不管subType is "fromLeft" or "fromRight",official只有一种效果   
animation.type = @"rippleEffect";   //滴水效果
animation.type = @"pageCurl";   //向上翻一页
animation.type = @"pageUnCurl"  //向下翻一页
animation.type = @"cameraIrisHollowOpen ";  //类似于ios的相机打开时的效果
animation.type = @"cameraIrisHollowClose ";  //类似于ios的相机关闭时的效果

不过根据

https://discussions.apple.com/message/7587837#7587837说明，可能会被拒？这个不管，改天做个实际的尝试！


然后也可以再尝试一下现在Apple官方支持的自定义转场动画的方式，微信公众订阅号中存在相关内容.

另外也可以参考：
[IOS动画之CoreAnimation](http://scottmaxiao.github.io/IOS%E5%8A%A8%E7%94%BB%E4%B9%8BCoreAnimation.html)
[CALayer&CoreAnimation](http://lucifer1988.github.io/blog/2015/11/09/calayer-and-coreanimation/)

这里面相对基础而全面.