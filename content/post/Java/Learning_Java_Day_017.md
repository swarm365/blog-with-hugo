+++
date = '2025-10-06T11:15:51+08:00'
title = 'Learning_Java_Day_17'
categories = ['tech']
tags = ['java-basics']
+++
# 异常（Exception）

## 运行时异常

### NullPointerException空指针异常

当应用程序试图在需要对象的地方使用 null 时，抛出该异常

```Java
		String name = null;
		System.out.println(name.length()); // 会抛出异常
```

### ArithmeticException数学运算异常

当出现异常的运算条件时，抛出该异常，如除以 0

### ArraylndexOutOfBoundsException数组下标越界异常

使用非法索引访问数组时，抛出该异常

### ClassCastException类型转换异常

当试图将对象强制转换为不是实例的子类时，抛出该异常

```Java
		public class ClassCastException_ {
			public static void main(String[] args) {
				Animal cat = new Cat(); // 向上转型
				Cat tom = (Cat) cat; // 向下转型，正常
				Dog dog = (Dog) cat; // 抛出异常
			}
		}

		class Animal {
		}

		class Cat extends Animal {
		}

		class Dog extends Animal {
		}
```

### NumberFormatException数字格式不正确异常

当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常 => 使用异常我们可以确保输入是满足条件数字

## 编译时异常

编译异常是指在编译期间，就必须处理的异常，否则代码不能通过编译

以下了解即可
1. SQLException 操作数据库时，查询表可能发生异常
2. IOException 操作文件时，发生的异常
3. FileNotFoundException 当操作一个不存在的文件时，发生异常
4. ClassNotFoundException 加载类，而该类不存在时，异常
5. EOFException 操作文件，到文件未尾，发生异常
6. IllegalArguementException 参数异常

## 异常处理

### try-catch-finally
程序员在代码中捕获发生的异常，自行处理

### throws
将发生的异常抛出，交给调用者（方法）来处理，最顶级的处理者就是 JVM

## 自定义异常

实现步骤
1. 定义类：自定义异常类名（程序员自己写）继承 Exception 或 RuntimeException
2. 如果继承 Exception ，属于编译异常
3. 如果继承 RuntimeException ，属于运行异常（一般来说，继承 RuntimeException）