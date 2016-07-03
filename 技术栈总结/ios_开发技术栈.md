# iOS 开发技术栈

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝

## 一 Objective-C语言相关
### 基本语法
1. init
2. 类方法与实例方法
3. property: 属性描述符
4. category
5. protocol
6. load, initialize
7. import与include关键字的区别
8. MVC的基本理解
9. NSArray VS NSSet VS NSDictionary
10. NSArray VS C++ std:vector
11. dynamic
12. synthesize

### 内存管理
1 属性关键字(weak, strong, retain, assign)
2 ARC/MRC
3 retain cycle
4 Autorelease Pool
5 CoreFoundation与OC对象的转换

### KVC && KVO
1. 使用方法
2. 原理
3. 意义

### block
1. __block关键字
2. block使用过程中的循环引用, weak_strong pattern
3. block原理
4. block在ARC和MRC下的差异

### Runtime
1. OC对象模型 (isa指针，method list)
2. 消息发送机制 (objc_msgsend, IMP, SEL)
3. 消息转发机制
4. 动态添加、修改、删除方法，method swizzling
5. super的含义
6. category原理

## 二. iOS开发基本知识

1. App的生命周期
2. View Controller的生命周期
(常见的问题：loadview的调用时机, viewdidunload, didReceiveMemoryWarning)
3. UIKit
	* 基本组件：UILabel(高度计算，自适应)、UIButton(扩大点击范围)、UIImageView（拉升）、UITextField、UISegementControl等
	* UITableView: UITableViewCell的重用机制, UITableViewCell自适应高度
	* UICollectionView
	* UIScrollView
	* UIAlertView VS UIAlertController
4. UIViewController	
	* Content Controller VS Container Controller
	* UINavigationController, push和present view controllers
	* UITabbarController
5. 仅主线程操作UI
6. 应用程序图标，启动图
7. UIView transform
8. 屏幕逻辑尺寸、物理尺寸、适配基础知识、基本适配方法与单位
   (关于适配这一块，尤其要总结给设计人员看，如何给出适配图等等)
9. MVC 
10. Frame VS Bounds
11. Content Mode
12. UIControl VS UIView VS CALayer
13. 旋转处理、横屏与竖屏
14. 富文本支持(UITextView)
15. UIWebView, JSBridge, WKWebView

### 三. iOS界面开发进阶

#### xib与Storyboard
1. Interface Builder
2. 代码加载
3. segue
4. 原型cell
5. 设置约束
6. Size Classes

#### 界面适配
1. AutoLayout
2. Masonry
3. Size Classes
4. Autosize Masking

#### CALayer
1. CALayer相关介绍
2. Layer和UIView的关系
3. 三棵树(Model Tree, Presentation Tree, Rendering Tree)
4. CAShapeLayer
5. 常见应用与例子
	* 圆角
	* 边框
	* mask
	* AnchorPoint
	* transform
6. Core Animation编程指南中相关内容

#### 绘制
1. UIKit绘制: UIBezierPath
2. Core Graphics绘制: Context, 坐标系，颜色，Path, Blend Mode
3. OpenGL ES绘制
4. Core Graphics应用例子
	* 进度动画
	* 滑块控件
	* 截屏
	* 圆角
5. drawRect触发时机与注意要点(避免不不要的绘制); drawRect调用流程
6. 获取context的三个方法
	* drawRect中
	* drawLayer中（drawLayer的注意事项，即不要将UIView设置为自己的代理）
	* 创建一个Context
7. 图文混排, Core Text

#### 响应链与手势
1. UIResponder chain
2. 事件处理: UIEvent、UITouch、UIControl、UIResponer
3. 自定义点击区域: HitTest、pointInside
4. 手势: UIGestureRecognizer, 自定义手势(touchBegan, touchEnd)
5. UIView的层级

#### 布局
1. AutoLayout
2. LayoutSubviews调用时机、适配流程
3. viewDidLayoutSubviews时机
4. 布局流程

#### 性能优化
1. 常用的性能优化方法与注意点:
	* 不要在主线程有耗时操作(网络与IO要异步、NSDateFormatter等耗时对象)
	* Insturments使用(Time Profiler)
2. UI性能优化
	* Insturments使用(Core Animation)
	* FPS
	* 离屏渲染
	* Blending(避免透明图层)
	* drawRect性能
3. 渲染过程分析
4. 异步绘制

#### 常见开源自定义控件
1. Segement Control
2. 滑块控件
3. 日历控件
4. Super Demo
5. 弹出控件自定义

#### 转场与转场动画
1. 自定义转场
2. 转场动画

## 四 动画
### 1. 动画原理、时间线、三棵树
### 2. UIView动画
1. 两个Category
2. 常见的基本动画
### 3. CoreAnimation
1. 常见的基本动画
2. 显示动画、隐示动画
3. 关键帧动画（CAKeyframeAnimation）
4. 一些例子与封装
5. 过渡动画(CATransaction)
6. 动画组
7. CALayer动画 VS UIView动画
8. Custom layer，CAShapeLayer等

### 4. 常见的转场动画

### 5. Facebook Pop库
1. CADisplayLink
2. 动画引擎的设计
3. Pop应用与例子

## 五. 多线程
1. NSThread
2. GCD: 串行队列、并行队列
3. NSOperation
4. NSRunLoop
5. 对于线程安全的理解、死锁问题的解决、线程间同步的方法、读写锁

## 六. 对象间通信机制
1. Target-Action
2. Delegate
3. Block
4. KVO
5. NSNotificationCenter

## 七. 数据持久化
1. NSUserDefault
2. Plist
3. Archive
4. CoreData
5. SqLite + FMDB
6. 沙盒、文件管理
7. 备份到iCloud属性的设置(非用户数据如果备份到iCloud, 审核会被拒)
8. 缓存的设计与实现

## 八. 网络请求与缓存
1. TCP/IP
2. HTTP协议、HTTPS
3. HTTP2/SPDY、长连接
4. AFNetworking
5. NSURLConnection
6. NSURLSession
7. SDWebImage
8. 网络层设计
9. Hybrid
10. 网络性能分析与优化
11. 其他网络库与相关设计分析
12. HTTP DNS
13. 服务器接口设计与数据解析

## 九. 设计与架构

### 设计模式
1. 代理模式(多播代理)
2. 观察者模式
3. 单例模式
4. Command模式
5. 适配器模式
6. MVC

### 设计与架构
1. MVC VS MVVM VS MVP VS VIPER
2. MVCS (Store), Fat Model, Thin Model
3. 依赖注入、控制反转
4. 面向对象设计
5. 组件化方案
6. AOP

## 十. 性能优化与改进
与之前的有些重复，主要是一些总结与整理

1. Instruments进行渲染性能分析，离屏渲染等
2. drawRect性能
3. 内存使用
4. 异步绘制
5. 性能对比分析

## 十一. 常用开源库
### 常用
1. AFNetworking
2. SDWebImage
3. Mantel
4. Masonry
5. 日志收集与处理

### 编程思想与框架
1. ReactiveCocoa
2. React Native
 
### 工具库
1. YYKit: YYModel等

### 异步绘制
1. AsyncDisplayKit

### 组件库


## 十二 工具使用
### Xcode
1. 基本使用
2. 插件
3. 开发插件
4. 调试技巧与工具

### Instuments
1. memory leak
2. time profiler
3. Core Animation

### 包管理
1. CocoaPods
2. Cathage
3. Swift Pack Manager
4. Git submodule

### 代码管理
1. Git
2. SVN

### 文档
1. Markdown(MacDown或者Mou)

### 其他
1. CheatSheet


## 十三 Cocoa框架
### 音频、视频
1. 音频播放相关
	* AudioSession
	* AVAudioPlayer
	* AVPlayer
	* AudioService
2. 视频播放相关
	* MPMediaPlayer
	* AVPlayer
3. 录音
	* AVAudioRecorder
4. 视频直播
	* HLS
### 相册、相机
1. UIImagePickerController
2. AVCaptureSession(自定义相机)
3. ALAsset
4. PhotoFramework

### 地图与定位
1. MapKit
2. CoreLocation
3. Baidu SDK使用
### 运动检测
1. CoreMotion
2. HealthKit
3. CMMotionManager(摇一摇？)
### 图像处理
1. 滤镜、模糊
2. CoreImage
3. GPUImage
4. 二维码

### 通信录

## 十四 工程管理与应用发布
### 管理
1. 工程管理与组织结构
2. 代码管理
3. 单元测试
4. 单元测试覆盖率
5. 冒烟测试

### 推送
1. APNS
2. 第三方推送

### 打包与证书
1. 开发者账号
2. 证书
3. Provising file
4. 自动打包脚本
5. 编译脚本

### 热更新与动态部署
1. JSPatch
2. Wax
3. Weex
4. RN

### 发布
1. Testflight
2. APP审核与上架(IDFA, 审核注意事项)
3. 需要递交的材料与准备

### 反馈与收集
1. 应用评分
2. 反馈收集
3. 崩溃日志收集
4. 埋点
5. 活动运营

## 十五 扩展与其他
1. 第三方登录与分享
2. IM(环信，云信)， XMPP
3. MQTT(第三方推送)
4. 应用安全、逆向、iTools(PP助手)

## 十六 Swift
1. 基本语法
2. 主要思想
3. Swift VS Objective-C
4. 函数、闭包、类、Optional Chaining、元组、集合操作符
5. Swift与Objective-C混编

## 十七  规范与风格
1. 代码规范
2. 工程组织规范
3. 视觉设计规范

## 十八 算法与思路
1. 算法导论
2. LeetCode
3. 常见的解决问题与分析问题的思路

## 十九 其他
1. 64bit Support
2. HTTPS Support
3. IPv6 Support

