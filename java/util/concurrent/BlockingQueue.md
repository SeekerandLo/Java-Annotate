## BlockingQueue

```java
public interface BlockingQueue<E> extends Queue<E>{
    ...
}
```

### class
- Queue 另外支持在检索元素时**等待队列变为非空**的操作，或者**等待存储元素时队列中可用的空间**

- BlockingQueue 的方法有四种方式，处理不能立即满足但是在未来会满足的操作
    - 抛出异常
    - 返回特殊值 `null` 或者 `false`
    - 锁住当前线程直到该操作成功
    - 当放弃的时候返回一个最大的超时时间

- BlockingQueue 不接受 null 元素。当试图 add()，put() 或者 使用poll() 方法插入一个 null 元素时会抛出异常，null 被当成 poll 操作失败的标志

- BlockingQueue 可能时容量有限的，在任意时间，都可能出现容量不足的情况，在没有 `Block` 的情况下，任意元素都不能再插入。没有内部容量限制的 BlockingQueue 在返回剩余容量时始终返回 `Integer.MAX_VALUE`

- BlocingQueue 的实现被设计成主要用于**生成者-消费者队列**，**？ 但是另外支持 Collection**，举个例子，用 remove() 方法可能从队列中移除任意的元素，然而此类方法通常效率不高，仅偶尔使用，例如到 队列消息 被取消时

- BlockingQueue 的实现时线程安全的，**所有**的方法利用内部锁或者其他并发控制方式实现原子性。然而大量的集合操作方法，除非在实现中另有规定，否则不必必须实现原子性
    >However, the bulk Collection operations {@code addAll}, {@code containsAll}, {@code retainAll} and {@code removeAll} are not necessarily performed atomically unless specified otherwise in an implementation.