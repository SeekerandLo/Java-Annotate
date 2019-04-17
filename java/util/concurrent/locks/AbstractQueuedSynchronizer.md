### AbstractQueuedSynchronizer
```java
public abstarct class AbstractQueuedSynchronizer extends AbstractOwnableSynchronizer implements java.io.Serializable {

}
```

### class

- 提供一个实现阻塞锁和关联同步(信号量，事件等)，依赖于先进先出队列的框架，这个类被设计成大多数依赖单个 int 值表示状态的同步(synchronizers)的基础，子类必须定义受保护的方法去改变状态，并定义这个状态对对象来说意味着获取还是释放[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)，有了这些，其他方法就能执行排队和阻塞机制。子类能够维持其他的状态属性，但是只有使用 getState()，setState()，compareAndSetState() 方法的**原子性**的更新是跟踪和遵守同步的



***
### Node
```java
static final class Node {
    ...
}
```
- 这是AbstractQueuedSynchronizer的内部类，等待队列节点类

### class

### property
- SHARED = new Node() 指示节点正在共享模式下的标志
- EXCLUSIVE = null 指示节点正在独占模式下的标志
- CANCELLED =1 **waitStatus**的值表示线程已经取消了
- SIGNAL = -1 **waitStatus**的值表示后继线程需要不停止(uparking)[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)
- PROPAGATE = -3 **waitStatus**的值表示下一个**acquireShared** [AQS]()无条件传播

- volatile int waitStatus
    - 状态值，只有以下的5个值
    - SIGNAL：这个节点的后继节点或即将是后继的节点是阻塞的状态，所以当前节点必须在释放和取消时取消对其后继节点的存储(取消存储，unpack)，为了避免竞争，[acquire]() 方法必须首先声明他们需要一个 SINGAL，重试原子获取，如果失败，锁住
    - CANCELLED：由于中断或者取消，节点不再离开此状态，换言之，节点永久处于取消状态，特别的是，具有取消状态的节点不会再阻塞
    - CONDITION：此节点当前处于条件队列中，不会用作同步节点，直到转移的时候，此时该状态将设置为0，(使用这个值与其他用途无关，但是可以简化一些东西)
    - PROPAGATE：
    - 0：

- volatile Node prev

- volatile Node next

- volatile Thread thread

- Node nextWaiter