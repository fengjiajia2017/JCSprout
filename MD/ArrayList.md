# ArrayList/Vector 的底层分析

## ArrayList
`ArrayList`是一个实现 `List` 接口的数组列表，底层实现为数组，允许为null、允许重复、支持随机访问
- 在数组扩容和插入新增时开销比较大（因为使用了数组拷贝）, 扩容的位置是在新增元素时（add方法）
- 默认大小为10，扩容比例为1.5倍
> 使用建议：在日常使用时最好是指定大小，尽量减少扩容。更要减少在指定位置插入数据的操作。

### ArrayList序列化
由于 ArrayList 是基于动态数组实现的，所以并不是所有的空间都被使用。因此使用了 `transient` 修饰，可以防止被自动序列化。
```java
transient Object[] elementData;
```
因此 ArrayList 自定义了序列化与反序列化：
> 当对象中自定义了 writeObject 和 readObject 方法时，JVM 会调用这两个自定义方法来实现序列化与反序列化，从实现中可以看出 ArrayList 只序列化了被使用的数据。

## Vector
`Vector` 也是实现于 `List` 接口，底层数据结构和 `ArrayList` 类似,也是一个动态数组存放数据。不过是在 `add()` 方法的时候使用 `synchronized` 进行同步写数据，但是开销较大，所以 `Vector` 是一个同步容器并不是一个并发容器。
