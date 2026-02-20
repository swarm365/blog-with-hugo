+++
date = '2025-10-05T16:48:13+08:00'
title = 'Learning_Java_Day_16'
categories = ['tech']
tags = ['java-basics']
+++
# enum 枚举类

当确定要创建哪几个对象，且设为只读不能修改，用枚举类，举例：创建一个季节类，那就只有春夏秋冬四个季节，不可能多一个或少一个，也不可能叫其他名字

注意事项
1. 用 enum 关键字后就不能~~继承其他类~~，因为 enum 会隐式继承 Enum
2. 和普通类一样，可以实现接口

## 实现方式

- 自定义类实现枚举
1. 私有化构造器，防止直接 new 对象，在本类创建一组对象（如春夏秋冬共四个对象），对外暴露 `public final static` 对象，可以提供 `get` 方法，不需要提供~~setXxx方法~~，因为枚举对象值通常为只读
2. 对枚举对象 / 属性使用 `final` + `static` 共同修饰，实现底层优化
3. 枚举对象名通常使用全部大写，常量的命名规范
4. 枚举对象根据需要，也可以有多个属性

- **`enum`** 关键字实现枚举

```Java
		enum AA{ //使用enum关键字代替class
			//枚举对象必须写在枚举类的行首
			//如果有多个常量，用 , 隔开
			SPRING("春天","温暖"),SUMMER("夏天","炎热"),AUTUMN("秋天","凉爽"),WINTER("冬天","寒冷");
			private String name;
			private String desc;
		}
```

1. 当用 enum 开发一个枚举类时，默认会继承 Enum 类，而且是一个 final 类
2. 将自定义枚举类的写法 `public final static Season SPRING = new Season("春天","温暖");` 简化成了 `SPRING("春天","温暖");` ，要明确调用了哪个构造器
3. 若用 无参构造器 创建 枚举对象，则实参列表和小括号都可省略

```Java
		enum BB{
			WHAT; // 对应3
			private Hello(){ // 无参构造器
			
			}
		}
```

## 常用方法
1. toString：Enum类已经重写过了，返回的是当前对象名。子类可以重写该方法，用于返回对象的属性信息
2. name：返回当前对象名（常量名），子类中不能重写

```Java
		Season spring = Season.SPRING;
		System.out.println(spring.name()); // 输出SPRING
```

3. ordinal：返回当前对象的位置号，默认从0开始

```Java
		Season summer = Season.SUMMER;
		System.out.println(summer.ordinal()); // 输出1
```

4. values：返回当前枚举类中所有的常量

```Java
		Season[] values = Season.values();
		for(Season season: values){
			System.out.println(season);
			/*
			* 输出 Season{name='春天', desc='温暖'}
			* 输出 Season{name='夏天', desc='炎热'}
			* 输出 Season{name='秋天', desc='凉爽'}
			* 输出 Season{name='冬天', desc='寒冷'}
			*/
		}
```

5. valueOf：将字符串转换成枚举对象，要求字符串必须为已有的常量名，否则报异常！

```Java
		Season autumn = Season.valueOf("AUTUMN");
		System.out.println(autumn); // 输出 Season{name='秋天', desc='凉爽'}
		// Season dingZhen = Season.valueOf("DINGZHEN"); // 会报错
```

6. compareTo：比较两个枚举常量，比较的就是编号！

```Java
		//返回的是Season.AUTUMN的编号[2] - Season.WINTER的编号[3]
		System.out.println(Season.AUTUMN.compareTo(Season.WINTER)); // 输出-1
```

# 注解（Annotation）

- 注解（Annotation）也被称为元数据（Metadata），用于修饰解释包、类、方法、属性、构造器、局部变量等数据信息
- 和注释一样，注解不影响程序逻辑，但注解可以被编译或运行，相当于嵌入在代码中的补充信息
- 在 JavaSE 中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在 JavaEE 中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替 JavaEE 旧版中所遗留的繁冗代码和XML配置等
- 使用 Annotation 时要在其前面增加 `@` 符号，并把该 Annotation 当成一个修饰符使用，用于修饰它支持的程序元素
- 三个基本的 Annotation ：
1. @Override：限定某个方法，是重写父类方法，该注解只能用于方法
2. @Deprecated：用于表示某个程序元素（类，方法等）已过时
3. @SuppressWarnings：抑制编译器警告