# 博客阅读 之 UIKit

===============================================================================================================

## 第一部分

### 1 关于UIView的LayoutSubviews方法

文章标题：
关于UIView的LayoutSubviews方法

文章链接：
http://bachiscoding.com/blog/2014/12/15/when-will-layoutsubviews-be-invoked/

主要内容：
介绍了layoutSubviews方法的作用以及何时被调用;

Key points:
1 由系统触发调用来进行UIView的布局; 
2 优先使用自动布局(auto layout)或者autoresizing (利用autoresizingMask)来进行自动布局;
3 当auto layout或者autoresizing不能解决问题的时候，可以通过layoutSubviews来进行自动布局，在这个时候，可以进行更细致的布局操作；

补充：
在有约束时，与updateConstraints的调用顺序

 updateConstraints是从子节点往父节点依次调用；layoutSubViews是从父节点向子节点调用；
 
 执行流程：
 
	 子节点的updateconstraints  --> 父节点的 updateconstraints  --> 父节点layoutsubviews 	--> 子节点的layoutsubviews

 对于根节点且requiresConstraintBasedLayout返回为YES的调用流程:

	 父节点的layoutsubviews -->  子节点的updateconstraints  --> 父节点的 updateconstraints  --> 父节点layoutsubviews --> 子节点的layoutsubviews
	 
第一次进入父节点的layoutsubviews，孩子节点并没有根据约束计算好排版信息（因为此时孩子孩子节点的updateConstraints都还没调用）。第二次进入父节点的layoutSubviews，孩子节点的排版信息已经计算好。

子节点的layouSubviews函数调用时，他自身以及孩子节点已经根据constraints计算好了排版信息。

### 2 自定义控件

文章标题：自定义控件

文章链接：
http://objccn.io/issue-3-4/

主要内容：
objc系列文章之一；
但是感觉有点文不对题，因为实际介绍自定义控件的部分比较少；

有意义的地方在于:
1 视图层次概览，三个概念，UIResponder, UIView, UIControl; （个人看法：不要忘记了CALayer, 不过CALayer和前面三个不在同一层上，只是说到视图层次的时候，应该要联想到CALayer）
2 自定义绘制与渲染；（基本没讲什么特别的，但有两点比较重要: a 尽量避免 drawRect:，使用现有的视图构建自定义视图 b 通常最快速的渲染方法是使用图片视图）
3 谈到了5种交互方式(Target-Action, Delegate, Block, KVO, NSNotificationCenter)

渲染速度比较
OpenGL > CoreImage > Core Graphics

BTW, 另外有一篇学习文档和这个几乎一样， https://github.com/ming1016/study/wiki/UIView.

### 3 View-Layer协作

文章标题：View-Layer协作

文章链接：
http://objccn.io/issue-12-4/

相关信息：
需要了解view和layer之间的关系，相关的文章有：

(TODO: 待加上)

主要内容：
objc 系列文章之一


