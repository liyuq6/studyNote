docker基本操作：

"https://gq2l3omv.mirror.aliyuncs.com" 阿里云加速地址

**注意liunx要关闭防火墙！**

**安装docker:**

yum install docker

**启动docker：**

systemctl start docker

docker -v //查看版本

systemctl enable docker  //开机自动启动docker

****

systemctl stop docker   //停止服务

docker search mysql		// 搜索镜像

docker images 				//查看镜像列表

docker rma [镜像id]      //删除镜像

docker run --name [运行时名字] -d [镜像：如redis] :latest

docker ps //查看运行中的容器

docker stop [容器id] //停止运行容器

docker rm [容器id] //删除容器

docker run -d -p 8888:8080 [tomcat]

-d 后台运行

-p 将主机的端口映射到容器的另一个端口   主机端口：容器端口

查看容器的日志

docker logs container-name/container-id

更多命令查看：

https://docs.docker.com/engine/reference/commandline/docker/

docker运行命令：

docker run 

docker run --name mysql5.7 -e MYSQL_ROOT_PASSWORD=123456 -d -p 3306:3306 mysql:5.7

docker exec -it mysql5.7 bash

mysql -u root -p

注意mysql插入数据的中文格式问题，默认的字段插入编码时latin1

https://blog.csdn.net/ch717828/article/details/41357431/

mysql表内容中文显示问题：

https://blog.csdn.net/weixin_44038167/article/details/106854584





-a:列出本地的所有镜像

-q：只显示镜像ID

--digests：显示镜像的摘要信息

--no-trunc：显示完整的镜像信息



docker search -s num tomcat  //找出点赞量超过num值的镜像

docker rmi hello-world：tag // 删除对应的镜像文件

docker rmi -f hello-world：tag //强制删除对应的镜像文件



docker rmi -f $(docker images -qa)//删除所有的镜像



docker run --name   //为容器指定一个名称

-d：后台运行容器，并返回容器ID，也即启动守护式容器

-i：以交互模式运行容器，通常与-t同时使用

-t：为容器重新分配一个伪输入终端，通常与-i同时使用

-P：随机端口映射

-p：指定端口映射，四种格式

​		ip:hostPort:containerPort

​		ip::containerPort

​		hostPort：containerPort   //通常用于tomcat

​		contaierPort





docker run -it  //启动交互式容器





docker ps -a   //查看正在运行的和历史运行过的容器

docker ps -n 3  //前三次运行的容器

docker ps -q //静默模式。只显示容器编号

--no-trunc：//完整的摘要信息



容器退出方式：

exit 容器停止退出

ctrl+PQ  容器不停止退出



docker kill 容器ID/容器名字  //强制关闭该容器

docker rm 容器ID/容器名字 //删除已经停止的容器

docker rm -f  $(docker ps -a -q)//删除所有容器

docker ps -a -q | xargs docker rm //删除多个容器，xargs是可变长参数



-t	加入时间戳

-f	跟随最新的日志打印

docker log -t -f --tail num 容器ID //查看日志 倒数num条



docker top 容器ID  //查看容器内运行的进程



docker inspect 容器ID  //查看容器内部细节



docker attach 容器ID //重新进入该容器，该操作仅仅是进入容器

docker exec -it 容器ID  //后面可以附加操作，会直接启动进程并执行操作



docker cp 容器ID：容器内的数据文件路径  本地存放的路径



docker commit  容器ID 调教使起成为一个新的容器副本

-m 提交的描述信息

-a “作者” 