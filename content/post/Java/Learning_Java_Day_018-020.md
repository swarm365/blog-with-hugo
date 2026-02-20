+++
date = '2025-10-07T11:08:23+08:00'
title = 'Learning_Java_Day_18-20'
categories = ['tech']
tags = ['java-basics']
+++
# 常用类／包装类（Wrapper）

| 基本数据类型 |  包装类   |  父类  |
| :----------: | :-------: | :----: |
|   boolean    |  Boolean  |        |
|     char     | Character |        |
|     byte     |   Byte    | Number |
|    short     |   Short   | Number |
|     int      |  Integer  | Number |
|     long     |   Long    | Number |
|    float     |   Float   | Number |
|    double    |  Double   | Number |

## 包装类 和 基本数据类型 的相互转换

以 int 和 Integer 为例
1. jdk5 前的手动装箱和拆箱方式，装箱：基本类型 -> 包装类型，反之，拆箱

```Java
		//手动装箱 int -> Integer
		int n1 = 15;
		Integer integer = new Integer(n1);
		Integer integer1 = Integer.valueOf(n1);

		//手动拆箱 Integer -> int
		int i = integer.intValue();
```

2. jdk5 及以后的自动装箱和拆箱方式

```Java
		//自动装箱 int -> Integer
		int n2 = 37;
		Integer integer2 = n2;

		//自动拆箱 Integer -> int
		int n3 = integer2;
```

3. 自动装箱底层调用的是 valueOf 方法，比如 lnteger.valueOf()

```Java
		//三元运算符要视作一个整体
		Object obj = true ? new Integer(1) : new Double(5.0);
		System.out.println(obj); // 输出 1.0
```

## 包装类 和 String 类型 的相互转换

以 Integer 和 String 为例

```Java
		//包装类（Integer） -> String
		Integer i = 15; //自动装箱
		//方式1
		String str1 = i + "";
		//方式2
		String str2 = i.toString();
		//方式3
		String str3 = String.valueOf(i);

		//String -> 包装类（Integer）
		String str4 = "15";
		//方式1
		Integer n1 = Integer.parseInt(str4); // 利用自动装箱
		//方式2
		Integer n2 = new Integer(str4); // 构造器
```

## String 类

- 字符串常量对象是用双引号括起的字符序列。例如："你好"、"12.97"、"boy" 等

- 字符串的字符使用 Unicode 字符编码，一个字符（不区分字母还是汉字）占两个字节

- String 类的常用构造方法
	1. String s1 = new String();
	2. String s2 = new String(String original);
	3. String s3 = new String(char[] a);
	4. String s4 = new String(char[] a, int startIndex, int count);
	5. String s5 = new String(byte[] b);

- String 类实现了接口 Serializable（可以串行化：可以在网络传输）、接口 Comparable（ string 对象可以比较大小）
- String 是 final 类，不能被其他的类继承
- String 有属性 private final char value[]：用于存放字符串内容
- 注意：value 是一个 final 类型，不可以修改（即 value 不能指向新的地址，但是单个字符内容可以变化）

```Java
		final char[] value = {'丁', '真'};
		value[0] = '1'; // 正确，里面的内容可以更改
		value[1] = '5'; // 同上
		char[] v2 = {'王', '源'};
		// value = v2; // 报错，value指向不可更改
```

### String 对象的创建方式

- 直接赋值，`String s = "丁真";`

先从常量池查看是否有 `"丁真"` 数据空间，如果有，直接指向；如果没有则重新创建，然后指向。最终指向的是常量池的空间地址

- 调用构造器，`String s = new String("丁真");`

先在堆中创建空间，里面维护了 value 属性，指向常量池的 `"丁真"` 空间，如果常量池没有 `"丁真"` ，重新创建；如果有，直接通过 value 指向。最终指向的是堆中的空间地址

### 字符串的特性

- String 是一个 final 类，代表不可变的字符序列，字符串是不可变的
- 一个字符串对象一旦被分配，其内容是不可变的

```Java
		String s = "丁真"; // 在常量池中创建"丁真"对象
		s = "王源"; // 在常量池中重新创建"王源"对象
		//共创建了2个对象
```

```Java
		//编译器底层会做优化，将该语句等价于 String s = "理塘丁真";
		String s = "理塘" + "丁真";
		//只创建了1个对象
```

```Java
		String s1 = "理塘";
		String s2 = "丁真";
		String s3 = s1 + s2; // 在堆中创建，指向堆中的地址
		//共创建了3个对象
		/* 底层是
		StringBuilder sb = new StringBuilder();
		sb.append(a);
		sb.append(b);
		sb是在堆中，并且 append 是在原来字符串的基础上追加的
		重要规则：
		String c1 = "芙蓉" + "王源"; 常量相加，看的是池
		String c1 = a + b; 变量相加，是在堆中
		*/
```

### String 类的常见方法

#### StringBuffer

- StringBuffer 的直接父类是 AbstractStringBuilder
- StringBuffer 实现了 Serializable，即 StringBuffer 的对象可以串行化
- 在父类中 AbstractStringBuilder 有属性 char[] value ，不是~~final~~，该 value 数组存放字符串内容，引出存放在堆中的
- StringBuffer 是一个 final 类，不能被继承

常用方法
1. 增 append
2. 删 delete(start,end)
3. 改 replace(start,end,string) ，将 start----end 间的内容替换掉,不含 end
4. 查 indexof ，查找子串在字符串第1次出现的索引，如果找不到返回-1
5. 插 insert
6. 获取长度 length

#### String VS StringBuffer

- String 保存的是字符串常量，里面的值不能更改，每次 String 类的更新实际上就是更改地址，效率较低
- StringBuffer 保存的是字符串变量，里面的值可以更改，每次 StringBuffer 的更新实际上可以更新内容，不用每次更新地址（即创建新对象），效率较高，指向的是堆

#### StringBuilder

- 一个可变的字符序列。此类提供一个与 StringBuffer 兼容的 APl ，但不保证同步（不是线程安全的）。该类被设计用作 StringBuffer 的一个简易替换，用在字符串缓冲区被单个线程使用的时候。如果可能，建议优先采用该类，因为在大多数实现中，它比 StringBuffer 要快
- 在 StringBuilder 上的主要操作是 append 和 insert 方法，可重载这些方法以接受任意类型的数据

#### String、StringBuffer 和 StringBuilder 的比较

- StringBuilder 和 StringBuffer 非常类似，均代表可变的字符序列，而且方法也一样
- String：不可变字符序列，效率低，但是复用率高
- StringBuffer：可变字符序列、效率较高（增删）、线程安全
- StringBuilder：可变字符序列、效率最高、线程不安全

- String 使用注意说明：
`String s = "a";` 创建了一个字符串　
`s += “b";` 实际上原来的"a"字符串对象已经丢弃了，现在又产生了一个字符串 s+"b"（也就是"ab"）。如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大影响程序的性能。 => 结论：如果我们对 String 做大量修改，不要使用 String
