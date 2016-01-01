# 博客阅读 之 iOS网络请求

## 第一部分
### 1 AFNetworking 2.0

文章标题:
AFNetworking 2.0

文章链接：
http://nshipster.cn/afnetworking-2/

主要内容:
AFNetworking是应用最为广泛的iOS网络库之一；
本文由AFNetworking的作者所写，主要介绍了AFNetworking 2.0相对于1.x的改变， AFNetworking的设计思路, 对于NSURLSession的支持等等;

Keypoints:
1 同时支持NSURLConnection和NSURLSession
2 与AFNetworking 1.x对比可以发现，做了很多模块化的工作，将序列化、监视网络状态等切分成单独的类来实现，从而实现解耦，使用起来会更便捷，核心功能模块AFHTTPOperationManager比原有的AFHttpClient更简洁干净;

### 2 NSURL Cache

文章标题:
NSURL Cache

文章链接:
http://nshipster.cn/nsurlcache/

主要内容:
介绍了NSURLCache的一般机制、HTTP提供的缓存语义、不同的CachePolicy的含义等；并且给出了应用HTTP默认提供的Cache的方法;

Keypoints:
1 尽量使用HTTP协议提供的Cache, 并且设置合适的Cache策略；一般设置默认的Cache策略即可.
2 要使用HTTP协议的Cache, 服务器需要做一些支持;
3 推荐的Cache使用模式是：在服务器支持下使用NSURLConnection以及HTTP协议默认提供的Cache机制；在application:didFinishLaunchingWithOptions:中正确的设置一个共享的URL Cache

其他相关链接：
https://github.com/steipete/SDURLCache
在这个链接中，实现了一个自己的NSURLCache子类，但是从作者的描述来看，已经不再需要自己实现NSURLCache子类了，只需要使用系统默认的即可.

## 第二部分 HTTPS相关

初学iOS的时候，我错误的认为对于HTTPS请求不需要额外处理的，后来才知道是因为我们一般使用的第三方库，无论是ASIHttpRequest, AFNetworking还是MKNetworkKit等等，都对HTTPS做了封装，所以我们不需要额外处理。
但是如果自己使用NSURLConnection来做的话，还是需要了解并熟悉其中的步骤。

更多相关问题，推荐直接查阅AFNetworking里面处理认证的代码，提供了不同的机制来处理HTTPS，包括忽略认证或者使用私有认证等等；核心还是与NSURLConnectionDelegate处理认证的三个代理方法

	– connection:canAuthenticateAgainstProtectionSpace:
	– connection:didReceiveAuthenticationChallenge:
	- connection:didCancelAuthenticationChallenge:

看AFNetworking源代码的好处是对于NSURLSession相关的HTTPS的处理也有
	
下面列出一些相关的文章.

### 1 使用NSURLConnection请求HTTPS(SSL)接口

文章标题：
使用NSURLConnection请求HTTPS(SSL)接口

文章链接：
http://danielxu.github.io/blog/2013/01/10/connection-https-ssl-with-nsurlconnection/

主要内容：
介绍了使用NSURLConnection请求HTTPS的常用流程； 主要涉及到NSURLConnectionDelegate处理认证的三个代理方法

Keypoints:
这篇文章其实相对简单，其实意义也不是太大，但是至少可以了解常见的处理SSL的两种方法，一个是“接收任何证书”，一个是"使用私有证书验证".


### 2 打造安全的App！iOS安全系列之 HTTPS

文章链接：
http://www.cocoachina.com/ios/20150810/12947.html

具体内容： TODO

### 3 Making HTTP and HTTPS Requests

文章链接：

https://developer.apple.com/library/ios/documentation/NetworkingInternetWeb/Conceptual/NetworkingOverview/WorkingWithHTTPAndHTTPSRequests/WorkingWithHTTPAndHTTPSRequests.html

具体内容： TODO
