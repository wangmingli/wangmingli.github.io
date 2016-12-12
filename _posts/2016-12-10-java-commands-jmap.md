---
layout: post
title: java command jmap
category: Java
---
jmap(Java Memory Map) 显示出java进程内存中的obj的使用情况
<br/>
内存错误
- outOfMemoryError
- outOfMemoryError:PermGen Space 
- outOfMemoryError:GC overhead limit exceed 
<br/> <br/> <br/> <br/> <br/>

jps [ options ] [ pid ]

-heap    打印heap的概要信息 <br/>
-permstat 打印classload和jvm heap持久层的信息和classload详细信息及内部String的数量和占用内存数也会打印出来  <br/>
-histo   打印所有class详细信息， VM的内部类名字开头会加上前缀‘*’ <br/>
-histo:live JVM会先触发gc，然后再统计信息 <br/>
-finalizerinfo 打印正等候回收的对象的信息 <br/>



