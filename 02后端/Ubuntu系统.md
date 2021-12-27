```
项目地址：
https://github.com/Joey777210/Socker.git
Ubuntu18.04IP地址：192.168.75.148	127.0.0.1
```



常规事项：

◆如果虚拟机->VM Tools安装变成灰色点击不了，需要先退出系统，将系统CD/DVD、CD/DVD2和软盘设置为自动检测三个步骤，再次重启，则该选项点亮。

◆Ubuntu常用配置

安装VMware tools

配置阿里下载源（不同版本的镜像，配置的源版本也不一样）

安装vim（用gedit也可以，比较方便）

------

◆**Ubuntu系统启动系统权限指令为**：sudu su

◆**Ubuntu退出root权限**：①使用exit	②使用ctrl+D

◆**快速打开终端**： ctrl+alt+t

◆若go显示没有安装，则执行一下$ source ~/.profile

◆**卸载go**	apt-get --purge remove golang-go

◆**下载go**，可自己修改版本	$ curl -O https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz

#### 常用Ubuntu系统命令

##### cd命令

```
进入home界面	使用cd /home/
返回根目录	cd /	
返回上一级目录		cd .. 	
返回上两级目录		cd ../.. 	
返回home目录	cd或cd ~	
```



##### ls命令

```
查看当前路径	使用pwd	
查看文件夹下的文件和文件夹	ls
查看当前路径下的所有文件	使用ls -a
显示当前路径下的所有文件及文件夹的详细信息	ls -l 
```



##### 移动文件

```
sudo cp -rf 文件名 /usr/local
```



##### 光标移动命令

```
光标移到行首	A
光标移到行尾	End
```



##### gedit命令

```
这是 Linux 下的一个纯文本编辑器,但你也可以把它用来当成是一个集成开发环境 (IDE), 它会根据不同的语言高亮显现关键字和标识符。
sudo apt-get update
sudo apt install gedit-gmate
sudo apt install gedit-plugins
sudo apt-get remove gedit
sudo apt install gedit
```



##### 防火墙与端口

```
开启防火墙	sudo ufw enable
查询当前防火墙状态	sudo ufw status
关闭某个端口,如80端口	sudo ufw deny 80
开启某个端口	sudo ufw allow 80

查看服务器运行的进程服务和监听端口	netstat -ntlp
```



##### Git

```
克隆到本地目标位置	git clone xxx.git	Ubuntu目标地址
```



##### Ubuntu卸载软件

```
显示的电脑安装的所有软件	dpkg --list
在终端中找到你需要卸载的软件的名称，列表是按照首字母排序的。
sudo apt-get --purge remove 包名
（--purge是可选项，写上这个属性是将软件及其配置文件一并删除，如不需要删除配置文件，可执行sudo apt-get remove 包名）
```



**读取文件内容及拼接文件**	cat 文件 

**清屏**	clear或ctrl+l

**终止命令**	ctrl+c

**退出vim**	要先按esc退出编辑，再按shift+zz或输入：wq!来退出。

**设置在文件夹打开终端**	sudo apt-get install nautilus-open-terminal	nautilus -q 

**操作文件获取权限**	sudo nautilus

**解压文件夹**	tar -xzvf 文件名

**创建文件夹**	mkdir	文件夹名



#### 常用Go命令

GOROOT就是go的安装路径

GOPATH是作为编译后二进制的存放目的地和import包时的搜索路径 (其实也是你的工作目录, 你可以在src下创建你自己的go源文件, 然后开始工作)。

GOPATH之下主要包含三个目录: bin、pkg、src。bin目录主要存放可执行文件; pkg目录存放编译好的库文件, 主要是*.a文件; src目录下主要存放go的源文件

在项目根目录下执行go build命令来构建你的项目, 构建后会生成hello文件。

当然你也可以直接运行命令go run hello.go来执行程序。

##### 配置GO路径

  需要把几个环境变量添加 profile 文件中（~/.bash_profile 或 /etc/profile）。如果是单用户使用，可以将环境变量添加在 home 目录下的 bash_profile 文件中，如果是多用户使用，需要添加在 /etc/profile 文件。（推荐大家在 /etc/profile 文件中设置环境变量）

使用`vi /etc/profile `命令打开 profile 文件，并将环境变量添加到文件末尾。  

```
export GOROOT=/usr/local/go
export GOPATH=/home/kaiser0830/goproject                                    
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOROOT/bin
export PATH=$PATH:$GOPATH/bin
```



##### Go语言标准库常用的包及功能

| Go语言标准库包名 | 功  能                                                       |
| ---------------- | ------------------------------------------------------------ |
| bufio            | 带缓冲的 I/O 操作                                            |
| container        | 封装堆、列表和环形列表等容器                                 |
| crypto           | 加密算法                                                     |
| database         | 数据库驱动和接口                                             |
| debug            | 各种调试文件格式访问及调试功能                               |
| encoding         | 常见算法如 JSON、XML、Base64 等                              |
| flag             | 命令行解析                                                   |
| fmt              | 格式化操作                                                   |
| go               | Go语言的词法、语法树、类型等。可通过这个包进行代码信息提取和修改 |
| html             | HTML 转义及模板系统                                          |
| image            | 常见图形格式的访问及生成                                     |
| io               | 实现 I/O 原始访问接口及访问封装                              |
| math             | 数学库                                                       |
| net              | 网络库，支持 Socket、HTTP、邮件、RPC、SMTP 等                |
| os               | 操作系统平台不依赖平台操作封装                               |
| path             | 兼容各操作系统的路径操作实用函数                             |
| plugin           | Go 1.7 加入的插件系统。支持将代码编译为插件，按需加载        |
| reflect          | 语言反射支持。可以动态获得代码中的类型信息，获取和修改变量的值 |
| regexp           | 正则表达式封装                                               |
| runtime          | 运行时接口                                                   |
| sort             | 排序接口                                                     |
| strings          | 字符串转换、解析及实用函数                                   |
| time             | 时间接口                                                     |
| text             | 文本模板及 Token 词法器                                      |



##### 基本语法

```
当标识符（包括常量、变量、类型、函数名、结构字段等等）以一个大写字母开头，如：Group1，那么使用这种形式的标识符的对象就可以被外部包的代码所使用（客户端程序需要先导入这个包），这被称为导出（像面向对象语言中的 public）；标识符如果以小写字母开头，则对包外是不可见的，但是他们在整个包的内部是可见并且可用的（像面向对象语言中的 protected ）。

强制规范，需要注意的是 { 不能单独放在一行。

声明变量的一般形式是使用 var 关键字。	var identifier type	         如var b, c int = 1, 2

省略var声明变量v_name := value。这是使用变量的首选形式，但是它只能被用在函数体内，而不可以用于全局变量的声明与赋值。

如果你声明了一个局部变量却没有在相同的代码块中使用它，会得到编译错误。但是全局变量是允许声明但不使用。

空白标识符 _ 也被用于抛弃值，如值 5 在：_, b = 5, 7 中被抛弃。_ 实际上是一个只写变量，你不能得到它的值。这样做是因为 Go 语言中你必须使用所有被声明的变量，但有时你并不需要使用从一个函数得到的所有返回值。

iota，特殊常量，可以认为是一个可以被编译器修改的常量。
iota 在 const关键字出现时将被重置为 0(const 内部的第一行之前)，const 中每新增一行常量声明将使 iota 计数一次(iota 可理解为 const 语句块中的行索引)。

select 语句类似于 switch 语句，但是select会随机执行一个可运行的case。如果没有case可运行，它将阻塞，直到有case可运行。

函数定义        func function_name( [parameter list] ) [return_types] {
                   函数体
                }

当一个指针被定义后没有分配到任何变量时，它的值为 nil。
nil 指针也称为空指针。
nil在概念上和其它语言的null、None、nil、NULL一样，都指代零值或空值。

```

##### Range

```
Go 语言中 range 关键字用于 for 循环中迭代数组(array)、切片(slice)、通道(channel)或集合(map)的元素。在数组和切片中它返回元素的索引和索引对应的值，在集合中返回 key-value 对。

    nums := []int{2, 3, 4}
    sum := 0
    for _, num := range nums {
        sum += num
    }
```

##### Map

```
定义 Map
可以使用内建函数 make 也可以使用 map 关键字来定义 Map:
/* 声明变量，默认 map 是 nil */
var map_variable map[key_data_type]value_data_type

/* 使用 make 函数 */
map_variable := make(map[key_data_type]value_data_type)


delete() 函数
delete() 函数用于删除集合的元素, 参数为 map 和其对应的 key。
/*删除元素*/ 	delete(countryCapitalMap, "France")
```

##### 切片

```
Go 数组的长度不可改变，在特定场景中这样的集合就不太适用，Go中提供了一种灵活，功能强悍的内置类型切片("动态数组"),与数组相比切片的长度是不固定的，可以追加元素，在追加时可能使切片的容量增大。

切片初始化	s :=[] int {1,2,3 } 

切片是可索引的，并且可以由 len() 方法获取长度。
切片提供了计算容量的方法 cap() 可以测量切片最长可以达到多少。

切片不需要说明长度。或使用make()函数来创建切片:
var slice1 []type = make([]type, len)
也可以简写为	slice1 := make([]type, len)
也可以指定容量，其中capacity为可选参数。
make([]T, length, capacity)
这里 len 是数组的长度并且也是切片的初始长度。capacity是切片的最大长度。
append() 和 copy() 函数

如果想增加切片的容量，我们必须创建一个新的更大的切片并把原分片的内容都拷贝过来。
下面的代码描述了从拷贝切片的 copy 方法和向切片追加新元素的 append 方法。
```

##### 并发

```
Go 语言支持并发，我们只需要通过 go 关键字来开启 goroutine 即可。
goroutine 是轻量级线程，goroutine 的调度是由 Golang 运行时进行管理的。

goroutine 语法格式：
go 函数名( 参数列表 )
```

##### 通道

```
通道（channel）是用来传递数据的一个数据结构。
通道可用于两个 goroutine 之间通过传递一个指定类型的值来同步运行和通讯。操作符 <- 用于指定通道的方向，发送或接收。如果未指定方向，则为双向通道。
        ch <- v    // 把 v 发送到通道 ch
        v := <-ch  // 从 ch 接收数据
                   // 并把值赋给 v

声明一个通道很简单，我们使用chan关键字即可，通道在使用前必须先创建：
ch := make(chan int)

通道可以设置缓冲区，通过 make 的第二个参数指定缓冲区大小：
ch := make(chan int, 100)

Go 遍历通道与关闭通道
Go 通过 range 关键字来实现遍历读取到的数据，类似于与数组或切片。格式如下：
v, ok := <-ch
如果通道接收不到数据后 ok 就为 false，这时通道就可以使用 close() 函数来关闭。
```



#### 常用Docker命令

##### docker基础命令

**启动docker**	systemctl start docker

**查看docker信息**	sudo docker info

**查看docker版本**	sudo docker version

##### 卸载docker

systemctl  stop docker

yum -y remove docker-ce

rm -rf /var/lib/docker

##### 配置阿里云加速器

sudo vim /etc/docker/daemon.json	添加内容

```
{
  "registry-mirrors": ["https://58uh725d.mirror.aliyuncs.com"]
}
```

sudo systemctl daemon-reload

##### 镜像

**查看所有镜像**	docker images

![1586790948397](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1586790948397.png)

```
REPOSITORY：表示镜像的仓库源
TAG：镜像的标签
IMAGE ID：镜像ID
CREATED：镜像创建时间
SIZE：镜像大小

同一仓库源可以有多个 TAG，代表这个仓库源的不同个版本，我们使用 REPOSITORY:TAG 来定义不同的镜像。

如果你不指定一个镜像的版本标签，例如你只使用 ubuntu，docker 将默认使用 ubuntu:latest 镜像

 
```

**查找镜像**	docker search image_name

**拉取镜像**	docker pull image_name:tag	可省略tag

**删除镜像**	docker rmi -f 镜像名字ID 

**删除全部镜像**	docker rmi $(docker images -qa)



#### 常用容器命令

##### 创建和删除容器

**创建容器**	sudo docker run -it ubuntu /bin/bash

**容器自定义名称创建**	sudo docker run --name kaiser_container -i -t ubuntu /bin/bash

```
-i标志保证容器中STDIN是开启的，-t是告诉Docker为要创建的容器分配一个伪tty终端。-d: 后台运行容器，并返回容器ID，也即启动守护式容器。
-P: 随机端口映射。
-p: 指定端口映射，有以下四种格式
      ip:hostPort:containerPort
      ip::containerPort
      hostPort:containerPort
      containerPort
      
ubuntu:latest以交互模式启动一个容器,在容器内执行/bin/bash命令。
```



**启动容器**	docker start 容器名或ID



##### 容器查看

**查看当前系统中容器的列表**	docker ps -a

**查看当前系统中正在运行的容器**	docker ps

**查看最后一次运行的容器**	docker ps -1

**启动已经停止的容器**(名称或id都可)	sudo docker start kaiser_container

**重新附着容器会话**（名称或id）	sudo docker attach kaiser_container

**显示系统最后x个容器，无论是否停止**	docker ps -n x

**获取更多容器信息**	sudo docker inspect damon_dave



**容器停止退出**	exit

**容器不停止退出**	ctrl + P + Q 



**停止容器**	docker stop 容器名或ID

**强制停止容器**	docker kill 容器ID或者容器名



**删除容器**(运行中的容器是无法删除的，需要先停止)	sudo docker rm kaiser_container 

**删除全部容器**：

```
docker rm -f $(docker ps -a -q)
或者
docker ps -a -q | xargs docker rm
或者
docker rm `docker ps -a -q`
上面的docker ps命令会列出现有的全部容器，-a标志代表列出所有容器，而-q标志则表示只需要返回容器的ID而不会返回容器的其他信息。这位将容器的列表传给docker rm命令。
```



基于新构建的镜像启动一个容器**：

```
sudo docker run -d -p 80 --name 容器名(static_web) jamtur01/static_web nginx -g "damon off"

基于新构建的镜像，启动一个名为static_web的新容器。指定了-d，告诉docker以分离（detached）的方式在后台进行。
我们也指定了需要在容器中运行的命令：nginx -g "daemon off;"。这将以前台运行的方式启动nginx，来作为我们web服务器。
使用-p标志，该标志用来控制docker在运行时应该公开哪些网络端口给外部（宿主机）
```



**查看容器端口分配情况**	sudo docker ps -l

![1584155206476](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1584155206476.png)

**查看容器的端口映射端口**	sudo docker port id名 端口号

![1584155600117](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1584155600117.png)

**创建容器时指定映射端口**（前面那个是宿主机端口）

```
sudo docker run -d -p 80:80 --name 容器名(static_web) jamtur01/static_web nginx -g "damon off"
```

![1584155745410](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1584155745410.png)

**创建容器时将容器端口绑定到宿主机的ip上**

```
sudo docker run -d -p 127.0.0.1:80:80 --name 容器名(static_web) jamtur01/static_web nginx -g "damon off"
```

**连接容器，查看web服务器内容**

```
curl localhost:49154
Hi, I am in your container
```



##### 重启容器

**重新启动一个容器**	sudo docker restart kaiser_container

如果由于某种错误而导致窗口停止运行，可以通过restart标志来让Docker自动重新启动该容器。restart标志会检查容器的退出代码，并据此来决定是否要重启容器。

```
sudo docker run --restart=always --name daemon_dave -d ubuntu /bin/sh -c "while true;do echo hello world; sleep 1; done"
```



##### 守护式进程

**创建守护式进程**

```
sudo docker run --name daemon_dave -d ubuntu /bin/sh -c "while true;do echo hello world; sleep 1; done"
-d参数会让Docker把容器放到后台运行，命令里使用了一个while循环，会一直打印hello world，直到容器或其进程停止运行。

#使用镜像centos:latest以后台模式启动一个容器
docker run -d centos
问题：然后docker ps -a 进行查看, 会发现容器已经退出
很重要的要说明的一点: Docker容器后台运行,就必须有一个前台进程.
容器运行的命令如果不是那些一直挂起的命令（比如运行top，tail），就是会自动退出的。
这个是docker的机制问题,比如你的web容器,我们以nginx为例，正常情况下,我们配置启动服务只需要启动响应的service即可。例如
service nginx start
但是,这样做,nginx为后台进程模式运行,就导致docker前台没有运行的应用,
这样的容器后台启动后,会立即自杀因为他觉得他没事可做了.
所以，最佳的解决方案是,将你要运行的程序以前台进程的形式运行
```

**停止守护式进程**	

```
sudo docker stop daemon_dave
docker stop命令会向Docker容器进程发送SIGTERM信号。如果你想快速停止某个容器，也可以使用docker kill命令来向容器进程发送SIGKILL信号。
```



##### 容器日志

**用容器日志来查看容器内部在干什么**	sudo docker logs daemon_dave

**退出日志跟踪**	ctrl+c

**获取日志的最后10行内容**	sudo docker logs --tail 10 daemon_dave

**跟踪某个容器的最新日志而不必读取整个日志文件**	sudo docker logs --tail 0 -f daemon_dave

**为日志加上时间戳**	sudo docker logs -ft daemon_dave

```
-t	加入时间戳
-f	跟随最新的日志打印
-tail 数字	显示最后多少条
```

**查看容器内的进程**	sudo docker top daemon_dave



##### 在容器内部运行进程

我们可以通过docker exec命令在窗口内部额外启动新进程，有两种类型：后台任务和交互式任务，后台任务在容器内运行且没有交互需求，而交互式任务则保持在前台保持。

```
sudo docker exec -d daemon_dave touch /etc/new_config_file
这里的-d标志需要运行一个后台进程，-d标志之后，指定的是要在内部执行这个命令的容器的名字以及要执行的命令。上面这条指令会在daemon_dave容器内创建一个空文件，文件名为/etc/new_config_file
```

也可以在daemon_dave容器中启动一个诸如打开shell的交互式任务：

```
sudo docker exec -t -i daemon_dave /bin/bash
上面的指令会在daemon_dave容器内创建一个新的bash会话，有了这个会话，我们就可以在该窗口中运行其他命令了。
```



##### 镜像

镜像保存在仓库中，而仓库存在于Registry中。默认的Registry是由Docker公司运营的公共Registry服务，即Docker Hub。

**查看镜像**	sudo docker images	名称

在仓库名后面加上一个冒号和标签名来指定该仓库中的某一镜像：

```
sudo docker run -t -i --name new_container ubuntu:12.04 /bin/bash
```

**拉取镜像**	sudo docker pull image_name

**查找镜像**	sudo docker search 镜像名

**查询镜像构建信息**	sudo docker history id名或容器名

**删除镜像**	sudo docker rmi jamtur01/static_web

**登录Docker Hub**

```
sudo docker login
Username: xxx
password:xxx
Email:xxx
Login Succeeded
你的个人认证将会保存到$HOME/.dockercfg文件中。
```

**将镜像推送到Docker Hub**

```
sudo docker push jamtur01/static_web
```



##### **Dockerfile**

如果在Dockerfile里指定了CMD指令，而同时在docker run命令行中也指定了要运行的命令，命令行中指定的命令会覆盖CMD指令。

如果Dockerfiler指定了多条CMD指令，也只有最后一条CMD指令会被使用。

**WORKDIR**	从镜像创建一个新容器时，在容器内部设置一个工作目录，ENTRYPOINT和CMD指定的程序会在这个目录下执行。

![1584157055441](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1584157055441.png)

也可以通过-w标志在运行时覆盖工作目录（该命令会将容器内的工作目录设置为/var/log）：

```
sudo docker run -ti -w /var/log ubuntu pwd /var/log
```

**ENV**	用来在镜像构建过程中设置环境变量

```
ENV RVM_PATH /home/rvm/
RUN gem install unicorn
```

**USER**	USER指令用来指定该镜像会以什么样的用户去运行

```
USER nignx
```

**VOLUME**	用来向基于镜像创建的容器添加卷

**ADD**	用来将构建环境下的文件和目录复制到镜像中

COPY	非常类似于ADD，它们根本的不同是COPY只关心在构建上下文复制本地文件，而不会去做提取和解压工作。

ONBUILD	能为镜像添加触发器

#### mosquitto

```
在windows中开启mosquitto	mosquitto.exe -c mosquitto.conf
订阅消息	mosquitto_sub -h localhost -t test -u "kaiser" -P "111"
发送消息	mosquitto_pub -h localhost -t "test" -m "hello world" -u "kaiser" -P "111"
修改mosquitto配置信息		sudo nano /etc/mosquitto/conf.d/default.conf
重启mosquitto		sudo systemctl restart mosquitto
开启mosquitto		mosquitto -c /etc/mosquitto/mosquitto.conf -d
```



##### Ubuntu中配置mosquitto的websocket

```
第一步：安装前准备用到的依赖包：
$ sudo apt-get update
$ sudo apt-get install build-essential python quilt devscripts python-setuptools python3
$ sudo apt-get install libssl-dev
$ sudo apt-get install cmake
$ sudo apt-get install libc-ares-dev
$ sudo apt-get install  uuid-dev
$ sudo apt-get install daemon

第二步：下载并编译安装最新版的libwebsockets
libwebsockets官网：https://www.libwebsockets.org/
GitHub地址：https://github.com/warmcat/libwebsockets
注意：尽量下载最新的libwebsockets包，否则会出现一些莫名其妙的错误
进入libwebsockets文件夹
$ mkdir build
$ cd build
$ cmake ..
$ make install
$ ldconfig
$ cd

第三步：下载并编译安装最新版mosquitto
进入mosquitto目录
更改config.mk，在config.mk的72行左右中将WITH_WEBSOCKETS:=no变成yes（这一步是做WebSocket支持）
$ make
$ make install
$ cp mosquitto.conf /etc/mosquitto
若出现error则使用sudo命令重新执行

第四步：配置Mosquitto能够使用WebSocket
请在/etc/mosquitto/mosquitto.conf 的“Default Listener” 一节添加如下几行：
port 1883
listener 1884
protocol websockets

第五步：运行Mosquitto：
$ mosquitto -c /etc/mosquitto/mosquitto.conf

第六步：安装普通版的Mosquito
指导链接：https://www.howtoing.com/how-to-install-and-secure-the-mosquitto-mqtt-messaging-broker-on-ubuntu-18-04

现在你可以试试使用Websocket客户端来连接你的MQTT服务器的1884端口！！！！！！！
host为mosquitto的域名，在本机上则为localhost
```



#### Ubuntu系统常见问题

##### 修改文件权限提示Operation not permitted

```
首先执行chmod 777 /etc/sysctl.conf时会报出错误：chmod: changing permissions of '/etc/sysctl.conf': Operation not permitted

然后执行命令lsattr /etc/sysctl.conff便可以看到当前文件的属

可以发现当前文件有个i属性，查阅命令帮助文档可以看到有i属性的文件是不能修改的，更不可被删除，即使是root用户也不可

所以相应的解决方案就是把文件的i属性去除，去除i属性：chattr -i /etc/sysctl.conf

然后就可以对此文件内容进行修改

最好在操作完成后恢复文件的i属性，添加i属性：chattr +i /etc/sysctl.conf，然后就完成了
```

