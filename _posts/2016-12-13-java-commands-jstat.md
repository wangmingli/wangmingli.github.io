---
layout: post
title: java command jstat
category: Java
---
jstat(Java Virtual Machine Statistics Monitoring Tool)用于监控基于HotSpot的JVM，对其堆的使用情况进行实时的命令行的统计

<br/>


jstat -<option> [-t] [-h lines] <pid> [interval [count]]  <br/> 


*  **-h n    用于指定每隔几行就输出列头,默认是只在第一行出现列头**

*  **-t     用于在输出内容的第一列显示时间戳，这个时间戳代表的时JVM开始启动到现在的时间**

*  **interval 间隔时间，单位可以是秒或者毫秒，通过指定s或ms确定，默认单位为毫秒**

*  **count   打印次数，如果缺省则打印无数次**
<br/> <br/> <br/>



jstat –class <pid>  显示加载class的数量，及所占空间等信息

* Loaded 装载的类的数量  
* Bytes 装载类所占用的字节数
* Unloaded 卸载类的数量
* Bytes 卸载类的字节数
* Time 装载和卸载类所花费的时间
 <br/>
jstat -compiler <pid>  显示VM实时编译的数量等信息

* Compiled 编译任务执行数量
* Failed 编译任务执行失败数量
* Invalid 编译任务执行失效数量
* Time 编译任务消耗时间
* FailedType 最后一个编译失败任务的类型
* FailedMethod 最后一个编译失败任务所在的类及方法


jstat -gcutil <pid>  显示GC信息    

* 时间单位: s




