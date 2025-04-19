# java thread（线程）

## 进程和线程

- 进程（`Process`）进程间程序空间、资源上下文独立，调度消耗大
- 线程（`Thread`）线程间共享进程程序空间、资源上下文，调度消耗小

## 并行性和并发性

- 并行性（`Parallel`）同一时刻有多条指令在多个处理器上同时执行
- 并发性（`Concurrency`）多个进程指令被快速轮换执行，而同一时刻仅一条指令执行

## 线程生命周期

### 新建（New）

- 创建实例时 `thread = new Thread()`

### 就绪（Runnable）

- 启动实例时 `thread.start()`

### 运行（Running）

- JVM调度执行时（得到处理器资源）
- 当`yield()`时线程让步、由运行态强制转为就绪态

### 阻塞（Blocked）

- 休眠 `sleep()`
- 等待结束 `join()`
- 挂起 `suspend()`
- 等待资源锁时
- 当`notify()`通知、`resume()`唤醒、阻塞条件消失时再次成为就绪态
- 注意：避免使用`suspend()`容易导致死锁

### 死亡（Dead）

- 停止 `stop()`
- 注意：避免使用`stop()`容易导致死锁

## 线程组（ThreadGroup）

- 同时管理一组线程

## 线程池（ThreadPool）

- 与数据库连接池类似、可有效控制系统中并发线程的数量
- 在系统启动时即创建大量空闲线程，用以执行指定Runnable对象的run()或call()方法

## 线程创建方式

### 继承`Thread`类，重载`run()`方法

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        // this获取当前线程
        this.getName()
    }
}
```

```java
new MyThread().start();
```

### 实现`Runnable`接口，实现`run()`方法

```java
public class MyRunnable implements Runnable {
    public void run() {
        // this无法获取当前线程
        Thread.currentThread().getName()
    }
}
```

```java
MyRunnable target = new MyRunnable()
new Thread(target, "线程名").start();
```

### 实现`Callable`接口，实现`call()`方法

```java
public class MyCallable implements Callable<返回类型> {
    public 返回类型 call() throws Exception {
        // this无法获取当前线程
        Thread.currentThread().getName()
        return 返回值;
    }
}
```

```java
// 由Future接口的实现类FutureTask包装类实例来接收返回值
FutureTask<返回类型> task = new FutureTask<返回类型>(new MyCallable());
new Thread(task, "线程名").start();
// get阻塞直至call执行完成返回
返回类型 ret = task.get();
```

## 线程控制

### 等待线程（`join`）

- 让一个线程等待另一个线程完成
- 线程A调用线程B的`join()`方法时，A将被阻塞，直至B线程执行完为止

### 守护线程（`daemon`）

- 后台线程、守护线程
- 调用Thread对象的`setDaemon(true)`方法可将线程设置为后台线程
- 当所有的前台线程死亡时，后台线程随之死亡
- Thread类提供了`isDaemon()`方法判断指定线程是否为后台线程

### 睡眠线程（`sleep`）

- 让当前正在执行的线程暂停一段时间，并进入阻塞状态
- 通过调用Thread类的静态`sleep()`方法来实现

### 线程让步（`yield`）

- 让当前正在执行的线程暂停，但不会阻塞该线程，而将该线程转入就绪状态
- 通过调用Thread的静态`yield()`方法来实现

### 线程优先级（`priority`）

- Thread.MIN_PRIORITY
- Thread.MAX_PRIORITY
- Thread.NORM_PRIORITY
- 通过调用Thread对象的`setPriority(int)`方法来实现优先级的改变
- 通过调用Thread对象的`getPriority()`方法可查看优先级

## 线程同步（`Synchronized`）

### 线程安全

- 系统对线程的调度具有一定的随机性
- 多个线程访问同一个数据时，容易出现线程安全问题

### 同步代码块

```java
synchronized(obj) { /* 同步代码块 */ }
```

- 对象锁
- obj为被监视的资源
- obj为被多个线程访问的对象，亦可指定为`Object lock = new Object()`创建的锁对象;
- 保证同一时间只有一个线程能执行该段代码

### 同步方法

```java
修饰符 synchronized 返回类型 方法名(参数) { /* 同步方法体 */ }
```

### 同步锁（`Lock`）

- `Lock` 接口
- `ReentrantLock` 实现（可重入锁）
- `ReadWriteLock` 接口
- `ReentrantReadWriteLock` 实现（可重入读写锁）

```java
private final ReentrantLock lock = new ReentrantLock();
// 加锁
lock.lock();
try { /* 需要保证线程安全的代码 */ }
// 释放锁
finally { lock.unlock(); }
```

### 死锁

- 当两个线程相互等待对方释放已获锁权时会发生死锁
- 线程A获得lock1等待lock2、而线程B获得lock2等待lock1时

## 线程通信

### 传统方式

- 由synchronized关键字保证同步
- Object类提供的三个方法wait()、notify()、notifyAll()来实现

### `Condition`方式

- 使用Condition控制线程通信
- 由Lock对象来保证同步、Condition类保持协调
- Condition类提供的三个方法await()、signal()、signalAll()来实现

```java
private final Lock lock = new ReentrantLock();
private final Condition cond = lock.newCondition();
lock.lock();
lock.unlock();
cond.await();
cond.signal();
cond.signalAll();
```

### `BlockingQueue`方式

- 使用阻塞队列BlockingQueue控制线程通信
- 当生产者线程试图向队列中放入元素时，如果队列已满则该线程被阻塞
- 当消费者线程试图从队列中取出元素时，如果队列为空则该线程被阻塞
- put()、take()等方法
- BlockingQueue接口
- ArrayBlockingQueue实现（基于数组）
- LinkedBlockingQueue实现（基于链表）
- PriorityBlockingQueue实现（根据一定优先规则）
- SynchronousQueue实现（基于同步、存取操作必须交替进行）
- DelayQueue实现（根据一定的时限）

## 线程池

### CachedThreadPool

```java
// 具有缓存功能的线程池
ExecutorService pool = Executors.newCachedThreadPool();
```

### FixedThreadPool

```java
// 可重用的具有固定线程数的线程池
ExecutorService pool = Executors.newFixedThreadPool(int);
```

### SingleThreadExecutor

```java
// 单线程的线程池
ExecutorService pool = Executors.newSingleThreadExecutor();
```

### ScheduledThreadPool

```java
// 指定延迟后执行线程任务的线程池
ScheduledExecutorService pool = Executors.newScheduledThreadPool(int);
```

### SingleThreadScheduledExecutor

```java
// 单线程的线程池，可指定延迟执行线程任务
ScheduledExecutorService pool = Executors.newSingleThreadScheduledExecutor(int);
```

### ForkJoinPool

```java
// 支持多CPU多核并行执行的线程池
ForkJoinPool pool = new ForkJoinPool();
```

### 示例

```java
ExecutorService pool = Executors.newFixedThreadPool(6);
pool.submit(new Thread(...));
pool.submit(new Thread(...));
pool.shutdown(); // 关闭线程池
```

## 相关类

### ThreadLocal类

- 线程局部变量
- 为每个线程创建变量的副本，避免并发访问的线程安全问题

```java
private ThreadLocal<String> name = new ThreadLocal<>();
this.name.set()
this.name.get()
```

### Collections类

- 提供以下静态方法包装线程不安全的集合（传入一般集合、返回线程安全的集合）
- ArrayList、LinkedList、HashSet、TreeSet、HashMap、TreeMap等都是线程不安全的

```java
synchronizedCollection(collection)
synchronizedList(list)
synchronizedMap(map)
synchronizedSortedMap(sortedMap)
synchronizedSet(set)
synchronizedSortedSet(sortedSet)
```

### 线程安全的集合类

- java.util.concurrent包下提供支持高效并发访问的集合接口和实现类

```java
// Concurrent开头
ConcurrentHashMap
ConcurrentSkipListMap
ConcurrentSkipListSet
ConcurrentLinkedQueue
ConcurrentLinkedDeque
```

```java
// CopyOnWrite开头，写锁、读不锁
CopyOnWriteArrayList
CopyOnWriteArraySet
```
