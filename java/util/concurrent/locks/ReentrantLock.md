## ReentrantLock
```java
public class ReentrantLock implements Lock,Serializable{
    ...
}
```

### class

- 一个可重入的相互的排斥锁与用 synchronized 实现的方法和语句基本行为和语义是相同的，但具有扩展能力

- 可重入锁由上个成功锁定且尚未解锁的线程获得。当锁不属于另一个线程时，调用锁的线程将返回并成功获取锁。当当前线程获取锁后，这个方法会立即返回。这能通过 isHeldByCurrentThread() 和 getHoldCount()方法进行检查

- 此类的构造函数接收可选的公平性参数，如果设置为 true，则在争用情况下，锁更倾向于给等待时间最长的线程，否则无法保证公平性。使用多线程访问的公平锁的程序看起来比使用默认设置的程序吞吐量底，**但在获得锁的时间上有较小的差异并保证饥饿**[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)，但是请注意，锁的公平性并不能保证线程调度的公平性，因此，使用公平锁的多个线程中的一个可能连续多次获得锁，而其他线程没有动作没有获得锁

- 也要注意不计时的方法 tryLock() 没有使用公平的设置，如果锁可用，即使其他线程正在等待，它也会成功

- 建议在使用了 lock 后立即写一个 try 块
```java
class X {
  private final ReentrantLock lock = neReentrantLock();
  // ...
  public void m() {
    lock.lock();  // block until condition holds
    try {
      // ... method body
    } finally {
      lock.unlock()
    }
  }
}
```

- 除了实现 Lock 的接口，此类定义了许多用于检查锁的状态的 public 方法和 protected 方法，其中一些方法仅用于**使用**(**instrumentation**)和监控[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)

- 此类的序列化与内置锁的行为方式相同：反序列化锁处于未锁定状态，与序列化时的状态无关。

- 该锁支持同一线程最多 2147483647 个**递归锁**[👉有问题，点击提issue](https://github.com/SeekerandLo/Java-Annotate/issues)。尝试超过此限制会导致 error 从锁方法抛出

***
[有问题，点击提issue](https://github.com/SeekerandLo/Java-Annotate/issues/new)
***
