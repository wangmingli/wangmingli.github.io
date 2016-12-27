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
       Person(String name){
            this.name = name; 
       } 
       //set、get method  omit....
    }
    public class FinalTest {
        private static Random random = new Random();
        private final String final_01 = "chenssy"; //编译期常量，必须要进行初始化，且不可更改
        private final String final_02; //构造器常量，在实例化一个对象时被初始化
        private final int final_03 = random.nextInt(50); //使用随机数来进行初始化
        public final Person final_04 = new Person("chen_ssy"); //final指向引用数据类型

        FinalTest(String final_02){
            this.final_02 = final_02;
        }
        public String toString(){
            return "final_01 = " + final_01 +" final_02 = " + final_02 + " final_03 = " + final_03 +
               " final_04 = " + final_04.getName();
        }
        public static void main(String[] args) {
            System.out.println("------------第一次创建对象------------");
            FinalTest final1 = new FinalTest("cm");
            System.out.println(final1);
            System.out.println("------------第二次创建对象------------");
            FinalTest final2 = new FinalTest("zj");
            System.out.println(final2);
            System.out.println("------------修改引用对象--------------");
            final2.final_04.setName("chenssy");
            System.out.println(final2);
        }
    }









jdflkdasjflsdjfldsj



	
	public class Person {
		private String name;
	
		Person(String name) {
			this.name = name;
		}
	
		public String getName() {
			return name;
		}
	
		public void setName(String name) {
			this.name = name;
		}
	
	}

