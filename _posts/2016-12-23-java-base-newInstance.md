---
layout: post
title: newInstance
category: Java
---
newInstance VS new <br/>  
* newInstance 弱类型。低效率。只能调用无参构造   
* newInstance 是一个方法，new 是一个关键字   
* newInstance 使用类加载机制创建一个实例，然而new创建一个新类  

在java里面任何class都要装载在虚拟机上才能运行，Class.forName(xxx.xx.xx) 返回具有指定名的类的 Class对象，在类装载的时候使用<br/>  A a = (A)Class.forName("pacage.A").newInstance();  <br/>  
or   
A a = new A();    <br/>   
Class.forName(xxx.xx.xx); 作用是要求JVM查找并加载指定的类,也就是说JVM会执行该类的静态代码段,静态代码是和class绑定的，class装载成功就表示执行了你的静态代码了  <br/>   


ExampleInterface是Example的接口，可以写成如下形式：    
```
String className = "Example"; <br/>   
class c = Class.forName(className);  <br/>   
factory = (ExampleInterface)c.newInstance();  <br/>   
```

进一步可以写成如下形式：    

     //从xml 配置文件中获得字符串 
     String className = readfromXMlConfig; 
     class c = Class.forName(className); 
     factory = (ExampleInterface)c.newInstance(); 


     
上面代码已经不存在Example的类名称，它的优点是，无论Example类怎么变化，上述代码不变，甚至可以更换Example的兄弟类Example2 , Example3 , Example4……，只要他们继承ExampleInterface就可以。 


