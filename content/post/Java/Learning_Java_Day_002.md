+++
date = '2025-09-21T21:52:22+08:00'
title = 'Learning_Java_Day_2'
categories = ['tech']
tags = ['java-basics']
+++
# 算术运算符

```Java
				int i = 1;
				i = i++;
				System.out.println(i); // 输出 1
```

解释说明

第 2 行代码执行时分 3 步
1. 将 `i` 的值 (第 `1` 行的 `i = 1`) 放入内存中的临时变量 `temp` ，**temp = i**
2. 自增 **i = i + 1** ，此时 `i` 的值为 `2`
3. 将临时变量 `temp`的值重新赋给 `i` (第 `2` 行中左侧的 `i` ) ，**i = temp**

补充： **`++i`** 规则 将上述过程的前 2 步对调

# 逻辑运算符

`&` 逻辑与 `&&` 短路与 之间的区别

```Java
				//对于 & 逻辑与而言，如果第一个条件为 false ，后面的条件仍然会判断
				int a = 3;
				int b = 7;
				if(a < 1 & ++b < 50) {
					System.out.println("ok300");
				}
				System.out.println("a= " + a + " b= " + b); // 3 8
```

```Java
				//对于 && 短路与而言，如果第一个条件为 false ，后面的条件不再判断
				int a = 3;
				int b = 7;
				if(a < 1 & ++b < 50) {
					System.out.println("ok300");
				}
				System.out.println("a= " + a + " b= " + b); // 3 7
```

`|` 逻辑或 `||` 短路或 同理

开发中通常用 **`&&` 短路与** 和 **`||` 短路或**，效率高

补充： `^` 逻辑异或

# 赋值运算符

```Java
				//复合赋值运算符会自动类型转换
				byte a = 37;
				a++; // 等价于 a = (byte) a + 1;
				a += 2; // 等价于 a = (byte) a + 2;
```

# 三元运算符

```Java
				int dingZhen = 15;
				int wangYuan = 0;
				String ans = dingZhen > wangYuan ? "维新派" : "传统派";
				System.out.println(ans); // 输出维新派
```

