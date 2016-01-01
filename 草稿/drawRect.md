# DrawRect相关资料与链接

## 1 The View Drawing Cycle 

### https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/WindowsandViews/WindowsandViews.html

The View Drawing Cycle
The UIView class uses an on-demand drawing model for presenting content. When a view first appears on the screen, the system asks it to draw its content. The system captures a snapshot of this content and uses that snapshot as the view’s visual representation. If you never change the view’s content, the view’s drawing code may never be called again. The snapshot image is reused for most operations involving the view. If you do change the content, you notify the system that the view has changed. The view then repeats the process of drawing the view and capturing a snapshot of the new results.

When the contents of your view change, you do not redraw those changes directly. Instead, you invalidate the view using either the setNeedsDisplay or setNeedsDisplayInRect: method. These methods tell the system that the contents of the view changed and need to be redrawn at the next opportunity. The system waits until the end of the current run loop before initiating any drawing operations. This delay gives you a chance to invalidate multiple views, add or remove views from your hierarchy, hide views, resize views, and reposition views all at once. All of the changes you make are then reflected at the same time.

Note: Changing a view’s geometry does not automatically cause the system to redraw the view’s content. The view’s contentMode property determines how changes to the view’s geometry are interpreted. Most content modes stretch or reposition the existing snapshot within the view’s boundaries and do not create a new one. For more information about how content modes affect the drawing cycle of your view, see Content Modes.
When the time comes to render your view’s content, the actual drawing process varies depending on the view and its configuration. System views typically implement private drawing methods to render their content. Those same system views often expose interfaces that you can use to configure the view’s actual appearance. For custom UIView subclasses, you typically override the drawRect: method of your view and use that method to draw your view’s content. There are also other ways to provide a view’s content, such as setting the contents of the underlying layer directly, but overriding the drawRect: method is the most common technique.

For more information about how to draw content for custom views, see Implementing Your Drawing Code.

## 2 Implementing Your Drawing Code 

### https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingViews/CreatingViews.html#//apple_ref/doc/uid/TP40009503-CH5-SW3

Implementing Your Drawing Code
For views that need to do custom drawing, you need to override the drawRect: method and do your drawing there. Custom drawing is recommended only as a last resort. In general, if you can use other views to present your content, that is preferred.

The implementation of your drawRect: method should do exactly one thing: draw your content. This method is not the place to be updating your application’s data structures or performing any tasks not related to drawing. It should configure the drawing environment, draw your content, and exit as quickly as possible. And if your drawRect: method might be called frequently, you should do everything you can to optimize your drawing code and draw as little as possible each time the method is called.

Before calling your view’s drawRect: method, UIKit configures the basic drawing environment for your view. Specifically, it creates a graphics context and adjusts the coordinate system and clipping region to match the coordinate system and visible bounds of your view. Thus, by the time your drawRect: method is called, you can begin drawing your content using native drawing technologies such as UIKit and Core Graphics. You can get a pointer to the current graphics context using the UIGraphicsGetCurrentContext function.

Important: The current graphics context is valid only for the duration of one call to your view’s drawRect: method. UIKit might create a different graphics context for each subsequent call to this method, so you should not try to cache the object and use it later.


## 3 The View Drawing Cycle

### https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/

The View Drawing Cycle
View drawing occurs on an as-needed basis. When a view is first shown, or when all or part of it becomes visible due to layout changes, the system asks the view to draw its contents. For views that contain custom content using UIKit or Core Graphics, the system calls the view’s drawRect: method. Your implementation of this method is responsible for drawing the view’s content into the current graphics context, which is set up by the system automatically prior to calling this method. This creates a static visual representation of your view’s content that can then be displayed on the screen.

When the actual content of your view changes, it is your responsibility to notify the system that your view needs to be redrawn. You do this by calling your view’s setNeedsDisplay or setNeedsDisplayInRect: method of the view. These methods let the system know that it should update the view during the next drawing cycle. Because it waits until the next drawing cycle to update the view, you can call these methods on multiple views to update them at the same time.

NOTE

If you are using OpenGL ES to do your drawing, you should use the GLKView class instead of subclassing UIView. For more information about how to draw using OpenGL ES, see OpenGL ES Programming Guide for iOS.

For detailed information about the view drawing cycle and the role your views have in this cycle, see View Programming Guide for iOS.


## 4 The View Drawing Cycle

### https://developer.apple.com/library/ios/documentation/2DDrawing/Conceptual/DrawingPrintingiOS/GraphicsDrawingOverview/GraphicsDrawingOverview.html

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

## The Runtime Interaction Model for Views

https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/WindowsandViews/WindowsandViews.html#//apple_ref/doc/uid/TP40009503-CH2-SW9

The following steps break the event sequence in Figure 1-7 down even further and explain what happens at each stage and how you might want your application to react in response.

1 The user touches the screen.
2 The hardware reports the touch event to the UIKit framework.
The UIKit framework packages the touch into a UIEvent object and dispatches it to the appropriate view. (For a detailed explanation of how UIKit delivers events to your views, see Event Handling Guide for iOS.)
The event-handling code of your view responds to the event. For example, your code might:
Change the properties (frame, bounds, alpha, and so on) of the view or its subviews.
Call the setNeedsLayout method to mark the view (or its subviews) as needing a layout update.
Call the setNeedsDisplay or setNeedsDisplayInRect: method to mark the view (or its subviews) as needing to be redrawn.
Notify a controller about changes to some piece of data.
Of course, it is up to you to decide which of these things the view should do and which methods it should call.
If the geometry of a view changed for any reason, UIKit updates its subviews according to the following rules:
If you have configured autoresizing rules for your views, UIKit adjusts each view according to those rules. For more information about how autoresizing rules work, see Handling Layout Changes Automatically Using Autoresizing Rules.
If the view implements the layoutSubviews method, UIKit calls it.
You can override this method in your custom views and use it to adjust the position and size of any subviews. For example, a view that provides a large scrollable area would need to use several subviews as “tiles” rather than create one large view, which is not likely to fit in memory anyway. In its implementation of this method, the view would hide any subviews that are now offscreen or reposition them and use them to draw newly exposed content. As part of this process, the view’s layout code can also invalidate any views that need to be redrawn.

If any part of any view was marked as needing to be redrawn, UIKit asks the view to redraw itself.
For custom views that explicitly define a drawRect: method, UIKit calls that method. Your implementation of this method should redraw the specified area of the view as quickly as possible and nothing else. Do not make additional layout changes at this point and do not make other changes to your application’s data model. The purpose of this method is to update the visual content of your view.

Standard system views typically do not implement a drawRect: method but instead manage their drawing at this time.

Any updated views are composited with the rest of the application’s visible content and sent to the graphics hardware for display.
The graphics hardware transfers the rendered content to the screen.

## 5 别人的理解权作参考

### 5.1 https://github.com/immoose/Note/blob/master/ios5ptl/ch6.md

View Drawing versus View Layout

UIView分离了layout("rearranging") of subviews和drawing("display")，这是因为layout往往比drawing更cheaper

UIView caches drawing onto GPU-optimized bitmaps
setNeedsDisplay标记UIView为"dirty"，并且在下一个drawing cycle中re-draw

当屏幕方向改变或者scroll的时候，UIView的subviews需要rearrange，UIKit会调用setNeedsLayout
这会调用layoutSubviews。Override layoutSubviews会使rotation和scroll变得更流畅，可以只rearrange subviews而不draw them

IOS在run loop中获取所有的drawing request，一次性地draw them


### 5.2 http://www.jianshu.com/p/438bcf8e3e53

- (void)setNeedsDisplay：在receiver标上一个需要被重新绘图的标记，在下一个draw周期自动重绘，iphone device的刷新频率是60hz，也就是1/60秒后重绘；


### 5.3 http://my.oschina.net/megan/blog/143027

二、drawRect在以下情况下会被调用：

1、如果在UIView初始化时没有设置rect大小，将直接导致drawRect不被自动调用。drawRect 掉用是在Controller->loadView, Controller->viewDidLoad 两方法之后掉用的.所以不用担心在 控制器中,这些View的drawRect就开始画了.这样可以在控制器中设置一些值给View(如果这些View draw的时候需要用到某些变量 值).

2、该方法在调用sizeToFit后被调用，所以可以先调用sizeToFit计算出size。然后系统自动调用drawRect:方法。

sizeToFit会自动调用sizeThatFits方法；

sizeToFit不应该在子类中被重写，应该重写sizeThatFits

sizeThatFits传入的参数是receiver当前的size，返回一个适合的size

sizeToFit可以被手动直接调用

sizeToFit和sizeThatFits方法都没有递归，对subviews也不负责，只负责自己

3、通过设置contentMode属性值为UIViewContentModeRedraw。那么将在每次设置或更改frame的时候自动调用drawRect:。

4、直接调用setNeedsDisplay，或者setNeedsDisplayInRect:触发drawRect:，但是有个前提条件是rect不能为0。

-setNeedsDisplay方法：标记为需要重绘，异步调用drawRect

-setNeedsDisplayInRect:(CGRect)invalidRect方法：标记为需要局部重绘

以上1,2推荐；而3,4不提倡

 

drawRect方法使用注意点：

1、 若使用UIView绘图，只能在drawRect：方法中获取相应的contextRef并绘图。如果在其他方法中获取将获取到一个invalidate 的ref并且不能用于画图。drawRect：方法不能手动显示调用，必须通过调用setNeedsDisplay 或 者 setNeedsDisplayInRect，让系统自动调该方法。

2、若使用calayer绘图，只能在drawInContext: 中（类似鱼drawRect）绘制，或者在delegate中的相应方法绘制。同样也是调用setNeedDisplay等间接调用以上方法

3、若要实时画图，不能使用gestureRecognizer，只能使用touchbegan等方法来掉用setNeedsDisplay实时刷新屏幕 


**UIImageView的子类不能重写drawRect**


### 5.4 http://nezha.gitbooks.io/ios-developmentarticles/content/UIView%E7%9A%84drawRect%E9%87%8D%E7%BB%98.html

**永远不要去调用drawRect,因为drawRect不是让你调用的，而是系统会去调用的**

问1：由UIImageView派生出的类，为什么在drawRect中，无法绘制矩形？但如果从UIView派出就可以？

答：苹果的官方文档说了， UIImageView是专门为显示图片做的控件，用了最优显示技术，是不让调用darwrect方法， 要调用这个方法，只能从uiview里重写。

问2：在ios开发中 ，为什么自定义UIView 重写drawRect方法之后，绘图区域之外为黑，合理的情况是，我没有绘制或者填充的区域应该是透明的才对啊，如果我希望没有绘制的地方为 透明 该如何做？

答：self.backgroundColor = [UIColor clearColor]; 并记得 [super drawRect];



