**postgreSQL**

psql -U postgres

123456//公司电脑

初始的启动服务器命令：

initdb.exe -D ../data

pg_ctl.exe start -D ..\data

之后打开一个新的cmd窗口输入：psql postgres

参考网站：

https://blog.csdn.net/ywg_1994/article/details/82391531

https://blog.csdn.net/m15217321304/article/details/105292612/

https://blog.csdn.net/csdn_xng/article/details/86679628

https://blog.csdn.net/hehong_78/article/details/6091011

创建用户：

postgres=# create user liyuqi with password '123';

切换用户：

\c - liyuqi     //切换数据库也是命令



\l 查看数据库



创建数据库：creat database test

进入用户为liyuqi的数据库test: psql -U liyuqi -d test



pg_restore -d [数据库名] .dmp

ALTER TABLE TABLENAME ALTER COLUMN 字段名 TYPE  类型