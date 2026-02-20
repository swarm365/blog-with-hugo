+++
date = '2025-09-25T00:03:11+08:00'
title = 'Learning_Java_Day_6-8'
categories = ['tech']
tags = ['java-basics']
+++
# 面向对象基础

## 类和对象的内存分配机制

### Java的内存结构分析
1. 栈：一般存放基本数据类型（局部变量）
2. 堆：存放对象（数组等）
3. 方法区：常量池（常量，比如字符串），类加载信息

## 成员方法

### 访问修饰符（作用是控制 方法使用的范围）

1. 如果不写默认访问，（共有四种：public，protected，默认，private）
2. 类只允许用 **`public`** 和 **`默认`** 修饰符访问

```Java
				public class A{}
				class B{}
				//protected C{} 错误，对应2
				//private D{} 错误，对应2
```

### 返回数据类型
1. 一个方法最多有一个返回值 （思考，如何返回多个结果 -> 返回**数组**）
2. 返回类型可以为任意类型，包含基本类型或引用类型（数组，对象）
3. 如果方法要求有返回数据类型，则方法体中最后的执行语句必须为return值：而且要求返回值类型必须和return的值类型一致或兼容
4. 如果方法是void，则方法体中可以没有return语句，或者只写return;
5. 方法名遵循驼峰命名法，最好见名知义，表达出该功能的意思即可，比如得到两个数的和 getSum ，开发中按照规范

### 方法体
里面写完成功能的具体的语句，可以为输入、输出、变量、运算、分支、循环、方法调用，但里面不能再定义方法！即：方法不能嵌套定义

```Java
				class AA{
					public void A(){
						...... // 执行语句
						//public void B(){ // 编译不通过，不能嵌套定义方法
							......
						}
					}
				}
```

### 调用细节
1. 同一个类中的方法调用：直接调用即可，如 `print(参数)`
2. 跨类中的方法A类调用B类方法：需要通过对象名调用，如 **对象名.方法名(参数)**
3. 特别说明一下：跨类的方法调用和方法的访问修饰符相关，先暂时这么提一下，后面我们讲到访问修饰符时，还要再细说

```Java
		public class XXX{
			public static void main(String args[]){
				A a = new A();
				a.sayOk();
				a.m1();
			}
		}

		class A{
			public void print(int n){
				System.out.println("print()方法调用 n = " + n);
			}

			public void sayOk{
				print(10); // 同类方法调用
				System.out.println("继续执行sayOk()方法");
			}

			public void m1(){ // 跨类中的方法A类调用B类方法
				// 创建B对象，再调用方法
				System.out.println("m1()方法调用");
				B b = new B();
				b.hi();
				System.out.println("m1()方法继续执行:)");
			}
		}

		class B{
			public void hi(){
				System.out.println("B类中的hi()方法执行");
			}
		}
```

## 可变参数

Java 允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法，可以通过可变参数实现

1. 实参可以为数组
2. 可变参数可以和普通类型的参数一起放在形参列表，但必须保证可变参数在最后
3. 一个形参列表中只能出现一个可变参数


不封装的情况下

```Java
		class SumMethod {
			public int sum(int n1, int n2){ // 2个数的和　
				return n1 + n2;
			}
			public int sum(int n1, int n2, int n3){ // 3个数的和
				return n1 + n2 + n3;
			}
			public int sum(int n1, int n2, int n3, int n4){ // 4个数的和
				return n1 + n2 + n3 + n4;
			}
		}
```

使用封装

```Java
		public class XXX{
			public static void main(String args[]){
				SumMethod a = new SumMethod();
				int ans1 = a.sum(1,2,3,4);
				int[] arr = {1,2,3};
				int ans2 = a.sum(arr); // 对应1，实参可为数组
				
			}
		}
		
		class SumMethod {
			//int... 表示接受可变参数，类型为int，即可接收任意个int（0个也可以）
			//使用可变参数时，可当作数组来使用，即nums可当作数组
			public int sum(int... nums){
				System.out.println("接收参数个数" + nums.length);
				int res = 0;
				for(int i = 0; i < nums.length; i++){
					res += nums[i];
				}
				return res;
			}
			
			//对应2
			public void f1(String str, int a, double b, double... scores){
				...
			}
			
			//对应3，不允许此写法
			/*public void f2(int... nums, double... scores){
				
			}*/
		}
```

## 作用域

1. **全局变量（属性 / 成员变量）**不赋值可直接使用，因为有默认值
2. **局部变量（定义在成员方法中的变量）**必须**赋值**后才能使用，没有默认值
3. 属性和局部变量可以重名，访问时遵循就近原则
4. 在同一个作用域中，比如在同一个成员方法中，两个局部变量，不能重名。
5. 全局变量可以加修饰符，**局部变量**不可加修饰符

```Java
		class Cat{
			protected int age = 15; // 全局变量
			public void hi(){
				int age = 18; // 局部变量，对应3
				System.out.println(age); // 输出18，对应3
				//public String name; // 错误，对应5
			}
		}
```

## 构造方法 / 构造器（constructor）

1. 构造方法又叫构造器，是类的一种特殊的方法，它的主要作用是完成对新对象的初始化
2. 构造器的修饰符可以默认，也可以是 `public` `protected` `private`
3. 构造器没有返回值，不要写 `return`
4. 方法名和类名必须一样
5. 参数列表 和 成员方法一样的规则
6. 在创建对象时，系统会自动的调用该类的构造器完成对象属性的初始化
7. 一个类可以定义多个不同的构造器，即构造器重载。比如：我们可以再给Person类定义一个构造器，用来创建对象的时候，只指定人名不需要指定年龄
8. 如果程序员没有定义构造方法，系统会自动给类生成一个默认无参构造方法（也叫默认构造方法），比如Person(){} ，使用javap指令反编译看看
9. 一旦定义了自己的构造器，默认的构造器就被覆盖了，就不能再使用默认的无参构造器，除非显式的定义一下，即：Person(){}

```Java
		public class XXX{
			public static void main(String args[]){
				Person p1 = new Person("丁真", 15); // 调用第1个构造器
				System.out.println("名字 " + p1.age);
				System.out.println("年龄 " + p1.age);
				Person p2 = new Person("王源"); // 调用第2个构造器
				
				//p2.Person(); // 错误，构造方法不允许这样调用
				
				Dog d1 = new Dog(); // 调用的是默认构造器
				
				//Person p3 = new Person(); // 错误，默认构造器被自己的构造器覆盖
				
				Cat c1 = new Cat(); // 正确，因为自己又显式定义
			}
		}
		
		class Person{
			String name;
			int age;
			//没有返回值，也不能写void
			public Person(String pName, int pAge){
				name = pName;
				age = pAge;
			}
			public Person(String pName){
				name = pName;
			}
		}
		
		class Dog{
			/*
			自己未定义构造器时，系统默认生成如下
			Dog(){
			
			}
			*/
		}
		
		class Cat{
            String name;
			public Cat(String cName){
				name = cName;
			}
			
			Cat(){
			
			}
		}
```

## this 关键字

1. this关键字可以用来访问本类的属性、方法、构造器
2. this用于区分当前类的属性和局部变量
3. 访问成员方法的语法：this.方法名(参数列表);
4. 访问构造器语法：this(参数列表) ：注意只能在构造器中使用，且如果要使用，必须为第1条语句
5. this不能在类定义的外部使用，只能在类定义的方法中使用

```Java
		public class XXX{
			public static void main(String args[]){
				T t1 = new T();
				t1.f2();
		}
		
		class T{
			String name = "丁真";
			
			public T(){
				//在这里访问T(String name, int age)，对应4
				this("丁真",15);
				System.out.println("T()构造器调用");
			}
			
			public T(String name, int age){
				System.out.println("T(String name, int age)构造器调用");
			}
			
			public void f1(){
				//this("王源",15); // 错误，对应4
				System.out.println("f1调用");
			}
			
			public void f2(){
				System.out.println("f2调用");
				//调用本类的f1
				//第1种方式
				f1();
				//第2种方式，对应3
				this.f1();
				//以上2种方式的区别会在继承中讲到
			}
			
			public void f3(){
				String name = "王源";
				//传统方法，就近原则
				System.out.println(name); // 输出王源
				//this方法
				System.out.println(this.name); // 输出丁真，对应1
			}
		}
```
