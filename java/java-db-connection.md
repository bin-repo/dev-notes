# java-db-connection（数据库连接）

## 连接Oracle8/8i/9i数据库（用thin模式）

```java
Class.forName("oracle.jdbc.driver.OracleDriver");

String url = "jdbc:oracle:thin:@localhost:1521:yourdbsid";
String user = "scott";
String password = "tiger";

Connection conn = DriverManager.getConnection(url, user, password);
```

## 连接Sql Server7.0/2000数据库

```java
Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver");

String url = "jdbc:microsoft:sqlserver://localhost:1433;DatabaseName=yourdb";
String user = "sa";
String password = "sa";

Connection conn = DriverManager.getConnection(url, user, password);
```

## 连接DB2数据库

```java
Class.forName("com.ibm.db2.jdbc.app.DB2Driver");

String url = "jdbc:db2://localhost:5000/yourdb";
String user = "admin";
String password = "123";

Connection conn= DriverManager.getConnection(url, user, password);
```

## 连接Informix数据库

```java
Class.forName("com.informix.jdbc.IfxDriver");

String url = "jdbc:informix-sqli://123.45.67.89:1533/yourdb:INFORMIXSERVER=myserver;user=testuser;password=testpassword";

Connection conn = DriverManager.getConnection(url);
```

## 连接Sybase数据库

```java
Class.forName("com.sybase.jdbc.SybDriver");

String url = "jdbc:sybase:Tds:localhost:5007/yourdb";

Properties sysProps = System.getProperties();
sysProps.put("user","userid");
sysProps.put("password","user_password");

Connection conn = DriverManager.getConnection(url, sysProps);
```

## 连接MySQL数据库

```java
Class.forName("org.gjt.mm.mysql.Driver");

String url = "jdbc:mysql://localhost:3306/yourdb?user=soft&password=soft1234&useUnicode=true&characterEncoding=8859_1" 

Connection conn = DriverManager.getConnection(url);
```

## 连接PostgreSQL数据库

```java
Class.forName("org.postgresql.Driver");

String url = "jdbc:postgresql://localhost/yourdb";
String user = "myuser";
String password = "mypassword";

Connection conn = DriverManager.getConnection(url, user, password); 
```
