# MyBatis 配置文件

## 配置文件结构（mybatis-config.xml）

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration desc="配置">
  <properties resource="mybatis-config.properties" desc="属性（可选文件定义）">
    <property name="" value="" desc="属性项（覆盖定义）" />
  </properties>
  <settings desc="设置">
    <setting name="" value="" desc="设置项" />
  </settings>
  <typeAliases desc="类型别名">
    <typeAlias alias="" type="" desc="别名项" />
  </typeAliases>
  <typeHandlers desc="类型处理器">
    <typeHandler handler="" desc="自定义处理器" />
  </typeHandlers>
  <objectFactory type="" desc="对象工厂">
    <property name="" value="" desc="初始属性值" />
  </objectFactory>
  <plugins desc="插件">
    <plugin interceptor="" desc="拦截器">
      <property name="" value="" desc="拦截器参数" />
    </plugin>
  </plugins>
  <environments desc="环境配置">
    <environment desc="环境变量">
      <transactionManager desc="事务管理器"></transactionManager>
      <dataSource desc="数据源">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <databaseIdProvider type="" desc="数据库厂商标识">
    <property name="" value="" desc="厂商参数" />
  </databaseIdProvider>
  <mappers desc="映射器"></mappers>
</configuration>
```

## Properties 属性

- 定义好的属性可通过 `${property_name}` 来进行引用
- 从 MyBatis 3.4.2 开始可通过 `${property_name:default_value}` 来指定属性默认值

```xml
<properties resource="mybatis-config.properties">
  <!-- 默认值特性默认关闭，可显式启用该特性 -->
  <property name="org.apache.ibatis.parsing.PropertyParser.enable-default-value" value="true"/>
  <!-- 默认值分隔符默认为:当属性名或默认值中包含该字符时，须更改分隔符，例如?: -->
  <property name="org.apache.ibatis.parsing.PropertyParser.default-value-separator" value="?:"/>
</properties>
```

## Settings 设置

```xml
<settings>
  <setting name="cacheEnabled" value="true" desc="是否全局开启所有映射器配置文件中已配置的任何缓存" />
  <setting name="lazyLoadingEnabled" value="false" desc="是否全局开启所有关联对象的延迟加载" />
  <setting name="aggressiveLazyLoading" value="false" desc="是否全局开启方法调用时加载该对象的所有延迟加载属性，未开启则按需加载" />
  <setting name="multipleResultSetsEnabled" value="true" desc="是否允许单个语句返回多结果集，但需数据库驱动支持"/>
  <setting name="useColumnLabel" value="true" desc="是否使用列标签代替列名，但需数据库驱动支持" />
  <setting name="useGeneratedKeys" value="false" desc="是否允许JDBC自动生成主键，但需数据库驱动支持" />
  <setting name="autoMappingBehavior" value="PARTIAL" desc="如何自动映射列到字段或属性（NONE不映射/PARTIAL无嵌套映射/FULL复杂映射）"/>
  <setting name="autoMappingUnknownColumnBehavior" value="NONE" desc="如何自动映射未知列（NONE不映射/WARNING警告日志/FAILING抛出异常）" />
  <setting name="defaultExecutorType" value="SIMPLE" desc="默认的执行器类型（SIMPLE普通/REUSE复用预处理语句/BATCH复用预处理语句及批量更新）"/>
  <setting name="defaultStatementTimeout" value="25" desc="默认语句执行超时时间（秒）null" />
  <setting name="defaultFetchSize" value="100" desc="默认查询结果集数量大小（行）null" />
  <setting name="defaultResultSetType" value="DEFAULT" desc="默认查询结果集类型（FORWARD_ONLY/SCROLL_SENSITIVE/SCROLL_INSENSITIVE/DEFAULT）" />
  <setting name="safeRowBoundsEnabled" value="false" desc="是否允许在嵌套语句中使用分页（false允许）" />
  <setting name="safeResultHandlerEnabled" value="true" desc="是否允许在嵌套语句中使用结果处理器（false允许）" />
  <setting name="mapUnderscoreToCamelCase" value="false" desc="是否开启驼峰命名自动映射，如A_ID映射为aId" />
  <setting name="localCacheScope" value="SESSION" desc="如何使用本地缓存机制（SESSION会话/STATEMENT语句）" />
  <setting name="jdbcTypeForNull" value="OTHER" desc="空值的默认JDBC类型（NULL/VARCHAR/OTHER）" />
  <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString" desc="对象的哪些方法触发一次延迟加载" />
  <setting name="defaultScriptingLanguage" value="org.apache.ibatis.scripting.xmltags.XMLLanguageDriver" desc="生成动态SQL的默认脚本语言" />
  <setting name="defaultEnumTypeHandler" value="org.apache.ibatis.type.EnumTypeHandler" desc="默认枚举类型处理器" />
  <setting name="callSettersOnNulls" value="false" desc="是否设置空结果集为null（注意基本类型不允许）" />
  <setting name="returnInstanceForEmptyRow" value="false" desc="是否为结果集中的空行返回空实列" />
  <setting name="logPrefix" value="" desc="指定日志前缀" />
  <setting name="logImpl" value="" desc="指定日志具体实现否则自动查找（SLF4J/LOG4J/LOG4J2/COMMONS_LOGGING等）" />
  <setting name="proxyFactory" value="JAVASSIST" desc="指定创建可延迟加载对象所用到的代理工具（CGLIB/JAVASSIST）" />
  <setting name="vfsImpl" value="" desc="指定 VFS 的实现类，以逗号分隔" />
  <setting name="useActualParamName" value="true" desc="使用方法签名中的名称作为语句参数名称" />
  <setting name="configurationFactory" value="" desc="指定一个提供 Configuration 实例的类，用于延迟加载配置属性值" />
</settings>
```

## TypeAliases 类型别名

```xml
<typeAliases>
  <typeAlias alias="Author" type="domain.blog.Author"/>
  <!--亦可指定包名进行自动扫描-->
  <package name="domain.blog" />
</typeAliases>
```

```java
@Alias("author")
public class Author { /* 别名注解方式 */ }
```

## TypeHandlers 类型处理器

默认类型处理器（BooleanTypeHandler / ByteTypeHandler等）例如：

- 类型处理器（`BooleanTypeHandler`）
- JAVA类型（`Boolean`/`boolean`）
- JDBC类型（`BOOLEAN`）

自定义类型处理器的方式：

- 实现 `org.apache.ibatis.type.TypeHandler` 接口
- 继承 `org.apache.ibatis.type.BaseTypeHandler` 类

```java
@MappedJdbcTypes(JdbcType.VARCHAR)
public class ExampleTypeHandler extends BaseTypeHandler<String> {
    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, String parameter, JdbcType jdbcType) throws SQLException {
        ps.setString(i, parameter);
    }
    @Override
    public String getNullableResult(ResultSet rs, String columnName) throws SQLException {
        return rs.getString(columnName);
    }
    @Override
    public String getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        return rs.getString(columnIndex);
    }
    @Override
    public String getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        return cs.getString(columnIndex);
    }
}
```

```xml
<typeHandlers>
  <typeHandler handler="org.mybatis.example.ExampleTypeHandler"/>
  <!--亦可指定包名进行自动扫描-->
  <package name="org.mybatis.example" />
</typeHandlers>
```

## ObjectFactory 对象工厂

- 每次创建结果对象的新实例时都会使用对象工厂ObjectFactory实例来完成实例化工作
- 默认通过调用无参构造器或参数映射调用带参构造器方法
- 可通过自定义对象工厂来实现对覆盖对象工厂的默认行为

```java
public class ExampleObjectFactory extends DefaultObjectFactory {
    public Object create(Class type) {
        return super.create(type);
    }
    public Object create(Class type, List<Class> constructorArgTypes, List<Object> constructorArgs) {
        return super.create(type, constructorArgTypes, constructorArgs);
    }
    public void setProperties(Properties properties) {
        super.setProperties(properties);
    }
    public <T> boolean isCollection(Class<T> type) {
        return Collection.class.isAssignableFrom(type);
    }
}
```

```xml
<objectFactory type="org.mybatis.example.ExampleObjectFactory">
  <property name="someProperty" value="100"/>
</objectFactory>
```

## Plugins 插件

允许使用插件来拦截的方法调用包括（可能会破坏MyBatis核心模块须谨慎使用）：

- Executor (update, query, flushStatements, commit, rollback, getTransaction, close, isClosed)
- ParameterHandler (getParameterObject, setParameters)
- ResultSetHandler (handleResultSets, handleOutputParameters)
- StatementHandler (prepare, parameterize, batch, update, query)

使用插件只需实现`Interceptor`接口，并指定想要拦截的方法签名即可

```java
@Intercepts({@Signature(type = Executor.class, method = "update",args = {MappedStatement.class, Object.class})})
public class ExamplePlugin implements Interceptor {
    private Properties properties = new Properties();
    public Object intercept(Invocation invocation) throws Throwable {
        // implement pre processing if need
        Object returnObject = invocation.proceed();
        // implement post processing if need
        return returnObject;
    }
    public void setProperties(Properties properties) {
        this.properties = properties;
    }
}
```

```xml
<plugins>
  <plugin interceptor="org.mybatis.example.ExamplePlugin">
    <property name="someProperty" value="100"/>
  </plugin>
</plugins>
```

## Environments 环境配置

- 可根据需要配置多种环境，例如开发、测试、生产环境等
- 每个SqlSessionFactory实例只能选择其中一种环境，所以连接多个数据库时，需创建多个SqlSessionFactory实例

```xml
<environments default="development">
  <environment id="development">
    <transactionManager type="JDBC"></transactionManager>
    <dataSource type="POOLED"></dataSource>
  </environment>
</environments>
```

### 事务管理

- 事务管理类型（`JDBC`提交和回滚 / `MANAGED`由应用容器管理）

```xml
<transactionManager type="MANAGED">
  <!-- 阻止默认的关闭连接行为 -->
  <property name="closeConnection" value="false"/>
</transactionManager>
```

- 可通过实现`TransactionFactory`和`Transaction`接口自定义事务管理

### 数据源

- 内建数据源类型（`UNPOOLED`短连接 / `POOLED`长连接 / `JNDI`）
- 可通过实现`org.apache.ibatis.datasource.DataSourceFactory`接口自定义数据源

```xml
<dataSource type="POOLED">
  <property name="driver" value="${driver}"/>
  <property name="url" value="${url}"/>
  <property name="username" value="${username}"/>
  <property name="password" value="${password}"/>
</dataSource>
```

#### 数据源属性（UNPOOLED和POOLED适用）

- `driver` 数据库驱动
- `url` 数据库地址
- `username` 数据库用户名
- `password` 数据库密码
- `defaultTransactionIsolationLevel` 默认的连接事务隔离级别
- `defaultNetworkTimeout` 等待数据库操作完成的默认网络超时时间（毫秒）

#### 数据源属性（POOLED适用）

- `poolMaximumActiveConnections` 处于活动（正在使用）状态的连接最大数量（默认：`10`）
- `poolMaximumIdleConnections` 处于空闲状态的连接最大数量
- `poolMaximumCheckoutTime` 在被强制返回之前，池中连接被检出时间（默认：`20000` 毫秒，即 `20` 秒）
- `poolTimeToWait` 连接等待时间，超时重新尝试获取一个连接（默认：`20000` 毫秒，即 `20` 秒）
- `poolMaximumLocalBadConnectionTolerance` 当获取到坏的连接时允许尝试重新获取新连接的次数（默认：`3`）
- `poolPingEnabled` 是否启用侦测查询（默认：`false`）
- `poolPingQuery` 侦测查询语句，用来检验连接是否正常工作并准备接受请求
- `poolPingConnectionsNotUsedFor` 配置侦测查询的间隔时间，可与数据库连接超时时间一致来避免不必要的侦测（默认：`0`）

#### 数据源属性（JNDI适用）

- `initial_context` 数据源初始上下文
- `data_source` 数据源路径

## DatabaseIdProvider 数据库厂商标识

```xml
<databaseIdProvider type="DB_VENDOR">
  <property name="SQL Server" value="sqlserver"/>
  <property name="DB2" value="db2"/>
  <property name="Oracle" value="oracle" />
</databaseIdProvider>
```

- 可通过实现`org.apache.ibatis.mapping.DatabaseIdProvider`接口自定义类型

## Mappers 映射器

```xml
<mappers>
  <!-- 使用相对于类路径的资源 -->
  <mapper resource="org/mybatis/builder/AuthorMapper.xml"/>
  <!-- 使用绝对路径的资源 -->
  <mapper url="file:///var/mappers/AuthorMapper.xml"/>
  <!-- 使用实现类 -->
  <mapper class="org.mybatis.builder.AuthorMapper"/>
  <!-- 指定包自动扫描 -->
  <package name="org.mybatis.builder"/>
</mappers>
```
