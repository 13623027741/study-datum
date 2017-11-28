##算法
**OC队列的实现 -- 先进先出**

.h

```
//是否为空
- (BOOL)isEmpty;
//数量
- (NSUInteger)count;
//入队
- (void)enqueue:(id)obj;
//出队
- (id)dequeue;
//队首
- (id)front;
```

.m 

```
@interface Queue()

@property(nonatomic,strong)NSMutableArray* arr; //队列缓存池

@end

@implementation Queue

-(NSMutableArray *)arr{
    if (!_arr) {
        _arr = [NSMutableArray array];
    }
    return _arr;
}

//是否为空
- (BOOL)isEmpty{
    
    return self.arr.count == 0 ? YES : NO;
}
//数量
- (NSUInteger)count{
    return self.arr.count;
}
//入队
- (void)enqueue:(id)obj{
    [self.arr addObject:obj];
}
//出队
- (id)dequeue{
    if (!self.arr.count) return nil;
    id obj = self.arr[0];
    [self.arr removeObjectAtIndex:0];
    return obj;
}
//队首
- (id)front{
    if (!self.arr.count) return nil;
    return self.arr[0];
}
@end

```

**OC栈实现 -- 后入先出**

.h

```

//是否为空
- (BOOL)isEmpty;
//数量
- (NSUInteger)count;
//推入
- (void)push:(id)obj;
//推出
- (id)pop;
//队首
- (id)front;


```

.m

```
@interface Stack()

@property(nonatomic,strong)NSMutableArray* arr;

@end

@implementation Stack

-(NSMutableArray *)arr{
    if (!_arr) {
        _arr = [NSMutableArray array];
    }
    return _arr;
}

//是否为空
- (BOOL)isEmpty{
    
    return self.arr.count == 0 ? YES : NO;
}
//数量
- (NSUInteger)count{
    return self.arr.count;
}
//推入
- (void)push:(id)obj{
    [self.arr addObject:obj];
}
//推出
- (id)pop{
    if (!self.arr.count) return nil;
    id obj = [self.arr lastObject];
    [self.arr removeLastObject];
    return obj;
}
//队首
- (id)front{
    if (!self.arr.count) return nil;
    return [self.arr lastObject];
}

```

##算法复杂度



