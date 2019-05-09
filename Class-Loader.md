# 加载器踩坑


案例：  
项目中存在同名不同版本jar包，结果代码报错
```
-rw-r--r-- 1 root root    63710 Mar 13 23:19 vip.osp-2018.12.27.jar
-rw-r--r-- 1 root root    63710 Apr 23 00:02 vip.osp-2019.02.20.jar
-rw-r--r-- 1 root root  9764696 Mar 13 23:19 vip.vop-2018.12.27.jar
-rw-r--r-- 1 root root  8634175 Apr 23 00:02 vip.vop-2019.02.20.jar
```
  
Q：为什么存在同名不同版本的jar包时会报错？  
A：
```
相关资料：
1.Java基础之《加载器对同名不同版本jar包加载的选择》: https://blog.csdn.net/csj50/article/details/79360488
2.图解Tomcat类加载机制: https://www.cnblogs.com/xing901022/p/4574961.html
3.Spring Boot ClassLoader: https://blog.csdn.net/caoyi1207/article/details/80606232
```