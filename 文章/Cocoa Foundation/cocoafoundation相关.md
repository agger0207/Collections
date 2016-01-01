# 文章阅读之CocoaFoundation相关

## 第一部分

### 1 NSCache

文章标题：
NSCache

文章链接：

南峰子的技术博客
http://southpeak.github.io/blog/2015/02/11/nscache/

作者：
南峰子

主要内容：
介绍了NSCache的特点与用法，包括缓存限制，存取方法, NSDiscardableContent协议等；

要点：
**1 如果我们需要构建缓存机制，则应该使用NSCache，而不是NSDictionary**;
原因是：Apple对NSCache做了优化，保证NSCache是线程安全的，而且对内存使用会有优化；

2 NSCache是线程安全的；

3 NSCache类结合了各种自动删除策略，从而确保不会占用过多的系统内存；

4 NSCache提供了接口来限制最大内存数和可以存储的条目；

5 缺点：NSCache没有提供遍历的接口来遍历所有的缓存记录并找到需要的记录；也就说，如果没有key的话，是找不到符合条件的object的

6 NSCache不会拷贝key对象.