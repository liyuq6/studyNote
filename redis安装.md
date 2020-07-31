redis安装：https://blog.csdn.net/gaokcl/article/details/82814134

![image-20200720171435457](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200720171435457.png)

![image-20200720171503843](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200720171503843.png)

![image-20200721083927081](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721083927081.png)

启动命令：redis-server.exe redis.windows.conf

新开命令行窗口：redis-cli.exe -h 127.0.0.1 -p 6379

go连接windows下的redis：https://blog.csdn.net/wangshubo1989/article/details/75050024

![image-20200721090001709](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721090001709.png)

![image-20200721090048869](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721090048869.png)

解决中文乱码问题：

1.cmd里面设置编码格式：chcp 65001

![image-20200721092912463](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721092912463.png)

2.启动客户端时加上 --raw

![image-20200721092853062](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721092853062.png)

 操作sadd/smembers/srem, del

![image-20200721093759405](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721093759405.png)

![image-20200721094058939](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721094058939.png)

![image-20200721094144899](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721094144899.png)

![image-20200721095252137](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200721095252137.png)

