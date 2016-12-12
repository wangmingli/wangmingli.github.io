---
layout: post
title: java command
category: Java
---

jps (Java Virtual Machine Process Status) 显示所有java进程pid的命令以及相关参数[当前用户下]

<br/>



实现机制如下：

java程序启动后，会在java.io.tmpdir指定的目录下[临时文件夹]，生成一个类似于hsperfdata_UserName的文件夹;

[在Linux中为/tmp/hsperfdata_{userName}/]，有几个文件->名字就是java进程的pid。所以列出当前运行的java进程，只是把这个目录里的文件名列一下而已。 

至于系统的参数什么，就可以解析这几个文件获得。
<br/> <br/> <br/>




jps [ options ] [ pid ]

*  **-m 列出传给main方法的参数**

*  **-l 列出应用程序main class的完整包名 or 应用程序的jar文件完整路径名**

*  **-v 列出传递给JVM的参数**
<br/> <br/> <br/>




jps 失效原因

                        磁盘读写问题、磁盘已满等，目录的权限问题以及文件丢失等问题...
