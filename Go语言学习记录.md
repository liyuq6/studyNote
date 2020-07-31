go语言标准库：https://studygolang.com/pkgdoc

go语言学习链接：http://shouce.jb51.net/gopl-zh/ch1/ch1-01.html

**go build -o "执行文件的名字"**





**CGO_ENABLED=0//禁用CGO**

**SET GOOS=linux //linux平台  windows  **

**SET GOARCH=AMD64   **

SET GOARCH=AMD64   

**SET GOOS=linux** //linux平台  GOOS=linux **SET GOARCH=AMD64   

**SET GOARCH=AMD64**   

**go build**    //会编译生成一个可以直接运行于linux系统下的执行文件



**go基本数据类型**:https://www.cnblogs.com/sunshineliulu/p/11616495.html

```go
%d          十进制整数
%x, %o, %b  十六进制，八进制，二进制整数。
%f, %g, %e  浮点数： 3.141593 3.141592653589793 3.141593e+00
%t          布尔：true或false
%c          字符（rune） (Unicode码点)
%s          字符串
%q          带双引号的字符串"abc"或带单引号的字符'c'
%v          变量的自然形式（natural format）
%T          变量的类型
%%          字面上的百分号标志（无操作数
```



**os库的常用方法详解**：https://blog.csdn.net/BigData_Mining/article/details/89881171



**注意——简短变量声明语句中必须至少要声明一个新的变量**



go run ./ 等同于 go run *.go （windows支持的是./）



**iota是golang语言的常量计数器,只能在常量的表达式中使用。**

**const 常量碰到iota时 iota初始为0,const里面每出现一次变量声明iota都会迭代一次，类似枚举**

```go
const（

a1 = iota //初始值为0

a2 //1

a3 //2

）
const(
_ = iota
KB = 1 <<(10*iota) //代表1左移10位，代表2^10 这里是2进制不是10进制
MB = 1 <<(10*iota) 2^20
)
```

%d表示十进制的整型  

%b表示二进制

%o表示八进制

%0x表示16进制

%T查看类型

%v默认类型

fmt.Println("%x\n",i1)



**GO默认小数都是float64**

float32类型的值不能直接赋值给float64类型的值

int类型和string类型的互相之间的转换使用到的包：“strconv“ 

使用例子：https://blog.csdn.net/zf766045962/article/details/105102622/

strconv包的详解：https://blog.csdn.net/xiaobafacai/article/details/77924491

fmt.Sprintf("%s%s",name,world) //字符串拼接

rune 表示中文类型 代表一个utf-8字符

byte的类型——unit8





**自动补充类型**：有error和bool型

error例如：os.Open（文件绝对路径）自己练习发现，其实fm.Scan和fmt.Scanln也会多返回一个error类型

bool例如：

```Go
v, ok = m[key]             // map lookup
v, ok = x.(T)              // type assertion
v, ok = <-ch               // channel receive
```



**go的键盘输入的几种方式：**

**bufio的os.Stdin对应的ReadLine()**

```go
func getInput() string {
	//使用os.Stdin开启输入流
	//函数原型 func NewReader(rd io.Reader) *Reader
	//NewReader创建一个具有默认大小缓冲、从r读取的*Reader 结构见官方文档
	in := bufio.NewReader(os.Stdin)
	//in.ReadLine函数具有三个返回值 []byte bool error
	//分别为读取到的信息 是否数据太长导致缓冲区溢出 是否读取失败
	str, _, err := in.ReadLine()
	if err != nil {
		return err.Error()
	}
	return string(str)
}
```

**bufio的os.Stdin对应的Scan()**

```go
func getInputByScanner() string {
	var str string
	//使用os.Stdin开启输入流
	in := bufio.NewScanner(os.Stdin)
	if in.Scan() {
		str = in.Text()
	} else {
		str = "Find input error"
	}
	return str
}
```

**fmt的Scanf**

```go
func getInputByFmt() string {
	//定义变量
	var str string
	//Scanf函数读取输入到变量中 两个返回值
	//分别为读取到的长度 失败信息
	length, err := fmt.Scanf("%s", &str)//注意使用%s读取输入字符串只能读取到空白符之前
	if err != nil {
		return err.Error()
	}
	fmt.Println("Read length is ", length)
	return str
}
```

**管道详解**：https://www.cnblogs.com/yetuweiba/p/4365488.html

chan  <-

**位运算**：https://www.cnblogs.com/yrjns/p/11246163.html

a10 := [...]int{0,1,2,5,4,9,6}自动推断有多少个数

**根据索引初始化**

a3 : = [5] int{0:1,4:2}//1，4都是索引的方式赋值

切片一旦扩充就是翻倍容量	

**切片的扩容机制**：https://blog.csdn.net/jayzym/article/details/104800977/

切片扩容对于不同数据类型的扩容方式也是不同的

切片的a[：4]是取不到最后的

字节切片的比较可用高效的bytes.Equal函数进行比较

其他类型的切片就需要自己进行展开比较



slice := make([]int, 3)[2:] //代表从底层数组下标为2的位置开始，其容量和长度都是1 ，切片为【0】



**make和new的区别：**

make和new都是用来申请内存的。

make只用来申请引用类型的内存申请：chan，切片，map，返回的是类型本身

new很少用，一般用来给基本数据类型申请内存，这个返回的是对应类型的指针



go doc builtin.方法名查看源码解释

**常用的go学习网站**：https://studygolang.com/pkgdoc

fmt.Sprintf("stu%02d",i) stu00~stu99



map和slice的组合：

元素类型为map的切片——var s1 = make([]map[int]string，10，10)

注意要初始化才能用：s[0] = make(map[int]string,1) 这还只是单次的初始化，完全初始化的话是要使用for循环对所有的数组进行对应的初始化map

值为切片类型的map

var s2 = make(map[string]\[]int,3)



判断是否是汉字——if unicode.Is(unicode.Han){}



**defer 后面的接的表达式表示延迟执行，后面的表达式会在程序执行即将退出之前执行** 

**如果多条defer语句按顺序后进先出**



**go语言中的return操作：return操作不是原子性的**

**1.首先是返回值赋值**

**2.如果有defer先做defer操作**

**3.真正的ret返回**



变量的作用域：

1.全局作用域

2.函数作用域：

​	1.先在函数内部找变量，找不到往外层找

​	2.函数内部的变量，外部是访问不到的

3.代码块作用域



匿名函数就是没有名字的函数，一般用于函数内部，因为函数内部是不能声明有名字的函数的



函数定义的最后加括号代表立即执行函数数 func(){}()



函数的闭包：闭包是一个函数，它包含了外部作用域的变量

底层原理：1.函数可以作为返回值

2.函数内部查找顺序是由内而外，先在内部找，找不到就去外部找





匿名成员：只给出一个类型不给出名字，可以通过简短访问去访问匿名成员，用在结构体的嵌套，不用大写声明为导出也可以进行访问

```Go
type Point struct {
    X, Y int
}
type Circle struct {
    Point
    Radius int
}

type Wheel struct {
    Circle
    Spokes int
}
var w Wheel
w.X = 8            // equivalent to w.Circle.Point.X = 8
w.Y = 8            // equivalent to w.Circle.Point.Y = 8
w.Radius = 5       // equivalent to w.Circle.Radius = 5
w.Spokes = 20
//不提供简短表示匿名成员的语法
w = Wheel{8, 8, 5, 20}                       // compile error: unknown fields
w = Wheel{X: 8, Y: 8, Radius: 5, Spokes: 20} // compile error: unknown fields
```

到目前为止，我们看到匿名成员特性只是对访问嵌套成员的点运算符提供了简短的语法糖。稍后，我们将会看到匿名成员并不要求是结构体类型；其实任何命名的类型都可以作为结构体的匿名成员。但是为什么要嵌入一个没有任何子成员类型的匿名成员类型呢？

答案是匿名类型的方法集。简短的点运算符语法可以用于选择匿名成员嵌套的成员，也可以用于访问它们的方法。实际上，外层的结构体不仅仅是获得了匿名成员类型的所有成员，而且也获得了该类型导出的全部的方法。这个机制可以用于将一个有简单行为的对象组合成有复杂行为的对象。组合是Go语言中面向对象编程的核心，



结构体中的大写字母代表导出



**编组：结构体slice转成JSON的过程叫做编组**

编组使用的函数是 json.Marshal(结构体slice) ——返回的是一个对象加一个err

```Go
data, err := json.Marshal(movies)
if err != nil {
    log.Fatalf("JSON marshaling failed: %s", err)
}
fmt.Printf("%s\n", data)
```

将json格式化输出json.MarshalIndent（jsondata，a,b）a代表每一行输出的前缀 ，b代表每一层级的缩进

```Go
json.Unmarshal(data, &titles)
```

将json字符反转转成结构体slice，可以选择只接受部分json成员，不要其他的成员

流式的json的解码器：json.Decoder



**GitHub的Web服务接口 https://developer.github.com/v3/** 



Sprintf是把格式化的数据写入到某个字符串中。返回值为字符串的长度

fprintf是用于文件操作的



```Go
// prereqs记录了每个课程的前置课程
var prereqs = map[string][]string{
    "algorithms": {"data structures"},
    "calculus": {"linear algebra"},
    "compilers": {
        "data structures",
        "formal languages",
        "computer organization",
    },
    "data structures":       {"discrete math"},
    "databases":             {"data structures"},
    "discrete math":         {"intro to programming"},
    "formal languages":      {"discrete math"},
    "networks":              {"operating systems"},
    "operating systems":     {"data structures", "computer organization"},
    "programming languages": {"data structures", "computer organization"},
}
```





os类的文件操作：

```go
func main()  {
   //1.创建一个目录,仅创建一层
   //err:=os.Mkdir("C:\\liu\\pro\\aa", 0666)
   //fmt.Println(err)
   //2.创建一个目录，可以多层
   //err = os.MkdirAll("C:\\liu\\pro\\bb\\cc" , 0666)
   //fmt.Println(err)

   //3.创建文件
   //file, err:=os.Create("C:\\liu\\pro\\bb\\cc\\ee.txt")
   //fmt.Println(err) //open C:\liu\pro\bb\cc\dd\ee.txt: The system cannot find the path specified.
   //fmt.Println(file) //<nil>

   // 4.删除：慎用，慎用，再慎用。。
   // remove C:\Ruby\pro\bb: The directory is not empty.
   //err := os.Remove("C:\\liu\\pro\\bb\\cc\\ee.txt") // bb\\cc\\ee.txt
   //fmt.Println(err)
   //删除文件或目录，无论目录中是否有内容
   //err:=os.RemoveAll("C:\\liu\\pro\\bb")
   //fmt.Println(err)

   //5.打开文件,当前程序和本地aa.txt文件之间建立了一个链接。。
   file,err:=os.Open("C:\\liu\\pro\\aa.txt")
   fmt.Println(err)
   fmt.Println(os.IsExist(err)) //false
   fmt.Println(os.IsNotExist(err)) //true
   fmt.Println(file)
   // 6.关闭文件
   defer file.Close()//断开程序和文件之间的链接，释放资源。
   // 读操作，写数据。。。


}
```



下面的声明语句，Celsius类型的参数c出现在了函数名的前面，表示声明的是Celsius类型的一个名叫String的方法，该方法返回该类型对象c带着°C温度单位的字符串：

```Go
func (c Celsius) String() string { return fmt.Sprintf("%g°C", c) }
```



**自定义类型：**

**类型别名：**

```go
type myInt = int
```



方法附加：只要底层类型不是指针或者接口即可



go语言封装的优点：

首先，因为调用方不能直接修改对象的变量值，其只需要关注少量的语句并且只要弄懂少量变量的可能的值即可。

第二，隐藏实现的细节，可以防止调用方依赖那些可能变化的具体实现，这样使设计包的程序员在不破坏对外的api情况下能得到更大的自由。

封装的第三个优点也是最重要的优点，是阻止了外部调用方对对象内部的值任意地进行修改。因为对象内部变量只可以被同一个包内的函数修改，所以包的作者可以让这些函数确保对象内部的一些值的不变性



字符串常用拼接：

```go
var bt bytes.Buffer

var bt bytes.Builder

bt.WriteString(s1)

bt.WriteString(s2)

s3 : =bt.String()
```



**fmt包详解：**https://www.cnblogs.com/Survivalist/articles/10287297.html



**指针接收者和值接受者的区别：**

值接受者：无论你传入的是值还是指针都可以使用，同时要注意值接受者传入你在方法里面进行的修改是修改不了原来的变量的。

指针接受者：只能接受指针的传入，指针接受者可以修改原来的变量的值。

![image-20200720091529232](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200720091529232.png)

**动态值和动态类类型：**

接口的类型可以接收赋值给他的实现类型：a=c2     //动态值

赋值之后的类型会变成main.cat类型或者*main.cat类型  // 动态类型





文件读写：

三种读文件操作的：os.Open(fileName)

**第一种：length，err :=fileObject.Read(接受文件内容的参数)**

```go
func main() {

  fileObject, err := os.Open("D:/GO/goFileTest/aaa.txt")

  if err != nil {

​    fmt.Printf("open file failed ,err :%v", err)

​    return

  }

  //关闭文件

  defer fileObject.Close()

  //读取文件内容

  var temp [128]byte

  length, err := fileObject.Read(temp[:])

  if err != nil {

​    fmt.Printf("read from file failed,err:%v", err)

​    return

  }

  fmt.Println("读取了%d个字节\n", length)

  fmt.Println(string(temp[:length]))

}
```

**第二种：reader :=bufio.NewReader(fileObject)**

line ,err: =reader.ReadString('\n')

与第一种的区别一个是第一种的直接Read的方法返回值是长度，这个bufio的Read是返回一行读取到的文件内容。

第二个区别是第一个是可以控制自己想要读多少字的，第二种是直接读取一行的内容



**第三种：io/ioutil包的读取** 

ret ,err:= ioutil.ReadFile(文件名的路径) 这种的区别就是一次将整个文件的内容全部读取进来了



文件写权限：https://studygolang.com/articles/5024

O_RDONLY：只读模式(read-only)
O_WRONLY：只写模式(write-only)
O_RDWR：读写模式(read-write)
O_APPEND：追加模式(append)
O_CREATE：文件不存在就创建(create a new file if none exists.)
O_EXCL：与 O_CREATE 一起用，构成一个新建文件的功能，它要求文件必须不存在(used with O_CREATE, file must not exist)
O_SYNC：同步方式打开，即不使用缓存，直接写入硬盘
O_TRUNC：打开并清空文件



文件的写操作：

1.fileObject.Write()

fileObject.WriteString()



2.writer := bufio.NewWriter(fileObject)

writer.WriterString("")



3.ioutil

str := "hello word"

err := ioutil.WriteFile("fileName",[]byte(str),0666)

在文件的中间位置去写，首先权限设置成os.O_RDWR (可读可写)

fileObject.Seek(1,0)    ab   ab中间的位置，如果是

a

b

Seek(3,0)windows后面是会有/r /n的



time类：time.Now()    //获取当前时间

time.Unix  //获取时间戳 对应的是秒

time.UnixNano   //纳秒时间戳

time.Unix(时间戳，0) 得到的是一个time对象



v=reflect.TypeOf(x)   //反射类得到x的具体类型

v.name()  //类型名字 如cat

v.kind()  //真正的类型  如struct



ValueOf().elem().setInt(200)  //获取指针进行修改参数的值

reflect.ValueOf(a).IsNil()  //判断指针是否为空

reflect.ValueOf(a).IsValid()  //判断值是否为空

reflect.ValueOf(b).MethodByNaName("abc").IsValid() //判断该结构体是否含有abc方法

reflect.ValueOf(b).FieldByNaName("abc").IsValid() //判断该结构体是否含有abc成员

reflect.ValueOf(b).MapIndex(reflect.ValueOf("key")).Isvalid()  //尝试在map中查找一个不存在的key



t:=reflect.TypeOf(stu1)

t.Numfield()//获取结构体的成员数量

field :=t.Field(i)  //获取每个成员变量

field.Name   //获取对应的成员名字

field.Index,    //获取对应的下标

field.Type,     //获取对应的类型

field.Tag.Get("zhoulin") //获取json tag映射的值

![image-20200723105910558](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200723105910558.png)

![image-20200723105927630](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200723105927630.png)

![image-20200723110321653](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200723110321653.png)

![image-20200723110335049](C:\Users\ZONST\AppData\Roaming\Typora\typora-user-images\image-20200723110335049.png)



strconv类：

strconv.parseInt(str,10,32)//表示将字符串转化为int32位的十进制类型的数，但是返回的是一个int64位的数，加一个err，是为了防止数据的丢失，之后类型可以转换不丢失数据

strconv.Atoi（str）//字符串转数字，返回int类型，加一个err

strconv.Itoa(i)  //数字转字符串

ParseBool(str)/Float //字符串转bool



groutine 一定要指定为一个函数，要使用go去开启一个groutine

如何判断groutine结束了用的是sync.WaitGroup



goroutine和线程

os线程（操作系统线程）一般独有固定的栈内存（通常为2MB），一个goroutine的栈在其生命周期开始时只有很小的栈（典型情况下时2KB），goroutine的栈不是固定的，他可以按需增大和缩小，goroutine的栈大小限制可以达到1GB，虽然极少会用到那么打。所以说GO语言中一次可以创建十万左右的goroutine也是可以的。

