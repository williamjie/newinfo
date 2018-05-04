subtext lime 
mac竖排选择
鼠标左键＋Option
－或者鼠标中键
－增加选择：Command，减少选择：Command+Shift

## 体系说明
点：
线：
面：
体：
快速发现解决问题能力：
创新解决问题能力：
推广技术方案能力：


## 业务快速迭代
业务稳定性
业务灾备（快速恢复）
雪崩等极端情况，提供基本服务。
新技术的应用以及老旧系统处理。
人员配置：前端，后端，测试，产品，运营等；
A岗 B岗
后备人员培养

------出现问题需要解决问题，先回答三个问题：
1.需求提出者需要解决什么问题
2.你解决的是什么问题
3.有没有更加好的办法

高可用是如何实现，如何保证高可用
高性能是如何实现，瓶颈在哪里

## 工具使用
### redis 
string list  hash set sortset
### mongdb
### grafna+statd
### phxqueue分布式消息队列（研究下）

# 前端
## JS
### vue 界面button 等可以使用原生功能
### vue 优点以及缺点：vue是MVVM框架,最主要是mvc，mvp 中的c 以及P 改为viewModel（数据直接与界面交互，关注业务逻辑，降级复杂度）
MVX框架模式：MVC+MVP+MVVM 
MVC：Model(模型)+View(视图)+controller(控制器)，主要是基于分层的目的，让彼此的职责分开
MVP：是从MVC模式演变而来的，都是通过Controller/Presenter负责逻辑的处理+Model提供数据+View负责显示。在MVP中，Presenter完全把View和Model进行了分离，主要的程序逻辑在Presenter里实现
MVVM：MVVM是把MVC里的Controller和MVP里的Presenter改成了ViewModel。Model+View+ViewModel。
MVVM模式的框架有：AngularJS+Vue.js和Knockout+Ember.js后两种知名度较低以及是早起的框架模式。



###### vue <div> 模块编辑，界面显示，通过初始化全部隐藏；部分全部显示来展示。
###### vue webpack 打包原理
  
###### 浏览器根据返回文件格式或者返回文件后缀名解析文件

##### html

##### css样式


## 客户端
安卓
IOS

## 后端
【golang】
1.hashmap结构
2.def  iterface
3.channel类型 <- 接收以及发送；阻塞；Range；select；timeout；ticker（定时器）；close

## C++

## java
##### hashmap
##### jvm垃圾回收；
##### jvm性能调优
##### java spring框架（ioc aop） 
##### java spring boot 框架可以直接mvn test package    java -jar xxx.jar 执行；web服务器超级方便；
##### java 代理  （1.静态代理 2.动态代理 3.Cglib代理）
##### 以及反射
##### synchronized 关键词
##### hashmap 结构
##### jvm优化：常见内存溢出   堆 栈 垃圾回收
##### 进程和线程区别异同

根据垃圾回收机制的不同，java堆有可能拥有不同的结构，常见的java堆分为新生代和老年代，目前还有永久代。其中新生代存放刚创建的对象及年龄不大的对象，老年带存放着在新生代中经历过多次回收后还存在的对象。
对象晋升过程：
新生代分为eden区s0,s1区（from，to）。多数情况下对象首先分配在eden区，在一次新生代回收后，存活下来的对象存入s0或s1区。每经过一次新生代的回收，对象的年龄加1。默认情况下年龄达到15的对象将晋升至老年代。如果在第一次回收的时候，存活的对象大于s0（s1）空间，将直接晋升至老年代，如果在为对象第一次分配空间时，对象空间大于eden空间的话，对象也直接分配到老年代。
（1）堆溢出：设置-Xmx调整最大可用堆空间
（2）直接内存溢出：可能是系统内存空间不足，同时没达到参数默认的上限，没有触发GC导致OOM，解决方法是通过-XX:MaxDirectMemorySize 来限制最大内存
(3)过多线程导致OOM：由于每开启一个线程都会给这个线程分配一个栈，因此当线程数达到一定程度，系统空间不足的时候就会内存溢出，可以尝试减少堆空间，或者可以通过设置参数-Xss限制每个栈的大小。
(4)永久区溢出：系统加载的类过多，导致永久区溢出，通过-XX:MaxPermSize来设置永久区最大可用空间。
(5)GC效率低下引起的OOM：GC是内存回收的关键，回收效率低很有可能引起内存溢出，可以通过合理的分配堆（包括新生代和老年代）空间去解决。

String造成的内存泄漏
内存泄漏是指，不再使用的对象占据内存不释放，导致可用内存不断减小，最终引起内存泄漏。在Java1.6中String.subString()方法就存在这样的问题。


## 机器linux性能调优：
top
iostat
free

### 技巧
非实时按秒统计QPS
cat access.log | awk -F '[' '{print $2}' | awk '{print $1}' | sort | uniq -c |sort -k1,1nr



## 存储
oracle
mysql
mongdb
PQ
redis
tair


## 算法数据结构：
二叉树，排序算法
哈希表
（左程云）算法1：实现一个特殊的栈，在实现的栈的基础功能上，再实现返回栈的最小元素的操作（要求1：pop，push，getMin 操作时间复杂度为O(1),设计的栈结构可以使用现成的栈结构）



## 网络传输
TCP：
tcp三次握手以及四次挥手，tcp黏连出现解决
UPD
HTTP：
http协议各个常用字段以及返回值意义
http GET POST 区别

## 架构
前中后
分层架构



## 项目说明：
消息推送系统：用户中心设备列表（快队列，慢队列） 日志系统  CMS系统，日志查询；
消息的推送保证（conn与sdk保障，sdk回复，删除消息；否则一直存储，离线消息以及在线消息；消息推送列表，用户可以直接查看，所有消息。）
消息一致性保证，消息分级；
完整短信系统；防止雪崩，降级发送，容灾，异常处理，日志记录；

短信系统：选型golang redis做队列；（本地redis队列和远端redis队列做缓存）灾备考虑

读取p12文件命令
keytool -list -v -keystore etj.p12 -storepass 123456 -storetype PKCS12

Kafka是最初由Linkedin公司开发，是一个分布式、分区的、多副本的、多订阅者，基于zookeeper协调的分布式日志系统（也可以当做MQ系统），常见可以用于web/nginx日志、访问日志，消息服务等等，Linkedin于2010年贡献给了Apache基金会并成为顶级开源项目。
主要应用场景是：日志收集系统和消息系统。
Kafka主要设计目标如下：
1.以时间复杂度为O(1)的方式提供消息持久化能力，即使对TB级以上数据也能保证常数时间的访问性能。
2.高吞吐率。即使在非常廉价的商用机器上也能做到单机支持每秒100K条消息的传输。
3.支持Kafka Server间的消息分区，及分布式消费，同时保证每个partition内的消息顺序传输。
4.同时支持离线数据处理和实时数据处理。
