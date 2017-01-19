---
layout: post
title: Link 
category: Linux
---
     
###  CONCEPT   
1. linux link: a、hark link     b、symbolic link   
    
2. index node :linux系统中，无论磁盘上的文件是什么类型，os都会为其分配一个编号   

   
### HARD LINK    
hard link --> 硬链接，linux os,其允许一个文件有多个有效的路径，多个文件指向同一个索引节点；最终的效果是防止 **[误删]**  <br/>    
对应目录的索引节点有多个链接，只删除一个连接并不影响文件的数据块，只有最后一个连接被删除后，文件的数据块及目录的连接才会被释放
ln  文件   标示文件         

### SYMBOLIC LINK   
symbolic link --> 软连接, 类似于windows的快捷方式；它在os中是一个特殊的文件，包含有目的文件的位置信息  

ln -s 文件   标示文件

	     [@sjs_37_169 tmp]# ln file.txt   file_hard.txt
	     [@sjs_37_169 tmp]# ln -s file.txt  file_symbolic.txt
	     [@sjs_37_169 tmp]# ll
	                        total 0
	                        -rw-r--r-- 2 root root 0 Jan 19 16:33 file_hard.txt
	                        lrwxrwxrwx 1 root root 8 Jan 19 16:34 file_symbolic.txt -> file.txt
	                        -rw-r--r-- 2 root root 0 Jan 19 16:33 file.txt


 

 


 
    


 
