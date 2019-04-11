## Queue

```java
public interface Queue<E> extends Collection<E>{

}
```
### class

- Queue 是一个用来保存数据的集合，除了 Collection 接口实现的收集操作外，队列提供了额外的插入，提取，检查操作，这些方法有两种形式：一种是如果操作失败则抛出异常，一种是返回一个特殊的值，比如null，比如false，取决于什么操作。后一种形式的插入操作专门设计用于容量受限的情况设计的，大多数实现中，插入不会失败。

- Queue 是典型的但不是必要的，规定里面的元素遵循 FIFO 的原则，有例外就是 priority queues(优先队列，根据比较器或者元素的自然顺序)，以及 LIFO 队列(后进先出队列)

- 无论遵循什么，要移除队列头部的元素都要使用 remove() 或者 poll() 方法，在 FIFO 队列中，所有新插入的元素都要插入的队列的尾部，其他队列可能使用不同类型的安置规则，每个队列的实现必须指定其排队顺序  

- 关于方法的描述请看下一小节，Queue 中定义的方法

- Queue 这个接口没有定义在**并发编程**中很常见的 blocking Queue 方法，这些方法会等待元素的出现或者空间可用，定义在 BlockingQueue 接口，实现了 Queue 接口

- Queue 的实现通常不允许插入 **null** 的元素，尽管一些方法，比如 LinkedList 没有禁止这样，甚至在一些实现中还实现了这个允许了，**null** 的元素不应该被插入到 Queue 中，** null ** 也是被用作 poll() 的特殊的返回值来代表这个队列不包含元素 
    - {@code Queue} implementations generally do not define element-based versions of methods {@code equals} and {@code hashCode} but instead inherit the identity based versions from class {@code Object}, because element-based equality is not always well-defined for queues with the same elements but different ordering properties.
