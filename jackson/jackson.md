# [jackson](https://github.com/FasterXML/jackson)

用于序列化和反序列化 json 的 Java 开源框架。

## 模块

- jackson-core（序列化和反序列化）
- jackson-databind（数据绑定）
- jackson-annotations（注解）

## Maven 依赖（pom.xml）

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.16.0</version>
</dependency>
```

## 基本用法

### 实体类（User）

```java
public class User {
    private String name;
    private int age;
    private Date birthday;

    public User() {} // 无参构造器（必须）
    public User(String name, int age, Date birthday) {}
}
```

### 序列化（Java Object => Json String）

```java
public String serialization(User user) throws JsonProcessingException {
    ObjectMapper objectMapper = new ObjectMapper();
    return objectMapper.writeValueAsString(user);
}

public void test() {
    String jsonStr = serialization(new User("张三", 18, new Date()));
    System.out.println(jsonStr)
}
```

### 反序列化（Json String => Java Object）

```java
public User deserialization(String jsonStr) throws JsonProcessingException {
    ObjectMapper objectMapper = new ObjectMapper();
    return objectMapper.readValue(jsonStr, User.class);
}

public void test() {
    String jsonStr = serialization(new User("张三", 18, new Date()));
    User user = deserialization(jsonStr);
}
```

## 日期处理

默认情况下，jackson 会将日期类型属性序列化成 long 型值（自 1970 年 1 月 1 日以来的毫秒数），实际应用需进行格式化。

```java
User user = new User("张三", 18, new Date());
ObjectMapper objectMapper = new ObjectMapper();

SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
objectMapper.setDateFormat(sdf);

String jsonStr = objectMapper.writeValueAsString(user);
```

## 数据形式

```java
// 字符串
objectMapper.readValue(jsonStr, User.class);
// 字节流
objectMapper.readValue(jsonStr.getBytes(), User.class);
// 字符流
Reader reader = new StringReader(jsonStr);
objectMapper.readValue(reader, User.class);
// 文件流
FileInputStream fis = new FileInputStream("user.json");
objectMapper.readValue(fis, User.class);
// 文件
File file = new File("user.json");
objectMapper.readValue(file, User.class);
// 网络文件
URL url = new URL("https://example.com/file/user.json");
objectMapper.readValue(url, User.class);
```

## 对象形式

```java
// 已知对象
User user = objectMapper.readValue(jsonStr, User.class);
// List
User[] users = objectMapper.readValue(jsonStr, User[].class);
List<User> users = objectMapper.readValue(jsonStr, new TypeReference<List<User>>(){});
// Map
Map<String, Object> map = objectMapper.readValue(jsonStr, new TypeReference<Map<String, Object>>(){});
// JsonNode
JsonNode rootNode = objectMapper.readTree(jsonStr);
rootNode.get("name").asText();
rootNode.get("age").asInt();
```

## 自定义序列化和反序列化

### 序列化

```java
SimpleModule simpleModule = new SimpleModule();
simpleModule.addSerializer(User.class, new JsonSerializer<User>(){
    @Override
    public void serialize(User user, JsonGenerator jsonGenerator, SerializerProvider serializerProvider) throws IOException {
        jsonGenerator.writeStartObject();
        jsonGenerator.writeStringField("username", user.getName());
        jsonGenerator.writeNumberField("userage", user.getAge());
        jsonGenerator.writeEndObject();
    }
});
// 使用自定义模块
objectMapper.registerModule(simpleModule);
objectMapper.writeValueAsString(user);
```

### 反序列化

```java
public class UserDeserializer extends StdDeserializer<User> {
    public UserDeserializer() { this(null); }
    public UserDeserializer(Class<?> vc) { super(vc); }

    @Override
    public User deserialize(JsonParser jp, DeserializationContext ctxt) throws IOException {
        JsonNode node = jp.getCodec().readTree(jp);
        String name = node.get("username").asText();
        int age = (Integer) ((IntNode) node.get("userage")).numberValue();

        return new User(name, age, new Date());
    }
}
```

```java
SimpleModule simpleModule = new SimpleModule();
simpleModule.addDeserializer(User.class, new UserDeserializer());
// 使用自定义模块
objectMapper.registerModule(simpleModule);
objectMapper.readValue(jsonStr, User.class);
```

## 树模型

- JsonNode
- ObjectNode（对应 JSON 对象，可通过.put(key,value)添加或更新属性）
- ArrayNode（对应 JSON 数组，可通过.add(value)插入新元素）
- TextNode、IntNode、LongNode、DoubleNode 等（对应 JSON 基本类型值）
- BooleanNode、NullNode（对应 JSON 布尔值和 null 值）

```java
ObjectMapper objectMapper = new ObjectMapper();
// 对象
ObjectNode node1 = objectMapper.createObjectNode();
node1.put("name", "张三");
node1.put("age", 18);
// 数组
ArrayNode node2 = objectMapper.createArrayNode();
node2.add("运动").add("音乐").add("睡觉");
// 子节点
node1.set('favor', node2);
// 序列化
System.out.println(node1.toString())
```
