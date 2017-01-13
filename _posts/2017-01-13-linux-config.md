---
layout: post
title: simple conf 
category: Linux
---
# 修改主机名称
### hostname new-hostname          


### vim  /etc/sysconfig/network, HOSTNAME=new-hostname;  以便于重启后依旧生效      


### vim /etc/hosts; 可以让服务器解析主机名       


# 生成安全信任关系证书    

### 在Client: ssh-keygen -t rsa、输入回车键[表示无证书密码]      
   
### 生成私钥证书->id_rsa、公钥证书->id_rsa.pub、在/root/.ssh/下     

### 将id_rsa.pub copy到 Server上的/root/.ssh/authorized_keys     


### file flags   
在vim or rm  file.txt  显示: Operation not permitted  <br/>    
	     lsattr  file.txt    [查看该文件是否被打了 flags，若file标记了i,则会出现以上该问题]  <br/>   
	     chattr -i file.txt  [去除这个标记]       <br/>    
	     chattr +i file.txt  [给保护文件添加标记]   <br/>   



 

 


 
    


 
