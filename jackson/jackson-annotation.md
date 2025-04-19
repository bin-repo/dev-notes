# jackson 注解用法

## @JsonIgnore（序列化或反序列化时忽略某个属性）

```java
@JsonIgnore
private String password;
```

## @JsonIgnoreProperties（序列化或反序列化时忽略某些属性）

```java
// 忽略指定属性集合
@JsonIgnoreProperties({"password", "age"})
public class User {}

// 反序列化时忽略所有未知属性，避免抛出异常
@JsonIgnoreProperties(ignoreUnknown = true)
public class User {}
```

## @JsonIgnoreType（序列化或反序列化时忽略整个类及类对象）

```java
// 类整体忽略
@JsonIgnoreType
public class Component {}

// 其类对象亦被忽略
public class Entity {
    private Component component;
}
```

## @JsonAutoDetect（调整 getter/setter 可见性规则）

## @JsonProperty（序列化或反序列化时重命名属性）

```java
@JsonProperty("username")
private String name;
```

## @JsonFormat（数据/时间格式化）

```java
@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd")
private Date birthday;
```

## @JsonInclude（序列化时控制包含哪些属性）

```java
// 类级
@JsonInclude(JsonInclude.Include.NON_NULL)
public class User {
    // 属性级
    @JsonInclude(JsonInclude.Include.NON_EMPTY)
    private String name;
}
```

## @JsonGetter（序列化时自定义类中未定义的计算属性）

```java
@JsonGetter("fullName")
public String getFullName() {
    return this.firstName + " " + this.lastName;
}
```

## @JsonSetter（反序列化时的方法或属性）

```java
@JsonSetter("first_name")
private String firstName;
```

## @JsonAnyGetter（序列化时对键值对进行解构）

```java
@JsonAnyGetter
public Map<String, Object> getAdditionalProperites() {
    Map<String, Object> map = new HashMap<>();
    return map;
}
```

## @JsonAnySetter（反序列化时设置未知属性）

```java
@JsonAnySetter
public void addAdditionalProperty(String key, Object value) {
    Map<String, Object> map = new HashMap<>();
    map.put(key, value);
}
```

## @JsonPropertyOrder（序列化时指定属性的排序规则）

```java
@JsonPropertyOrder({"name","age"})
public class User {
    @JsonPropertyOrder(alphabetic = true)
    private Map<String, String> experts;
}
```

## @JsonRawValue（序列化时若属性值为 JSON 数据时保持其原数据及其结构不做转义）

```java
@JsonRawValue
private String rawJsonProperty = "{\"key\":\"value\"}";
```

## @JsonValue（序列化时以指定的属性或方法返回值作为整个对象的 JSON 数据，忽略其他所有属性）

```java
@JsonValue
public Sting asJsonString() {
    return "{\"key\":\"value\"}"
}
```

## @JsonSerialize（为类、属性等指定自定义的序列化方法）

```java
@JsonSerialize(using = MyBooleanSerializer.class)
private boolean enabled = false;
```

## @JsonDeserialize（为类、属性等指定自定义的反序列化方法）

```java
@JsonDeserialize(using = MyBooleanDeserializer.class)
private boolean enabled = false;
```

## @JsonCreator（反序列化时指明构造器，默认使用无参构造器）

```java
@JsonCreator
public User(@JsonProperty("name") String name, @JsonProperty("age") int age) {}
```

## @JacksonInject（反序列化时注入额外缺省的属性及数据）

```java
@JacksonInject("defaultEmail")
private String defaultEmail;
```

```java
InjectableValues injectables = new InjectableValues.Std().addValue("defaultEmail", "hr@example.com");
ObjectMapper mapper = new ObjectMapper().setInjectableValues(injectables);
```
