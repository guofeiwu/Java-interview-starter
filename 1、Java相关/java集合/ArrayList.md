# Java 集合

- List 
> 一、List继承于Collection接口。常用的实现类：ArrayList，LinkedList，Vector。
>
> 二、List允许存放重复的值，任意多个，包括null值，并且List是一个有序的集合，可以通过下标来进行访问。
>
> 三、ArrayList底层是一个Object类型的数组，初始化容量为10，查找快，数组是可以直接按索引查找；增删慢，在增和删的时候会牵扯到数组增容, 以及拷贝元素；非线程安全。
>
> ```java
> private void grow(int minCapacity) { 
>         // overflow-conscious code
>         int oldCapacity = elementData.length;
>    int newCapacity = oldCapacity + (oldCapacity >> 1);
>         if (newCapacity - minCapacity < 0)
>             newCapacity = minCapacity;
>         if (newCapacity - MAX_ARRAY_SIZE > 0)
>             newCapacity = hugeCapacity(minCapacity);
>     // minCapacity is usually close to size, 
>     //so this is a win:
> elementData = Arrays.copyOf(elementData, newCapacity);
>     }
> ```
>
> 四、扩容方式： JDK1.8  newCapacity为原来数组实际长度加上原来数组实际长度的一半，也就是1.5 倍的oldCapacity；
>
> 五、LinkedList 底层是链表，链表的增删快，查询慢；
>
> ```java
> private void grow(int minCapacity) {
>         // overflow-conscious code
>         int oldCapacity = elementData.length;
>         int newCapacity = oldCapacity + ((capacityIncrement > 0) ?                  capacityIncrement : oldCapacity);
>         if (newCapacity - minCapacity < 0)
>             newCapacity = minCapacity;
>         if (newCapacity - MAX_ARRAY_SIZE > 0)
>             newCapacity = hugeCapacity(minCapacity);
> elementData = Arrays.copyOf(elementData, newCapacity);
>     }
> ```
>
> 六、Vector与 ArrayList原理相同, 但线程安全, 效率略低 ；初始化容量为10，扩容方式分为两种情况：Vector 当扩容容量增量大于0时、新数组长度为原数组长度+扩容容量增量 ，扩容容量增量不大于0则为2倍的当前数组实际元素长度。


- Set 

> 一、Set继承于Collection接口，常用的实现类：HashSet，LinkedHashSet，TreeSet。
>
> 二、Set中不允许重复元素存在，即使插入相同元素也会进行替换，存储的元素是无序的，不能通过下表进行访问。
>
> 三、HashSet的底层是HashMap。default initial capacity (16) and load factor (0.75).
>
> 四、LinkedHashSet继承于HashSet，集合是有序的。
>
> 五、TreeSet存放的是TreeMap。


- Map

> 一、它有四个实现类,分别是 HashMap Hashtable LinkedHashMap 和TreeMap，ConcurrentHashMap 。
>
> 二、Map主要用于存储健值对，根据键得到值，因此不允许键重复(重复了覆盖了),但允许值重复。
>
> 三、HashMap 是一个最常用的Map,它根据键的HashCode值存储数据,根据键可以直接获取它的值，具有很快的访问速度，遍历时，取得数据的顺序是完全随机的。 HashMap最多只允许一条记录的键为Null;允许多条记录的值为 Null;HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap（非线程安全）;可能会导致数据的不一致。如果需要同步，可以用 Collections的synchronizedMap方法使HashMap具有同步的能力，或者使用ConcurrentHashMap。
>
> 四、Hashtable(初始容量11)（Vector 10）与 HashMap(初始容量16)类似,它继承自Dictionary类和实现Map接口，不同的是:它不允许记录的键或者值为空;它支持线程的同步（线程安全），即任一时刻只有一个线程能写Hashtable,因此也导致了 Hashtable在写入时会比较慢。
>
> 五、LinkedHashMap 是HashMap的一个子类，保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的.也可以在构造时用带参数，按照应用次数排序。在遍历的时候会比HashMap慢，不过有种情况例外，当HashMap容量很大，实际数据较少时，遍历起来可能会比 LinkedHashMap 慢，因为LinkedHashMap的遍历速度只和实际数据有关，和容量无关，而HashMap的遍历速度和他的容量有关。TreeMap实现SortMap接口，能够把它保存的记录根据键排序,默认是按键值的升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。
>
> 六、一般情况下，我们用的最多的是HashMap,在Map 中插入、删除和定位元素，HashMap 是最好的选择。但如果您要按自然顺序或自定义顺序遍历键，那么TreeMap会更好。如果需要输出的顺序和输入的相同,那么用LinkedHashMap 可以实现,它还可以按读取顺序来排列。
>
> 七、HashMap是一个最常用的Map，它根据键的hashCode值存储数据，根据键可以直接获取它的值，具有很快的访问速度。HashMap最多只允许一条记录的键为NULL，允许多条记录的值为NULL。
>
> 八、HashMap不支持线程同步，即任一时刻可以有多个线程同时写HashMap，可能会导致数据的不一致性。如果需要同步，可以用Collections的synchronizedMap方法使HashMap具有同步的能力。
>
> 九、 HashMap存放在数组（链表、红黑数）中、通过hash算法计算出数组的下标，然后放到对应的位置，若对应的位置有元素，则通过equal方法进行比较，判断里面的内容是否是一样的、如果是一样的则替换，若不一样则形成一个链表。在数组的内容达到默认的加载因子（0.75）的时候就自动进行扩容，但是如果形成的列表的长度越长查询效率会变的很低，所以java8引入了红色树（二叉树的一种），这样除了插入其他的效率提高了很多。
>
> 十、Node<K,V>[] 数组，若数组会空怎么使用时会创建大小是16的Node数组，用15 & key的hash值获取当前key的下标若所在下标不存在数据，则生成一个新Node。若有数据则分三种情况：
> 一、去判断hash值，key，value是不是都一致，若hash值，key，value都一致则表示是条相同的数据，最后直接返回旧值。
> 二、是不是树。
> 三、单链表，查找有没有hash，key，value都一样的数据，若有直接返回旧值，若没有则将其加到该单链表的最后，当单链表的长度大于等于8之后转化为树。
>
> 十一、ConcurrentHashMap 是用于并发情况，使用了CAS无锁算法，线程安全。

