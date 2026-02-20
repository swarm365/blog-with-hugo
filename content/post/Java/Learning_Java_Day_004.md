+++
date = '2025-09-23T11:22:23+08:00'
title = 'Learning_Java_Day_4'
categories = ['tech']
tags = ['java-basics']
+++
# 循环

## switch

1. 表达式数据类型，应和 `case` 后的常量类型一致，或者是可以自动转成可以相互比较的类型，比如输入的是 字符 ，而常量是 int

```Java
				char c = 'b';
				switch(c) {
					case 'a' :
						System.out.println("a");
					case 98 :
						System.out.println("b");
				}
				//输出 b
```

2. `switch` （表达式）中表达式的返回值必须是：（ `byte` , `short` , `int` , `char` , `enum[枚举]` , `String` ），如 ~~double c = 1.1; switch(c){...}~~ 不能通过编译。不过 double c = 1.1; switch((int)c){...} 是可以的，因为表达式类型强转成了 int
3. `case` 子句中的值必须为 **常量** ，不可为变量

```Java
				char c = 'a';
				char c1 = 'b';
				switch(c) {
					case 'b' - 1 : // 允许，表达式结果为常量
						System.out.println("a");
					case c1 : // 报错，这里不能为变量
						System.out.println("b");
				}
```

## for

1. 循环初始值可以有多条初始化语句，但要求类型一样，并且中间用逗号隔开
2. 循环变量迭代也可以有多条变量迭代语句，中间用逗号隔开

```Java
				int count = 3;
				for (int i = 0,j = 0; i < count; i++, j += 2) {
					System.out.println("i= " + i + " j=" + j);
				}
```

## 编程思想 (以 for 循环为例)

Q：打印 1~100 之间所有是 9 的倍数的整数，统计个数及总和。

两个编程思想（技巧）： **化繁为简** ， **先死后活**
1. **化繁为简**：将复杂的需求，拆解成简单的需求，逐步完成
2. **先死后活**：先考虑固定的值，然后转成可以灵活变化的值

思路分析：

### 化繁为简
1. 完成输出 1-100 的值

```Java
				for(int i = 1; i <= 100; i++){
					System.out.println("i=" + i);
				}
```

2. 在输出时过滤出只有 9 的倍数

```Java
				for(int i = 1; i <= 100; i++){
					if(i % 9 == 0){
						System.out.println("i=" + i);
					}
				}
```

3. 统计个数 定义一个计数器 count ，当条件满足时 count++

```Java
				int count = 0;
				for(int i = 1; i <= 100; i++){
					if(i % 9 == 0){
						System.out.println("i=" + i);
						count++;
					}
				}
				System.out.println("count=" + count);
```

4. 统计总和 定义一个 sum，当条件满足时 sum += i

```Java
				int count = 0;
				int sum = 0;
				for(int i = 1; i <= 100; i++){
					if(i % 9 == 0){
						System.out.println("i=" + i);
						count++;
						sum += i;
					}
				}
				System.out.println("count=" + count);
				System.out.println("sum=" + sum);
```

### 先死后活
1. 为了适应更好的变化需求，把 **起始值** 与 **终值** 定为变量

```Java
				int count = 0;
				int sum = 0;
				int start = 1; // 若以后计算5-300，将start改成5即可
				int end = 100; // 若以后计算5-300，将end改成300即可
				for(int i = start; i <= end; i++){
					if(i % 9 == 0){
						System.out.println("i=" + i);
						count++;
						sum += i;
					}
				}
				System.out.println("count=" + count);
				System.out.println("sum=" + sum);
```

2. 更进一步，将 9 倍数也定为变量

```Java
				int count = 0;
				int sum = 0;
				int start = 1;
				int end = 100;
				int times = 9; // 若以后计算7的倍数，将times改成7即可
				for(int i = start; i <= end; i++){
					if(i % times == 0){
						System.out.println("i=" + i);
						count++;
						sum += i;
					}
				}
				System.out.println("count=" + count);
				System.out.println("sum=" + sum);
```

## break、continue

1. `break` 语句可以指定退出哪层
2. `label1` 是标签，名字由程序员指定
3. `break` 后指定到哪个 `label` 就退出到哪里
4. 在实际开发中，尽量不要使用标签，会导致可读性变差
5. 如果没有指定 `break` ，默认退出最近的循环体
6. `continue` 同理

```Java
			label1:
				for(int j = 0; j < 4; j++){
			label2:
					for(int i = 0; i < 10; i++){
						if(i == 2){
							break label1;
						}
						System.out.println("i = " + i); // 输出 0 1
					}
				}
```
