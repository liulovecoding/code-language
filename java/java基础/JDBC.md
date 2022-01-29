
## JDBC
- JDBC：用于数据库编程
- 作用：连接数据库，发送SQL语句到数据库中，接受数据库执行SQL语句得到的结果

## 目录
1. 连接数据库
2. 实例1
3. 执行sql
4. 接收与处理结果集
5. 实例2
6. 执行SQL的对象(三个)批处理

## 一：连接数据库

1. 加载数据库驱动
```java
Class.forName("driverClass");
```
2. 连接数据库
```java
Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
//用DriverManager.getConnection方法建立连接并将结果返回给conn
/*
url=协议名+子协议名+数据源名，与数据库有关
实例：jdbc:mysql://machine_name:port/dbname
"jbdc:":是协议(都是这个)
"mysql://":子协议名,不同的数据库其值不同
machine_name：数据库所在的机器的地址，值为localhost(指本机地址)或本机IP地址
port：端口号
dbname:要连接数据库的名字
*/
//user:要连接的数据库的用户名
//password:要连接的数据库的密码
```
### 实例1
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class DbUtil {

    public static final String url = "jdbc:mysql://";
    public static final String machine_name="localhost";
    public static final Strin post="3306";
    public static final Strin dbname="imooc";
    public static final String USER = "liulx";
    public static final String PASSWORD = "123456";
    public static final String URL=url+machine_name+":"+post+"/"+dbname;
    public static void main(String[] args) throws Exception {
        //1.加载MySQL驱动程序
        Class.forName("com.mysql.jdbc.Driver");
        //2. 获得数据库连接
        Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
        ...
        }
    }
}
```

## 二：执行SQL
### 方法一： 创造一个Statement对象
该对象用于执行不带参数的简单SQL语句
```java
 Statement stmt = conn.createStatement();
 ```
 - Statemen对象的方法
 ```
 1.boolean execute(String SQL)
 //执行任何SQL,执行后第一个结果是ResultSet，则返回true，否则返回false(用于SQL语句类型不确定的情况下)
 
 2.int executeUpdate(String SQL)
 //执行查询,更新SQL,返回更新语句匹配的行数
 
 3.ResultSet executeQuery (String SQL) 
 //只能执行查询SQL，执行后返回代表查询结果的ResultSet对象
 
 ```
### 方法二： 创造一个PreparedStatement对象
该对象用于执行带或不带 IN 参数的预编译 SQL 语句
```java
PreparedStatement ptmt = conn.prepareStatement(sql);
//PreparedStatement接口是从Statement接口扩展来的，该语句能动态的提供/接收参数
//SQL语句可以包含多个IN参数，因为在 SQL 语句创建时IN的值未被指定，所以该语句为每个 IN 参数保留一个问号（“？”）作为占位符
//问号的值必须在该语句执行之前，通过适当的setXXX 方法来提供
```
- PreparedStatement对象的方法
```java
//因为是扩展的缘故，具有上文提到的Statement对象的三个方法
1. setXXX(int parameterIndex, XXX x)
 //作用：把x赋给prepareStatement(sql)中出现的sql中的问号, 通过parameterInde指定是第几个问号
 //XXX是类型
```
- 实例
```java
PreparedStatement pstmt  =  con.prepareStatement( " UPDATE EMPLOYEES
                                      SET SALARY  =   ?  WHERE ID  =   ? " );
    pstmt.setBigDecimal( 1 ,  153833.00 ) // 将153833.00赋给第一个参数
    pstmt.setInt( 2 ,  110592 ) // 将110592赋给第二个参数(即第二个问号)
```
### 方法三：创建一个CallableStatement对象
该对象用于执行对数据库已存在的存储过程的调用
```java
CallableStatement cstmt = con.prepareCall(SQL);
```

## 三：接收与处理结果集
### 1.创造一个ResultSet对象来接收结果集
ResultSet接口表示数据库执行SQL语句返回的数据表
- 创建基本的ResultSet
```java
ResultSet re = stmt.executeQuery(sql);
//stmt:是第二步中的三个类中的一个类对象
//re的 resultSetType值是ResultSet.TYPE_FORWARD_ONLY
while(re.next()){
//获取数据
}
```
- 创建对象stmt(三种)时创建ResultSet对象
```java
1. Statement stmt = conn. createStatement (int resultSetType, int resultSetConcurrency) ;
2. PreparedStatement stmt = conn.prepareStatement(string sql,int resultSetType, int resultSetConcurrency);
3. CallableStatement  stmt = con.prepareCall(string sql,int resultSetType, int resultSetConcurrency);
```
- 参数

1. resultSetType：设置ResultSet对象的类型标示是否可滚动


| ResultSet.TYPE_FORWARD_ONLY           |          光标只能向前滚动(这是默认值)                            |
| ------------------------------------- | ----------------------------------------------------------------|
| ResultSet.TYPE_SCROLL_INSENSITIVE     |        光标能前后滚动，对创建结果集之后的数据库修改不影响结果集   | 
| Result.TYPE_SCROLL_SENSITIVE          |               光标能前后滚动，...影响结果集                      |

>note: ResultSet.TYPE_FORWARD_ONLY：存储查询结果，只能读一次，只能用该对象的next()来一个个的读数据


 2. resultSetConcurrency：设置ResultSet对象中数据记录是否能够修改的
 
 
| ResultSet.CONCUR_READ_ONLY      |         ResultSet中的数据记录只能读          |
| ------------------------------- | --------------------------------------------|
| ResultSet.CONCUR_UPDATABLE      |     能对ResultSet和数据库中的数据记录修改    |

>note:设置了可更新的ResultSet的不一定能完成更新

- ResultSet的方法

![36](https://user-images.githubusercontent.com/90401274/137615420-1e771ad8-a141-4f63-9821-23c9025f0f31.png)
![37](https://user-images.githubusercontent.com/90401274/137615454-d430b631-ca70-433c-8183-3de6e9b2f5a0.png)
![38](https://user-images.githubusercontent.com/90401274/137615459-e240bfaa-b7db-4af6-ba85-e6d4e6c4d01a.png)
![39](https://user-images.githubusercontent.com/90401274/137615463-33a12ac1-0914-4088-95eb-509a57024062.png)
![40](https://user-images.githubusercontent.com/90401274/137615467-939a2060-16b6-4a4a-9ef8-8afbd04bcf91.png)
![41](https://user-images.githubusercontent.com/90401274/137615469-b891b3cf-93ed-4f5d-8493-ca86c591d7d4.png)
![42](https://user-images.githubusercontent.com/90401274/137615475-616a44c4-8f3f-4ce4-8b4e-1c6028cb52d9.png)
![43](https://user-images.githubusercontent.com/90401274/137615476-7969d97d-9277-4cf3-920c-8a443f946745.png)


### 实例2
```java
//接着前面实例1的省略号写
Statement stmt = conn.createStatement();
ResultSet re=conn.execute(String SQL);
while(re.next()){
System.out.println(rs.getString("UserName") + " " + rs.getString("Password"));
}
//另一种写法
Statement stmt =conn.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE,ResultSet.CONCUR_UPDATABLE );
ResultSet re=conn.execute(String SQL);
//依次关闭资源
rs.close();
statement.close();	
conn.close();
```

## 执行SQL的对象(三个)批处理
### 实例3
```java
//第一步：创建对象(三个随便一个)stmt
Statement stmt = conn.createStatement();
PreparedStatement ptmt = conn.prepareStatement(sql);
···
//第二步：将自动提交设置为false
conn.setAutoCommon(false);
//第三步：调用对象stmt的addBatch()将sql语句加入批处理中
stmt.addBatch(sql1);
stmt.addBatch(sql2);
stmt.addBatch(sql3);
//用stmt的executeBAtchison()方法执行所有的sql语句(这里指sql1,sql2,sql3)
int [] count =stmt.executeBatch();
//最后一步：提交事务
conn.commit();
```
