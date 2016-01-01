# iOS 开发技术栈

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝

## Objective-C语言相关
### 基本语法
1 init
2 类方法与实例方法
3 property
4 category
5 protocol
6 load, initialize
7 import与include关键字的区别
8 MVC的基本理解
9 NSArray VS NSSet VS NSDictionary
10 NSArray VS C++ std:vector

### 内存管理
1 属性关键字(weak, strong, retain, assign)
2 ARC/MRC
3 retain cycle
4 Autorelease Pool
5 CoreFoundation与OC对象的转换

### block
1 __block关键字
2 block使用过程中的循环引用, weak_strong pattern
3 block原理
4 block在ARC和MRC下的差异

### 消息发送机制
1 objc_msgsend, IMP, SEL

### Runtime相关
1 OC对象模型
2 消息转发机制
3 动态添加、修改、删除方法，method swizzling
4 super的含义
5 category原理

## iOS开发基本知识
1 App的生命周期
2 View Controller的生命周期
(常见的问题：loadview的调用时机, viewdidunload, didReceiveMemoryWarning)
3 UIKit
a) UITableView
b) UICollectionView
c) UIViewController, UINavigationController, push和present view controllers
d) UITableViewCell的重用机制
e) UITableViewCell自适应高度
4 仅主线程操作UI

## 界面开发相关
1 UIKit(UITableView, UIScrollView)
2 界面性能优化
3 UIResponder chain
4 手势
5 HitTest
6 AutoLayout
7 Autosize Masking
8 Interface Builder
9 适配
10 LayoutSubviews调用时机，适配流程
11 drawRect与CoreGraphics
12 Layer和UIView的关系
13 CALayer相关
14 三棵树(Model Tree, Presentation Tree, Rendering Tree)
15 渲染过程

## 动画
1 动画原理
2 转场动画
3 CoreAnimation
4 关键帧动画
5 Facebook Pop库

## 多线程
1 NSThread
2 GCD
3 NSOperation
4 对于线程安全的理解
5 NSRunLoop

## 对象间通信机制
1 Target-Action
2 Delegate
3 Block
4 KVO
5 NSNotificationCenter

## 数据持久化
1 NSUserDefault
2 Plist
3 Archive
4 CoreData
5 SqLite + FMDB

## 网络请求与缓存
1 AFNetworking
2 SDWebImage
3 HTTP协议, HTTPS
4 NSURLConnection
5 NSURLSession

## 设计模式
1 代理模式
多播代理

2 观察者模式

3 单例模式

4 Command模式

5 适配器模式

6 MVC

## 代码组织与结构
MVC
MVVM
MVP
MVCS (Store)
Fat Model, Thin Model

## 性能优化与改进
1 Instruments进行渲染性能分析，离屏渲染等
2 drawRect性能

## 工具使用
1 XCode
2 Instruments
3 CocoaPods
4 Git Submodule
5 Git
6 Mou

## 编程思想与框架
1 ReactiveCocoa
2 React Native

## 应用功能扩展
1 APNS
2 定位
3 视频与音频
4 长连接
5 相机与图片处理
6 第三方登录与分享
7 IM(环信，云信)
8 转场动画

## 工程配置

## Swift
1 基本语法
2 主要思想
3 作用，异同，方向

## 规范与风格
代码规范

## 其他
64bit Suppprt