---
layout: post
title: LinkedList VS ArrayList
category: Java
---
首先看一下LinkedList和ArrayList的继承关系,两者都实现List接口，前者实现RandomAccess接口，后者实现Queue接口<br/>

public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, Serializable <br/>  

public class LinkedList<E> extends AbstractSequentialList<E> implements List<E>, Queue<E>, Cloneable, Serializable  <br/> 

<br/>   
            
####  ArrayList  动态数组结构 
ArrayList其实是包装了一个数组 Object[]，当实例化一个ArrayList时，一个数组也被实例化，当向ArrayList中添加对象是，数组的大小也相应的改变 <br/> 

1. 快速随即访问 你可以随即访问每个元素而不用考虑性能问题，通过调用get(i)方法来访问下标为i的数组元素  
2. 向其中添加对象速度慢 当你创建数组是并不能确定其容量，所以当改变这个数组时就必须在内存中做很多事情   
3. 操作其中对象的速度慢 当你要想数组中任意两个元素中间添加对象时，数组需要移动所有后面的对象     

<br/>  
       
#### LinkedList  链表结构   
LinkedList是通过节点直接彼此连接来实现的。每一个节点都包含前一个节点的引用，后一个节点的引用和节点存储的值。当一个新节点插入时，只需要修改其中保持先后关系的节点的引用即可，当删除记录时也一样。   


* 操作其中对象的速度快 只需要改变连接，新的节点可以在内存中的任何地方    
* 不能随即访问 虽然存在get()方法，但是这个方法是通过遍历接点来定位的所以速度慢   








































