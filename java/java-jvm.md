# java-jvm（虚拟机）

## JVM虚拟机（`Java Virtual Machine`）

## 类加载子系统

- 负责从文件系统或者网络中加载Class信息
- 加载的信息存放在一块称之为方法区的内存空间

## 方法区/永久区（`Perm`）

- 静态区
- 存放类信息、常量信息、常量池信息、包括字符串字面量和数字常量等

## Java堆（`Heap`）

- 主要内存工作区域，存放对象实例等，堆空间所有线程共享
- 动态申请、分配
- 划分新生代、老年代两个区域，便于GC做回收

## 直接内存（`Memory`）

- 速度和性能优于Java堆

## Java栈（`Stack`）

- 每个虚拟机线程都有一个私有栈
- 保存局部变量、方法参数、方法调用、返回值等

## 本地方法栈（`Native`）

- 用于本地方法调用JNI（C语言编写的native原生方法）

## 垃圾收集系统（`GC`）

- 垃圾回收（GarbageCollection）、资源释放、内存清理
- 串行收集器（Serial）单线程
- 并行收集器（Parallel）多线程
- 其他收集器（CMS-Concurrent Mark-Sweep、G1-Garbage-First）

## PC寄存器

## 执行引擎

- 负责执行虚拟机字节码

## 虚拟机主要参数（`vm Options`）

### -XX

- `-XX:+PrintGC` 虚拟机启动后只要遇到GC就会打印日志
- `-XX:+PrintGCDetails` 可以查看详细信息，包括各个区的情况
- `-XX:+PrintGCDateStamps` 为GC日志添加时间戳
- `-XX:+UseGCLogFileRotation` 开启GC日志文件的轮替
- `-XX:NumberOfGCLogFiles=5` 指定GC日志文件的数量
- `-XX:GCLogFileSize=20M` 指定GC日志文件的大小
- `-XX:+UseSerialGC` 使用串行回收器
- `-XX:+PrintCommandLineFlags` 显示或隐式配置的VM参数项打印出来
- `-XX:SurvivorRatio=eden/from=eden/to` 设置新生代堆中eden空间和from/to空间的比例
- `-XX-XX:NewRatio=老年代/新生代` 设置新生代堆和老年代堆大小的比例
- `-XX:+HeapDumpOnOutOfMemoryError` 堆空间不足抛出内存溢出错误时导出整个堆信息
- `-XX:HeapDumpPath=路径` 导出堆的存放路径
- `-XX:PermSize=64M` 方法区（永久区）大小
- `-XX:MaxPermSize=64M` 最大方法区（永久区）大小
- `-XX:MaxDirectMemorySize=512M` 最大直接内存大小（默认值为最大堆空间）
- `-XX:+UseStringDeduplication` 开启JVM字符串去重功能，有助于减少堆内存的占用
- `-XX:MetaspaceSize=256m` 设置初始元空间大小，元空间用于存放类元数据
- `-XX:MaxMetaspaceSize=512m` 设置最大元空间大小，以限制其无限增长可能导致的问题

### -Xlog

- `-Xlog:gc` 启用GC日志
- `-Xloggc:/var/log/myproj/myapp-gc.log` 将GC日志写入指定文件

### -Xms

- `-Xms128m` 初始堆内存大小

### -Xmx

- `-Xmx512m` 最大堆内存大小

### -Xmn

- `-Xmn50m` 新生代堆大小（影响老年代堆大小）

### -Xss

- `-Xss10m` 最大栈空间大小（决定了函数可调用的最大深度）
