## Iterable

```java
public interface Iterable<T> {
    ...
}
```

### class
- 实现这个接口允许一个对象成为 “for each loop” 语句的目标

#### Iterator<T> iterator()
-


#### void forEach(Consumer<? super T> action)


#### Spliterator<T> spliterator()