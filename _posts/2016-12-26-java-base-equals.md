---
layout: post
title: equals and hashCode 
category: Java
---
当对象类没有override equals()和hashcode()方法的时候，两个对象做比较   
1. 如果equals()比较相同，那么hashcode()肯定相同    
2. 如果hashcode()比较相同，那么equals()不一定相同      


               public native int hashCode(),说明hashCode是一个本地方法，它的实现是根据本地机器相关的          
               由于哈希码在生成的时候产生冲突造成的      


       <br/>      
String 、Math、还有Integer、Double..这些封装类重写了Object中的equals()方法，让它不再比较句柄（引用），而是比较对象中实际包含的整数的值，即比较的是内容。而Object的equals()方法比较的是地址值 <br/>    
一般来说，如果你要把一个类的对象放入容器中，那么通常要为其重写equals()方法，让他们比较地址值而不是内容值。特别地，如果要把你的类的对象放入散列中，那么还要重写hashCode()方法；要放到有序容器中，还要重写compareTo()方法。 只有用到Hashtable、HashMap、HashSet、LinkedHashMap等时才要注意hashcode，其他地方hashcode无用      
    
           
### 为什么要重写hashCode方法          
在java的集合中，判断两个对象是否相等的规则是 
首先判断两个对象的hashCode是否相等,如果不相等，认为两个对象也不相等 
如果相等，则判断两个对象equals运算是否相等,如果不相等则认为不相等 ,如果相等则认为两个对象相等 
我们在equals方法中需要向下转型，效率很低，所以先判断hashCode方法可以提高效率。

我的理解是在object、String等类中都能使用。在object类中，hashcode()方法是本地方法，返回的是对象的地址值，而 object类中的equals()方法比较的也是两个对象的地址值，如果equals()相等，说明两个对象地址值也相等，当然hashcode()也 就相等了；
在String类中，equals()返回的是两个对象内容的比较，当两个对象内容相等时， Hashcode()方法根据 String类的重写代码的分析，也可知道hashcode()返回结果也会相等。


### 在hashset中不允许出现重复对象，元素的位置也是不确定的。在hashset中又是怎样判定元素是否重复的呢？
1. 判断两个对象的hashCode是否相等 如果不相等，认为两个对象也不相等，完毕 如果相等，转入2;（这一点只是为了提高存储效率而要求的，其实理论上没有也可以，但如果没有，实际使用时效率会大大降低，所以我们这里将其做为必需的） 
2. 判断两个对象用equals运算是否相等 
如果不相等，认为两个对象也不相等 
如果相等，认为两个对象相等（equals()是判断两个对象是否相等的关键） 
为什么是两条准则，难道用第一条不行吗？不行，因为前面已经说了，hashcode()相等时，equals()方法也可能不等

	public class ParentClass {
		private String value;
	
		public ParentClass(String value) {
			super();
			this.value = value;
		}
		public String getValue() {
			return value;
		}
	
		@Override
		public int hashCode() {
			return value.hashCode();
		}
		@Override
		public boolean equals(Object arg0) {
			if (arg0 == this) {
				return true;
			}
			if (arg0 instanceof ParentClass) {
				return value.equals(((ParentClass) arg0).getValue());
			}
			return false;
		}
	}
	public class DerivedClass extends ParentClass { 
	    public DerivedClass(String value) { 
	        super(value); 
	    } 
	}
	public class CollectionUtils {
		 public static void main(String args[]) { 
	         String str = "Hello"; 
	         DerivedClass s1 = new DerivedClass(str); 
	         ParentClass s2 = new ParentClass(str); 
	         System.out.println("s1 == s2?"+ (s1 == s2));// false 
	         System.out.println("s1.equals(s2)?"+s1.equals(s2));// true   
	         System.out.println("s1.hashCode(): "+s1.hashCode());// s1.hashcode()等于s2.hashcode() 
	         System.out.println("s2.hashCode()"+s2.hashCode()); 
	         Set hashset = new HashSet(); 
	         hashset.add(s1); 
	         hashset.add(s2); 
	         Iterator it = hashset.iterator(); 
	         while (it.hasNext()) { 
	             System.out.println(it.next());  
		     //只打印出了一个对象,根据上面的第1.2条原则判定时，hashset认为它们是相等的对象
	         } 
	     } 
	}



根据hashcode()对两次建立的new Student(1,"zhangsan")对象进行比较时，生成的是不同的哈希码值，所以hashset把他当作不同的对象对待了，当然此时的 equals()方法返回的值也不等。那么为什么会生成不同的哈希码值呢？
它是一个本地方法，比较的是对象的 地址（引用地址），使用new方法创建对象，两次生成的当然是不同的对象了，造成的结果就是两个对象的hashcode() 返回的值不一样。所以根据第一个准则，hashset会把它们当作不同的对象对待，自然也用不着第二个准则进行判定了。
那么怎么解决这个问题呢？？ 答案是：在Student类中重新hashcode()和equals()方法。 





	public class HashSetTest {
	
		public static void main(String[] args) {
			HashSet hs = new HashSet();
			hs.add(new Student(1, "zhangsan"));
			hs.add(new Student(2, "lisi"));
			hs.add(new Student(3, "wangwu"));
			hs.add(new Student(1, "zhangsan"));
	
			Iterator it = hs.iterator();
			while (it.hasNext()) {
				System.out.println(it.next());
			}
		}
	}
	
	
	class Student {
		int num;
		String name;
	
		Student(int num, String name) {
			this.num = num;
			this.name = name;
		}
	
		public int hashCode() {
			return num * name.hashCode();
		}
	
		public boolean equals(Object o) {
			Student s = (Student) o;
			return num == s.num && name.equals(s.name);
		}
	
		public String toString() {
			return num + ":" + name;
		}
	}
	//class Student {
	//	int num;
	//	String name;
	//
	//	Student(int num, String name) {
	//		this.num = num;
	//		this.name = name;
	//	}
	//
	//	public String toString() {
	//		return num + ":" + name;
	//	}
	//}

    


 
