# java IO（输入输出）

## File 类

### 功能

- 访问文件和目录（新建、删除、重命名等）
- 访问文件内容（读、写等）时需使用输入、输出流

### 访问文件名相关方法

- `getName()` 名称
- `getPath()` 路径
- `getParent()` 上级目录
- `getAbsoluteFile()` 转成绝对路径对象
- `getAbsolutePath()` 返回绝对路径
- `renameTo(File newName)` 重命名

### 文件检测相关方法

- `exists()` 存在
- `canWrite()` 可写
- `canRead()` 可读
- `isFile()` 文件
- `isDirectory()` 目录
- `isAbsolute()` 绝对路径

### 获取常规文件信息

- `lastModified()` 最后修改时间
- `length()` 文件大小

### 文件操作相关方法

- `createNewFile()` 创建文件
- `delete()` 删除文件或目录
- `createTempFile(prefix, suffix=".tmp")` 创建临时文件
- `createTempFile(prefix, suffix=".tmp", directory)` 创建临时文件
- `deleteOnExit()` 注册一个删除钩子，当JVM退出时删除File对象所对应的文件和目录

### 目录操作相关的方法

- `mkdir()` 创建目录
- `list()` 可接收一个`FilenameFilter`参数对列出的文件进行过滤，返回`String[]`
- `listFiles()` 文件列表，返回`File[]`
- `listRoots()` 列出系统所有根路径，返回`File[]`

### 文件过滤（FilenameFilter接口）

```java
class MyFilenameFilter impements FilenameFilter {
    public boolean accept(File dir, String name) {
        // 按需调整
        return name.endsWith(".java") || new File(name).isDirectory();
    }
}

File file = new File(".");
String[] nameList = file.list(new MyFilenameFilter());
```

## 字节流（8bits）

### 字节流抽象类

- `InputStream`
- `OutputStream`
- `FilterInputStream` 过滤输入
- `FilterOutputStream` 过滤输出

### InputStream 实现

- `FileInputStream` 访问文件
- `ByteArrayInputStream` 访问数组
- `PipedInputStream` 访问管道
- `BufferedInputStream` 缓冲流
- `ObjectInputStream` 对象流，反序列化（Deserialize）

### OutputStream 实现

- `FileOutputStream`
- `ByteArrayOutputStream`
- `PipedOutputStream`
- `BufferedOutputStream`
- `ObjectOutputStream` 对象流，序列化（Serialize）

## 字符流（16bits）

### 字符流抽象类

- `Reader`
- `Writer`
- `FilterReader` 过滤读
- `FilterWriter` 过滤写

### Reader 实现

- `FileReader`
- `CharArrayReader`
- `PipedReader`
- `BufferedReader`
- `StringReader` 访问字符串
- `InputStreamReader` 转换流

### Writer 实现

- `FileWriter`
- `CharArrayWriter`
- `PipedWriter`
- `BufferedWriter`
- `StringWriter`
- `OutputStreamWriter` 转换流

## IO、NIO、NIO.2

### IO

- 阻塞型（Block IO）
- `java.io`包相关
- 面向流的处理（每次只能处理一个字节或一个字符）
- `File`、`InputStream`、`OutputStream`、`Reader`、`Writer`等相关类

### NIO

- 从JDK 1.4开始，Java提供了一系列改进的输入/输出处理的新功能
- `java.nio`包相关（New IO）
- `java.nio.channels`、`java.nio.charset`子包相关
- 新增`Buffer`（缓冲）、`Channel`（通道）两个核心对象实现面向块的处理
- 写数据 `->` Buffer（块）`->` Channel（输入、输出、映射）`->` Buffer（块）`->` 读数据
- `Charset`字符集工具类（进行字符编解码）
- 阻塞型（Block IO）

#### Buffer 抽象

- ByteBuffer
- CharBuffer
- ShortBuffer
- IntBuffer
- LongBuffer
- FloatBuffer
- DoubleBuffer
- 主要方法：put()、get()、clear()

```java
// 创建一个指定容量的Buffer对象
static XxxxBuffer allocate(int);
```

#### Channel 接口

- 必须通过Buffer进行数据读写
- 主要方法：map()、read()、write()

```java
FileChannel inChannel = new FileInputStream(xxx).getChannel();
FileChannel outChannel = new FileOutputStream(xxx).getChannel();
```

### NIO.2

- Java 7对原有的NIO进行重大改进，提供了全面的文件IO和文件系统访问支持，基于异步Channel的IO
- `java.nio.file`包相关（包含监控文件系统功能）
- `java.nio.channels`包相关（异步通道实现）
- 非阻塞型（Non-Block IO）
- 异步型（Asynchronous IO）
