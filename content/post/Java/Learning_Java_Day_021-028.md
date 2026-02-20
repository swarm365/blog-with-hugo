+++
date = '2025-10-10T12:52:31+08:00'
title = 'Learning_Java_Day_21-28'
categories = ['tech']
tags = ['java-basics']
+++
# 集合

1. 集合主要是两组（单列集合，双列集合）
2. Collection 接口有两个重要的子接口 **`List`** **`Set`**，他们的实现子类都是单列集合
3. Map 接口的实现子类是双列集合，存放的 key-value

## Collection 接口

1. Collection 实现子类可以存放多个元素，每个元素可以是 Object
2. 有些 Collection 的实现类，可以存放重复的元素，有些不可以
3. 有些 Collection 的实现类，有些是有序的（List），有些不是有序（Set）
4. Collection 接口没有直接的实现子类，是通过它的子接口 Set 和 List 来实现的

遍历元素方式

- 使用迭代器（Iterator）

1. Iterator 对象称为迭代器，主要用于遍历 Collection 集合中的元素
2. 所有实现了 Collection 接口的集合类都有一个 iterator() 方法，用以返回一个实现了 Iterator 接口的对象，即可以返回一个迭代器
3. Iterator 仅用于遍历集合， Iterator 本身并不存放对象

- 集合增强 for

底层调用的仍是迭代器，相当于简化版的 Iterator

### List 接口

List 接口是 Collection 接口的子接口

1. List 集合类中元素有序（即添加顺序和取出顺序一致)，且可重复
2. List 集合中的每个元素都有其对应的顺序索引，即支持索引
3. List 容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素

List 集合里添加了一些根据索引来操作集合元素的方法
1. void add(int index, Object ele)：在index位置插入ele元素
2. boolean addAll(int index, Collection eles)：从index位置开始将eles中的所有元素添加进来
3. Object get(int index)：获取指定index位置的元素
4. int indexOf(Object obj)：返回obj在集合中首次出现的位置
5. int lastlndexOf(Object obj)：返回obj在当前集合中末次出现的位置
6. Object remove(int index)：移除指定index位置的元素，并返回此元素
7. Object set(int index, Object ele)：设置指定index位置的元素为ele，相当于是替换
8. List subList(int fromlndex, int tolndex)：返回从fromlndex到tolndex位置的子集合

遍历元素方式
同 collection 接口

#### ArrayList

1. ArrayList 可以存放任意类型的元素，甚至是 `null`
2. ArrayList 是由数组来实现数据存储的
3. ArrayList 基本等同于 Vector，除了 ArrayList 是线程不安全（执行效率高）。多线程情况下，不建议使用 ArrayList

底层操作
1. ArrayList 中维护了一个 Object 类型的数组 elementData、transient object[] elementData（transient表示不会被序列化）
2. 当创建 ArrayList 对象时，如果使用的是无参构造器，则初始 elementData容量为0，第1次添加，则扩容 elementData 为10，如需要再次扩容，则扩容 elementData 为1.5倍
3. 如果使用的是指定大小的构造器，则初始 elementData 容量为指定大小，如果需要扩容，则直接扩容 elementData 为1.5倍

#### Vector

1. Vector 底层也是一个对象数组，protected Object[] elementData
2. Vector 是线程同步的，即线程安全，Vector 类的操作方法带有 synchronized
3. 在开发中，需要线程同步安全时，考虑使用 Vector

#### LinkedList

1. LinkedList 实现了双向链表和双端队列
2. 可以添加任意元素（元素可以重复），包括 null
3. 线程不安全，没有实现同步

底层操作
1. LinkedList 底层维护了一个双向链表
2. LinkedList 中维护了两个属性 first 和 last 分别指向首节点和尾节点
3. 每个节点（Node对象），里面又维护了 prev、next、item 三个属性，其中通过 prev 指向前一个，通过 next 指向后一个节点，最终实现双向链表
4. LinkedList 元素的添加和删除，不是通过数组完成的，相对来说效率较高

### Set 接口

1. 无序（添加和取出的顺序不一致），没有索引
2. Set 接口的实现类的对象（Set接口对象），不允许重复元素，所以最多包含一个 null
3. Set 接口对象存放数据是无序（即添加的顺序和取出的顺序不一致）
4. 注意：取出的顺序虽然不是添加的顺序，但是固定

遍历元素方式
除不支持用索引的方式获取外（即不能用普通for循环），同 collection 接口

#### HashSet

1. 实际上是 HashMap
2. 不保证元素是有序的，取决于 hash 后，再确定索引的结果

底层操作
1. 添加一个元素时，先得到 hash 值，会转成索引值
2. 找到存储数据表 table，看这个索引位置是否已经存放元素，如果没有，直接加入；如果有，调用 equals 比较，如果相同，就放弃添加，如果不相同，则添加到最后
3. 在 Java8 中，如果一条链表的元素个数达到或超过 TREEIFY_THRESHOLD（默认是8），并且 table的大小 >= MIN_TREEIFY_CAPACITY（默认64），就会进行树化（红黑树）
4. 第一次添加时，table 数组扩容到 16，临界值（threshold）是 16 * 加载因子（loadFactor = 0.75）= 12。如果 table 数组使用到了临界值 12，就会扩容到 16 * 2 = 32，新的临界值就是 32 * 0.75 = 24，依次类推

##### LinkedHashSet

1. 是 HashSet 的子类
2. 底层是一个 LinkedHashMap，维护了一个数组 + 双向链表
3. 根据元素的 hashCode 值来决定元素的存储位置，同时使用链表维护元素的次序，这使得元素看起来是以插入顺序保存的
4. 不允许添加重复元素
5. 存入顺序和取出顺序一致，这点与 HashSet 不同

#### TreeSet

1. 当使用 无参构造器 创建 TreeSet 时，仍然是无序的

```Java
		TreeSet treeSet = new TreeSet();
		treeSet.add("ano");
		treeSet.add("tomori");
		treeSet.add("soyo");
		treeSet.add("rikki");
		treeSet.add("rana");
		System.out.println(treeSet); // 取出顺序不同于放入顺序
```

2. 若希望添加的元素，按照字符串大小来排序，可使用 TreeSet 提供的一个构造器，可以传入一个比较器 Comparator（匿名内部类重写该接口）并指定排序规则

```Java
		TreeSet treeSet = new TreeSet(new Comparator() {
			@Override
			public int compare(Object o1, Object o2) {
				return ((String)o2).compareTo((String)o1); // 从大到小排序
			}
		});
		treeSet.add("ano");
		treeSet.add("tomori");
		treeSet.add("soyo");
		treeSet.add("rikki");
		treeSet.add("rana");
		System.out.println(treeSet); // 输出[tomori, soyo, rikki, rana, ano]
```

底层操作
本质是 TreeMap

## Map 接口（JDK 8）

1. Map 与 Collection 并列存在，常用实现类有HashMap、Hashtable、Properties，用于保存具有映射关系的数据 Key-Value
2. Map 中的 key 和 value 可以是任何引用类型的数据，会封装到 HashMap$Node 对象中
3. Map 中的 key 不允许重复，原因和 HashSet 一样，前面分析过源码
4. Map 中的 value 可以重复
5. Map 的 key 可以为 null，value 也可以为 null，注意 key 为 null，只能有一个 value 为null，可以多个
6. 常用 String 类作为 Map 的 key
7. key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到对应的 value

常用方法
1. put：添加
2. remove：根据键删除映射关系
3. get：根据键获取值
4. size：获取元素个数
5. isEmpty：判断个数是否为0
6. clear：清除
7. containsKey：查找键是否存在

遍历元素方式
1. 支持所有的 collection 接口方法
2. keySet：获取所有的键

```Java
		//取出所有的key，通过key取出对应的value
		Set keySet = hashmap.keySet();
		System.out.println("-----------keySet()增强for-----------");
		for (Object key : keySet) {
			System.out.println(key + " - " + hashmap.get(key));
		}

		System.out.println("-----------keySet()迭代器-----------");
		Iterator iterator1 = keySet.iterator();
		while (iterator1.hasNext()) {
			Object key = iterator1.next();
			System.out.println(key + " - " + hashmap.get(key));
		}
```

3. values：获取所有的值

```Java
		//取出所有的values
		Collection values = hashmap.values();
		System.out.println("-----------values()增强for-----------");
		for (Object value : values) {
			System.out.println(value);
		}

		System.out.println("-----------values()迭代器-----------");
		Iterator iterator2 = values.iterator();
		while (iterator2.hasNext()) {
			Object value = iterator2.next();
			System.out.println(value);
		}
```

4. entrySet：获取所有关系 k-v

```Java
		//获取k-v
		Set entryset = h.entrySet();
		System.out.println("-----------entrySet()增强for-----------");
		for (Object obj : entryset) {
			Map.Entry map = (Map.Entry) obj;
			System.out.println(map.getKey() + " - " + map.getValue());
		}

		System.out.println("-----------entrySet()迭代器-----------");
		iterator = entryset.iterator();
		while (iterator.hasNext()) {
			Object obj = iterator.next();
			Map.Entry map = (Map.Entry) obj;
			System.out.println(map.getKey() + " - " + map.getValue());
		}
```

### HashMap

底层操作
1. HashMap 底层维护了 Node 类型的数组 table，默认为 null
2. 当创建对象时，将加载因子（loadfactor）初始化为 0.75
3. 当添加 key-val 时，通过 key 的哈希值得到在 table 的索引。然后判断该索引处是否有元素，如果没有元素直接添加。如果该索引处有元素，继续判断该元素的 key 是否和准备加入的 key 相等，如果相等，则直接替换 val；如果不相等，需要判断是树结构还是链表结构，做出相应处理。如果添加时发现容量不够，则需要扩容
4. 扩容机制同HashSet

### Hashtable

1. 存放的元素是键值对：即 K-V
2. Hashtable 的键和值都不能为 null
3. Hashtable 使用方法基本上和 HashMap 一样
4. Hashtable 是线程安全的，HashMap 是线程不安全的

底层操作
初始化大小为 11，达到临界值（11 * 0.75 = 8）后扩容到**原来的2倍再加1**（11＊2+1=23）

#### Properties

1. Properties 类继承自 Hashtable 类并且实现了 Map 接口，也是使用一种键值对的形式来保存数据
2. 使用特点和 Hashtable 类似
3. Properties 还可以用于从 xxx.properties 文件中，加载数据到 Properties 类对象并进行读取和修改
4. 说明：工作后 xxx.properties 文件通常作为配置文件，这个知识点在 IO 流举例

### TreeMap

同 TreeSet

## Collection 工具类

操作 Set、List 和 Map 等集合的工具类，提供的方法均为 static 方法

常用方法
1. reverse(List)：反转 List 中元素的顺序
2. shuffle(List)：对 List 集合元素进行随机排序
3. sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
4. sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
5. swap(List，int，int)：将指定 List 集合中的 i 处元素和 j 处元素进行交换
6. Object max(List)：根据元素的自然顺序，返回给定集合中的最大元素
7. Object max(List, Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
8. Object min(List)
9. Object min(List, Comparator)
10. int frequency(List, Object)：返回指定集合中指定元素的出现次数
11. void copy(List dest, List src)： 将 src 中的内容复制到 dest 中
12. boolean replaceAll(List list, Object oldVal, Object newVal)：使用新值替换 List 对象的所有旧值