**GOROOT和GOPATH的区别和含义：**

GOROOT是go的安装路径

执行go命令配置要用的 %GOROOT%\bin



GOPATH的路径go install 和go get都要用到GOPATH环境变量

GOPATH是作为编译后的二进制的存放默地的和import包时的搜索的路径

GOPATH其实也是你的工作路径，可以在src文件下写你自己的go源文件

GOPATH路径下有3个文件pkg、bin、src文件

bin目录存可执行文件；pkg目录存放编译好的库文件，主要是*.a文件；src目录下主要存放的go的源文件



**GOPATH和GOMODULE的区别开发流程的区别：**

GOPATH无法解决版本依赖问题，GOPATH因为第三方库很容易发生变化，以往解决办法是通过引入了vender机制，导致依赖寻找的顺序变成了vender ->GOROOT ->GOPATH，go mod不需要vender机制，go mod自己管理依赖

GOPATH开发过程项目必须在src目录下才能编译，否则找不到程序，而go mod可以不在src目录下开发，可以在任意目录下开发





**go包的循环引用问题**：https://blog.csdn.net/ggq89/article/details/81148558?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase



**俩种方式解决：**

一种是拆包：适用于软依赖——也就是package a去调用了package c的方法，package c调用了package a的方法，这种属于软依赖的，具体做法是抽取其中一个package调用的方法，新建另外一个包去定义实现这个方法，然后让package依赖这个包，从而不会产生一个环的包引用。

第二种是定义接口：适用于硬依赖——硬依赖是指package a和package b有彼此的指针，这种属于硬依赖，具体做法是定义一个a接口在b package中，将所有在b中用到了package的变量或者方法转换为使用a接口的方法，然后在package a中实现package b中的a 接口的方法



**go引用外部依赖的几种方式：**

### go get

确保你的GOPATH是工程目录，代码在src目录下，然后在命令提示符中输入：go get github.com/astaxie/beego，然后在本地的src下就生成了要引入的外部包。

 注意：在使用GoLand工具时，配置settings->Go->GOPATH->Project GOPATH为当前工程目录

### go module

Go 的 1.11版本以上才能使用Go Module，1.13版本以下Go Module默认关闭，

​    首先需要设置环境变量 set GO111MODULE=on，新建项目文件夹，进入新建路径执行go mod init，在文件夹下生成go.mod文件，然后将需要引入外部包的go文件置于项目目录下，编译文件，就会把外部包下载到本地的GOPATH/pkg/mod目录下

​    注意：在使用GoLand工具时，不要配置Project GOPATH为当前工程目录，最好不要配置Project GOPATH，而是配置Module GOPATH

### vendor目录

​     首先安装govendor : **go get -u -v github.com/kardianos/govendor，**下载完，配置环境变量GOPATH/bin，键入命令

**govendor -version** 检查是否安装成功。

​     在GOPATH/src的目录下，新建项目文件夹，进入新建路径执行gogovendor init，就会在文件夹下生成vendor/vendor.json。

​     然后将需要引入外部包的go文件置于项目目录下， 使用命令**govendor fetch github.com/golang/glog** 将外部文件下载到本地vendor/下，并在vendor.json中添加该依赖包的信息，其中govendor fetch是从从远端库添加依赖包，而从 $GOPATH 中添加依赖包，使用govendor add