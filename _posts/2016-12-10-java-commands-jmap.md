---
layout: post
title: java command jmap
category: Java
---
jmap(Java Memory Map) 显示出java进程内存中的obj的使用情况,制作堆Dump[二进制格式] <br/>  

<br/> 
 
常见内存错误 

*  outOfMemoryError

*  outOfMemoryError  PermGen Space

*  outOfMemoryError  GC overhead limit

   
<br/> <br/> <br/>

jmap [ options ] [ pid ]

* **-heap    打印heap的概要信息** 
* **-permstat 打印classload和jvm heap持久层的信息和classload详细信息及内部String的数量和占用内存数也会打印出**
* **-histo   打印所有class详细信息， VM的内部类名字开头会加上前缀‘*’**
* **-histo:live JVM会先触发gc，然后再统计信息**
* **-finalizerinfo 打印正等候回收的对象的信息**
* **jmap -dump:format=b,file=/search/dumpFileName pid,如果Dump文件太大，可能需要加上-J-Xmx512m这种参数指定最大堆内存，即jhat -J-Xmx512m -port 9998 /search/dumpFileName,就可在浏览器中查看了**
            -XX:+HeapDumpOnOutOfMemoryError  --> jvm 在内存异常时,自动生成堆Dump



----------------------------------------------------------------------------------------------------------------

jhat(Java Heap Analysis Tool) 解析Java堆dump并启动一个web服务器,就可以在浏览器中查看堆的dump文件了<br/> 


* **-J< flag > jhat会启动一个JVM来执行, -J 可以在启动JVM时传入一些启动参数**


* **-port portNum  defalult 7000**


   
* Show instance counts for all classes (excluding platform)   
  
* Show heap histogram   
  
* Show finalizer summary


