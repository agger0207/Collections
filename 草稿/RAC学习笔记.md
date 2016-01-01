http://www.cocoachina.com/industry/20140609/8737.html

signal作为local变量时，如果没有被subscribe，那么方法执行完后，该变量会被dealloc。但如果signal有被subscribe，那么subscriber会持有该signal，直到signal sendCompleted或sendError时，才会解除持有关系，signal才会被dealloc。


常用的模式
 
map + switchToLatest
 
switchToLatest: 的作用是自动切换signal of signals到最后一个，比如之前的command.executionSignals就可以使用switchToLatest:。
 
map:的作用很简单，对sendNext的value做一下处理，返回一个新的值。


一般不推荐使用RACSubject，因为它过于灵活，滥用的话容易导致复杂度的增加


map + switchToLatest模式，这样就可以自动取消上一次的网络请求


RAC我自己感觉遇到的几个难点是: 1) 理解RAC的理念。 2) 熟悉常用的API。3) 针对某些特定的场景，想出比较合理的RAC处理方式






ReactiveCocoa的目的就是定义一个统一的事件处理接口，这样它们可以非常简单地进行链接、过滤和组合。




map操作使用提供的block来转换事件数据(那和flattenMap的区别呢？)


flattenMap: 在map的基础上使其flatten，也就是当Signal嵌套（一个Signal的事件是另一个Signal）的时候，会将内部Signal的事件传递给外部Signal 


RACSignal组合方法可以组合任何数量的信号，而reduce块的参数会对应每一个信号。


http://southpeak.github.io/blog/2014/08/02/reactivecocoazhi-nan-%5B%3F%5D-:xin-hao/

在这篇文章的Demo里面描述了如何将一个异步API表示为一个信号！
所以我们的工作的核心就是如何将一个异步API表示为一个信号；我是希望做一个上层的封装后再表示为信号；否则的话，RestKit底下的调用是比较难表示为信号的


创建信号

幸运的是，将一个已存在的异步API表示为一个信号相当简单。我们来看看



号的subscribeNext:块中订阅内部信号。但这会引起嵌套的麻烦。幸运的是，这是个普遍的问题，而ReactiveCocoa已经提供了解决方案。

Signal of Signals

这个问题有解决方案是直观的，只需要使用flattenMap来替换map

这里面明确提到使用flattenMap来解决信号的信号这个问题

map返回的是id; flattenMap的参数block返回的一定是一个RACStream (信号或者sequence)



http://southpeak.github.io/blog/2014/08/02/reactivecocoazhi-nan-er-:twittersou-suo-shi-li/?utm_source=tuicool

也包含了将异步请求封装为RACSiganl的例子, 可以仿照其中的代码; 然后其中的twitter的例子介绍了多个请求互相依赖的做法！


这说明了ReactiveCocoa框架的一个重要点。上面显示的操作是在信号初始发出事件时的那个线程执行。尝试在管道的其它步骤添加断点，我们会很惊奇的发现它们会运行在多个不同的线程上。

因此，我们应该如何来更新UI呢？当然ReactiveCocoa也为我们解决了这个问题。我们只需要在flattenMap:后面添加deliverOn:操作：(线程切换)

（但是错误重发这种，好像只能在外部调度，而无法在内部处理....）



TODO: YTKNetworking支持RAC, + Mantel支持对象映射, 支持Swift, 换用NSURLSession, 缓存持久化存储的方式改变