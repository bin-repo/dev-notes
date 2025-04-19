# java

## 术语

### `JVM`（Java Virtual Machine）虚拟机

- 提供统一标准（指令集、寄存器、类文件格式、栈、垃圾回收堆、存储区等）最终实现平台无关性

### `JDK`（Java SE Development Kit）开发包

- 包含Java编译器、Java运行时环境、常用Java类库等

### `JRE`（Java Runtime Environment）运行时环境

- 包含JVM、类加载器、字节码校验器及大量的基础类库

### `GC`（Grabage Collection）垃圾回收

### `OO`（Object-Oriented）面向对象

三个基本特征

- 封装（Encapsulation）
- 继承（Inheritance）
- 多态（Polymorphism）

### `OOA`（Object-Oriented Analysis）面向对象分析

### `OOD`（Object-Oriented Design）面向对象设计

### `OOP`（Object-Oriented Program）面向对象编程

### `UML`（Unified Modeling Language）统一建模语言

- 用于描述并记录OOA、OOD
- UML2.0包括13种类型图形
- 常用7种（用例图、类图、组件图、部署图、顺序图、活动图和状态机图）

### `AWT`（Abstract Window Toolkits）抽象窗口工具集

- 用于构建图形用户界面（GUI）程序

### `JAR`（Java Archive File）档案文件

- 压缩文件，亦称JAR包，由jar工具进行压缩
- 与普通压缩文件ZIP的区别在于包含一个名为META-INF/MANIFEST.MF的清单文件

### `WAR`（Web Archive File）Web应用档案文件

### `EAR`（Enterprise Archive File）企业应用档案文件

### `JNI`（Java Native Interface）本地化接口

- 调用由C/C++生成的动态库（.dll 或 .so）
- 平台依赖

## 常用命令

### 编译（`javac`）

```sh
# 源码（.java）编译为字节码（.class）
# javac [ -d destDir ] srcFile
javac HelloWorld.java
```

### 运行（`java`）

```sh
# 解释执行字节码
# java [ -classpath classPath ] className
# 多个路径时的连接符[ Window ; Linux : ]
java HelloWorld
```

### 运行（`javaw`）

### 打包（`jar`）

```sh
# 创建JAR包（覆盖原有）
jar cf xxxx.jar xxxx

# 创建但不生成清单文件（-M）
# 不生成META-INF/MANIFEST.MF文件
jar cfM xxxx.jar xxxx

# 创建并使用自定义清单文件内容（-m）
# 生成META-INF/MANIFEST.MF文件并追加manifest.mf内容
# manifest.mf可以是任意文本文件，行内容为key: value，须以空行结束
jar cfm xxxx.jar manifest.mf xxxx

# 查看JAR包内容，当内容过多时可重定向到文件后查看（ > xxx.txt ）
jar tf xxxx.jar

# 解压缩JAR包
jar xf xxxx.jar

# 更新JAR文件（添加或更新JAR包中对应的class文件）
jar uf xxxx.jar path/zzzz.class

# 创建可执行JAR包（-e）
# 通过 java -jar xxxx.jar 或 javaw xxxx.jar 执行
jar cfe xxxx.jar path/主类 *.class

# 以上命令添加-v选项显示过程信息或详细内容
```

## 源码注释

```java
// 单行注释
/* 多行注释 */
/** 文档注释 */
```

## 数据类型

### 基本类型（Primitive Type）

布尔类型及其封装类型

- `boolean`/`Boolean` ( 1bit )

整数类型及其封装类型

- `byte`/`Byte` (1Byte)
- `short`/`Short` (2Bytes)
- `int`/`Integer` (4Bytes) 默认
- `long`/`Long` (8Bytes) 范围超出`int`时须加`l`/`L`后缀
- `char`/`Character` (2Bytes) 字符类型（`Unicode`字符编码）
- `float`/`Float` (4Bytes)
- `double`/`Double` (8Bytes)

```java
// 布尔
boolean isValid = true || false;

// 整数
int oct = 013; // 八进制（0开头）
int hex = 0x13 || 0xaF; // 十六进制（0x或oX开头）
int bin =  0b00010011 || 0b0001_0011; // 二进制（0b或0B开头）

// 浮点
float f1 = 3.14; // 十进制形式
float f2 = 5.12e2 || 5.12E2; // 科学计数法

// 浮点特殊值
double d1 = POSITIVE_INFINITY; // 正无穷
double d2 = NEGATIVE_INFINITY; // 负无穷
double d3 = NaN; // 非数

// 字符
char c1 = '9' || 'A' || '中'; // 普通字符
char c2 = '\n' || '\t' || '\\'; // 转义字符
char c3 = '\uxxxx'; // 十六进制Unicode值
```

### 引用类型（Reference Type）

- `class` 类
- `interface` 接口
- `Arrays` 数组
- `null` 空

```java
int[] arr = null;
int[] arr = {1,2,3};
int[] arr = new int[]{1,2,3};
int[] arr = new int[3];
```

## 开发要点

### 面向对象的三个特征

- 封装（由`private`、`protected`、`public`关键字限定类、类成员变量、类成员方法的访问）
- 继承（由`extends`指定继承，可重写父类方法，重写会破环封装性）
- 多态（引用变量存在两个类型：`编译时`类型、`运行时`类型，编译运行不一致时出现多态）

### 继承唯一直接父类

- `class 父类 extends 爷类 { }`
- `class 子类 extends 父类 { }` 直接继承父类，间接继承爷类

### this & super

- `this(参数,..)` 调用自身构造器
- `this.方法(参数,...)` 调用自身方法
- `super(参数,...)` 调用父类构造器
- `super.方法(参数,...)` 调用父类被重写的方法

### 方法重载（`overload`）

- 类内同名不同参数的方法

### 方法重写（`override`）

- 子类继承父类后，同名同参数的方法

### 强制类型转换异常（`ClassCastException`）

```java
Object obj = new Integer(5);
// 异常
String str = (String)obj;
// 解决方式
if (obj instanceof String) { String str = (String)obj; }
```

### 继承（is-a）& 组合（has-a）

- 继承破坏封装性，父类构造器中不调用将被子类重写的方法，否则可能存在风险
- 组合可降低对封装的破坏及耦合性，类内部创建私有引用类实例

### 类元素

- 初始化块（static{静态初始化块}、{初始化块}）
- 构造器（隐式返回this即实例本身）
- 成员变量（static限定区分为类/实例）
- 成员方法（static限定区分为类/实例）

### 单例（Singleton）类

```java
public class MySingleton {
    private static MySingleton instance;
    // 隐藏构造器
    private MySingleton() {}
    // 获取实例
    public static MySingleton getInstance() {
        if (instance == null) {
            instance = new MySingleton();
        }
        return instance;
    }
}
```

### `final`限定

- 类（不允许被继承）
- 方法（不允许被子类重写，可重载）
- 变量（仅允许被赋值一次）

### `abstract`限定

- 抽象类（仅被继承，不能创建实例）
- 抽象方法（由子类实现）

### `interface`接口

- 更彻底的抽象类（与类不同，接口允许直接继承多个父接口）
- 所有方法均为抽象方法（关键字public abstract可省略，不允许static限定）
- 可定义常量（关键字public static final可省略）

### `implements`实现

- 接口实现

### `enum`枚举类

- enum 枚举类 extends 父类 implements 接口1,接口2...{}

### 内部类

- `class A { class B { } }` 编译生成`A.class`、`A$B.class`

### 闭包 & 回调

```java
// 当A需要使用B和C内同名方法时可采用内部类实现
class A extends B implements C {}

// 内部类实现
class A extends B {
    class AC implements C {}
    public C getCallbackReference() { return new AC; }
}

// 同名方法调用
A.方法()
A.getCallbackReference().方法()
```

### 垃圾回收

- 仅回收堆内存中的对象，不回收任何物理资源（如数据库连接、网络I/O等资源）
- 无法精确控制垃圾回收的运行，当对象永久性地失去引用后，系统会在合适的时候回收它所占内存
- 回收任何对象之前，总会先调用对象的`finalize()`方法，该方法可能使对象被重新引用而导致取消回收
- 主动通知垃圾回收`System.gc()`和`Runtime.getRuntime().gc()`等效

### 枚举类

- 静态常量实现

```java
// 缺点：类型容易混淆，需添加相应前缀"SEASON_"
public static final int SEASON_SPRING = 1;
public static final int SEASON_SUMMER = 2;
public static final int SEASON_FALL   = 3;
public static final int SEASON_WINTER = 4;
```

- 普通实现

```java
public class Season {
    private final String name;
    private final String desc;

    public static final Season SPRING = new Season("春","春暖花开");
    public static final Season SUMMER = new Season("夏","夏日炎炎");
    public static final Season FALL   = new Season("秋","秋高气爽");
    public static final Season WINTER = new Season("冬","冬雪瑟瑟");

    public static Season getSeason(int seasonNum) { ... }
    private Season(String name, String desc) { ... }
}
```

- 枚举类实现

```java
// 省略了new语法，简化代码
public enum Season {
    SPRING, SUMMER, FALL, WINTER;
}
```

```java
// 带构造器
public enum Season {
    SPRING("春"),SUMMER("夏"),FALL("秋"),WINTER("冬");
    private final String name;
    private Season(String name){this.name = name};
}
```

```java
// 还可带代码块，用于实现抽象方法或接口
public enum Season {
    SPRING("春") { ... },
    SUMMER("夏") { ... },
    FALL("秋") { ... },
    WINTER("冬") { ... };
}
```

- 编译生成Season.class、Season$1.class、Season$2.class、Season$3.class、Season$4.class（被视为内部类
）

### `Scanner`键盘输入

- 可从文件、输入流、字符串中解析出基本类型值和字符串值

```java
// 标准输入
Scanner sc = new Scanner(System.in); 
// 文件输入
Scanner sc = new Scanner(new File("Scanner.java"));

// 字符串
while (sc.hasNext()) { sc.Next(); }
// 基本类型值（Int、Long等）
while (sc.hasNextLong()) { sc.NextLong(); }
// 按行读取
while (sc.hasNextLine()) { sc.NextLine(); }

// 指定分隔符（默认为空白符）
sc.useDelimiter("\n");
```

### `BufferedReader` 字符流输入

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
br.readline();
```

### `System` 系统相关

- 运行平台系统属性、环境变量等

```java
// 环境变量（所有）
Map<String,String> env = System.getenv();
for (String name : env.keySet()) { env.get(name)); }

// 环境变量（指定）
System.getenv("JAVA_HOME");

// 系统属性（所有）
Properties props = System.getProperties();
props.store(new FileOutputStream("props.txt"), "System Properties");

// 系统属性（指定）
System.getProperty("os.name");
```
