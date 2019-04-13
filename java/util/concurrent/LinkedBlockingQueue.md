## LinkedBlockingQueue
```java
public class LinkedBlockingQueue<E> extends AbastractQueue<E> implements BlockingQueue<E>,java.io.Serializable {
...
} 
```

### class

- 可选的有界限的阻塞队列以链表节点为基础，使用链表实现，这个队列以先进先出排列元素。队列的头部节点是在该队列中时间最长的节点，这个队列的尾巴是在该队列中时间最短的节点。新元素插入到队列的尾部，队列检索操作获取队列头部的元素。用链表实现的队列明显比用数组实现的队列有更高的吞吐量，但在大多数并发应用程序中可预测性能较差

- 可选的容量绑定构造函数参数用作防止过度队列扩展的一种方法。如果没有定义容量，则该队列的容量等于 Integer.MAX_VALUE，每次插入时都会动态创建链接节点，除非这会使队列超出容量。

- 这个类和其迭代器实现了所有 Collection 和 Iterator 接口的可选的方法[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)