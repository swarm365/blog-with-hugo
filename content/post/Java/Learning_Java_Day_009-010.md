+++
date = '2025-09-28T11:16:57+08:00'
title = 'Learning_Java_Day_9-10'
categories = ['tech']
tags = ['java-basics']
+++
# 面向对象三大特性

## 封装

暂无...

## 继承

父类，也叫基类，超类
子类，也叫派生类

1. 子类继承了所有的属性和方法，非私有的属性和方法可以在子类直接访问，但是私有属性和方法要通过父类提供的公共方法才能访问，不能在子类直接访问

```Java
		//父类
		public class Base {
			public int n1 = 100;
			protected int n2 = 200;
			int n3 = 300;
			private int n4 = 400;

			public Base() {
				System.out.println("Base() 调用...");
			}

			public int getN4() {
				return n4;
			}

			public void test100() {
				System.out.println("test100");
			}

			protected void test200() {
				System.out.println("test200");
			}

			void test300() {
				System.out.println("test300");
			}

			private void test400() {
				System.out.println("test400");
			}

			public void callTest400() {
				test400();
			}
		}
```

```Java
		//子类
		public class Sub extends Base {
			public Sub() {
				System.out.println("Sub() 调用...");
			}

			public void sayOK() {
				n1 = 1;
				n2 = 5;
				n3 = 3;
				// n4 = 7; // 编译不通过，不允许直接调用父类的private属性
				System.out.println("n4 = " + getN4()); // 允许，相当于代替子类访问n4
				test100();
				test200();
				test300();
				// test400(); // 编译不通过，不允许直接调用父类的private方法
				callTest400(); // 允许，相当于代替子类访问test400()
			}
		}
```

2. 子类必须调用父类的构造器，完成父类的初始化
3. 当创建子类对象时，不管使用子类的哪个构造器，默认情况下总会去调用父类的无参构造器

```Java
		public class Sub extends Base {
			public Sub() {
				// super(); // 默认执行该语句，调用父类的无参构造器
				System.out.println("Sub() 调用...");
			}
		}
```

```Java
		public class Test{
			public static void main(String[] args) {
				Sub sub1 = new Sub(); // 控制台会先输出Base() 调用...，再输出Sub() 调用...
			}
		}
```

4. 如果父类没有提供无参构造器，则必须在子类的构造器中用 `super` 去指定使用父类的那个构造器完成对父类的初始化工作，否则，编译不会通过

```Java
		public class Base {
			//现在父类默认的无参构造器被覆盖
			public Base(String name, int age) {
				System.out.println("Base(String name, int age) 调用...");
		}
```

```Java
		public class Sub extends Base {
			public Sub() {
				super("丁真", 15); // 必须写，否则编译不通过
				System.out.println("Sub() 调用...");
			}
		}
```

```Java
		public class Test{
			Sub sub1 = new Sub(); // 控制台会先输出Base(String name, int age) 调用...，再输出Sub() 调用...
		}
```

5. 如果想调用指定的父类构造器，那就用 `super(参数列表)` 显示调用
6. `super()` 只能在构造器中使用
7. `super()` 和 `this()` 都必须放在构造器第 1 行，因此同一构造器不得同时用这两个方法，即两个方法不能同时用于同一个构造器中

### Super

`super` 代表父类的引用，用于访问父类的属性、方法、构造器，但不能访问 `private` 属性和 `private` 方法

### Override（方法覆盖、方法重写）
1. 子类方法的参数方法名称，要和父类方法的参数，方法名称完全一样
2. 子类方法的返回类型和父类方法返回类型一样，或者是父类返回类型的子类，比如父类返回类型是 `Obiect` ，子类方法返回类型是 `String`
3. 子类方法不能缩小父类方法的访问权限，如父类 `void say(){}` ，子类 `public void say(){}` ，不可为 ~~private void say(){}~~
4. 属性无法重写，属性的值看编译类型

```Java
			public class Test{
				public static void main(String[] args){
					Base base = new Sub(); // 看编译类型，即左侧
					System.out.println(base.n1); // 输出 100
					Sub sub = new Sub(); // 看编译类型，即左侧
					System.out.println(sub.n1); // 输出 15
				}
			}

			class Base{
				int n1 = 100;
			}

			class Sub extends Base{
				int n1 = 15;
			}
```

## 多态

### 向上转型

本质：父类的引用指向了子类的对象

语法：父类类型 引用名 = new 子类类型();

特点
1. 一个对象的编译类型和运行类型可以不一致
2. 编译类型在定义对象时，就确定了，不能改变
3. 运行类型是可以变化的
4. 编译类型看定义时 = 的左边，运行类型看 = 的右边
5. 可以调用父类中的所有成员（需遵守访问权限），不能调用子类中特有成员。因为在编译阶段，编译器认为是父类的成员，父类中怎么可能有子类的特有成员呢，所以编译不会通过

### 向下转型

本质：父类的引用指向的是当前目标类型的对象

语法：子类类型 引用名 =（子类类型）父类引用; 如 `Cat tom = (Cat) Animal;`

特点
1. 只能强转父类的引用，不能强转父类的对象
2. 当向下转型后，可以调用子类类型中所有的成员

### 动态绑定机制

1. 当调用对象方法的时候，该方法会和该对象的内存地址/运行类型绑定，哪里声明，哪里使用
2. 当调用对象属性时，没有动态绑定机制

```Java
		class A {
			public int i = 10;

			public int sum() { // 发现B类没有sum()方法，于是在A类找，找到了便调用A中的sum()方法
				return getI() + 10; // 执行时getI()调用B类的方法
			}

			public int sum1() { // 调用属性时不存在动态绑定，那么就用本类的值
				return i + 10;
			}

			public int getI() {
				return i;
			}
		}

		class B extends A {
			public int i = 20;

			public int getI() { // 父类和子类都有getI()，因为运行时是子类类型，那就调用子类的方法
				return i;
			}
		}

		public class Test {
			public static void main(String[] args) {
				A a = new B();
				//运行时先从B类找方法，找不到就到父类（即A类）继续找
				System.out.println(a.sum()); // 输出 30
				System.out.println(a.sum1()); // 输出 20
			}
		}
```

### 多态数组

1. 数组定义类型为父类，实际保存的元素是子类
2. 若要调用子类特有的方法，用类型判断和向下转型

```Java
		//Person是父类，Student和Teacher都是Person的子类，所有类都有say()方法
		public static void main(String[] args) {
			Person[] persons = new Person[5];
			persons[0] = new Person("bob", 20);
			persons[1] = new Student("jack", 18, 100);
			persons[2] = new Student("smith", 19, 30.1);
			persons[3] = new Teacher("scott", 30, 20000);
			persons[4] = new Teacher("king", 50, 25000);

			for (int i = 0; i < persons.length; i++) {
				//判断运行时类型是否为Student
				if (persons[i] instanceof Student) {
					/*
					相当于这2条语句
					Student student = (Student)persons[i];
					student.study();
					*/
					((Student)persons[i]).study();
				}
				persons[i].say(); // 动态绑定机制
			}
		}
```

### 多态参数

方法定义的形参类型为父类，实参类型允许为子类

