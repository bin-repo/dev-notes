# MyBatis 映射文件

## 映射文件结构（Mapper.xml）

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <insert></insert>
  <update></update>
  <delete></delete>
  <select></select>
</mapper>
```

## 顶级标签元素

- `cache` 该命名空间的缓存配置
- `cache-ref` 引用其它命名空间的缓存配置
- `resultMap` 描述如何从数据库结果集中加载对象，是最复杂也是最强大的元素
- `sql` 可被其它语句引用的可重用语句块
- `insert` 映射插入语句
- `update` 映射更新语句
- `delete` 映射删除语句
- `select` 映射查询语句

## 标签属性

- `id` 唯一标识
- `parameterType` 参数类型（可选）可通过类型处理器（TypeHandler）自动推断
- `resultType` 结果类型（与`resultMap`互斥）
- `resultMap` 结果映射（与`resultType`互斥）
- `flushCache` 是否清空缓存（默认`false`）
- `useCache` 是否启用缓存（`select`元素默认`true`）
- `timeout` 等待数据库返回请求结果超时时间（秒），默认未设置，依赖数据库驱动
- `fetchSize` 数据库结果集的获取行数，默认未设置，依赖数据库驱动
- `statementType` 语句类型（`STATEMENT`/`PREPARED`默认/`CALLABLE`），分别对应（Statement/PreparedStatement/CallableStatement）
- `resultSetType` 结果集类型（`FORWARD_ONLY`/`SCROLL_SENSITIVE`/`SCROLL_INSENSITIVE`/`DEFAULT`默认）
- `databaseId` 根据数据库厂商标识（databaseIdProvider）加载语句
- `resultOrdered` 是否嵌套结果集或是分组（默认`false`）
- `resultSets` 多结果集时使用（以逗号分隔）
- `useGeneratedKeys` 是否使用数据库内部生成的主键，如自动递增字段（默认`false`）仅适用于insert和update
- `keyProperty` 指定能够唯一识别对象的属性（以逗号分隔）仅适用于insert和update
- `keyColumn` 指定列名（以逗号分隔）仅适用于insert和update
- `order` 语句在主语句之前还是之后执行（`BEFORE`/`AFTER`）

## 参数形式

### `#{property}` 形式

- 会创建`PreparedStatement`参数占位符`?`避免SQL注入攻击风险
- #{property,mode=,javaType=,jdbcType=,jdbcTypeName=,typeHandler=,resultMap=,numericScale=保留小数位数}
- 通常#{property}即可，其他由MyBatis自动推断

```java
@Select("select * from user where id = #{id}")
User findById(@Param("id") long id);

@Select("select * from user where name = #{name}")
User findByName(@Param("name") String name);
```

### `${property}` 形式

- 直接取值，不进行转义，例如 `order by ${columnName}`

```java
// 不需要单独提供findById和findByName方法
@Select("select * from user where ${column} = #{value}")
User findByColumn(@Param("column") String column, @Param("value") String value);
```

## 标签元素（`select`）查询

```xml
<!-- 查询结果映射为HashMap对象 -->
<select id="selectPerson" parameterType="int" resultType="hashmap">
  select * from person where id = #{id}
</select>
```

```xml
<!-- 查询结果映射为Person对象 -->
<select id="selectPerson" resultType="Person">
  select * from person where id = #{id}
</select>
```

## 标签元素（`insert`）插入

```xml
<!-- 自动映射Author对象的属性作为字段参数 -->
<insert id="insertAuthor" parameterType="Author">
  insert into author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>
```

```xml
<!-- 自动映射各个字段参数 -->
<insert id="insertAuthor">
  insert into author (id,username,password,email,bio)
  values (#{id},#{username},#{password},#{email},#{bio})
</insert>
```

```xml
<!-- 当id为自增主键时 -->
<insert id="insertAuthor" useGeneratedKeys="true" keyProperty="id">
  insert into author (username,password,email,bio)
  values (#{username},#{password},#{email},#{bio})
</insert>
```

```xml
<!-- 当数据库支持批量插入时，可通过foreach拼接后插入 -->
<insert id="insertAuthors" useGeneratedKeys="true" keyProperty="id">
  insert into author (username, password, email, bio) values
  <foreach item="author" collection="list" separator=",">
    (#{author.username}, #{author.password}, #{author.email}, #{author.bio})
  </foreach>
</insert>
```

```xml
<!-- 当数据库不支持自增字段时，可预先准备主键 -->
<insert id="insertAuthor">
  <selectKey keyProperty="id" resultType="int" order="BEFORE" statementType="PREPARED">
    select gen_id from my_gen_id_table
  </selectKey>
  insert into author (id, username, password, email, bio, favourite_section)
  values (#{id}, #{username}, #{password}, #{email}, #{bio}, #{favouriteSection,jdbcType=VARCHAR})
</insert>
```

## 标签元素（`update`）更新

```xml
<update id="updateAuthor">
  update author set
    username = #{username},
    password = #{password},
    email = #{email},
    bio = #{bio}
  where id = #{id}
</update>
```

## 标签元素（`delete`）删除

```xml
<delete id="deleteAuthor">
  delete from Author where id = #{id}
</delete>
```

## 标签元素（`sql`）片段

```xml
<!-- 定义代码片段 -->
<sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>
```

```xml
<!-- 引用代码片段 -->
<!-- 结果列：t1.id,t1.username,t1.password,t2.id,t2.username,t2.password -->
<select id="selectUsers" resultType="map">
  select
    <include refid="userColumns"><property name="alias" value="t1"/></include>,
    <include refid="userColumns"><property name="alias" value="t2"/></include>
  from some_table t1
  cross join some_table t2
</select>
```

```xml
<!-- 定义片段1 -->
<sql id="sometable">
  ${prefix}Table
</sql>
<!-- 定义片段2 -->
<sql id="someinclude">
  from <include refid="${include_target}"/>
</sql>
<!-- 嵌套引用片段 -->
<select id="select" resultType="map">
  select field1, field2, field3
  <include refid="someinclude">
    <property name="include_target" value="sometable"/>
    <property name="prefix" value="Some"/>
  </include>
</select>
```

## 标签元素（`resultMap`）结果映射

- 设置`resultType`属性，隐式创建一个ResultMap来实现列字段到目标对象属性的映射
- 当列字段名与目标对象属性名不一致时，可采用`select 列 as 列别名`的方式达成一致
- 设置`resultMap`属性，显式指定映射关系

```xml
<!-- 映射关系定义 -->
<resultMap id="userResultMap" type="User">
  <id property="id" column="user_id" />
  <result property="username" column="user_name"/>
  <result property="password" column="hashed_password"/>
</resultMap>

<!-- 显式指定映射关系 -->
<select id="selectUsers" resultMap="userResultMap">
  select user_id, user_name, hashed_password
  from some_table
  where id = #{id}
</select>
```

## 标签元素（`resultMap`）高级结果映射

- `constructor` 构造器映射（可含`idArg`、`arg`子元素）
- `association` 关联映射（适用于成员对象）
- `collection` 集合映射（适用于成员集合）
- `discriminator` 判断型（可含`case`子元素）根据条件进行映射

```java
// 作者
public class Author {
  private int id;
  private String name;
}
```

```java
// 图书
public class Book {
  private int id;
  private String code;
  private String name;
  private Author author;
}
```

```java
// 网站
public class WebSite {
  private int store_id;
  private String store_url;
}
```

```java
// 商店
public class Store {
  private int id;
  private String name;
  private String address;
  private Auther auther;
  private List<Book> books;
  private int hasWebSite;
  private WebSite webSite;

  public BookStore(int id, String name) { ... }
}
```

```xml
<!-- 复杂查询 -->
<select id="selectStore" resultMap="storeResultMap">
  select
    s.id as store_id,
    s.name as store_name,
    s.address as store_address,
    s.has_web_site as hasWebSite,
    w.url as store_url,
    a.id as author_id,
    a.name as author_name,
    b.id as book_id,
    b.code as book_code,
    b.name as book_name
  from store s
    left join web_site w on w.id = s.id
    left join author a on a.id = s.author_id
    left join book b on b.id = a.book_id
  where s.id = #{id}
</select>
```

```xml
<!-- 复杂查询结果映射 -->
<resultMap id="storeResultMap" type="Store">
  <!-- Store store = new Store(int,String) -->
  <constructor>
    <idArg column="store_id" javaType="int" />
    <arg column="store_name" javaType="String" />
  </constructor>
  <!-- store.setAdress(String)方法 -->
  <result property="address" column="store_address" />

  <!-- Author author = new Author() -->
  <association property="author" javaType="Author">
    <!-- author.setId(int) -->
    <id property="id" column="author_id" />
    <!-- author.setName(String) -->
    <result property="name" column="author_name" />
  </association>

  <!-- List<Book> books = new ArrayList<>() -->
  <!-- Book book = new Book() -->
  <collection property="books" ofType="Book">
    <!-- book.setId(int) -->
    <id property="id" column="book_id" />
    <!-- book.setCode(String) -->
    <result property="code" column="book_code" />
    <!-- book.setName(String) -->
    <result property="name" column="book_name" />
    <!-- books.add(book) -->
  </collection>

  <!-- switch-case then new WebSite() -->
  <discriminator javaType="int" column="hasWebSite">
    <case value="1" resultType="WebSite" />
  </discriminator>
</resultMap>
```

## 标签元素（`cache`）缓存

- `eviction` 清除策略（`LRU`最近最少使用，默认/`FIFO`先进先出/`SOFT`软引用/`WEAK`弱引用）
- `flushInterval` 刷新间隔时间（毫秒）
- `size` 引用数目（默认1024）
- `readOnly` 是否只读（默认false）

```xml
<cache/>
<cache eviction="FIFO" flushInterval="60000" size="512" readOnly="true"/>
<!-- 支持自定义缓存，实现org.apache.ibatis.cache.Cache接口 -->
<cache type="com.domain.something.MyCustomCache"/>
```

## 标签元素（`cache-ref`）缓存引用

- 引用另一个缓存

```xml
<cache-ref namespace="com.someone.application.data.SomeMapper"/>
```

## 动态SQL

### 子标签（`if`）条件判断

- 注意where的第一个条件是静态值

```xml
<select id="findActiveBlogLike" resultType="Blog">
  select * from blog where state = 'ACTIVE'
  <if test="title != null">
    and title like #{title}
  </if>
  <if test="author != null and author.name != null">
    and author_name like #{author.name}
  </if>
</select>
```

### 子标签（`choose`-`when`-`otherwise`）条件判断

- 注意where的第一个条件是静态值

```xml
<select id="findActiveBlogLike" resultType="Blog">
  select * from blog where state = 'ACTIVE'
  <choose>
    <when test="title != null">
      and title like #{title}
    </when>
    <when test="author != null and author.name != null">
      and author_name like #{author.name}
    </when>
    <otherwise>
      and featured = 1
    </otherwise>
  </choose>
</select>
```

### 子标签（`where`）生成WHERE子句

- 动态生成`WHERE`子句，自动去除多余的`AND`或`OR`

```xml
<select id="findActiveBlogLike" resultType="Blog">
  select * from blog
  <where>
    <if test="state != null">
      state = 'ACTIVE'
    </if>
    <if test="title != null">
      and title like #{title}
    </if>
  </where>
</select>
```

```xml
<!-- 与where标签等效 -->
<trim prefix="WHERE" prefixOverrides="AND |OR "><!--AND和OR后的空格是必要的-->
  ...
</trim>
```

### 子标签（`set`）生成SET子句

- 动态生成`SET`子句，自动去除多余的逗号

```xml
<update id="updateAuthorIfNecessary">
  update Author
    <set>
      <if test="username != null">username=#{username},</if>
      <if test="password != null">password=#{password},</if>
      <if test="email != null">email=#{email},</if>
      <if test="bio != null">bio=#{bio}</if>
    </set>
  where id=#{id}
</update>
```

```xml
<!-- 与set标签等效 -->
<trim prefix="SET" suffixOverrides=",">
  ...
</trim>
```

### 子标签（`foreach`）遍历集合

```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  select * from post p where id in
  <foreach item="item" index="index" collection="list" open="(" separator="," close=")">
    #{item}
  </foreach>
</select>
```

```xml
<insert id="insertUsers">
  insert into user (username, password) values
  <foreach collection="userList" item="user" separator=",">
    (#{user.username}, #{user.password})
  </foreach>
</insert>
```

### 子标签（`bind`）绑定临时变量

```xml
<select id="selectBlogsLike" resultType="Blog">
  <bind name="pattern" value="'%' + _parameter.getTitle() + '%'" />
  select * from blog where title like #{pattern}
</select>
```
