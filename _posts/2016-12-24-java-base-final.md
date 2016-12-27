---
layout: post
title: final 
category: Java
---

final是java的关键字，它所表示的是“这部分是无法修改”。不想被改变的原因：效率、设计。使用到final的有三种情况：数据、方法、类   

#### 数据  
对于这些恒定不变的数据我可以叫做“常量”。
1. 编译期常量，永远不可改变
2. 行期初始化时，我们希望它不会被改变

对于编译期常量，它在类加载的过程就已经完成了初始化，所以当类加载完成后是不可更改的，编译期可以将它代入到任何用到它的计算式中，也就是说可以在编译期执行计算式。对于编译期常量，只能使用基本类型，而且必须要在定义时进行初始化 <br/>    

有些变量，我们希望它可以根据对象的不同而表现不同，但同时又不希望它被改变，这个时候我们就可以使用运行期常量。对于运行期常量，它既可是基本数据类型，也可是引用数据类型;基本数据类型不可变的是其内容，而引用数据类型不可变的是其引用，引用所指定的对象内容是可变的。[exmple：StringBuffer ]  <br/>  

	
	public class Person {
		private String name;
	
		Person(String name) {
			this.name = name;
		}
                set、get method  omit....	
	}

        
	public class Test {
		private static Random random = new Random();
		private final String t1 = "one"; 
		private final String t2; 
		private final int t3 = random.nextInt(30); 
		public final Person t4 = new Person("happy"); 
	
		Test(String t2) {
			this.t2 = t2;
		}
		@Override
		public String toString() {
			return "Test [t1=" + t1 + ", t2=" + t2 + ", t3=" + t3 + ", t4=" + t4.getName()
					+ "]";
		}
	
		public static void main(String[] args) {
			Test test1 = new Test("s");
			System.out.println(test1);
			Test test2 = new Test("ms");
			System.out.println(test2);
			test2.t4.setName("abc");
			System.out.println(test2);
		}
	}

