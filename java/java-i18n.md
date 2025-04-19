# java I18N（国际化）

## 简介

- 全球化软件，根据客户端请求来自的国家/地区/语言的不同相应显示不同的用户界面
- `I18N` 国际化（Internationalization）
- `L10N` 本地化（Localization）

## 关键类

- `java.util.ResourceBundle` 加载国家语言资源包
- `java.util.Locale` 封装特定的国家/区域、语言环境
- `java.text.MessageFormat` 格式化带占位符的字符串

## 关键工具

- `native2ascii` `源.properties` `目标.properties`
- 对包含非西欧字符（如含中文）的资源文件进行字符转换（Unicode编码）

```sh
native2ascii mess.properties mess_zh_CN.properties
```

## 资源文件（键值对 key=value）

- base资源名.properties
- base资源名_language语言代码.properties
- base资源名_language语言代码_country国家代码.properties

## 访问来源（客户端语言环境）

```java
Locale locale = Locale.getDefault();
```

## 资源绑定

```java
// 将根据客户端语言环境自动适配properties文件
ResourceBundle bundle = ResourceBundle.getBundle("base资源名", locale);
```

## 获取资源

```java
msg = bundle.getString("key键");
```

### 值为常量

- `mess=love`
- `mess=爱`

### 值含占位符

- `mess={0} love {1}`
- `mess={0} 爱 {1}`

```java
msg = MessageFormat.format(msg, value0, value1)
```

## 数据格式化

### NumberFormat

- getCurrencyInstance()
- getIntegerInstance()
- getNumberInstance()
- getPercentInstance()

### DateFormat

- getDateInstance()
- getTimeInstance()
- getDateTimeInstance()

### SimpleDateFormat

- `new SimpleDateFormat("yyyy-mm-hh")`

## 使用类文件代替资源文件

```java
public class myMess_zh_CN extends ListResourceBundle {
    private final Object myData[][] = {
        {"mess", "{0} 爱 {1}"}
    };

    public Object[][] getContents() {
        return myData;
    }
}
```

## 获取Java所支持的全部国家和语言

```java
Locale[] localeList  = Locale.getAvailableLocales();
```

## ResourceBundle搜索资源文件的顺序

- myMess_zh_CN.class
- myMess_zh_CN.properties
- myMess_zh.class
- myMess_zh.properties
- myMess.class
- myMess.properties
