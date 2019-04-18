### AbstractQueuedSynchronizer
```java
public abstarct class AbstractQueuedSynchronizer extends AbstractOwnableSynchronizer implements java.io.Serializable {
    ...
    static final class Node{
        ...
    }
    ...
    public class ConditionObject implements Condition, java.io.Serializable {
        ...
    }
    ...
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
    - PROPAGATE：分享状态(RealeasShared)应该被分享到其他节点，这是仅对头节点为了确保传播继续的设置，即使其他操作已经干预。
    - 0：在他之上没有节点
    - 这些值用数字表示使用起来是非常简单的，非负数的值表示节点不需要去标志，所以大多数代码不需要去检查特定的值，仅仅为了标记
    - 普通 Sync 节点的这个值初始化为0，[Condition]() 节点初始化为 CONDITION，它是用 [CAS]() 修改的，(or when possible, unconditional volatile writes)。[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)

- volatile Node prev
    - 链接到当前线程/节点依赖的的前一个节点，为了检查 waitStatus。在排队过程中分配，只有在出列的时候才为空(为了[GC]())。

- volatile Node next

- volatile Thread thread
    - 入队节点的线程，创造时创建，使用完后取消
    - 链接到下一个等待条件的节点，或者一个特殊的value——SHARED(该内部类的一个属性)，因为条件队列只能在独享状态下才能被访问，我们仅仅需要一个简单的链表去保存节点，当他们在等待条件时。然后他们会被转移到该队列重新获得。但是因为条件只能被独享，我们用特殊的值表示共享状态[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)

- Node nextWaiter