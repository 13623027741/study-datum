###iOS - NSTimer释放问题深入分析

NSTimer是一个事件，如果想要运行需要添加到runloop上，我们在平常使用NSTimer类方法

```
[NSTimer scheduledTimerWithTimeInterval:(NSTimeInterval) target:(nonnull id) selector:(nonnull SEL) userInfo:(nullable id) repeats:(BOOL)]
```
系统已经帮我们将NSTimer事件添加到runloop中，在多线程编程指南中我们会发现所有的source如果要起作用的话就需要添加到runloop中，同样的Timer事件也需要添加到runloop中，如果一个runloop中没有任何事件或者Source的话，那么在开启runloop后也会立即退出runloop循环，我们APP的主线程runloop不需要我们添加事件和Source也能一直运行，是由于系统添加了监听UI事件和系统Source，所以我们主线程的runloop才没有退出。

通过使用上述方法创建的Timer事件，会在系统处理UI事件的时候没有响应，原因是Timer事件的runloop运行模式优先级默认低于UI事件，通常我们通过创建NSTimer对象，然后手动的设置Timer对象的runloop模式，这样就可以避免当用户触摸UI的时候Timer事件没有响应。

##销毁

当通过上述方法创建Timer事件时，Timer强引用了视图控制器，如果没有释放Timer事件，那么视图控制器的引用计数值就一直不为0，没有办法调用dealloc方法，从而造成了内存泄漏

##总结
当NSTimer事件创建后通常添加在MainRunloop中，当NSTimer强引用了当前的视图控制器的话，需要释放NSTimer事件来避免造成内存泄漏



