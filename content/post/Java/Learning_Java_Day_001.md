+++
date = '2025-09-20T17:36:56+08:00'
title = 'Learning_Java_Day_1'
categories = ['tech']
tags = ['java-basics']
+++
# 变量的小知识

## 整型

`byte`[1]，`short`[2]，`int`[4]，`long`[8]

Java 中默认整型常量为 **int** 型，如果要声明为 **long** 型，需要在数尾 + "**l**" 或 "**L**"

## 浮点型

浮点数 = 符号位 + 指数位 + 尾数位

`float`[4]，`double`[8]

Java 中默认浮点型常量（小数）为 **double** 型，如果要声明为 **float** 型，需要在数尾 + "**f**" 或 "**F**"

**.512** 即 0.512

**科学计数法**

1. **5.12e2** 表示 5.12 \* 10^2
2. **5.12E-3** 表示 5.12 / 10^3

## 字符型

`char`[2]

## 布尔型

`boolean`[1]

Java 中 **boolean** 只能是 **true** 或 **false** ，不可为 0 或 1 等任何数字，这点与其他语言不同

## 自动类型转换

精度（容量）从小到大

`char` -> `int` -> `long` -> `float` -> `double`
或者
`byte` -> `short` -> `int` -> `long` -> `float` -> `double`

1. 有多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的数据类型，然后再进行计算
2. 当我们把精度（容量）大的数据类型赋值给精度（容量）小的数据类型时，就会报错，反之就会进行动类型转换
```Java
				int a = 97;
				char b = a; // 错误
```
3. （` byte` ， `short` ）和 `char` 之间不会相互自动转换
```Java
				byte b1 = 97;
				char a = b1; // 错误
```
4. `byte` ， `short` ， `char` 他们三者可以计算，在计算时首先转换为 **int** 类型
```Java
				byte b1 = 97;
				short s1 = 98;
				short s2 = b1 + s1; // 错误
				byte b2 = 1;
				byte b3 = b1 +b2; // 错误
				int num1 = b1 +b2; // 正确
				char c = 99;
				int num2 = b1 + s1 + c; // 正确
```
5. `boolean` 不参与转换
6. 自动提升原则：表达式结果的类型自动提升为 操作数中最大的类型

## 基本数据类型转为 String 类型

```Java
				String str = "37"; // 必须为数字，否则编译正常通过，运行时抛出异常
				byte num1 = Byte.parseByte(str); // 输出 37
				short num2 = Short.parseShort(str); // 输出 37
				Long num3 = Long.parseLong(str); // 输出 37
				int num4 = Integer.parseInt(str); // 输出 37
				float num5 = Float.parseFloat(str); // 输出 37.0
				double num6 = Double.parseDouble(str); // 输出 37.0
				boolean b = Boolean.parseBoolean("true");
```

