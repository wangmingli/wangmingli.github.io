---
layout: post
title: GC  summary
category: Java
---
堆内存大小 = 年轻代大小 + 年老代大小 <br/>
内存大小   = 堆内存大小 + 持久代大小  

<br/>   

垃圾回收器的特性:  
1. 该回收的对象一定要回收，不该回收的对象一定不能回收
2. 一定要有效，并且要快！尽可能少的暂停应用的运行 
3. 需要在  *时间，空间，回收频率*  这三个要素中平衡 
4. 内存碎片的问题（压缩）

<br/>  
       
GC性能的指标:
* 吞吐量    应用花在非GC上的时间百分比 
* GC负荷    与吞吐量相反
* 暂停时间   应用花在GC stop-the-world 的时间 
* GC频率     顾名思义 
* Footprint   一些资源大小的测量，比如堆的大小 
* 反应速度   从一个对象变成垃圾道这个对象被回收的时间 

一个交互式的应用要求暂停时间越少越好，然而，一个非交互性的应用，当然是希望GC负荷越低越好 <br/> 
一个实时系统对暂停时间和GC负荷的要求，都是越低越好 <br/>  
一个嵌入式系统当然希望Footprint越小越好 <br/>  


<br/>   

### GC类型
年轻代GC叫young GC[minor GC]。年老代或者永久代的GC叫full GC[major GC]。也就是说，所有的代都会进行GC  <br/>  
首先是进行年轻代的GC，然后是年老代和永久代使用相同的GC。如果要压缩，每个代需要分别压缩。  <br/>  
有时候，如果年老区本身就已经很满了，满到无法放下从survivor熬出来的对象，那么，YGC就不会再次触发，而是会使用FullGC对整个堆进行GC（除了CMS这种GC，因为CMS不能对年轻代进行GC）   <br/>   

### 连续 VS 并行
连续垃圾回收器，即使在多核的应用中，在回收时，也只有一个核被利用;并行GC会使用多核，GC任务会被分离成多个子任务，然后这些子任务在各个CPU上并行执行。并行GC的好处是让GC的时间减少，但缺点是增加了复杂度，且存在产生内存碎片的可能。   <br/>  

### 并发 VS. stop-the-world
使用stop-the-world 方式的GC在执行时，整个应用会暂停。而并发是指GC可以和应用一起执行，不用stop the world。一般的说，并发GC可以做到大部分的运行时间，是可以和应用并发的，但还是有一些小任务，不得不短暂的stop the world。stop the world 的GC相对简单，因为heap被冻结，对象的活动也已经停止。缺点是不太满足对实时性要求很高的应用。相应的，并发GC的stop the world时间非常短，但需要做一些额外的事情，因为并发的时候，对象的引用状态有可能发生改变的。所以并发GC需要花费更多的时间，需要较大的heap。  <br/>  

### 压缩 VS. 不压缩 VS. 复制
在GC确定内存中哪些是有用的，哪些是可回收的对象后，就可以压缩内存，把有用的对象放到一起，并把剩下的内存进行清理。压缩之后，分配对象就会快，内存指针可以很快的指向下一个要分配的内存地址。一个不压缩的GC，就原地把不被引用的对象回收。好处:回收的速度变快；缺点:产生了碎片。在有碎片的内存上分配一个对象的代价要远远大于在没有碎片的内存上分配。复制算法的GC，他是把所有被引用的对象复制到另外一个内存区域中。好处:原来的内存区域可以被毫无顾忌的清空了。缺点:需要更多的内存，以及额外的时间来复制。  <br/> <br/>  <br/>  


###  分代
最广泛的分代应属年轻代和年老代了。根据各种GC算法的特征，可以相应的被应用到不同的代中 <br/>  
大部分的对象在分配后不久，就不被引用了。也就是他们在很早就挂了。只有很少的对象熬过来了。年轻代的GC相当的频繁，高效率并且快。因为年轻代通常比较小，并且很多对象都是不被引用的。如果年轻代的对象熬过来了，那么就晋级到年老代中了
![](https://github.com/wangmingli/wangmingli.github.io/raw/master/pic/gc_1.jpg)   <br/>  

年老代要比年轻代大，而且增长也比较慢。所以GC在年老代发生的频率非常低，不过一旦发生，就会占据较长的时间。<br/>  
年轻代通常使用时间占优的GC，因为年轻代的GC非常频繁;年老代通常使用善于处理大空间的GC，因为年老代的空间大，GC频率低 ;
![](https://github.com/wangmingli/wangmingli.github.io/raw/master/pic/gc_2.jpg)     
年轻代也进行划分，划分成:一个Eden和两个survivor  <br/>  
大部分的对象被直接分配到年轻代的eden区（很大的对象会被直接分配到年老代中）<br/>  
survivor区里面放至少熬过一个YGC的对象，在survivor里面的对象，才有机会被考虑提升到年老代中。
同一时刻，两个survivor只被使用一个，另外一个是用来进行复制GC时使用的。  
  <br/>  <br/>

### GC过程
1. eden空间被分配完,就会发生一次垃圾收集.eden中仍存活的对象会被复制到survivorspace1中,其他对象直接丢弃,其占用的内存回收.  

2. 垃圾回收后,JVM在eden中创建对象.当eden的空间再次被分配完,又会发生一次垃圾收集.将eden中存活的对象复制到另一个survivorspace2中  

3. 为survivorspace1中的每一个对象计算年龄age和存活期threshold.age小于threshold的将会被复制到survivorspace2中,这些对象被称为aged对象(老化对象),等于小于threshold的将会被复制到old generation.清空的survivorspace1为下一次的次要垃圾收集中复制的目的地

           age是对象在复制到old generation之前经历过垃圾收集的次数
           threshold是在这一次的次要垃圾收集将会被复制到old generation的对象的门槛


    
![](https://github.com/wangmingli/wangmingli.github.io/raw/master/pic/gc_3.jpg)   <br/>







































