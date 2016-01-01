DrawRect

If you subclass UIView directly, your implementation of this method does not need to call super. However, if you are subclassing a different view class, you should call super at some point in your implementation.

Special Considerations

### 2 也就是，如果子类化一个UIImageView的话，那么基本上是无法自己去做drawRect的。

The UIImageView class is optimized to draw its images to the display. UIImageView will not call drawRect: in a subclass. If your subclass needs custom drawing code, it is recommended you use UIView as the base class.

这个也可以理解

所以如果要自己画一个UIImageView,那么应该子类化UIView.


### 1 重要：DrawRect的顺序

一定是parent view先调用drawRect; 然后是子view的drawRect一个个被调用； （非常重要；之前是由于测试代码有问题）
无论parent view的drawRect是否调用了[]super drawRect], 都是这样的顺序


### 3 如果仅仅是改变Button的文本内容，那么不会重新调用DrawRect （为什么呢？）
但是如果尝试去设置Button的背景颜色，那么drawRect会被调用；

### 4 drawRect里面去设置backgroundColor

如果在CustomButton里面去调用self.backgroundColor = [UIColor greenColor];
那么会发现这个时候是没有生效的，在里面调用setNeedsDisplay也不会生效

只有到下一个runLoop的时候去调用了setNeedsDisplay,当前的设置才会生效

### 父类和子类的setNeedsDisplay没有相互影响

也就是不存在说子类setNeedsDisplay后，父类会drawRect; 反过来也不会！

这个也可以理解！
实际上是各自绘制各自的内容；最后是一个绘制内容的叠加！
绘制过程中不涉及到渲染.





https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/

The View Drawing Cycle (下一个View绘制周期)
View drawing occurs on an as-needed basis. When a view is first shown, or when all or part of it becomes visible due to layout changes, the system asks the view to draw its contents. For views that contain custom content using UIKit or Core Graphics, the system calls the view’s drawRect: method. Your implementation of this method is responsible for drawing the view’s content into the current graphics context, which is set up by the system automatically prior to calling this method. This creates a static visual representation of your view’s content that can then be displayed on the screen.

When the actual content of your view changes, it is your responsibility to notify the system that your view needs to be redrawn. You do this by calling your view’s setNeedsDisplay or setNeedsDisplayInRect: method of the view. These methods let the system know that it should update the view during the next drawing cycle. Because it waits until the next drawing cycle to update the view, you can call these methods on multiple views to update them at the same time. (一定是下一个绘制周期，至于是否是RunLoop, 这里没有说明)

NOTE

If you are using OpenGL ES to do your drawing, you should use the GLKView class instead of subclassing UIView. For more information about how to draw using OpenGL ES, see OpenGL ES Programming Guide for iOS.

For detailed information about the view drawing cycle and the role your views have in this cycle, see View Programming Guide for iOS.

这个是View Controller Programming Guide里面的内容

The View Drawing Cycle
The UIView class uses an on-demand drawing model for presenting content. When a view first appears on the screen, the system asks it to draw its content. The system captures a snapshot of this content and uses that snapshot as the view’s visual representation. If you never change the view’s content, the view’s drawing code may never be called again. (只有真正需要重绘的时候才会被调用到) The snapshot image is reused for most operations involving the view. If you do change the content, you notify the system that the view has changed. The view then repeats the process of drawing the view and capturing a snapshot of the new results.

When the contents of your view change, you do not redraw those changes directly. (这里很重要，先标记失效，再重绘)Instead, you invalidate the view using either the setNeedsDisplay or setNeedsDisplayInRect: method. These methods tell the system that the contents of the view changed and need to be redrawn at the next opportunity. The system waits until the end of the current run loop before initiating any drawing operations. (这里明确说明了是一个run Loop; 那么一个main run loop会是多少时间呢？和帧率是对应的吗？用另一种说法就是在一个runloop的最后阶段刷新) This delay gives you a chance to invalidate multiple views, add or remove views from your hierarchy, hide views, resize views, and reposition views all at once. All of the changes you make are then reflected at the same time. (在下一个Run Loop里面这些事情都会被做掉; 这也就说明了为什么在drawRect里面去更改了背景颜色或者调用了setNeedsDisplay不会有问题)

The 'update cycle' happens at the end of the current run loop cycle.

setNeedsLayout must be called on the main thread (main runloop).
(那么也就还是在main runloop)

Note: Changing a view’s geometry does not automatically cause the system to redraw the view’s content. (这是说明了一个例外情况)The view’s contentMode property determines how changes to the view’s geometry are interpreted. Most content modes stretch or reposition the existing snapshot within the view’s boundaries and do not create a new one. For more information about how content modes affect the drawing cycle of your view, see Content Modes.
When the time comes to render your view’s content, the actual drawing process varies depending on the view and its configuration. System views typically implement private drawing methods to render their content. Those same system views often expose interfaces that you can use to configure the view’s actual appearance. For custom UIView subclasses, you typically override the drawRect: method of your view and use that method to draw your view’s content. There are also other ways to provide a view’s content, such as setting the contents of the underlying layer directly, but overriding the drawRect: method is the most common technique. (重写绘制代码)

For more information about how to draw content for custom views, see Implementing Your Drawing Code.

The View Drawing Cycle
The basic drawing model for subclasses of the UIView class involves updating content on demand. The UIView class makes the update process easier and more efficient; however, by gathering the update requests you make and delivering them to your drawing code at the most appropriate time.

When a view is first shown or when a portion of the view needs to be redrawn, iOS asks the view to draw its content by calling the view’s drawRect: method.

There are several actions that can trigger a view update:

Moving or removing another view that was partially obscuring your view
Making a previously hidden view visible again by setting its hidden property to NO
Scrolling a view off of the screen and then back onto the screen
Explicitly calling the setNeedsDisplay or setNeedsDisplayInRect: method of your view
System views are redrawn automatically. For custom views, you must override the drawRect: method and perform all your drawing inside it. Inside your drawRect: method, use the native drawing technologies to draw shapes, text, images, gradients, or any other visual content you want. The first time your view becomes visible, iOS passes a rectangle to the view’s drawRect: method that contains your view’s entire visible area. During subsequent calls, the rectangle includes only the portion of the view that actually needs to be redrawn. For maximum performance, you should redraw only affected content.

After calling your drawRect: method, the view marks itself as updated and waits for new actions to arrive and trigger another update cycle. If your view displays static content, then all you need to do is respond to changes in your view’s visibility caused by scrolling and the presence of other views.

If you want to change the contents of the view, however, you must tell your view to redraw its contents. To do this, call the setNeedsDisplay or setNeedsDisplayInRect: method to trigger an update. For example, if you were updating content several times a second, you might want to set up a timer to update your view. You might also update your view in response to user interactions or the creation of new content in your view.

Important: Do not call your view’s drawRect: method yourself. That method should be called only by code built into iOS during a screen repaint. At other times, no graphics context exists, so drawing is not possible. (Graphics contexts are explained in the next section.)




### 另外一篇相关的blog

UIView drawing cycle
What this topic is about?
Helps to understand how a view is rendered.
Redrawing controls which is inherited from UIView
Use of setNeedsDisplay: and setNeedsDisplayInRect: methods

Drawing cycle:
UIView follows an interesting drawing model called an on-demand drawing model. When a view is rendered very first time the system draws the view and its contents and take a snapshot of the view's visual representation. Until the view's content is changed the system uses the same snapshot for rendering the view. So the views drawing code will never be called again until its contents are changed. If the contents are changed then the system takes the snapshot again and use it for rendering later.

When a content of the view is changed and needs to be redrawn you can invalidate the view by calling setNeedsDisplay: or setNeedsDisplayInRect: methods. When one of these method is called, it says the system to redraw the view. Before drawing the requested view the system will wait for the current run loop to finish. This delay help us to do further changes to the view's properties or you can even add or remove views from the hierarchy and finally all the changes will get effect at the end of the current run loop.

You should override the drawRect: method in your custom UIView only if you need to perform custom drawing. An empty implementation of drawRect: method will adversely affects the performance during animation. You should not call drawRect: method directly to redraw the view. Instead you should always call setNeedsDisplay: or setNeedsDisplayInRect: methods.

setNeedsDisplay: method causes the entire rectangle of the view to be redrawn whereas setNeedsDisplayInRect: method causes the specified rectangle of the view to be redrawn.

One interesting point to note here is changing the view's geometry does not cause the system to redraw the view's content. The view's contentMode property determines how the changes to the view's geometry are interpreted. Other than UIViewContentModeRedraw, most contentMode values causes the system to just stretch or reposition the existing snapshot of the view within the view's boundaries.


Summary:
UIView follows an on-demand drawing model.
System takes a snapshot of the view and reuses it for the next time.
System will redraw the view only when its contents are changed.
To redraw the view you should not call drawRect: method directly instead you should call setNeedsDisplay: or setNeedsDisplayInRect: method.
For custom drawing you should override drawRect: method in the UIView.

核心也还是那么几点！

http://coreios.blogspot.sg/2012/05/uiview-drawing-cycle.html


### View Rendering的文章 （上次链接打不开的那篇文章的另一个地址）

http://vizlabxt.github.io/blog/2012/10/22/UIView-Rendering/

也许要先从Runloop开始说，iOS的mainRunloop是一个60fps的回调，也就是说每16.7ms会绘制一次屏幕，这个时间段内要完成view的缓冲区创建，view内容的绘制（如果重写了drawRect），这些CPU的工作。然后将这个缓冲区交给GPU渲染，这个过程又包括多个view的拼接(compositing)，纹理的渲染（Texture）等，最终显示在屏幕上。因此，如果在16.7ms内完不成这些操作，比如，CPU做了太多的工作，或者view层次过于多，图片过于大，导致GPU压力太大，就会导致“卡”的现象，也就是丢帧。

苹果官方给出的最佳帧率是：60fps，也就是1帧不丢，当然这是理想中的绝佳的体验。

这个60fps改怎么理解呢？一般来说如果帧率达到25+fps，人眼就基本感觉不到停顿了，因此，如果你能让你ios程序稳定的保持在30fps已经很不错了，注意，是“稳定”在30fps，而不是，10fps，40fps，20fps这样的跳动，如果帧频不稳就会有卡的感觉。60fps真的很难达到，尤其在iphone4，4s上。

总的来说，UIView从绘制到Render的过程有如下几步：

每一个UIView都有一个layer，每一个layer都有个content，这个content指向的是一块缓存，叫做backing store。

UIView的绘制和渲染是两个过程，当UIView被绘制时，CPU执行drawRect，通过context将数据写入backing store

当backing store写完后，通过render server交给GPU去渲染，将backing store中的bitmap数据显示在屏幕上


**从这个解释就可以知道，mainRunloop和一帧是对应的！**
