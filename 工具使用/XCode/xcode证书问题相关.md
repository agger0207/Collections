# XCode证书问题相关

## Framework编译需要Code Sign的问题

### 问题：
Framework编译，如果是arm架构（选择ios Device）的时候，会提示“**CodeSign error: code signing is required for product type 'Framework' in SDK 'iOS 8.3'**”

### 参考答案：

主要参照下面的链接中黑体的答案. (答案是问题的提出者自己总结的)

[Creating iOS/OSX Frameworks: is it necessary to codesign them before distributing to other developers?](http://stackoverflow.com/questions/30963294/creating-ios-osx-frameworks-is-it-necessary-to-codesign-them-before-distributin)

原始链接URL：
http://stackoverflow.com/questions/30963294/creating-ios-osx-frameworks-is-it-necessary-to-codesign-them-before-distributin


核心就几点：
1 Framework是一定要签名的，无论这个Framework是编译成为静态库还是动态库；（在build setting -> Link中可以设置Mach-O Type的）。这个是XCode的限制.
2 如果是Cocoa Libaray, 那么是不需要签名的；
3 Framework的签名可以随便签，使用默认的iPhone Developer就足够了；因为应用一定会重新再签名，覆盖掉Framework的签名的。

原文：
iOS

**Developer:**

Builds iOS framework for device. Codesigning is required by Xcode, "iPhone Developer" identity is enough.
Builds iOS framework for simulator.
Uses lipo that produces universal iOS framework from previous two. At this point the codesigning identity of 1 step is lost: universal framework binary "is not signed at all" but that is fine since "Consumer does not care".
Gives it to Consumer

**Consumer:**

Receives iOS framework from Developer
Copies framework to Frameworks/ directory (this step may be redundant depending on what script in step 3 is.)
Uses special script as a part of build process: this script strips simulator slices off the iOS framework and then re-codesigns it on his, Consumer's, behalf.

### 其他相关链接与讨论

上述参考答案中是有一些讨论的链接的；下面也附上一些讨论链接. 一般只需要看上面的参考答案就足够了.

1 [Document how to set up code signing for iOS and Mac frameworks](https://github.com/Carthage/Carthage/issues/399#issuecomment-86089516)

2 [RealmSwift.framework 0.92.3 on OSX: code signing problem](https://github.com/realm/realm-cocoa/issues/1998)

3 [Does my iOS 8 framework need its own code signing for distribution?](http://stackoverflow.com/questions/28731267/does-my-ios-8-framework-need-its-own-code-signing-for-distribution)

4 [深入浅出Cocoa之Framework](http://www.cocoachina.com/ios/20120516/4255.html)

5 [Xcode6 code signing required for referenced frameworks?](http://stackoverflow.com/questions/28289652/xcode6-code-signing-required-for-referenced-frameworks)

6 [iOS8 Dynamic Frameworks -> CodeSign error: code signing is required for product type 'Framework' in SDK 'iOS 8.3'](http://stackoverflow.com/questions/29836356/ios8-dynamic-frameworks-codesign-error-code-signing-is-required-for-product)