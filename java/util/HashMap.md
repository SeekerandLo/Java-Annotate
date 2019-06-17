## HashMap
```java
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable {
        ...
}
```

### class

### property

- TREEIFY_THRESHOLD  
    使用树而不是列表的容器容量阈值，当向一个容器中添加一个元素时，如果数量到达了 TREEIFY_THRESHOLD 时，容器会转换为树来存储。这个值必须大于2且最小为8，为了满足再由树转化为普通容器的假设

- UNTREEIFY_THRESHOLD
    这个阈值是为非树化容器在重新改变大小时准备的，不能比 TREEIFY_THRESHOLD 大，最多是6，去匹配[拆除时的收缩检测]()