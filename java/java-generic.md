# java generic（泛型）

## 简介

- 当一个对象放入Java集合中时，会被当成Object类型处理，而不记忆原类型，从集合中取出后需要进行强制类型转换
- 引入泛型支持后的集合可以记住集合中元素的类型，并在编译时检查集合中元素类型，避免ClassCastException异常
- 泛型类不局限于集合类，任何类均适用

## 采用`<>`型语法

- `<>`内可包含多个类型以逗号分隔，例：`<E>`、`<K,V>`
- 可任意字母

## 通配符`?`表示所有类型

## 类型限定（`extends`）上限

- `<E extends T>` E须为T的子类
- `<? extends T>` 任何类型但须为T的子类

## 类型限定（`super`）下限

- `<E super T>` E须与T类型相同或者是T的父类
- `<? super T>` 任何类型但须与T类型相同或者是T的父类

## 定义泛型接口或泛型类

```java
public interface DemoInterface<E> {
    DemoInterface<E> method(DemoInterface<E> demoInterface);
}
```

```java
public class DemoClass<E> {
    public DemoClass<E> method(DemoClass<E> demoClas) {}
}
```

## 定义泛型方法

```java
public interface DemoInterface {
    public <T> void methodf(T t);
}
```

```java
public class DemoClass {
    public <T> void method(T t) {}
}
```

## 混合定义

```java
public interface DemoInterface<E> {
    method1(DemoInterface<E> demoInterface);
    public <T> void method2(T t);
}
```

```java
public class DemoClass<E> {
    method1(DemoClass<E> demoClass) {}
    public <T> void method2(T t) {}
}
```

## 注意事项

### 泛型类`<E>`内部变量和方法包含`<E>`泛型时不能被`static`修饰

- 因为在对类进行初始化时还不能确定`E`的类型，只有在创建对象使用时才能确定
- 而`static`修饰要求在初始化阶段必须确认类型，否则报异常

### 实现类或派生子类时必须指定具体类型

```java
public class DemoChildClass extends Demo1Class<String, String> implements Demo2Class<String> {}
```

### 使用时传入类型实参

```java
DemoClass<String> demoCLass = new DemoClass<String>();
DemoClass<String> demoCLass = new DemoClass<>();
```

### 泛型方法中可使用`?`通配符及`extends`、`super`限定类型范围

### 泛型方法`限定符 <类型> 返回类型 方法名(类型 变量)`可以用`static`修饰

## 示例

```java
public interface List<E> {
    void add(E x);
    Iterator<E> iterator();
}
```

```java
public interface Iterator<E> {
    E next();
    boolean hasNext();
}
```

```java
public interface Map<K, V> {
    Set<K> keySet();
    V put(K key, V value);
}
```

```java
// 未使用泛型，元素可以是任意对象
List strList = new ArrayList();

// 使用泛型，元素只能是String对象
List<String> strList = new ArrayList<String>();
```

```java
public class MyPrint {
    public static <T> void print(T t){...}
}

MyPrint.print("test");
MyPrint.print(123);
```
