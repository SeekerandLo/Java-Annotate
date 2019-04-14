### AbstractQueuedSynchronizer
```java
public abstarct class AbstractQueuedSynchronizer extends AbstractOwnableSynchronizer implements java.io.Serializable {

}
```

### class

- 提供一个框架实现阻塞锁和关联同步(信号量，事件等)，依赖于先进先出队列，这个类被设计成大多数依赖单个 int 值表示状态的同步(synchronizers)的基础，子类必须定义受保护的方法去改变状态，并定义这个状态对对象来说意味着获取还是释放[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)，有了这些，其他方法就能执行排队和阻塞机制。子类能够维持其他的状态属性，但是只有使用 getState() setState() compareAndSetState() 方法的原子性的更新是跟踪和遵守同步的