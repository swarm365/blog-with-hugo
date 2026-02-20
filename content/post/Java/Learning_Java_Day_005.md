+++
date = '2025-09-24T12:14:34+08:00'
title = 'Learning_Java_Day_5'
categories = ['tech']
tags = ['java-basics']
+++
# 数组

## 使用方式

1. 动态初始化

```Java
				//创建一个容量为5的int类型数组，标号0-4
				int[] a = new int[5]; // 或者 int a[]...; 两种写法等价
```
或者
```Java
				int a[];
				a = new int[10];
```

2. 静态初始化

```Java
				int a[] = {1,2,3,4,5,6,7,8};
```

数组创建后，若未赋值，默认为初始值，如 `char` 0，`boolean` false， `String` null

## 赋值机制

数组在默认情况下是 **引用传递** （地址拷贝），赋的值是 **地址** ，赋值方式为 **引用赋值** （深拷贝）

```Java
				int[] arr1 = {1,2,3};
				int[] arr2 = arr1;
				arr2[0] = 15; // arr1[0]也会同步变化为15
```

若只想复制数据的值而数据空间独立（任何一个数据变化不影响另一个数组），需要遍历数组

```Java
				int[] arr1 = {1,2,3};
				//开辟新的内存空间
				int[] arr2 = new int[arr1.length];
				//遍历
				for(int i = 0; i < arr1.length; i++){
					arr2[i] = arr1[i];
				}
```
