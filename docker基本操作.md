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