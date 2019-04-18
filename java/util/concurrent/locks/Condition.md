## Condition
```java
public interface Condition {
    ...
}
```

### class

- {@code Condition} factors out the {@code Object} monitor methods ({@link Object#wait() wait}, {@link Object#notify notify} and {@link Object#notifyAll notifyAll}) into distinct objects to give the effect of having multiple wait-sets per object, by combining them with the use of arbitrary {@link Lock} implementations.[👉看不懂，怎么理解好](https://github.com/SeekerandLo/Java-Annotate/issues)。当一个 Lock 代替 Synchronized 修饰的方法和语句，一个 Condition 代替 Object 的监视方法

- Conditions 也被理解成条件队列，或条件变量，提供一个意思是一个线程推迟执行(to wait)直到被其他现在状态是 true 的线程通知，因为对共享状态信息的访问发生在不同的线程中，这必须被保护，所以某种形式的锁与 condition 有关。等待条件提供的key value是自动释放关联锁，推迟/暂停(suspends)[👉有问题，提issue](https://github.com/SeekerandLo/Java-Annotate/issues)当前线程，就想 Object 的 wait()

- 一个 Condition 实例是一个 Lock 的内在的约束，获得一个 Lock 的 Condition 实例使用它的 newCondition() 方法

- 举个例子，假如有一个有限的缓冲区，支持 put() 和 take() 方法，如果试图对一个空的缓冲区使用 take() ，这个线程会阻塞直到元素可以取出，如果对一个满的缓冲区使用 put()，线程会阻塞直到空间可以使用，我们将 put 的线程和 take 的线程储存在分隔(separate) 的等待集合中以至于如果元素或空间可用，我们能够最佳的在一个时间通知一个线程，用两个 Condition 实例就能实现
    ```java
    class BoundedBuffer {
        final Lock lock = new ReentrantLock();
        final Condition notFull = lock.newCondition();
        final Condition notEmpty = lock.newCondition();

        final Object[] items = new Object[100];
        int putptr,takeptr,count;

        public void put(Object x) throws InterruptedException {
            lock.lock();
            try{
                while(count == items.length){
                    notFull.await();
                }
                items[putptr] = x;
                if(++putptr == items.length){
                    putptr = 0;
                }
                ++count;
                notEmpty.signal();
            } finally {
                lock.unlock();
            }
        }

        public Object take() throws InterruptedException {
            lock.lock();
            try{
                while(count == 0){
                    notEmpty.await();
                }
                Object x = items[takeptr];
                if(++putptr == items.length){
                    takeptr = 0;
                }
                --count;
                notFull.signal();
            } finally {
                lock.unlock();
            }
        }

    }
    ```
- 