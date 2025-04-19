# java JNI（原生接口）

## 简介

- JNI（Java Native Interface）本地化接口/原生接口
- 用于在Java中调用C/C++生成的动态库（`.dll` `.so`）
- 由动态库实现该接口定义的方法

## 编写JNI类

- 包含由`native`限定的方法

```java
// HelloJNI.java
package com.sample.jni;
public class HelloJNI {
    static {
        // hello.dll 或 libhello.so
        System.loadLibrary("hello");
    }
    
    private native void sayHello();

    public static void main(String[] args) {
        // invoke the native method
        new HelloJNI().sayHello();
    }
}
```

## 编译JNI类

- `javac`命令编译生成`.class`文件

```sh
javac HelloJNI.java
```

## 生成JNI头文件

- `javah`命令生成`.h`头文件

```sh
javah -jni -classpath E:\hello\out\com\sample\jni -d E:\hello\jni com.sample.jni.HelloJNI
```

## 编写C方法实现JNI头文件中函数

- `.h`文件中引用了JDK中的`jni.h`和`jni_md.h`文件

## 编译生成动态库

### 编译环境

- Visual C/C++
- Visual Studio
- MinGW
- Cygwin
- GCC
- 等

### 编译

```sh
gcc -c -I"${JAVA_HOME}\include" -I"${JAVA_HOME}\include\win32" HelloJNI.c
gcc -Wl,--add-stdcall-alias -shared -o hello.dll HelloJNI.o
```

## 为JVM指定动态库目录

- VM options中加入`-Djava.library.path=E:\hello\lib`

## 动态库加载

- System.loadLibrary(动态库名)
- Runtime.loadLibrary(动态库名)
- 动态库名不包含`.dll`或`.so`后缀
