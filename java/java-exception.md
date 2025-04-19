# java Exception（异常处理）

## 两种非正常情况（共同父类`Throwable`）

- `Error` 错误（系统崩溃、虚拟机错误、动态链接失败等，无法恢复或捕获、会导致程序中断）
- `Exception` 异常（可以被捕获并做异常处理）

## 资源回收

- Java垃圾回收机制只能回收堆内存中对象所占用的内存
- Java垃圾回收机制不能释放物理资源（如数据库连接、网络连接和磁盘文件等），需显式回收

## 五个关键字

- try
- catch
- finally
- throw
- throws

## 捕获异常

```java
try { 捕获 }
catch (Exception e) { 异常处理 }
finally { 资源回收 }
```

```java
// 异常独立处理
try { 捕获 }
catch (XxException e1) { 异常处理 }
catch (YyException e2) { 异常处理 }
finally { 资源回收 }
```

```java
// 异常合并处理
try { 捕获 }
catch (XxException | YyException e) { 异常处理 }
finally { 资源回收 }
```

## 抛出异常

- 将指定异常交由方法调用者来处理，方法内不捕获和处理该指定异常

```java
void method () throws XxException, YyException { 方法体 }
```

## 主动异常

- 方法内主动抛出异常实例

```java
void method () {
    try { throw new Exception("不符合设计要求"); }
    catch (Exception e) { 异常处理 }
    finally { 资源回收 }
}
```

## 访问异常信息

- 异常对象常用方法

```java
// 返回错误信息描述
e.getMessage()

// 异常跟踪栈信息输出到标准错误输出
e.printStackTrace()

// 异常跟踪栈信息输出到指定输出流
e.printStackTrace(PrintStream s)

// 返回异常跟踪栈信息
e.getStackTrace()
```

## 自定义异常类

- 应继承`Exception`或`RuntimeException`基类
- 提供两个构造器（无参构造器、字符串参数构造器）
- 调用getMessage()时将返回字符串参数构造器的输入参数

```java
public class MyException extends Exception {
    public MyException() {}
    public MyException(String msg) { super(msg); }
    // 其他自定义方法
}
```

## 常见异常类

- Exception
- SQLException
- IOException
- RuntimeException
- IndexOutOfBoundsException
- NullPointerException
- ClassCastException
